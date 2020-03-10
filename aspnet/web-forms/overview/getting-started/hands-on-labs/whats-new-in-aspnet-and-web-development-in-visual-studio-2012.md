---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Visual Studio 2012 ' de ASP.NET ve Web geliştirme yenilikleri | Microsoft Docs
author: rick-anderson
description: Visual Studio 'nun yeni sürümü, Web teknolojileriyle çalışırken deneyim ve performansı iyileştirmeye odaklanan birkaç geliştirme sunar...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525937"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>Visual Studio 2012'de ASP.NET ve Web Geliştirme Yenilikleri

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

> Visual Studio 'nun yeni sürümü, Web teknolojileriyle çalışırken deneyim ve performansı iyileştirmeye odaklanmış bir dizi geliştirme sunar. CSS, JavaScript ve HTML için Visual Studio düzenleyicileri, IntelliSense ve otomatik girintileme gibi en çok isteğe bağlı kod yardımlarının çoğunu kapsayacak şekilde tamamen yeniden belirlenmiştir. Performans, paketleme ve küçültmeye yönelik özellikler artık sayfa yükleme süresini kolayca azaltmak için yerleşik özellikler olarak tümleşiktir.
> 
> Visual Studio, en son Web sitesi teknolojileriyle çalışmanıza olanak sağlar. Ayrıca, yeni HTML5 öğelerinden ve özelliklerden yararlanarak sitenizin istemci platformundan bağımsız olarak çalıştığından emin olmak için tarayıcılar arası CSS3 kod parçacıklarını kullanabilirsiniz.
> 
> JavaScript kodu yazma ve profil oluşturma, bu Visual Studio sürümü ile daha kolay olmalıdır. IntelliSense listeleri, tümleşik XML belgeleri ve gezinti özellikleri artık JavaScript kodu için kullanılabilir. Artık JavaScript kataloğu elinizin altında. Ayrıca, betiklerle ECMAScript5 uyumluluğunu denetleyebilir ve sözdizimi hatalarını erken bir aşamada tespit edebilirsiniz.
> 
> Son olarak, bu Visual Studio sürümü yerleşik paketlemeyi ve küçültmeye göre kullanır. Betik dosyalarınız ve stil sayfaları, sitenin daha hızlı bir şekilde gerçekleşmesini sağlayacak şekilde paketlenecek ve sıkıştırılır.
> 
> Bu laboratuvar, daha önce kaynak klasörde sunulan örnek bir Web uygulamasına küçük değişiklikler uygulayarak açıklanan geliştirmeler ve yeni özellikler konusunda size kılavuzluk eder.
> 
> Tüm örnek kod ve kod parçacıkları [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- CSS düzenleyicisinde yeni özellikleri ve geliştirmeleri kullanın
- HTML düzenleyicisinde yeni özellikleri ve geliştirmeleri kullanın
- JavaScript düzenleyicisinde yeni özellikleri ve geliştirmeleri kullanın
- Paketlemeyi ve küçültmeye göre yapılandırma ve kullanma

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

- [Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) (Kurulum betikleri Için, Windows 8 ve windows Server 2008 R2 'de zaten yüklü)
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) veya HTML5 uyumlu tarayıcı

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Laboratuvar için bu uygulamalı, aşağıdaki alıştırmaları içerir:

1. [Alıştırma 1: CSS düzenleyicideki yenilikler](#Exercise1)
2. [Alıştırma 2: HTML Düzenleyicinizdeki yenilikler](#Exercise2)
3. [Alıştırma 3: JavaScript düzenleyicideki yenilikler](#Exercise3)
4. [Alıştırma 4: paketleme ve Minbirleşme](#Exercise4)

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>Alıştırma 1: CSS düzenleyicideki yenilikler

Web geliştiricileri, CSS düzenlemeyle ilgili birçok zorluklara alışkın olmalıdır. CSS stillendirme en büyük sorunlarından biri tarayıcılar arası uyumlulukta olur. Bu, genellikle sitenize Stil uygulandıktan sonra başka bir tarayıcı veya cihazda açtığınızda farklı göründüğünü fark etmeksizin meydana gelir. Bu nedenle, bu görsel sorunları düzeltmek için önemli bir zaman harcayabilir ve son olarak bir tarayıcıda çalıştığını fark edebilirsiniz.

Visual Studio artık geliştiricilerin CSS stil sayfalarını etkin bir şekilde erişmesine, çalışmasına ve düzenlenmesine yardımcı olan özellikler içerir. Bu alıştırmada, etkin bir kuruluş ve sürüm için yeni özellikleri ve tarayıcılar arası uyumluluk için CSS3 kod parçacıklarını karşılamanız gerekir.

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>Görev 1-yeni düzenleyici özellikleri

Bu görevde, CSS düzenleyicisinin yeni özelliklerini keşfedeceksiniz. Bu yeni düzenleyici, yeni akıllı girintileme, geliştirilmiş kod açıklamaları ve geliştirilmiş IntelliSense listesinden yararlanarak üretkenliğinizi artırmanıza yardımcı olur.

1. **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.
2. Çözüm Gezgini, **Stiller** klasörünün altında bulunan **site. css** dosyasını açın. **Metin düzenleyici** araçlarının araç çubuğunda göründüğünden emin olun. Bunu yapmak için, | **araç çubuklarını** **görüntüle** menü seçeneğini belirleyin ve **metin Düzenleyicisi** seçeneklerini işaretleyin. Bu yeni sürüm, **yorum** düğmesi (![açıklama düğmesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) **ve açıklama düğmesi** (![Açıklama düğmesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)) CSS Düzenleyicisi için de etkinleştirildiğinden emin olun.

    ![Düzenleyici ve CSS araçlarını etkinleştirme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Düzenleyici ve CSS araçlarını etkinleştirme")

    *Düzenleyici ve CSS araçlarını etkinleştirme*
3. Kodu kaydırın ve herhangi bir CSS sınıfı tanımını seçin. Seçili satırları **açıklamaya yönelik açıklama (![** yorum-düğme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) düğmesine tıklayın. Ardından, değişiklikleri geri almak için **Açıklama** (![açıklama/adım](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)) düğmesine tıklayın.
4. **Daraltma** (![daraltma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png) **) ve metnin** sol kenar boşluğunda bulunan (![Genişlet](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) düğmeleri ' ne tıklayın. Artık, daha temiz bir görünüm sağlamak için kullandığınız stilleri gizleyebildiğinize dikkat edin.

    ![CSS sınıflarını daraltma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "CSS sınıflarını daraltma")

    *CSS sınıflarını daraltma*
5. Akıllı girintileme özelliğinin etkinleştirildiğinden emin olun. **Araçlar** | **Seçenekler** menü seçeneğini belirleyin ve ardından ekranın sol bölmesindeki **metin düzenleyici** | **CSS** | **biçimlendirme** sayfasını seçin. **Hiyerarşik girintileme** seçeneğini işaretleyin.

    ![Hiyerarşik girintileme etkinleştiriliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Hiyerarşik girintileme etkinleştiriliyor")

    *Hiyerarşik girintileme etkinleştiriliyor*
6. Ana sınıf tanımını (. Main) bulun ve div öğelerine bir stil ekleyin. Kodun otomatik olarak hizalandığını fark edersiniz. Bu, kullanıcıların üst sınıfları bir bakışta bulmasına yardımcı olur.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![CSS 'de hiyerarşik hizalama](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "CSS 'de hiyerarşik hizalama")

    *CSS 'de hiyerarşik hizalama*
7. **. Main div** sınıfı içinde, kenarlığın sonundaki imleci bulun **: 0px;** ve IntelliSense listesini göstermek için **ENTER** tuşuna basın. **Üste** yazmaya başlayın ve siz yazarken listenin nasıl filtrelendiğine dikkat edin. Listede, sözcüğün herhangi bir bölümünde **üst** olan öğeler görüntülenir (Visual Studio 'nun önceki sürümlerinde, liste terimle *başlayan* öğelere göre filtrelenir).

    ![CSS 'de IntelliSense geliştirmeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "CSS 'de IntelliSense geliştirmeleri")

    *CSS 'de IntelliSense geliştirmeleri*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>Görev 2-renk seçici

Bu görevde, Visual Studio IntelliSense ile tümleştirilmiş yeni CSS renk seçiciyi keşfedeceksiniz.

1. **Site. css ' de,** üstbilgi sınıfı tanımını (. Header) bulun ve imleci &quot;:&quot; ve Bu kod satırındaki &quot; karakter &quot;# **.**

    ![İmleci bulma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "İmleci bulma")

    *İmleci bulma*
2. **İki nokta üst üste** (:) ve renk seçiciyi göstermek için yeniden yazın. Göreceğiniz ilk renklerin sitenizin en sık kullanılan renkleriyle olduğunu unutmayın. Beyaz renge tıklarsanız, HTML renk kodu (#fff), stil sayfasındaki geçerli renk kodunun yerini alır.

    ![Renk seçici](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Renk seçici")

    *Renk seçici*
3. Renk degradesini göstermek için renk seçicisindeki **genişletme** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) düğmesine basın ve ardından farklı bir renk seçmek için gradyan imlecini sürükleyin. Bundan sonra, **damlalık** düğmesine tıklayın ve ekrandaki herhangi bir rengi seçin. İmleci taşırken arka plan rengi değerinin dinamik olarak değiştiğine dikkat edin.

    ![Renk seçici gradyanı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Renk seçici gradyanı")

    *Renk seçici gradyanı*
4. **Opaklık kaydırıcısının** saydamlığını azaltmak için seçiciyi çubuğun ortasına taşıyın. Arka plan rengi değerinin artık ölçeğini RGBA olarak değiştirdiğine dikkat edin.

    ![Renk seçici geçirgenliği](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Renk seçici geçirgenliği")

    *Renk seçici geçirgenliği*

    > [!NOTE]
    > CSS3 ' deki RGBA (kırmızı, yeşil, mavi, alfa) renk tanımı, tek bir öğe için renk opaklık değerini tanımlamanızı sağlar. **Opaklığın** aksine, RGBA renkleri **-** benzer bir CSS özniteliği de en son tarayıcılarla uyumludur.

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>Görev 3-CSS uyumlu kod parçacıkları

Bu görevde, Web sitenizde bazı özellikler uygulamak için tarayıcılar arası uyumlu CSS3 parçacıklarını nasıl kullanacağınızı öğreneceksiniz.

1. **Site. css** dosyasında **üst bilgi** CSS sınıf tanımını (. Header) bulun ve imleci **/\*Border Radius /\*** yeni bir kod parçacığı eklemek için buraya yerleştirin. IntelliSense listesini göstermek için **ENTER** tuşuna basın ve listeyi filtrelemek için **RADIUS** yazın. Bir çift tıklama ile listeden **Border-Radius** seçeneğini seçin ve ardından parçacığı eklemek için **sekme** tuşuna basın. Sonra, piksel cinsinden bir yarıçap boyutu yazın ve **ENTER**tuşuna basın. Örneğin, **15 piksel**yazın.

    Kod parçacığı tarafından eklenen CSS3 öznitelikleri, Mozilla ve WebKit tabanlı tarayıcılar dahil olmak üzere çoğu HTML5 uyumluluk tarayıcılarında yuvarlatılmış kenarlıkları işler.

    ![Border-Radius parçacığı kullanma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Border-Radius parçacığı kullanma")

    *Border-Radius parçacığı kullanma*
2. Sayfa stilinde (. Page) aynı **Kenarlık** parçacıklarını uygulayın.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. Çözümü çalıştırmak için **F5** tuşuna basın. Her sayfanın artık kenarlığı yuvarlatılmış olduğuna dikkat edin.

    ![Yuvarlak köşeler](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Yuvarlak köşeler")

    *Yuvarlak köşeler*
4. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.
5. **Stiller** klasörünün altında bulunan **Custom. css** dosyasını açın ve imleci **div. Images ul li img** Class tanımının içine yerleştirin.
6. IntelliSense listesini göstermek için ENTER tuşuna basın, **Box-Shadow** yazın ve varsayılan gölge kod parçacığını sınıf tanımının içine eklemek için **Tab** tuşuna iki kez basın. Gölge değerlerini **10px 10px 5px #888**olarak ayarlayın. Ardından **Border-Radius** yazın ve kod parçacığını ekleyin. Yarıçap boyutunu ayarlamak için **15 piksel** yazın ve **ENTER**tuşuna basın.

    ![Gölgeli yuvarlak köşeler](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Gölgeli yuvarlak köşeler")

    *Gölgeli yuvarlak köşeler*

    > [!NOTE]
    > Bu anda, Mozilla ve WebKit (Chrome, Safari, Konkeror) tarayıcılarını desteklemek için ilgili önek (Moz, WebKit, o) ile birlikte Shadow özniteliği eklenir.
7. Yeni bir sınıf **div oluşturun. bu görüntüleri ul li img:** **div. Images ul li img** Class tanımının altına gelin ve imleci köşeli ayracın içine yerleştirin **.**

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. Dönüştürme kod parçacığını eklemek için **Dönüştür** yazın ve **Tab** tuşuna iki kez basın. Ardından, görüntülerin üzerine gelindiğinde döndürme açısı değerini değiştirmek için **döndürme (-15deg)** girin.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. **F5** tuşuna basarak çözümü ÇALıŞTıRıN ve CSS3 sayfasına gidin. Görüntülerin köşeleri ve kutu gölgeleri yuvarlatılmış olduğuna dikkat edin. Fareyi görüntülerin üzerine getirin ve döndürmeyi izleyin.

    ![Görüntü döndürme parçacığı dönüştürme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Görüntü döndürme parçacığı dönüştürme")

    *Görüntü döndürme parçacığı dönüştürme*

    > [!NOTE]
    > Internet Explorer 10 kullanıyorsanız ve gölgeleri göremiyorsanız, belge modunun ıE10 standartları olarak ayarlandığından emin olun. Internet Explorer Geliştirici Araçları 'nı açmak için **F12** tuşuna basın ve IE10 standartlarına geçmek Için **belge modu** ' na tıklayın.

    ![yaklaşık-US](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>Alıştırma 2: HTML Düzenleyicinizdeki yenilikler

Visual Studio 'Nun gelişmiş bir HTML Düzenleyicisi vardır. Bu sürüme dahil olan geliştirmelerden bazıları HTML belgelerindeki akıllı girintileme, HTML5 parçacıkları, HTML başlangıç ve bitiş etiketi eşleştirmesi ve HTML doğrulaması ' na sahiptir. Bu alıştırmada, Web sitesi biçimlendirmesinde çalışırken bu değişikliklerin akıcı bir şekilde nasıl iyileştirebileceğinizi göreceksiniz.

CSS Düzenleyicisi gibi, HTML Düzenleyicisi de geliştirilmiştir. Bu geliştirmelerin çoğu, Web geliştiricisi ömrünü daha kolay hale getirir. HTML belgesi DOCTYPE 'ı hedeflemek ve doğrulamak için kod parçacıkları, akıllı girintileme, eşleşen başlangıç ve bitiş etiketleri gibi şeyler bu geliştirmelerden bazılarıdır.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>Görev 1-Iyileştirilmiş DOCTYPE doğrulaması

Bu, tanım ana sayfada olsa da, HTML Düzenleyicisi artık sayfanızın DOCTYPE 'ı kontrol edebilir. Sayfanızın DOCTYPE öğesine bağlı olarak, HTML Düzenleyicisi doğru kurallar kümesiyle doğrulanır ve IntelliSense listesini, DOCTYPE öğelerini ele alacak şekilde filtreleyecek.

Bu görevde, HTML Düzenleyicisi davranışının uygun şekilde nasıl değiştiği görmek için bir sayfanın DOCTYPE öğesini değiştirirsiniz.

1. Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.
2. **Site. Master** sayfasını açın.
3. Doğrulama araç çubuğunun hedef şemasına dikkat edin. HTML düzenleyicisinin davranış şekli (doğrulama, IntelliSense, vb.), seçilen doctype öğesine uyacak şekilde düzgün şekilde değişir.

    ![HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın")

    *HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın*
4. Hedef şemayı HTML 4,01 olarak değiştirin.

    ![HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı değiştirme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı değiştirme")

    *HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı değiştirme*
5. İmleci **gövde** öğesinin altına YERLEŞTIRIN ve HTML5 öğesinin adını yazmaya başlayın (örneğin, **video**). Öğesinin IntelliSense listesinde mevcut olmadığına dikkat edin.

    ![HTML5 öğeleri listelenmemiş](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "HTML5 öğeleri listelenmemiş")

    *HTML5 öğeleri listelenmemiş*
6. Doğrulama araç çubuğunun hedef şemasında yapılan değişiklikleri geri almak için, açılan listeden DOCTYPE: XHTML5 öğesini seçerek.

    ![HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "HTML kaynak düzenlemesi araç çubuğunda DOCTYPE kullanın")

    *HTML kaynak düzenlemesi araç çubuğunda DOCTYPE 'ı Sıfırla*
7. İmleci **gövde** öğesinin altına YERLEŞTIRIN ve HTML5 öğesini yeniden yazmaya başlayın (örneğin, **video**gibi). HTML5 öğelerinin artık IntelliSense listesinde kullanılabilir olduğuna dikkat edin.

    ![Listelenen HTML5 öğeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "Listelenen HTML5 öğeleri")

    *Listelenen HTML5 öğeleri*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>Görev 2-başlangıç/bitiş etiketleri otomatik güncelleştirme

Visual Studio artık, düzenlemekte olduğunuz öğenin HTML açılış veya kapanış etiketlerini birbirleriyle eşleşecek şekilde güncelleştirir. Bu yeni özellik, HTML etiketlerini düzenlenirken üretkenliğinizi artırır.

1. **Default. aspx** sayfasında, başlıklı bir **H3** öğesi ekleyin (örneğin, Visual Studio 2012 Rok!).

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. **H3** etiketini değiştirin ve **H2** veya H1 yazın **.**

    Bitiş etiketinin otomatik olarak güncelleştirdiğine dikkat edin. Başlangıç etiketinin de aynı şekilde güncelleştii görmek için bitiş etiketini de değiştirebilirsiniz.

    ![Bitiş etiketinin otomatik güncelleştirilmesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Bitiş etiketinin otomatik güncelleştirilmesi")

    *Bitiş etiketinin otomatik güncelleştirilmesi*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>Görev 3-yeni HTML5 kod parçacıkları

Visual Studio artık birkaç HTML5 kod parçacığı içerir. Bu görevde, bu kod parçacıklarında bazılarını kullanacaksınız.

1. Web sitesi klasörünün köküne **Ses** adlı yeni bir klasör ekleyin. Windows Gezgini 'ni açın ve tüm ses dosyalarını **WhatsNewASPNET. sln** çözümünün **Ses** klasörüne kopyalayın.
2. **Default. aspx** sayfasında, Web11 Rosin!! altındaki imleci bulun. Üst bilgi. **Ses** YAZıN ve Tab tuşuna basın.

    Yeni HTML Düzenleyicisi HTML5 içeriğine yönelik kod parçacıklarını içerir. HTML5 parçacıklarını etkinleştirmek için uygun DOCTYPE tanımını kullanmayı unutmayın.

    ![HTML5 kod parçacıkları ekleme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "HTML5 kod parçacıkları ekleme")

    *HTML5 kod parçacıkları ekleme*
3. Ses kaynağını, var olan bir ses dosyasına işaret etmek üzere güncelleştirin.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > Bu çözüme ses dosyası eklemeniz gerekir.
4. Siteyi çalıştırmak ve sesi oynatmak için **F5** tuşuna basın.

    ![Ses denetimini çalıştırma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Ses denetimini çalıştırma")

    *Ses denetimini çalıştırma*

    > [!NOTE]
    > Visual Studio 'da video, şekil vb. dahil olmak üzere daha fazla kod parçacığı de deneyebilirsiniz.
5. Şimdi sayfanın bazı bölümünde bir denetim eklemeyi deneyin. Örneğin, bir **GridView** denetimi eklemeyi deneyin, ancak **&lt;oyutlandır** yazmak yerine **GV&lt;** yazmaya başlayın. IntelliSense listesinde **ASP: GridView** denetimi gösterildiğine dikkat edin.

    HTML düzenleyicisinde IntelliSense artık başlık büyük-küçük harf araması ve kısmi eşleştirme (terimi içeren tüm öğeleri alma) sağlar.

    ![IntelliSense listeleriyle GridView ekleme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "IntelliSense listeleriyle GridView ekleme")

    *IntelliSense listeleriyle GridView ekleme*

    **&lt;Grid** yazarsanız, terimiyle eşleşen tüm öğeleri alırsınız, ancak Visual Studio **GridView** denetimini önerir:

    ![IntelliSense listeleriyle bir GridView ekleme ve kısmi eşleştirme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "IntelliSense listeleriyle bir GridView ekleme ve kısmi eşleştirme")

    *IntelliSense listeleriyle bir GridView ekleme ve kısmi eşleştirme*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>Görev 4-HTML Düzenleyicisi akıllı etiketleri

HTML düzenleyicisinde başka bir geliştirme de Akıllı Etiketler özelliğidir. Akıllı Etiketler, genel veya yinelenen geliştirme görevlerini denetim başına temelinde gerçekleştirmeyi kolaylaştırır. Bu özellik HTML tasarımcısında zaten kullanılabilir, ancak HTML düzenleyicisinde mevcut değil.

1. **Site. Master** ' i açın ve **ASP: Menu** öğesini bulun. İmleci başlangıç etiketine yerleştirin ve küçük glifin öğenin altında görüntülendiğini unutmayın. akıllı görevler menüsünü açmak için tıklayın. Menü denetimiyle ilgili bazı görevlere hızlı erişiminizin olduğuna dikkat edin.

    ![Menü denetimi için akıllı görevler](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Menü denetimi için akıllı görevler")

    *Menü denetimi için akıllı görevler*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>Görev 5-akıllı girintileme

HTML 'deki en iyi uygulamalardan biri, kodu okunabilir tutmak için iç içe geçmiş öğeleri girintileyerek. Visual Studio 2012 ' de, kodu yazarken düzenleyicinin öğeleri otomatik olarak girintiettiğini fark edeceksiniz.

> [!NOTE]
> Visual Studio 'nun önceki sürümünde, akıllı girintileme, XML düzenleyicisinde kullanılabilir ancak HTML düzenleyicisinde yok.

1. HTML düzenleyicisinde girintileme yapılandırmasının akıllı girintileme olarak ayarlandığından emin olun. Bunu yapmak için **araçları seçin | Seçenekler** menü seçeneği ve sonra **metin düzenleyiciyi seçin | HTML |** Ekranın sol bölmesindeki sekmeler sayfası. Akıllı girintileme seçeneğini belirleyin.

    ![HTML Düzenleyicisi ayarları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "HTML Düzenleyicisi ayarları")

    *HTML Düzenleyicisi ayarları*
2. **Default. aspx** sayfasında, Audio öğesinin altındaki tüm içeriği kaldırın.
3. İmleci açma **sesi** öğesinin sonuna yerleştirin ve **ENTER**tuşuna basın.

    İmlecin yeni konumunun ek bir girintileme düzeyine sahip olduğuna dikkat edin.

    ![HTML düzenleyicisinde akıllı girintileme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "HTML düzenleyicisinde akıllı girintileme")

    *HTML düzenleyicisinde akıllı girintileme*
4. Kaldırdığınız içerikle ses etiketini geri yükleyin veya değişiklikleri kaydetmeden **default. aspx** ' i kapatın.

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>Görev 6-Kullanıcı denetimine Ayıkla

Visual Studio 'ya eklenen ve kodun bir bölümünü bir işleve ayıklama gibi yeniden düzenleme araçları, geliştirme ve mevcut kodu yeniden düzenleme işlemlerini kolaylaştıran harika özelliklerdir. ASP.NET sayfaları için karşılık gelen, bir kullanıcı denetimine HTML kodunun ayıklanması olacaktır. Bunu el ile yapmak, yeni bir kullanıcı denetimi oluşturma, kod bölümünü Kullanıcı denetimine taşıma, Kullanıcı denetimi için bir etiket öneki kaydetme ve son olarak sayfalardaki Kullanıcı denetiminin örneğini oluşturma gibi çeşitli adımları kapsar. Şimdi, yeni *kullanıcıya Ayıkla denetim* aracı sizin için tüm bu adımları otomatik olarak gerçekleştirir.

Bu görevde, seçilen koddan yeni bir kullanıcı denetimi oluşturmak için yeni bir kullanıcı denetimi bağlama işlemini kullanacaksınız.

1. **Default. aspx** sayfasında **H2** ve **Audio** öğelerini seçin.
2. Sağ tıklayın ve **Kullanıcı denetimine Ayıkla**' yı seçin.

    ![Kullanıcıya Ayıkla Denetim menüsü seçeneği](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Kullanıcıya Ayıkla Denetim menüsü seçeneği")

    *Kullanıcıya Ayıkla Denetim menüsü seçeneği*
3. Yeni Kullanıcı denetimi için bir ad yazın. Örneğin, **Jukebox. ascx**' i ve ardından **Tamam**' ı tıklatın.

    ![Ayıklanan Kullanıcı denetimini kaydetme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Ayıklanan Kullanıcı denetimini kaydetme")

    *Ayıklanan Kullanıcı denetimini kaydetme*
4. Seçili kodun bir kullanıcı denetimine ayıklandığına ve seçili kodun özgün konumunun yeni kullanıcı denetiminin bir örneğiyle değiştirildiğini unutmayın.

    ![Sayfa Yeni Kullanıcı denetimini kullanacak şekilde otomatik olarak güncelleştirildi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Sayfa Yeni Kullanıcı denetimini kullanacak şekilde otomatik olarak güncelleştirildi")

    *Sayfa Yeni Kullanıcı denetimini kullanacak şekilde otomatik olarak güncelleştirildi*
5. Sayfayı çalıştırmak için **F5** tuşuna basın ve denetimin çalıştığını doğrulayın.

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>Alıştırma 3: JavaScript düzenleyicideki yenilikler

Özellikle uygulamanız boyutu büyümeye başladığı ve uzun dosyalarla ve yüzlerce işlevlerle ilgilenirken JavaScript kodu yazmak veya düzenlenmesinin kolay bir görev değildir. Betik geliştiricilerinin genellikle kod okunabilirliğini sürdürmek ve dosyalar arasında gezinmek için bazı ek işler yapması gerekir. JQuery gibi JavaScript kitaplıklarının dahil edilmesi halinde, kod uzunluğu nedeniyle betik gezintisi bir sınama haline geldi.

Visual Studio, kod modunu erişilebilir ve düzenlenebilir hale getirmek için Promise ile JavaScript düzenleyicisini yeniledi. C# Veya vb düzenleyicilerinde zaten var olan birçok Visual Studio özelliği artık JavaScript düzenleyicisinde uygulandı: yazarken tanıma, otomatik girintileme, belgeler ve doğrulama bölümüne gidin. Yenilenen IntelliSense listesinde, JavaScript işlev kataloğuna parmaklarınızın ucunda olursunuz.

Bu alıştırmada, JavaScript Düzenleyicisi 'nin yeni özellik ve iyileştirmelerinden bazılarını öğreneceksiniz. Örnek dosyalara gözatıp, JavaScript programlarınızın Visual Studio 2012 içinde daha verimli olmasını sağlayacak yeni özelliklerden her birini keşfedeceksiniz.

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>Görev 1-JavaScript Düzenleyicisi yeni özellikler

Bu görev sizi, kodunuzun düzenlenmesine ve daha iyi bir kullanıcı deneyimi getirmeye odaklanarak yeni JavaScript Düzenleyicisi özelliklerinden bazılarını tanıtacaktır.

1. Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.
2. Uygulamayı çalıştırmak için **F5** tuşuna basın, ardından gezinti çubuğundaki JavaScript bağlantısına tıklayın. Sayfayı birkaç kez yenileyin ve sayacın nasıl artısaymadığını denetleyin.

    ![Sayfa sayacı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Sayfa sayacı")

    *Sayfa sayacı*
3. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.
4. **JavaScript. aspx** sayfasını açın ve **&lt;betiği&gt;** bloğunu (aşağıda gösterilmiştir) bulun.

    Aşağıdaki kod, sayfanın geçerli kullanıcı tarafından ziyaret edilme sayısını depolayan *Pageloadcount* değişkenini depolamak için HTML5 yerel depolama kullanır. Yerel depolama, HTML5 standardına göre sunulan bir istemci tarafı anahtar-değer veritabanıdır. Veriler, kullanıcının tarayıcısının içindeki yerel makineye kaydedilir.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > Sonraki adımlarla devam etmeden önce DOCTYPE 'ın XHTML5 olarak ayarlandığından emin olun.
5. Kodu düzenleyin ve JavaScript için IntelliSense 'in yerel depolama gibi HTML5 özellikleri ve bunların iç yöntemleri içerdiğine dikkat edin.

    ![JavaScript 'te HTML5 JavaScript özellikleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "JavaScript 'te HTML5 JavaScript özellikleri")

    *JavaScript 'te HTML5 JavaScript özellikleri*
6. Betik kodundan herhangi bir açma köşeli ayracı ( **{** ) tıklatın ve köşeli ayracın vurgulandığını unutmayın.

    ![Köşeli ayraçlar vurgulanır](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Köşeli ayraçlar vurgulanır")

    *Köşeli ayraçlar vurgulanır*
7. **Testautoalign ()** işlevinin açıklamasını kaldırın (üç satırı seçin ve **CTRL** + **K**kullanabilirsiniz; **CTRL** + **U**) ve işlev kodu içindeki imleci bulun. İkinci bir satırı eklemek için ENTER tuşuna basın. Kodun artık **hizalandığını** ve **Otomatik girintili**olduğunu unutmayın.

    ![JavaScript kodu otomatik hizalı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScript kodu otomatik hizalı")

    *JavaScript kodu otomatik hizalı*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>Görev 2-JavaScript doğrulanıyor

Bu görevde, ECMAScript5 Standard için yeni JavaScript doğrulamasını keşfedeceksiniz. Bu özellik uyumlu JavaScript kodu yazmanıza yardımcı olur, ancak site dağıtımından önce betik oluşturma sorunlarını önler.

> [!NOTE]
> Visual Studio 2010 ECMAStript3 uyumluluğunu uyguladık, Visual Studio 2012 ECMAScript5 uyumluluğu sağlar.

1. **Scripts\custom** proje klasörünün altında bulunan **ECMA5script5. js** ' i açın. Artık ECMAScript5 Standard için doğrulamayı test edersiniz.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    ECMAScript5 **katı modu**sağlayan, dosyanın ilk satırında **katı** &quot; yönü &quot; kullanıma alabilirsiniz. Bu mod, önceki sürümden belirsizlikleri açıklığa kavuşturtiren dilin bir alt kümesiyle oluşur ve alıcıları ve ayarlayıcılar, JSON için kitaplık desteği ve nesne özellikleri üzerinde daha fazla yansıma gibi bazı yeni özellikler ekler.
2. Zaten açılmadıysa **hata listesi** açın (**Görünüm** menüsü | **Hata listesi**). **İşlev** bildiriminin altı çizili olduğuna dikkat edin. Bunun nedeni, ECMA5 standart işlevlerinin dil yapıları içinde yer alamaz. Aşağıdaki hata listesinde, uyarı ayrıntılarını görürsünüz.

    ![JavaScript doğrulama hata iletisi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "JavaScript doğrulama hata iletisi")

    *JavaScript doğrulama hata iletisi*
3. **&quot;katı&quot;yönünü kullanın** ve hataların kaybolduğunu, ancak uyarıların kaldığını unutmayın.
4. Dosyanın son satırına, **&quot;test&quot;** gibi bir dize yazın (dize olarak göstermek için tırnak işaretleri ekleyin). IntelliSense listesini göstermek için dizenin yanına bir nokta yazın ve **Kırp** seçeneğini belirleyin.

    ECMAScript5 Standard 'da, dize değerleri ve değişkenleri, trim, büyük harfler, ara ve Değiştir gibi tanımlanmış dize yöntemlerine sahiptir.

    ![JavaScript 'te IntelliSense listesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "JavaScript 'te IntelliSense listesi")

    *JavaScript 'te IntelliSense listesi*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>Görev 3-JavaScript için XML belgeleri

Bu görevde JavaScript 'te XML belgeleri için Visual Studio özelliklerini araştıracaktır. JavaScript IntelliSense listesinin şimdi her bir işlevin XML belgelerini gösterdiğini görürsünüz. Ayrıca, gezinme özelliğini JavaScript 'te keşfedeceksiniz.

1. **Betikler/özel** proje klasöründe bulunan **xmlDoc. js** dosyasını açın. Bu dosya JavaScript işlevlerinin her birinde XML belgelerini içerir.

    ![IntelliSense ile tümleştirilmiş JavaScript XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "IntelliSense ile tümleştirilmiş JavaScript XML belgeleri")

    *IntelliSense ile tümleştirilmiş JavaScript XML belgeleri*
2. **XmlDoc. js** dosyasındaki **Add** işlevi altında, **Test**adlı yeni bir işlev oluşturun.
3. **Test** işlevinde, iki parametre alan **çarpma** işlevini çağırın. Araç ipucu kutusunda **çarpma** işlevi belgelerinin gösterildiğini görebilirsiniz.

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![JavaScript işlevleri için XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "JavaScript işlevleri için XML belgeleri")

    *JavaScript işlevleri için XML belgeleri*
4. İşlev çağrısı ifadesini doldurun ve döndürülen değer üzerinde IntelliSense listesini açmak için bir *nokta* yazın. Visual Studio 'Nun belgelerde **döndürülen** değeri algılayarak değeri sayı olarak kabul ettiğini unutmayın.

    ![Dönüş türleri için XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "Dönüş türleri için XML belgeleri")

    *Dönüş türleri için XML belgeleri*
5. Şimdi, Add işlevi için bir çağrı ekleyin. JavaScript düzenleyicisinin artık işlev aşırı yüklerini desteklediğini unutmayın. Bir işlev adı yazdığınızda, belgelerde belirtilen kullanılabilir aşırı yüklerden birini seçebileceksiniz.

    ![Aşırı yüklemeler için XML belgeleri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "Aşırı yüklemeler için XML belgeleri")

    *Aşırı yüklemeler için XML belgeleri*
6. **Sayfaydefinition. js** dosyasını açın ve **$ (). html ()** işlev çağrısını bulun. **HTML**üzerinde imleci bulun.
7. **F12** tuşuna basın ve tanıma gidin. Artık **bul** aracını kullanmadan JavaScript kodunuza erişip erişebileceğinizi fark edebilirsiniz.
8. Kod dosyasının alt kısmındaki imza bloğundan önce jQuery yönergesinin üzerindeki imleci bulun. **F12**tuşuna basın. JQuery kitaplık dosyasına gitmeniz gerekir. Ayrıca, **F12**kullanarak jQuery dosyaları arasında gezinmeniz fark edebilirsiniz.

    ![JQuery tanımlarına gitme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "JQuery tanımlarına gitme")

    *JQuery tanımlarına gitme*

> [!NOTE]
> Dosyayı kaydetmeden önce, Sayfaydefinition. js ' nin sözdizimi hatası olmadığından emin olun.

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>Alıştırma 4: paketleme ve Minbirleşme

Web siteleriniz kaç kez bir JavaScript veya CSS dosyası içeriyor? Bu, paketleme ve küçültme, dosya boyutunu azaltmaya ve sitenin daha hızlı gerçekleşmesini sağlamaya yardımcı olan çok yaygın bir senaryodur. ASP.NET 4,5 ' deki yeni paketleme özelliği, bir dizi JS veya CSS dosyasını tek bir öğe halinde paketler ve içeriği (gerekmeyen boş alanları kaldırmak, açıklamaları kaldırmak ve tanımlayıcıları azaltmak) için boyutunu azaltır.

ASP.NET 4,5 ' de paketleme ve küçültme, çalışma zamanında gerçekleştirilir, böylece işlem Kullanıcı aracısını tanımlayabilir (örneğin, IE, Mozilla, vb.) ve bu nedenle Kullanıcı tarayıcısını hedefleyerek (örneğin, Mozilla 'e özgü olan öğeleri kaldırma) sıkıştırma işlemini geliştirebilirsiniz istek IE 'den geldiğinde).

Bu alıştırmada, ASP.NET 4,5 ' de farklı paketleme ve küçültme türlerini nasıl etkinleştireceğinizi ve kullanacağınızı öğreneceksiniz.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>Görev 1-NuGet 'den paketleme ve Minbirleşme paketini yükleme

1. Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.
2. NuGet Paket Yöneticisi konsolunu açın. Bunu yapmak için, **diğer Windows** | **paket Yöneticisi konsolu** | menü **görünümünü** kullanın.

    ![Paket Yöneticisi file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole açılıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Paket Yöneticisi konsolunu açma")

    *Paket Yöneticisi konsolunu açma*
3. **Paket Yöneticisi konsolunda** **Install-Package Microsoft. Web. Optimization** yazın ve **ENTER**tuşuna basın.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>Görev 2-varsayılan demeti

Paketleme ve minmate kullanmanın en basit yolu, varsayılan paketleri etkinleştirmektir. Bu yöntem, bir klasördeki JS ve CSS dosyaları için paketlenmiş ve küçültülmüş sürüme başvuru yapmanızı sağlamak için kuralları kullanır.

Bu görevde, paketlenmiş ve küçültülmüş JS ve CSS dosyalarını nasıl etkinleştirip başvurulacağını ve elde edilen çıktıyı görüntülemenize öğreneceksiniz.

1. Zaten açık değilse, **Visual Studio 'yu** başlatın ve bu laboratuvarın **Source\WhatsNewASPNET** klasöründe bulunan **WhatsNewASPNET. sln** çözümünü açın.
2. **Çözüm Gezgini**, **Styles**, **scripts\custom** ve **scripts\demeti** klasörlerini genişletin.

    Uygulamanın birden fazla CSS ve JS dosyası kullandığını unutmayın.

    ![Uygulamada birden çok stil sayfaları ve JavaScript dosyası](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Uygulamada birden çok stil sayfaları ve JavaScript dosyası")

    *Uygulamada birden çok stil sayfaları ve JavaScript dosyası*
3. **Global.asax.cs** dosyasını açın.

    Yeni **Microsoft. Web. Optimization** ad alanının, dosyanın başlangıcında yorum oluşturulduğuna dikkat edin. Paketleme ve küçültmeye yönelik özellikleri eklemek için using yönergesinin açıklamasını kaldırın.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. **Uygulama\_start** metodunu bulun.

    Bu yöntemde, aşağıdaki kod parçacığında gösterildiği gibi Enabledefaultdemeti çağrısının açıklamasını kaldırın. Bu, söz konusu klasörün yolunu ve &quot;CSS&quot; ya da &quot;JS&quot; sonekini kullanarak bir klasördeki CSS dosyalarının paketlenmiş bir koleksiyonuna başvurmamızı sağlar.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. **Optimizasyon. aspx** dosyasını açın ve **headcontent**denetiminin içerik denetimini bulun.

    CSS dosyalarına ve JS dosyalarına başvurulan tek bir etiket olduğuna dikkat edin.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > Bu kod tanıtım amaçlıdır. İdeal olarak, site. master dosyasındaki paketlerdir. Bu örnek kodda, bazı paketlenmiş dosyalara da site. master dosyası tarafından başvurulduğunu ve bu son başvurunun gereksiz olduğunu fark edersiniz.
6. Bağlantıların, sırasıyla Styles ve Scripts\custom klasöründen tüm CSS veya JS dosyalarını almak için **href** özniteliğinde paketleme kurallarını kullandığını unutmayın.

    **Komut dosyaları/özel** klasör IÇINDEKI tüm JS dosyalarını paketleyip daha fazla kullanmak için aşağıda gösterildiği gibi **komut dosyalarını/özel/JS** yolunu kullanabilirsiniz. Varsayılan değer olan varsayılan davranıştır.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. **Styles\site.exe** dosyasını açın.

    Özgün CSS dosyasının girintili kod, boş alanlar ve dosyayı büyüten Yorumlar içerdiğini unutmayın. (Ayrıca, JavaScript dosyası boş boşluklar ve açıklamalar içerir).

    ![Betikler klasöründeki özgün CSS dosyalarından biri](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Betikler klasöründeki özgün CSS dosyalarından biri")

    *Betikler klasöründeki özgün CSS dosyalarından biri*
8. **F5** tuşuna basarak uygulamayı çalıştırın ve **iyileştirme** sayfasına gidin.
9. Dosyayı indirmek ve açmak için **CSS paketi** bağlantısına tıklayın.

    Küçültülmüş olan paketlenmiş dosyaya göz atın. Tüm boş boşlukların, yorumların ve girintileme karakterlerinin kaldırıldığını, daha küçük bir dosya oluşturduğunu fark edeceksiniz.

    ![Paketlenmiş CSS dosyaları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Paketlenmiş CSS dosyaları")

    *Paketlenmiş CSS dosyaları*
10. Şimdi, JavaScript paketlenmiş dosyasını açmak için **js paket** bağlantısına tıklayın. Gezgin uyarısını güvenle yoksayabilirsiniz. **Özel** klasör altındaki JavaScript dosyalarının da paketlenmiş ve küçültülmüş olduğunu fark edebilirsiniz.

    ![Paketlenmiş JavaScript dosyaları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Paketlenmiş JavaScript dosyaları")

    *Paketlenmiş JavaScript dosyaları*

    CSS veya JS dosyaları için sıkıştırmayı etkinleştirmek, önceki ASP.NET sürümünde çok daha karmaşıktır. Artık gördüğünüz gibi, paketlemeyi etkinleştirmek için *Global. asax* dosyasına bir satır eklemeniz ve sonra sitenizdeki paketlenmiş dosyalara başvurmanız yeterlidir.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>Görev 3-statik demeti

Statik paket yaklaşımı, kullanılacak dosya kümesini, başvuruyu ve kullanılacak minbirleşme yöntemini özelleştirmenize olanak sağlar.

Bu görevde, bir statik paketi, paketleyip daha sonra ayarlanacak belirli bir dosya kümesini tanımlayacak şekilde yapılandıracaksınız.

1. Tarayıcıyı kapatın.
2. **Global.asax.cs** dosyasını açın ve **uygulama\_start** metodunu bulun.
3. Aşağıdaki kodda gösterildiği gibi statik paket kodunun açıklamasını kaldırın.

    &quot; **~/Staticdemeti**&quot; sanal yol ile başvurulacak bir statik paket tanımlıyor ve tüm belirtilen dosyaları **AddFile** yöntemiyle birlikte kullanmak Için **jsminbelirt** komutunu kullanın. Son olarak, statik demeti **paketleme** ve olanaklı hale getirecek olursunuz.

    Dosyaların aynı yerde olmadığına dikkat edin; Bu, varsayılan paketlemeye göre başka bir avantajdır.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. **Optimizasyon. aspx** dosyasını açın.

    **STATIK js demeti** bağlantısının, Global.asax.cs dosyasındaki statik paketi yapılandırırken bildirdiğiniz yolu kullandığını ve **/staticdemeti**olduğunu unutmayın.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. Uygulamayı çalıştırmak için **F5** tuşuna basın ve ardından **iyileştirme** sayfasına gidin.
6. Dosyayı açmak için **STATIC js paket** bağlantısına tıklayın.

    Küçültülmüş olan paketlenmiş JavaScript dosyasının, &quot;/Staticdemeti&quot;yolu altındaki statik paket dosyasında yapılandırılan tüm JavaScript dosyaları için çıkış olduğunu unutmayın.

    ![Statik JavaScript dosyaları demeti](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Statik JavaScript dosyaları demeti")

    *Statik JavaScript dosyaları demeti*
7. Tarayıcıyı kapatın ve Visual Studio 'ya geri dönün.

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>Görev 4-dinamik klasör demeti

Bu görevde, dinamik klasör paketlerini yapılandırmayı öğreneceksiniz. Dinamik paket oluşturma işleminin gücü, statik JavaScript 'in yanı sıra JavaScript 'e derlenen dillerdeki diğer dosyaları da dahil edebilir ve bu nedenle, paket yürütülmeden önce bazı işlemler yapılmasını gerektirir.

Bu örnekte, CofeeScript içinde yazılmış dosyalar için dinamik bir paket oluşturmak üzere **Dynamicfolderdemeti** sınıfını nasıl kullanacağınızı öğreneceksiniz. CofeeScript, JavaScript 'e derlenen ve JavaScript kodunu yazmak, JavaScript 'in kısaltma ve okunabilirliğini geliştirmek için daha basit bir sözdizimi sağlayan bir programlama dilidir.

1. **Global.asax.cs** dosyasını açın ve **uygulama\_start** metodunu bulun.
2. Aşağıdaki kodda gösterildiği gibi dinamik paket kodunun açıklamasını kaldırın.

    Yalnızca &quot; **. kahve**&quot; uzantısı (CoffeeScript dosyaları) olan dosyalara uygulanacak olan **CoffeeMinify** özel minbirleşme işlemcisini kullanacak dinamik bir klasör paketi tanımlamanız gerekir. '\*. kahve ' gibi bir klasör içinde paketedilecek dosyaları seçmek için bir arama kalıbı kullanacağınızı unutmayın.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. NuGet Paket Yöneticisi konsolunu açın. Bunu yapmak için, **diğer Windows** | **paket Yöneticisi konsolu** | menü **görünümünü** kullanın.
4. **Paket Yöneticisi konsolunda** **Install-Package CoffeeSharp** yazın ve **ENTER**tuşuna basın.
5. **Çözüm Gezgini** penceresindeki **tüm dosyaları göster** düğmesine tıklayın

    ![Tüm dosyalar gösteriliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Tüm dosyalar gösteriliyor")

    *Tüm dosyalar gösteriliyor*
6. **Çözüm Gezgini** **CoffeeMinify.cs** dosyasına sağ tıklayın ve **projeye dahil et** ' i seçin

    ![CoffeeMinify.cs dosyasını projeye dahil et](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "CoffeeMinify.cs dosyasını projeye dahil et")

    *CoffeeMinify.cs dosyasını projeye dahil et*
7. **CoffeeMinify.cs** dosyasını açın.

    Bu sınıf, CoffeeScript kod derlemesinden kaynaklanan JavaScript çıkışını minmek için Jsminbelirt 'ten devralır. Önce JavaScript kodunu oluşturmak için CoffeeScript derleyicisini çağırır ve sonra ortaya çıkan kodu minsminbelirt. Process yöntemine gönderir.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. **Betikler/paket** klasöründen **Script1. kahve** ve **Script2. kahve** dosyalarını açın.

    Bu dosyalar, CoffeeMinify sınıfı ile paketleme gerçekleştirilirken derlenecek CoffeScript kodunu içerir.

    Kolaylık sağlamak için, belirtilen CoffeeScript dosyaları yalnızca CoffeeScript örnek kodu dahil edilmiştir. Yorumlar, Jsminbelirt işlemi tarafından dışlanır.

    ![CoffeeScript dosyaları](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "CoffeeScript dosyaları")

    *CoffeeScript dosyaları*

    > [!NOTE]
    > [Cofeescript](https://github.com/jashkenas/coffeescript/) , JavaScript kodu yazmak, JavaScript 'in breçekimi ve okunabilirliğini geliştirmek için daha basit bir sözdizimi sağlar ve dizi kavrama ve model eşleştirme gibi diğer özellikleri de ekler.
9. **Optimizasyon. aspx** dosyasını açın ve paket bağlantılarını bulun.

    **Dınamık js demeti** bağlantısının, dinamik klasör paketi için yapılandırdığınız **/Coffee** sonekini kullanarak **betikler/paket** klasörüne başvurduğuna dikkat edin.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. Uygulamayı çalıştırmak için **F5** tuşuna basın ve ardından **iyileştirme** sayfasına gidin.
11. Oluşturulan dosyayı açmak için **dınamık js paketi** bağlantısına tıklayın.

    Bu pakete eklenen içeriğin yalnızca **. kahve** dosyaları içerdiğini unutmayın. Ayrıca, CoffeeScript kodunun JavaScript 'e derlendiğini ve açıklamalı hatların kaldırıldığını de görebilirsiniz.

    ![Dinamik JS dosya demeti](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Dinamik JS dosya demeti")

    *Dinamik JS dosya demeti*

> [!NOTE]
> Ek olarak, bu uygulamayı Microsoft Azure Web siteleri ' ne ek [B: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixB)için de dağıtabilirsiniz.

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu laboratuvar, Visual Studio 2012 ' de ASP.NET ve Web geliştirme 'daki yenilikleri ve Visual Studio 2012 ' deki çeşitli geliştirmelerden nasıl yararlanabilmenizi sağlar.

Bu uygulamalı Laboratuvarı tamamlayarak, CSS, JavaScript ve HTML için Visual Studio 2012 düzenleyicilerde yeni özellik ve geliştirmeleri nasıl kullanacağınızı öğrenirsiniz. Ayrıca, Visual Studio 2012 'nin yerleşik paketleme ve küçültmeye nasıl uyguladığı hakkında bilgi edinirsiniz.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *Web için VS Express kutucuğu*

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Ek B: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama

Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma

1. [Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.

    > [!NOTE]
    > Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz. [Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.

    ![Windows Azure portal oturum açın](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Windows Azure portal oturum açın")

    *Windows Azure 'da oturum açma Yönetim Portalı*
2. Komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web sitesi oluşturma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Yeni bir Web sitesi oluşturma")

    *Yeni bir Web sitesi oluşturma*
3. **İşlem** | **Web sitesi**' ne tıklayın. Sonra **hızlı oluştur** seçeneğini belirleyin. Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.

    > [!NOTE]
    > Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar. Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar. Bir veritabanı ayarlamaya yönelik adımları içermez.

    ![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")

    *Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*
4. Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.
5. Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın. Yeni Web sitesinin çalışıp çalışmadığını denetleyin.

    ![Yeni Web sitesine göz atma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Yeni Web sitesine göz atma")

    *Yeni Web sitesine göz atma*

    ![Web sitesi çalışıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Web sitesi çalışıyor")

    *Web sitesi çalışıyor*
6. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.

    ![Web sitesi yönetim sayfalarını açma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Web sitesi yönetim sayfalarını açma")

    *Web sitesi yönetim sayfalarını açma*
7. **Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.

    > [!NOTE]
    > *Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir. Yayımlama profili, bir yayımlama yönteminin etkinleştirildiği her bir uç noktasına bağlanmak ve kimlik doğrulaması yapmak için gereken URL'leri, kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir. **Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.

    ![Web sitesi yayımlama profili indiriliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Web sitesi yayımlama profili indiriliyor")

    *Web sitesi yayımlama profili indiriliyor*
8. Yayımlama profili dosyasını bilinen bir konuma indirin. Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.

    ![Yayımlama profili dosyası kaydediliyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Yayımlama profili kaydediliyor")

    *Yayımlama profili dosyası kaydediliyor*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Görev 2-veritabanı sunucusunu yapılandırma

Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir. SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.

1. Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır. SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz. Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz. **Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın. Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.

    ![SQL veritabanı sunucu panosu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "SQL veritabanı sunucu panosu")

    *SQL veritabanı sunucu panosu*
2. Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir. Bunu yapmak için **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın. Kural için bir ad girin ve Add-Client-ip-Address-ok-Button](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) düğmesine ![tıklayın.

    ![Istemci IP adresi ekleniyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *Istemci IP adresi ekleniyor*
3. **ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.

    ![Değişiklikleri Onayla](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *Değişiklikleri Onayla*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama

1. ASP.NET MVC 4 çözümüne geri dönün. **Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.

    ![Uygulama yayımlanıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Uygulamayı Yayımlama")

    *Web sitesi yayımlanıyor*
2. İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.

    ![Yayımlama profilini içeri aktarma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Yayımlama profilini içeri aktarma")

    *Yayımlama profili içeri aktarılıyor*
3. **Bağlantıyı doğrula**' ya tıklayın. Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.

    > [!NOTE]
    > Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.

    ![Bağlantı doğrulanıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Bağlantı doğrulanıyor")

    *Bağlantı doğrulanıyor*
4. **Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.

    ![Web dağıtımı yapılandırması](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Web dağıtımı yapılandırması")

    *Web dağıtımı yapılandırması*
5. Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:

   - **Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.
   - **Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.
   - **Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.
   - Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.

     ![Hedef bağlantı dizesi yapılandırılıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Hedef bağlantı dizesi yapılandırılıyor")

     *Hedef bağlantı dizesi yapılandırılıyor*
6. Daha sonra, **Tamam**'a tıklayın. Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Veritabanı oluşturma](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Veritabanı dizesi oluşturuluyor")

    *Veritabanı oluşturma*
7. Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir. Ardından **İleri**'ye tıklayın.

    ![SQL veritabanı 'na işaret eden bağlantı dizesi](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "SQL veritabanı 'na işaret eden bağlantı dizesi")

    *SQL veritabanı 'na işaret eden bağlantı dizesi*
8. **Önizleme** sayfasında **Yayımla**' ya tıklayın.

    ![Web uygulaması yayımlanıyor](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Web uygulaması yayımlanıyor")

    *Web uygulaması yayımlanıyor*
9. Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.

    ![Windows Azure 'da yayımlanan uygulama](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Windows Azure 'da yayımlanan uygulama")

    *Windows Azure 'da yayımlanan uygulama*
