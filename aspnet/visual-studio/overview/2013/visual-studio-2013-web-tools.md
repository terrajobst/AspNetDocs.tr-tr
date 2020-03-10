---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 'Uygulamalı laboratuvar: Visual Studio 2013 web araçları | Microsoft Docs'
author: rick-anderson
description: Visual Studio, için mükemmel bir geliştirme ortamıdır. NET tabanlı Windows ve Web projeleri. Bu, kolayca kullanılabilecek güçlü bir metin Düzenleyicisi içerir...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622677"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a>Uygulamalı Laboratuvar: Visual Studio 2013 Web Araçları

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

> Visual Studio, için mükemmel bir geliştirme ortamıdır. NET tabanlı Windows ve Web projeleri. Bu, bir proje olmadan tek başına dosyaları düzenlemek için kolayca kullanılabilecek güçlü bir metin Düzenleyicisi içerir.
> 
> Visual Studio, her dosyayı düzenlerken tam özellikli bir ayrıştırma ağacı sağlar. Bu, Visual Studio 'Nun, geliştirme deneyimini çok daha hızlı ve daha fazla zevk hale getirerek benzersiz otomatik tamamlama ve belge tabanlı eylemler sağlamasına olanak tanır. Bu özellikler özellikle HTML ve CSS belgelerinde etkilidir.
> 
> Bu gücün hepsi, uzantılar için de kullanılabilir ve bu da düzenleyicilerin gereksinimlerinize uyacak şekilde güçlü yeni özelliklerle genişlemelerini kolaylaştırır. Web Essentials, Visual Studio 'Da Web ile ilgili geliştirmelerin (çoğunlukla) bir koleksiyonudur. Çok sayıda yeni IntelliSense tamamlamaları (özellikle CSS için), yeni tarayıcı bağlantısı özellikleri, JavaScript dosyaları için otomatik JSHint, HTML ve CSS için yeni uyarılar ve modern web geliştirme için gerekli olan diğer birçok özellik içerir.
> 
> Tüm örnek kod ve kod parçacıkları [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.

<a id="Overview"></a>
## <a name="overview"></a>Genel bakış

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Zengin HTML5 kod parçacıkları ve Zen kodlama gibi Web Essentials 'ta bulunan yeni HTML düzenleyici özelliklerini kullanın
- Renk Seçicisi ve tarayıcı matrisi araç ipucu gibi Web temelleri 'nde bulunan yeni CSS Düzenleyici özelliklerini kullanın
- Dosyaya Ayıkla ve tüm HTML öğeleri için IntelliSense gibi Web temelleri 'nde bulunan yeni JavaScript Düzenleyici özelliklerini kullanın
- Tarayıcı bağlantısı kullanarak tarayıcınızla ve Visual Studio arasında veri alışverişi

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) veya üzeri
- [Web temelleri 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.

1. Bir Windows Explorer penceresi açın ve laboratuvarın **kaynak** klasörüne gidin.
2. Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.
3. Kullanıcı hesabı denetimi iletişim kutusu gösterilirse, devam etmek için eylemi onaylayın.

> [!NOTE]
> Kurulumu çalıştırmadan önce bu laboratuvarın tüm bağımlılıklarını denetlediğinizden emin olun.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Kod parçacıklarını kullanma

Laboratuvar belgesi boyunca kod blokları eklemeniz istenir. Kolaylık olması için, bu kodun çoğu Visual Studio Code kod parçacığı olarak sağlanır ve bu, el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio 2013 içinden erişebilirsiniz.

> [!NOTE]
> Her alıştırma, her alıştırmanın bağımsız olarak her birini takip etmenizi sağlayan alıştırmanın **BEGIN** klasöründe bulunan bir başlangıç çözümüdür. Lütfen bir alıştırma sırasında eklenen kod parçacıklarının bu başlangıç çözümlerinde eksik olduğunu ve Alıştırmayı tamamlayana kadar çalışmadığının farkında olun. Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir **son** klasör de bulacaksınız. Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.

---

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:

1. [Tarayıcı bağlantısı ve Web temel bileşenleri ile çalışma](#Exercise1)
2. [Kod parçacıkları ve IntelliSense avantajlarından yararlanma](#Exercise2)

> [!NOTE]
> Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir. Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler. Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır. Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>Alıştırma 1: tarayıcı bağlantısı ve Web temel bileşenleri ile çalışma

**Web temel** bileşenleri, modern web geliştirme için pek çok yararlı özellik ekleyen, genellikle Web geliştirme deneyiminin çok daha hızlı ve daha fazla zevk hale getirilmesi için kullanabileceğiniz bir Visual Studio uzantısıdır. Web Essentials 'ı Visual Studio 'daki uzantı galerisinden yükleyebilirsiniz.

**Tarayıcı bağlantısı** , VISUAL Studio IDE ve Visual Studio ile veri alışverişi yapmak için herhangi bir açık tarayıcı arasında bir kanal sağlayan yeni bir özelliktir Visual Studio 2013. Web Essentials, tarayıcı bağlantısını, DOM nesne modelini ve Web sayfalarınızın CSS stillerini doğrudan tarayıcıdan işlemek için araçlar ile genişletir.

Bu alıştırmada, **Web Essentials** ve **tarayıcı bağlantısı** tarafından desteklenen özelliklerden bazılarını inceleyerek basit bir test sayfasını geliştirebilirsiniz.

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>Görev 1-birden çok tarayıcıda projeyi çalıştırma

Bu görevde, Web uygulamanızı birden çok tarayıcıda çalışacak şekilde yapılandıracaksınız, bu, tarayıcılar arası testler için kullanışlıdır.

1. **Microsoft Visual Studio**açın.
2. **Dosya** menüsünde Aç ' ı seçin **| Proje/çözüm...** ve laboratuvarın **kaynak** klasöründe **Ex1-WorkingwithBrowserLinkandWebEssentials\Begin** (C:\WebCampsTK\HOL\VSWebTooling\Source) konumuna gidin. **Başlat. sln** ' yi seçin ve **Aç**' a tıklayın.
3. Visual Studio araç çubuğunda tarayıcı menüsünü genişletin ve **Bununla birlikte araştır...** seçeneğini belirleyin.

    ![Menü seçeneği Ile araştır](visual-studio-2013-web-tools/_static/image1.png "İle araştır... tarayıcı menüsünde")

    *Menü seçeneği Ile araştır*
4. **Ile araştır** iletişim kutusunda, **CTRL** tuşunu basılı tutarak ve **Varsayılan olarak ayarla**' ya tıklayarak **Google Chrome** ve **Internet Explorer** ' ı seçin.

    ![İletişim kutusu ile araştır](visual-studio-2013-web-tools/_static/image2.png "İletişim kutusu ile araştır")

    *Birden çok varsayılan tarayıcı seçme*
5. Artık Google Chrome ve Internet Explorer varsayılan tarayıcılar olarak görünmelidir. İletişim kutusunu kapatmak için **iptal** ' e tıklayın.

    ![Google Chrome ve Internet Explorer varsayılan tarayıcılar olarak](visual-studio-2013-web-tools/_static/image3.png "Google Chrome ve Internet Explorer varsayılan tarayıcıları")

    *Google Chrome ve Internet Explorer varsayılan tarayıcılar olarak*

    > [!NOTE]
    > Varsayılan tarayıcıları yapılandırdıktan sonra, tarayıcı menüsünde **birden çok tarayıcı** seçeneği seçilidir.
    > 
    > ![Birden çok tarayıcı](visual-studio-2013-web-tools/_static/image4.png "Birden çok tarayıcı")
6. Uygulamayı hata ayıklamadan çalıştırmak için **CTRL** + **F5** tuşuna basın.
7. Her iki tarayıcı penceresi açık olduğunda, her iki tarayıcıda da aynı anda güncelleştirmeleri görmek için bunlardan birini diğerinin üzerine yerleştirin. Tarayıcılar açık mavi dikdörtgenle bir Web sayfası görüntülemelidir.

    ![Diğerinin üzerine bir tarayıcı yerleştirme](visual-studio-2013-web-tools/_static/image5.png "Diğerinin üzerine bir tarayıcı yerleştirme")

    *Diğerinin üzerine bir tarayıcı yerleştirme*
8. Tarayıcıları kapatmayın. Bunları bir sonraki görevde kullanacaksınız.

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>Görev 2-HTML öğeleri oluşturmak için Zen kodlaması kullanma

**Zen kodlaması** , kodlama ve düzenleme için yüksek hızlı HTML, XML, XSL (veya başka bir yapılandırılmış kod biçimi) için bir düzenleyici eklentisidir. Bu eklentinin çekirdeği, CSS seçicilerinin HTML koduna benzer ifadeler genişletmenizi sağlayan güçlü bir kısaltma altyapısıdır. Zen kodlaması, CSS stil Seçicisi sözdizimi kullanarak HTML yazmanın hızlı bir yoludur.

Bu alıştırmada, sorunun seçeneklerini temsil eden HTML düğmelerini oluşturmak için Web Essentials tarafından sunulan Zen kodlama özelliğini kullanacaksınız.

1. Visual Studio 'ya geri dönün.
2. **Görünümler** | **giriş** klasöründe bulunan **Index. cshtml** dosyasını açın.
3. **&lt;!--TODO: aşağıdaki kodla açıklama ekleyin--&gt;** yazın ve **Tab**tuşuna basın.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. Kod HTML olarak genişletilmelidir.

    ![Genişletilmiş HTML](visual-studio-2013-web-tools/_static/image6.png "Genişletilmiş HTML")

    *Genişletilmiş HTML*

    > [!NOTE]
    > Zen kodlama sözdizimi hakkında daha fazla bilgi edinmek için aşağıdaki [makaleye](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/)bakın.
5. Her iki tarayıcıyı da güncelleştirmek için **bağlı tarayıcıları Yenile** düğmesine tıklayın.

    ![Bağlı tarayıcıları Yenile](visual-studio-2013-web-tools/_static/image7.png "Bağlı tarayıcıları Yenile")

    *Bağlı tarayıcıları Yenile*

    ![Internet Explorer-sayfa dört düğme ile güncelleştirildi](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer-sayfa dört düğme ile güncelleştirildi")

    *Internet Explorer-sayfa dört düğme ile güncelleştirildi*

    ![Google Chrome-sayfa dört düğme ile güncelleştirildi](visual-studio-2013-web-tools/_static/image9.png "Google Chrome-sayfa dört düğme ile güncelleştirildi")

    *Google Chrome-sayfa dört düğme ile güncelleştirildi*
6. Visual Studio 'ya geri dönün.
7. Düğmeleri sayfaya eklediniz, ancak yine de bir şablon sorusu eklemeniz gerekiyor. Bunu yapmak için, Web Essentials 'ta **Lorem Ipsum Generator**adlı yeni bir özellik kullanacaksınız. **Sınıf** özniteliği **önünde** **div** öğesini bulun.
8. Aşağıdaki kodu **div**öğesinin ilk alt öğesi olarak ekleyin ve **Tab**tuşuna basın.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. Kod HTML olarak genişletilmelidir.

    ![Lorem Ipsum otomatik olarak oluşturulur](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum otomatik olarak oluşturulur")

    *Lorem Ipsum otomatik olarak oluşturulur*

    > [!NOTE]
    > Zen kodlama kapsamında artık doğrudan HTML düzenleyicisinde Lorem Ipsum kodu oluşturabilirsiniz. **Lorem** ve hit **sekmesini** yazmanız yeterlidir ve bir 30 sözcük Lorem Ipsum metni eklenecektir. Örneğin *lorem10* 10 Lorem Ipsum sözcüklerini ekler.
10. Web Essentials 'ta **lorem pixel Oluşturucu**adlı başka bir yeni özellik kullanarak, sorunun en üstüne bir logo ekleyeceksiniz. Aşağıdaki **kodu, Container öğesinin ilk** alt öğesi olarak **kapsayıcı** **sınıf** değeri olarak ekleyin ve **Tab**tuşuna basın.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. Kod HTML olarak genişletilmelidir.

    ![Lorem piksel otomatik olarak oluşturulur](visual-studio-2013-web-tools/_static/image11.png "Lorem piksel otomatik olarak oluşturulur")

    *Lorem piksel otomatik olarak oluşturulur*

    > [!NOTE]
    > Zen kodlama kapsamında, doğrudan HTML düzenleyicisinde Lorem pixel kodu da oluşturabilirsiniz. Yalnızca **PIX-200x200-hayvanlar** ve vuruş **sekmesine** ve bir hayvan 'nin 200x200 görüntüsüne sahip bir **img** etiketi eklenecektir. Daha fazla bilgi için [lorem pixel](http://www.lorempixel.com)bölümüne bakın.
12. Her iki tarayıcıyı da güncelleştirmek için **bağlı tarayıcıları Yenile** düğmesine tıklayın.

    ![Internet Explorer-otomatik olarak görüntü ve metin](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer-otomatik olarak görüntü ve metin")

    *Internet Explorer-otomatik olarak görüntü ve metin*

    ![Google Chrome-otomatik oluşturulan görüntü ve metin](visual-studio-2013-web-tools/_static/image13.png "Google Chrome-otomatik oluşturulan görüntü ve metin")

    *Google Chrome-otomatik oluşturulan görüntü ve metin*

    > [!NOTE]
    > Kod parçacığı eklenirken görüntü rastgele seçildiğinden, tarayıcılarda gösterilen resim farklı olabilir.
13. Tarayıcıları kapatmayın. Bunları bir sonraki görevde kullanacaksınız.

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>Görev 3-stil özelliğini güncelleştirme

Bu görevde, belirli DOM öğesinin oluşturulduğu konumun tam konumunu tespit etmek ve ardından Web Essentials tarafından sunulan bir renk seçici kullanarak söz konusu öğenin Color özelliğini güncellemek için tarayıcı bağlantısının **Inceleme modu** özelliğini kullanacaksınız.

1. Internet Explorer tarayıcısında, Inceleme modunu etkinleştirmek için **CTRL** + **alt** + **I** tuşlarına basın.
2. İşaretçiyi açık mavi kenarlığının üzerine taşıyın ve öğesine tıklayın.

    ![İşaretçiyi açık mavi kenarlık üzerine taşıma](visual-studio-2013-web-tools/_static/image14.png "İşaretçiyi açık mavi kenarlık üzerine taşıma")

    *İşaretçiyi açık mavi kenarlık üzerine taşıma*
3. Visual Studio 'ya geri dönün. Tarayıcıda seçtiğiniz HTML öğesinin Visual Studio HTML düzenleyicisinde de seçili olduğunu unutmayın.

    ![Visual Studio HTML düzenleyicisinde seçili HTML öğesi](visual-studio-2013-web-tools/_static/image15.png "Visual Studio HTML düzenleyicisinde seçili HTML öğesi")

    *Visual Studio HTML düzenleyicisinde seçili HTML öğesi*
4. Şimdi, seçili öğenin stilini değiştirmek için **ön** CSS sınıfını güncelleşolursunuz. Bunu yapmak için **CTRL** +  **'** e basarak aramaya **Git** kutusunu açın. Dosyayı açmak için **site. css** yazın ve **ENTER** tuşuna basın.

    ![Dosya sitesi. css açılıyor](visual-studio-2013-web-tools/_static/image16.png "Dosya sitesi. css açılıyor")

    *Dosya sitesi. css açılıyor*
5. CSS seçiciyi bulmak için **CTRL** + **F** tuşlarına basın ve **. Flip-Container. Front** yazın.
6. Renk seçiciyi açmak için sınıfın Border özelliğindeki açık mavi kare öğesine tıklayın.

    ![Renk seçiciyi açma](visual-studio-2013-web-tools/_static/image17.png "Renk seçiciyi açma")

    *Renk seçiciyi açma*
7. Köşeli çift ayraç düğmesine tıklayıp yeni bir renk seçerek renk seçiciyi genişletin.

    ![Renk seçiciyi genişletme](visual-studio-2013-web-tools/_static/image18.png "Renk seçiciyi genişletme")

    *Renk seçiciyi genişletme*
8. Bağlı tarayıcıları yenilemek için **CTRL** + **alt** + **ENTER** tuşlarına basın.
9. Internet Explorer 'a geçin ve kenarlığın renginin nasıl değiştiğini unutmayın.

    ![Internet Explorer-kenarlık rengi güncelleştirildi](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer-kenarlık rengi güncelleştirildi")

    *Internet Explorer-kenarlık rengi güncelleştirildi*
10. Google Chrome 'a geçin ve kenarlığın renginin nasıl değiştiğini görürsünüz.

    ![Google Chrome-kenarlık rengi güncelleştirildi](visual-studio-2013-web-tools/_static/image20.png "Google Chrome-kenarlık rengi güncelleştirildi")

    *Google Chrome-kenarlık rengi güncelleştirildi*
11. Visual Studio 'ya geri dönün.
12. **Site. css** dosyasının sonuna gidin ve **. btn** seçicisini bulmak için **CTRL** + **F** tuşlarına basın.
13. **-WebKit-Border-Radius** özelliğinin yeşil renkte altı çizili olduğuna dikkat edin.

    ![-WebKit-Border-yarıçap özelliği btn Seçicisi](visual-studio-2013-web-tools/_static/image21.png "-WebKit-Border-yarıçap özelliği btn Seçicisi")

    *-WebKit-Border-yarıçap özelliği btn Seçicisi*
14. Giriş işaretini **-WebKit-Border-Radius** özelliğine yerleştirin. Özelliğin ilk sözcüğünün ilk harfinin altında mavi bir çizgi görünmelidir. Bu **akıllı etikettir**.
15. **CTRL** + tuşuna basın **.** Öneriler menüsünü açmak için **eksik standart özelliği Ekle (kenarlık-yarıçap)** seçeneğine tıklayın.

    ![Eksik standart özellik önerisi Ekle](visual-studio-2013-web-tools/_static/image22.png "Eksik standart özellik önerisi Ekle")

    *Eksik standart özellik önerisi Ekle*
16. **Border-Radius** özelliği CSS kuralına otomatik olarak eklenir.

    ![Eksik standart özellik eklendi](visual-studio-2013-web-tools/_static/image23.png "Eksik standart özellik eklendi")

    *Eksik standart özellik eklendi*
17. **Tarayıcı matris araç ipucunu**göstermek için işaretçiyi **Border-Radius** özelliğinin üzerine taşıyın. **Tarayıcı matrisi araç ipucu** , her tarayıcıda özelliğin kullanılabilirliğini gösterir.

    ![Tarayıcı matrisi araç ipucu](visual-studio-2013-web-tools/_static/image24.png "Tarayıcı matrisi araç ipucu")

    *Tarayıcı matrisi araç ipucu*
18. **Border-Radius** özelliğinin değerinin hala altı çizili olduğuna dikkat edin. Uyarı iletisini görmek için işaretçiyi değerin üzerine taşıyın.

    ![Border-RADIUS Özellik değeri uyarısı](visual-studio-2013-web-tools/_static/image25.png "Border-RADIUS Özellik değeri uyarısı")

    *Border-RADIUS Özellik değeri uyarısı*
19. Araç İpucu tarafından önerildiği şekilde **Border-Radius** özelliği değerinin birimini kaldırın.
20. **Sınır-yarıçap** , yuvarlatılmış kenarlık köşelerinin nasıl olduğunu tanımlamaya yönelik standart bir özelliktir, **-WebKit-Border-Radius** özelliğini ve değeri CSS kuralından kaldırabilirsiniz.
21. Giriş işaretini **Word Wrap** özelliğine yerleştirin ve akıllı etiketin aşağıda da göründüğünü unutmayın.
22. Menüyü açın ve **eksik satıcı Özellikleri Ekle**' ye tıklayın.

    ![Eksik satıcı özellikleri önerisi Ekle](visual-studio-2013-web-tools/_static/image26.png "Eksik satıcı özellikleri önerisi Ekle")

    *Eksik satıcı özellikleri önerisi Ekle*
23. **-MS-Word-Wrap** özelliği CSS kuralına otomatik olarak eklenir.

    ![Satıcıya özgü özellik eklendi](visual-studio-2013-web-tools/_static/image27.png "Satıcıya özgü özellik eklendi")

    *Satıcıya özgü özellik eklendi*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>Görev 4-tarayıcıdan HTML kodu güncelleştiriliyor

Bu görevde, tarayıcı bağlantısının **tasarım modu** ÖZELLIĞINI kullanarak DOM nesnesini tarayıcıdan düzenleyebilir ve değişiklikleri Visual STUDIO 'daki HTML kaynak dosyasına aktaracaksınız.

1. Google Chrome 'da tasarım modunu etkinleştirmek için **CTRL** + **alt** + **D** tuşlarına basın.
2. İşaretçiyi **Lorem Ipsum dolor, amet** etiketinin üzerine taşıyın ve öğesine tıklayın.

    ![Soruyu düzenleniyor](visual-studio-2013-web-tools/_static/image28.png "Soruyu düzenleniyor")

    *Soruyu düzenleniyor*
3. Bir imleç görünmelidir. Özgün metni, *daha uzun bir soru yazarken nasıl görüneceğine benzer bir*şekilde değiştirin ve ardından tasarım modundan çıkmak için **ESC** tuşuna basın.

    ![Soru düzenlendi](visual-studio-2013-web-tools/_static/image29.png "Soru düzenlendi")

    *Soru düzenlendi*
4. Visual Studio 'ya geri dönün ve henüz açılmadıysa **Index. cshtml**dosyasını açın. **&lt;p&gt;** öğesinin iç metninin güncelleştirildiğinden emin olun.

    ![HTML sayfasında güncelleştirilmiş soru](visual-studio-2013-web-tools/_static/image30.png "HTML sayfasında güncelleştirilmiş soru")

    *HTML sayfasında güncelleştirilmiş soru*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>Görev 5-SEO Ilgili uyarıları gözden geçirme

**Arama motoru iyileştirmesi** (SEO), bir arama altyapısının sonuç listesinde bir Web sitesi sırası daha yüksek hale getirme işlemidir. Site ne kadar yüksek olursa ve daha tutarlı bir şekilde listeleniyorsa, sitenin ilgili arama altyapısından daha fazla ziyaretçi olur. Web Essentials, HTML 'yi inceleyen, bulunan sorunları raporlayan ve bunları çözmek için yardım sağlayan bir analitik araç içerir.

1. **Görünüm** menüsüne gidin ve **hata listesi** ' ye tıklayarak **hata listesi** penceresini açın.

    ![Görünüm menüsündeki Hata Listesi](visual-studio-2013-web-tools/_static/image31.png "Görünüm menüsündeki Hata Listesi")

    *Görünüm menüsündeki Hata Listesi*
2. Sayfa açıklaması için bir **&lt;meta&gt;** etiketinin eksik olduğunu BILDIREN bir SEO uyarısı olduğuna dikkat edin. Bu çözümü onarmak için SEO uyarı girişine çift tıklayın.

    ![Hata Listesi penceresi](visual-studio-2013-web-tools/_static/image32.png "Hata Listesi penceresi")

    *Hata Listesi penceresi*
3. **Web Essentials** iletişim kutusunda, bir açıklama &lt;meta&gt; etiketi eklemek için **Evet** ' e tıklayın.

    ![Web Essentials iletişim kutusu](visual-studio-2013-web-tools/_static/image33.png "Web Essentials iletişim kutusu")

    *Web Essentials iletişim kutusu*
4. **Layout. cshtml\_** Düzenleyicisi açılır ve **&lt;meta&gt;** etiketi HTML dosyasının **baş** bölümüne otomatik olarak eklenir.

    ![Meta etiketi _Layout sayfasına otomatik olarak eklendi](visual-studio-2013-web-tools/_static/image34.png "Meta etiketi _Layout sayfasına otomatik olarak eklendi")

    *Meta etiketi \_düzen sayfasına otomatik olarak eklendi*
5. **İçerik** özniteliğinin değerini *geektest* olarak değiştirin ve dosyayı kaydedin.

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>Alıştırma 2: kod parçacıkları ve IntelliSense 'den yararlanın

Web Essentials ile HTML Düzenleyicisi, ek işlevlerle genişletilmiştir. Bu alıştırmada, Web uygulamaları geliştirirken yararlı olan bazı yeni özellikler göreceksiniz.

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>Görev 1-HTML belgelerinde IntelliSense kullanma

Bu görevde göreceğiniz ilk yeni özelliğe **dinamik IntelliSense**denir. Dinamik IntelliSense, kullanacağınız olası kimlikleri çıkarması için diğer etiketleri ve öznitelikleri okur.

Bu görevde, bir etiket ve bir giriş alanı içeren yeni bir HTML form öğesi oluşturacaksınız. Ardından etikete bağlamak için etiketine bir **for** özniteliği ekleyeceksiniz ve kapsamdaki girişlerin kimliklerine bağlı olarak IntelliSense önerilerini görürsünüz.

1. **Web için Visual Studio Express 2013** ve **kaynak/EX2-TakingAdvantageofCodeSnippetsandIntelliSense/BEGIN** klasöründe bulunan **BEGIN. sln** çözümünü açın. Alternatif olarak, önceki alıştırmada elde ettiğiniz çözüme devam edebilirsiniz.
2. **Çözüm Gezgini**' de, **Görünümler** | **giriş** klasöründe bulunan **Index. cshtml** dosyasını açın.
3. Aşağıdaki formu **&lt;section&gt;** öğesi içine ekleyin.

    (Kod parçacığı- *VisualStudio2013WebTooling* - *EX2* - *form*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. Giriş etiketinin önünde, alanın açıklamasını içeren bir etiket gelmelidir. Giriş etiketinden önce aşağıdaki etiketi ekleyin.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. **&lt;etiketinin** **for** özniteliği&gt;bir etiketin hangi form öğesine bağlandığını belirtir. Özniteliğin değeri ilgili öğenin kimliğine eşit olmalıdır. **For** özniteliğini **&lt;Label&gt;** öğesine ekleyin. Aşağıdaki şekilde gösterildiği gibi, &quot;adı&quot; değeri IntelliSense kutusunda, aynı kapsamdaki öğelerin kimliğine (kapsayan **&lt;formu&gt;** ) göre açılır.

    ![IntelliSense 'de kimliği gösterme](visual-studio-2013-web-tools/_static/image35.png "IntelliSense 'de kimliği gösterme")

    *IntelliSense 'de kimliği gösterme*
6. Son eklenen **&lt;form&gt;** öğesini ve içeriğini silin.

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>Görev 2-HTML kod parçacıkları kullanma

HTML5, 25 ' ten fazla yeni anlam etiketi sunmuştur. Visual Studio 'Da bu etiketler için IntelliSense desteği zaten vardı, ancak Visual Studio 2013 yeni kod parçacıkları ekleyerek biçimlendirme yazmayı daha hızlı ve kolay hale getirir. Bu Etiketler karmaşık olmasa da, *Ses* etiketi için doğru codec geri dönüşleri ekleme gibi birkaç küçük alt tleki daha vardır. Bu görevde, ses etiketi için HTML kod parçacıklarını görürsünüz.

1. **Index. cshtml** dosyasında, aşağıdaki şekilde gösterildiği gibi **&lt;bölümü&gt;** öğesi içinde **&lt;AUD** yazın.

    ![Ses öğesi ekleme](visual-studio-2013-web-tools/_static/image36.png "Ses öğesi ekleme")

    *Ses öğesi ekleme*
2. **Sekme** tuşuna iki kez basın ve aşağıdaki kodun sayfada nasıl eklendiği ve imlecin ilk kaynağın **src** özniteliğinde nasıl yerleştirildiği hakkında dikkat edin.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > **Sekme** tuşuna iki kez basarak kod parçacığı eklenir. Ses parçacığı, gelişmiş destek için iki kaynak dosyası ile *Ses* etiketinin standart kullanımını gösterir.
3. İkinci satırı silin ve Webkampstv Katana göster: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3)için aşağıdaki bağlantıyı kullanarak ilk satırın kaynağını güncelleştirin. Sonuç kodu aşağıda gösterilmiştir.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > Örnek olarak, *Katanaproje. mp3* kaynak dosyası kullanılır. İsterseniz başka bir kaynak kullanabilirsiniz.
4. Dosyayı kaydetmek için **CTRL** + **S** tuşuna basın.
5. Uygulamayı başlatmak için **CTRL** + **F5** tuşuna basın.
6. Uygulamaya bir ses oyuncusunun eklendiğine dikkat edin.

    ![Internet Explorer 'da ses oynatıcı](visual-studio-2013-web-tools/_static/image37.png "Internet Explorer 'da ses oynatıcı")

    *Internet Explorer 'da ses oynatıcı*

    ![Google Chrome 'da ses oynatıcı](visual-studio-2013-web-tools/_static/image38.png "Google Chrome 'da ses oynatıcı")

    *Google Chrome 'da ses oynatıcı*
7. Tarayıcıları kapatmayın. Bunları bir sonraki görevde kullanacaksınız.

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>Görev 3-JavaScript belgelerinde IntelliSense kullanma

Web Essentials 2013, stil sayfaları ve HTML sayfaları, kimlikler ve sınıf adlarının bir listesini oluşturur. Bu görevde, bu listelerin Web Essentials 2013 ' de JavaScript IntelliSense desteğini nasıl geliştirdikleri hakkında bilgi edineceksiniz.

1. **Index. cshtml** dosyasında, JavaScript kodu için bir **komut dosyası** etiketi tanımlamak üzere aşağıdaki kodu ekleyin.

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. **Komut dosyası** etiketinin içine, Ready geri çağırma işlevini tanımlamak için aşağıdaki kodu ekleyin.

    (Kod parçacığı- *VisualStudio2013WebTooling* - *EX2* - *readyfunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. Giriş işaretini **betik** etiketine yerleştirip **CTRL** + tuşuna basın **.** öneri menüsünü açmak için.
4. **Dosyaya Ayıkla**' ya tıklayın.

    ![JavaScript dosya önerisine Ayıkla](visual-studio-2013-web-tools/_static/image39.png "JavaScript dosya önerisine Ayıkla")

    *JavaScript dosya önerisine Ayıkla*
5. **Farklı kaydet** penceresinde, **komut dosyaları** klasörünü seçin, **init. js** dosyasını adlandırın ve **Kaydet**' e tıklayın.

    ![Pencere olarak kaydet](visual-studio-2013-web-tools/_static/image40.png "Pencere olarak kaydet")

    *Pencere olarak kaydet*

    > [!NOTE]
    > **İnit. js** dosyası oluşturulur ve betiğin içeriği dosyaya taşınır.
    > 
    > ![Init. js dosyası eklenen içerikle oluşturuldu](visual-studio-2013-web-tools/_static/image41.png "Init. js dosyası eklenen içerikle oluşturuldu")
    > 
    > *Init. js dosyası eklenen içerikle oluşturuldu*
6. **Index. cshtml** dosyasını açın ve betik etiketinin, **init. js** dosyasına yönelik bir başvuruya göre değiştirildiğini kontrol edin.

    ![Init. js html başvurusu](visual-studio-2013-web-tools/_static/image42.png "Init. js html başvurusu")

    *Init. js html başvurusu*
7. **Çözüm Gezgini** gidin ve **init. js** dosyasının çözüme otomatik olarak eklendiğinden emin olun.

    ![Çözüme dahil olan Init. js dosyası](visual-studio-2013-web-tools/_static/image43.png "Çözüme dahil olan Init. js dosyası")

    *Çözüme dahil olan Init. js dosyası*
8. **Hazırlık işlevi geri** aramasını güncelleştirmek için **Init. js** dosyasına dönün.
9. *Ready*öğesine geçirilen işlev geri çağırma tanımının içinde, tüm öğeleri belirli bir sınıf özniteliğine göre almak için aşağıdaki kodu ekleyin.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. **GetElementsByClassName** işlev çağrısının içindeki tırnak işaretleriyle **CTRL** + **boşluk** tuşlarına basın.

    ![GetElementsByClassName işlevi için IntelliSense gösteriliyor](visual-studio-2013-web-tools/_static/image44.png "GetElementsByClassName işlevi için IntelliSense gösteriliyor")

    *GetElementsByClassName işlevi için IntelliSense gösteriliyor*

    > [!NOTE]
    > IntelliSense 'in proje stil sayfalarında tanımlanan sınıfları gösterdiğini unutmayın.
11. Oluşturduğunuz satırı aşağıdaki kodla değiştirin.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. İmleci, **GetElementsByTagName** işlevindeki tekliflerin içinde **au** 'Dan sonra konumlandırın ve **CTRL** + **Space**tuşuna basın.

    ![GetElementByTagName yöntemi için IntelliSense gösteriliyor](visual-studio-2013-web-tools/_static/image45.png "GetElementByTagName yöntemi için IntelliSense gösteriliyor")

    *GetElementsByTagName yöntemi için IntelliSense gösteriliyor*
13. Listeden **&quot;ses&quot;** seçin ve **ENTER**tuşuna basın. Sonuç aşağıdaki şekilde gösterilmiştir.

    ![Ses öğeleri alınıyor](visual-studio-2013-web-tools/_static/image46.png "Ses öğeleri alınıyor")

    *Ses öğeleri alınıyor*
14. **Çözüm Gezgini**' de, **betikler** klasöründeki **init. js** dosyasını sağ tıklatın ve **Web Essentials** menüsünden **JavaScript dosyalarını minbelirt** ' i seçin.

    ![JavaScript dosyalarını minbelirt](visual-studio-2013-web-tools/_static/image47.png "JavaScript dosyalarını minbelirt")

    *JavaScript dosyalarını minbelirt*
15. Kaynak dosya değiştiğinde otomatik olarak küçültmeye izin istendiğinde **Evet**' e tıklayın.

    ![Otomatik küçültmeye yönelik uyarı etkinleştiriliyor](visual-studio-2013-web-tools/_static/image48.png "Otomatik küçültmeye yönelik uyarı etkinleştiriliyor")

    *Otomatik küçültmeye yönelik uyarı etkinleştiriliyor*

    > [!NOTE]
    > **İnit. min. js** oluşturulur ve **init. js** dosyasının bir bağımlılığı olarak eklenir.
    > 
    > ![Init. min. js dosyası oluşturuldu](visual-studio-2013-web-tools/_static/image49.png "Init. min. js dosyası oluşturuldu")
    > 
    > *Init. min. js dosyası oluşturuldu*
16. **İnit. min. js** dosyasını açın ve dosyanın küçültülmüş olduğuna dikkat edin.

    ![Init. min. js dosya içeriği](visual-studio-2013-web-tools/_static/image50.png "Init. min. js dosya içeriği")

    *Init. min. js dosya içeriği*
17. **İnit. js** dosyasında, tüm ses öğelerini oynatmak Için **GetElementsByTagName** işlev çağrısının altına aşağıdaki kodu ekleyin.

    (Kod parçacığı- *VisualStudio2013WebTooling* - *EX2* - *playaudioelements*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. Dosyayı kaydetmek için **CTRL** + **S** ' e tıklayın. Küçültülmüş dosya zaten açık olduğundan, dosyanın kaynak Düzenleyici dışında değiştirildiğini söyleyen bir iletişim kutusu görürsünüz. **Evet**'i tıklayın.

    ![Microsoft Visual Studio uyarısı](visual-studio-2013-web-tools/_static/image51.png "Microsoft Visual Studio uyarısı")

    *Microsoft Visual Studio uyarısı*
19. Dosyanın yeni kodla güncelleştirildiğinden emin olmak için **Init. min. js** dosyasına dönün.

    ![Init. min. js dosyası güncelleştirildi](visual-studio-2013-web-tools/_static/image52.png "Init. min. js dosyası güncelleştirildi")

    *Init. min. js dosyası güncelleştirildi*
20. **Tarayıcı bağlantısı yenileme** düğmesine tıklayın.
21. Her iki tarayıcı da yenilendiğinde, önceki görevde gördüğünüz ses oyuncuları otomatik olarak yürütülmeye başlayacaktır.

    ![Görünümde ses oynatıcı dahil](visual-studio-2013-web-tools/_static/image53.png "Görünümde ses oynatıcı dahil")

    *Görünümde ses oynatıcı dahil*

---

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak şu şekilde nasıl yapılacağını öğrendiniz:

- Zengin HTML5 kod parçacıkları ve Zen kodlama gibi Web Essentials 'ta bulunan yeni HTML düzenleyici özelliklerini kullanın
- Renk Seçicisi ve tarayıcı matrisi araç ipucu gibi Web temelleri 'nde bulunan yeni CSS Düzenleyici özelliklerini kullanın
- Dosyaya Ayıkla ve tüm HTML öğeleri için IntelliSense gibi Web temelleri 'nde bulunan yeni JavaScript Düzenleyici özelliklerini kullanın
- Tarayıcı bağlantısı kullanarak tarayıcınızla ve Visual Studio arasında veri alışverişi
