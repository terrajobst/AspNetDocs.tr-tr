---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Visual Studio 'da sayfa denetçisini kullanma 2012 | Microsoft Docs
author: rick-anderson
description: Bu uygulamalı laboratuvarda, Visual Studio 'da Web sayfası sorunlarını bulmak ve gidermek için kullanabileceğiniz yeni bir araç bulacaksınız-sayfa denetçisi. Sayfa denetçisi b... için yeni bir araçtır.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586256"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a>Visual Studio 2012'de Sayfa Denetçisini Kullanma

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

> Bu uygulamalı laboratuvarda, Visual Studio 'da Web sayfası sorunlarını bulmak ve gidermek için kullanabileceğiniz yeni bir araç bulacaksınız-sayfa denetçisi.
> 
> Sayfa denetçisi, tarayıcı tanılama araçlarını Visual Studio 'ya getiren ve tarayıcı, ASP.NET ve kaynak kodu arasında tümleşik bir deneyim sağlayan yeni bir araçtır. Doğrudan Visual Studio IDE içinde bir Web sayfası (HTML, Web Forms, ASP.NET MVC veya Web sayfaları) oluşturur ve hem kaynak kodu hem de elde edilen çıktıyı incelemenizi sağlar. Sayfa denetçisi, bir Web sitesini kolayca ayırmayı, sıfırdan hızlıca sayfa oluşturmayı ve sorunları hızlı bir şekilde tanılamayı sağlar.
> 
> Günümüzde, esnek ve ölçeklenebilir Web sitelerini zamanında ve ASP.NET MVC ve WebForms gibi bir şekilde oluşturan çok sayıda Web Çerçevelerimiz vardır. Diğer yandan, içerik, şablon tabanlı sayfalarda ve dinamik içerikte tasarımcı görünümünü desteklemediğinden, sayfalardaki sorunları bulmayı zorlaştırır. Bu nedenle, bir kullanıcıya nasıl göründüğünü görmek için bu web sitelerinin bir tarayıcıda açılması gerekir.
> 
> Web geliştiricileri, tarayıcıda düzenli olarak çalışan sorunları bulmak için dış araçlar kullanır. Ardından, IDE 'ye geri dönerek düzeltmeye başlar. IDE ile bu geri ve ileri etkinlik, tarayıcı ve profil oluşturma araçları verimsiz olabilir ve bazen bir sorunu yeniden oluşturmak istediğiniz her seferinde yeni bir dağıtım ve önbellek temizleme gerektirir.
> 
> Sayfa denetçisi, Birleşik bir özellikler kümesi kullanarak her iki dünyanın en iyi yanı sıra istemci (tarayıcı araçları) ve sunucu (ASP.NET ve kaynak kodu) arasında Web geliştirmede bir boşluk köprüleme.
> 
> Sayfa denetçisi 'ni kullanarak, kaynak dosyalardaki (sunucu tarafı kod dahil) hangi öğelerin tarayıcıda işlenecek HTML işaretlemesini üretdiğine bakabilirsiniz. Sayfa denetçisi ayrıca, tarayıcıda hemen yansıtılan değişiklikleri görmek için CSS özelliklerini ve DOM öğesi özniteliklerini değiştirmenize imkan tanır.
> 
> Bu uygulamalı laboratuvar, sayfa denetçisi özellikleri boyunca size kılavuzluk eder ve Web uygulamalarındaki sorunları gidermek için bunları nasıl kullanabileceğinizi gösterir. **Bu laboratuvar, benzer akışlar kullanan ancak farklı teknolojileri hedefleyen iki alıştırmada bulunur. Bir ASP.NET MVC geliştiricisiyseniz, alıştırma yapın; bir WebForms geliştiriciyseniz, Alıştırmayı iki izleyin**.
> 
> Bu laboratuvar, daha önce kaynak klasörde sunulan örnek bir Web uygulamasına küçük değişiklikler uygulayarak açıklanan geliştirmeler ve yeni özellikler konusunda size kılavuzluk eder.
> 
> Tüm örnek kod ve kod parçacıkları [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409)adresinden erişilebilen Web Camps eğitim seti ' ne dahildir.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Sayfa denetçisini kullanarak bir Web sitesini kaldırma
- Sayfa denetçisi ile CSS stilleri değişikliklerini İnceleme ve Önizleme
- Sayfa denetçisi 'ni kullanarak Web sayfalarınızdaki sorunları algılayın ve giderin

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:

- [Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek A](#AppendixA) oku).
- Internet Explorer 9 veya üzeri

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:

1. [Alıştırma 1: ASP.NET MVC projelerinde sayfa denetçisini kullanma](#Exercise1)
2. [Alıştırma 2: WebForms projelerinde sayfa denetçisini kullanma](#Exercise2)

> [!NOTE]
> Her alıştırma, alıştırmanın BEGIN klasöründe bulunan bir başlangıç çözümü ile birlikte her alıştırmanın bağımsız olarak izlenmesi için bir çözüm sağlar. Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir son klasör de bulacaksınız. Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **30 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>Alıştırma 1: ASP.NET MVC projelerinde sayfa denetçisini kullanma

Bu alıştırmada, **sayfa denetçisi**'ni kullanarak BIR **ASP.NET MVC 4** çözümünde önizleme ve hata ayıklama işlemlerini öğreneceksiniz. İlk olarak, Web hata ayıklama işlemini kolaylaştıran özellikleri öğrenmek için araç etrafında kısa bir lap gerçekleştirirsiniz. Daha sonra, stil sorunları içeren bir Web sayfasında çalışacaksınız. Sorunu oluşturan kaynak kodunu bulmak ve onarmak için sayfa denetçisi 'ni nasıl kullanacağınızı öğreneceksiniz.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>Görev 1-sayfa denetçisini keşfetme

Bu görevde, sayfa denetçisini bir fotoğraf galerisini gösteren bir ASP.NET MVC 4 projesi bağlamında nasıl kullanacağınızı öğreneceksiniz.

1. **Kaynak/Ex1-MVC4/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın.

   1. Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. Çözüm Gezgini, **/views/Home** proje klasörü altındaki **Index. cshtml** görünümünü bulun, sağ tıklayın ve **sayfa denetçisinde görüntüle**' yi seçin.

    ![Sayfa denetçisinde önizlemesi yapılacak bir dosya seçme](using-page-inspector-in-visual-studio-2012/_static/image1.png "Sayfa denetçisinde önizlemesi yapılacak bir dosya seçme")

    *Sayfa denetçisinde önizlemesi yapılacak bir dosya seçme*
3. Sayfa denetçisi penceresinde, seçtiğiniz kaynak görünümüne eşlenen */Home/Index* URL 'si gösterilir.

    ![PageInspector ile ilk iletişim](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *Sayfa denetçisi ile ilk iletişim*

    Sayfa denetçisi Aracı, Visual Studio ortamınızda tümleşiktir. Denetleyici, güçlü bir HTML Profil Oluşturucusu ile birlikte gömülü bir tarayıcı içerir. Sayfalarınızın nasıl göründüğünü görmek için çözümü çalıştırmanız gerekmediğine dikkat edin.

    > [!NOTE]
    > Sayfa denetçisi tarayıcısının genişliği, açılan sayfanın genişliğinden az olduğunda, sayfayı düzgün bir şekilde görmezsiniz. Bu durumda, sayfa denetçisinin genişliğini ayarlayın.
4. Sayfa denetçisi ' nde **dosyalar** sekmesine tıklayın.

    Dizin sayfasını oluşturan tüm kaynak dosyaları görüntülenir. Bu özellik, özellikle kısmi görünümler ve şablonlar ile çalışırken, tüm öğeleri bir bakışta belirlemesine yardımcı olur. Bağlantılara tıkladığınızda dosyaların her birini de açabildiğine dikkat edin.

    ![-Files-Tab](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *Dosyalar sekmesi*
5. Sekmelerin solunda bulunan **Inceleme modunu aç** düğmesine tıklayın.

    Bu araç, sayfanın herhangi bir öğesini seçmenizi ve HTML ve Razor kodunu görmenizi sağlar.

    ![Değiştirme-Inceleme modu-düğme](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *Inceleme modunu değiştirme düğmesi*
6. Sayfa denetçisi tarayıcısında, fare işaretçisini sayfa öğelerinin üzerine taşıyın. Fare işaretçisini işlenmiş sayfanın herhangi bir bölümünde taşıdığınızda, öğe türü görüntülenir ve ilgili kaynak biçimlendirme veya kod Visual Studio Düzenleyicisi 'nde vurgulanır.

    ![İnceleme modu, eylemde](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *İnceleme modu, eylemde*

    > [!NOTE]
    > Sayfa denetçisi penceresini en üst düzeye çıkarmayın veya kaynak kodu gösteren önizleme sekmesini göremezsiniz. Sayfa denetçisinde öğeyi ekranı kapladıktan sonra seçerseniz, seçimin kaynak kodu görüntülenir, ancak sayfa denetçisi penceresini gizleyecek.

    **Index. cshtml** dosyasına dikkat etmeniz durumunda, seçili öğeyi üreten kaynak kodu bölümünün vurgulandığını fark edeceksiniz. Bu özellik, koda erişmenin doğrudan ve hızlı bir yolunu sağlayarak uzun kaynak dosyalarını düzenlemenizi kolaylaştırır.

    ![Öğeleri İnceleme](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *Öğeleri İnceleme*
7. **Inceleme modunu aç** düğmesine tıklayın (![HTML kodunu sayfa DENETÇISI tarayıcısında oluşturulan HTML kodunu göstermek Için HTML sekmesini seçin.](using-page-inspector-in-visual-studio-2012/_static/image7.png "Sayfa denetçisi tarayıcısında işlenen HTML kodunu göstermek için HTML sekmesini seçin.") ) imleci devre dışı bırakır.
8. Sayfa denetçisi tarayıcısında işlenen HTML kodunu göstermek için **HTML** sekmesini seçin.
9. HTML biçimlendirmesinde, Koala bağlantısı olan liste öğesini bulun ve seçin.

    Kodu seçtiğinizde ilgili çıktının tarayıcıda otomatik olarak vurgulandığını unutmayın. Bu özellik, sayfada bir HTML bloğunun nasıl oluşturulduğunu görmek için yararlıdır.

    ![Sayfada HTML öğesi seçiliyor](using-page-inspector-in-visual-studio-2012/_static/image8.png "Sayfada HTML öğesi seçiliyor")

    *Sayfada HTML öğesi seçiliyor*
10. İnceleme modunu etkinleştirmek için **Inceleme modunu aç** düğmesine *tıklayın ve gezinti* çubuğuna tıklayın. HTML kodunun sağında, stiller bölmesinde, seçili öğeye CSS stillerinin uygulandığını içeren bir liste görürsünüz.

    > [!NOTE]
    > Üst bilgi site düzeninin bir parçası olduğundan, sayfa denetçisi de \_Layout. cshtml dosyasını açıp etkilenen kod segmentini vurgulayacaktır.

    ![Stiller bulunuyor](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *Seçili bir öğenin stilleri ve kaynak dosyaları bulunuyor*
11. Değiştirme denetimi işaretçisi etkinken, fare işaretçisini mavi öne çıkan çubuğun altına taşıyın ve yarım daireye tıklayın.

    ![Öğe seçme](using-page-inspector-in-visual-studio-2012/_static/image10.png "Öğe seçme")

    *Öğe seçme*
12. Stiller bölmesinde, **. Main-Content** grubunun altındaki **Background-Image** öğesini bulun. **Arka plan resminin** **işaretini kaldırın** ve neler olduğunu görün. Tarayıcının değişiklikleri hemen yansıtmasını ve dairenin gizli olduğunu fark edeceksiniz.

    > [!NOTE]
    > Sayfa denetçisi stilleri sekmesinde uyguladığınız değişiklikler özgün stil sayfasını etkilemez. Stillerin işaretini kaldırabilir veya değerlerini istediğiniz kadar değiştirebilirsiniz, ancak sayfa yenilendikten sonra geri yüklenir.

    ![CSS stillerini etkinleştirme ve devre dışı bırakma](using-page-inspector-in-visual-studio-2012/_static/image11.png "CSS stillerini etkinleştirme ve devre dışı bırakma")

    *CSS stillerini etkinleştirme ve devre dışı bırakma*
13. İnceleme modunu kullanarak başlıktaki '**buraya logonuz**' düğmesine tıklayın.
14. **Stiller** sekmesinde, **. site-title** grubu altında **yazı tipi-boyutu** CSS özniteliğini bulun. Öznitelik değerine çift tıklayın ve 2,3 em değerini **3 em**ile değiştirin ve ardından **ENTER**tuşuna basın. Başlığın daha büyük göründüğünü unutmayın.

    ![Sayfa denetçisindeki CSS değerlerini değiştirme](using-page-inspector-in-visual-studio-2012/_static/image12.png "Sayfa denetçisindeki CSS değerlerini değiştirme")

    *Sayfa denetçisindeki CSS değerlerini değiştirme*
15. Sayfa denetçisinin sağ bölmesinde bulunan **Izleme stilleri** sekmesine tıklayın. Bu, seçime uygulanan tüm stilleri, öznitelik adına göre sıralanmış olarak görmeniz için alternatif bir yoldur.

    ![CSS stilleri izleme](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *Seçili öğenin CSS stilleri izleniyor*
16. Sayfa denetçisinin başka bir özelliği de düzen bölmesidir. İnceleme modunu kullanarak, gezinti çubuğunu seçin ve sağ bölmedeki **Düzen** sekmesine tıklayın. Seçilen öğenin tam boyutunu, bunun yanı sıra onun sapmasını, kenar boşluğunu, doldurmasını ve kenarlık boyutunu görürsünüz. Bu görünümden değerleri de değiştirebildiğinize dikkat edin.

    ![Sayfa denetçisindeki öğe düzeni](using-page-inspector-in-visual-studio-2012/_static/image14.png "Sayfa denetçisindeki öğe düzeni")

    *Sayfa denetçisindeki öğe düzeni*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>Görev 2-Fotoğraf galerisindeki stil sorunlarını bulma ve düzeltme

Visual Studio 'nun önceki sürümleriyle Web sayfaları sorunlarını nasıl tanılıyorsunuz? Internet Explorer Geliştirici Araçları veya Firebug gibi Visual Studio IDE dışında çalışan Web hata ayıklama araçları hakkında bilginiz olabilir. Tarayıcılar yalnızca HTML, komut dosyası ve stilleri anladıktan sonra, temel alınan bir çerçeve işlenecek HTML 'yi oluşturur. Bu nedenle, Web sayfalarının nasıl göründüğünü görmek için genellikle tüm siteyi dağıtmanız gerekir.

Web sitenizdeki bir sorunu tespit etmek ve onarmak istediğinizde muhtemelen bu adımları takip etmiş olursunuz:

1. Çözümü Visual Studio 'dan çalıştırın veya sayfayı Web sunucusuna dağıtın.
2. Tarayıcıda, kullandığınız geliştirici araçlarını açın veya yalnızca kaynak kodu ve stilleri açıp sorunu eşleştirmeye çalışın. Dahil edilen dosyaları bulmak için, &quot;arama&quot; veya &quot;dosyalarda ara&quot; özellikleri stil sınıflarının adı ile kullandınız.
3. Hata algılandıktan sonra, Web tarayıcısını ve sunucuyu durdurun.
4. Tarayıcı önbelleğini temizleyin.
5. Bir çözüm uygulamak için Visual Studio 'ya dönün. Test etmek için tüm adımları tekrarlayın.

ASP.NET MVC 4 ' te gerçek bir WYSıWYG olmadığından, stil sorunlarının çoğu daha sonraki bir aşamada, Web uygulamasını çalıştırdıktan veya dağıttıktan sonra algılanır. Artık sayfa denetçisi ile, çözümü çalıştırmadan herhangi bir sayfanın önizlemesini yapmak mümkündür.

Bu görevde, sayfa denetçisini kullanacaksınız ve Fotoğraf Galerisi uygulamasının bazı sorunlarını giderecaksınız.

1. Sayfa denetçisi 'ni kullanarak üstbilginin sol tarafındaki **kayıt** ve **oturum açma** bağlantılarında bulun.

    Bağlantıların sağdaki beklenen yerde gösterilmediğine ve madde işaretli bir liste gibi gösterildiğine dikkat edin. Artık bağlantıları sağa hizalamanız ve bunlara göre yeniden stillendirilecektir.

    ![Kayıt ve oturum açma bağlantılarını bulma](using-page-inspector-in-visual-studio-2012/_static/image15.png "Kayıt ve oturum açma bağlantılarını bulma")

    *Kayıt ve oturum açma bağlantılarını bulma*
2. Değiştirme Inceleme modu seçiliyken, kodunu açmak için Kaydet bağlantısına tıklayın.

    Bağlantıların kaynak kodunun dizin. cshtml değil **\_LoginPartial. cshtml** dosyasında, ilk yerde görünebileceği yer olan \_Layout. cshtml dosyasında bulunduğundan emin olun. Doğru kaynak dosyasına doğrudan yerleştirdiniz.
3. **Stiller** sekmesinde, bu bağlantıların HTML kapsayıcısı olan **#login öğesi >\<bölümünü** bulun ve tıklayın.

    **#Login** stilin, ' a tıkladıktan sonra **site. css** ' de otomatik olarak bulunduğuna dikkat edin. Ayrıca, kod artık vurgulanmıştır.

    ![CSS stillerini seçme](using-page-inspector-in-visual-studio-2012/_static/image16.png "CSS stillerini seçme")

    *CSS stillerini seçme*
4. Açılan ve kapanış karakterlerini kaldırarak ve **site. css** dosyasını kaydettikten sonra vurgulanan koddaki **metin hizalama** özniteliğinin açıklamasını kaldırın.

    Sayfa denetçisi, geçerli sayfayı oluşturan tüm farklı dosyaların farkındadır ve bu dosyalardan herhangi birinin değiştiğini tespit edebilir. Tarayıcıdaki geçerli sayfa kaynak dosyalarla eşitlendiğinde sizi uyarır.
5. Sayfa denetçisi tarayıcısında, sayfayı yeniden yüklemek için adres çubuğunun altında bulunan çubuğa tıklayın.

    ![Sayfayı yeniden yükleme](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *Sayfayı yeniden yükleme*

    Bağlantılar artık doğru, ancak yine de madde işaretli bir liste gibi görünüyor. Şimdi, madde işaretlerini kaldıracak ve bağlantıları yatay olarak hizalacaksınız.

    ![Güncelleştirilmiş sayfa](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *Güncelleştirilmiş sayfa*
6. İnceleme modunu kullanarak, &quot;kaydet&quot; ve &quot;oturum&quot; bağlantılarını içeren **&lt;li&gt;** öğelerinden herhangi birini seçin. Ardından, **&gt;&lt;bölümüne tıklayarak #login** öğe **stilleri. css** koduna erişin.

    ![Stili bulma](using-page-inspector-in-visual-studio-2012/_static/image19.png "Stili bulma")

    *Stili bulma*
7. **Style. css**' de **#login li** öğeler için kodun açıklamasını kaldırın. Eklediğiniz stil, madde işaretini gizler ve öğeleri yatay olarak görüntüler.

    ![Oturum açma bağlantılarını yeniden Stillendirme](using-page-inspector-in-visual-studio-2012/_static/image20.png "Oturum açma bağlantılarını yeniden Stillendirme")

    *Oturum açma bağlantılarını yeniden Stillendirme*
8. **Style. css** dosyasını kaydedin ve sayfayı yeniden yüklemek için adresin altında bulunan çubukta bir kez tıklayın. Bağlantıların doğru şekilde göründüğünden emin olun.

    ![Sağ tarafa hizalanmış bağlantılar](using-page-inspector-in-visual-studio-2012/_static/image21.png "Sağ tarafa hizalanmış bağlantılar")

    *Sağ tarafa hizalanmış bağlantılar*
9. Son olarak, üst bilgi başlığını değiştirirsiniz. **Logonuzu buraya** tıklayıp onu oluşturan kaynak koduna ulaşmak için İnceleme modunu kullanın.
10. Artık **\_Layout. cshtml**' de çalışıyorsunuz, '**logonuzu buraya**'**Fotoğraf Galerisi**' ile değiştirin. Sayfa denetçisi tarayıcısını kaydedin ve güncelleştirin.

    ![Yeni bir başlık atanıyor](using-page-inspector-in-visual-studio-2012/_static/image22.png "Yeni bir başlık atanıyor")

    *Yeni bir başlık atanıyor*

    ![Fotoğraf Galerisi sayfası](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *Fotoğraf Galerisi sayfası güncelleştirildi*
11. Son olarak, **Photogallery** projesini seçin ve **F5** tuşuna basarak uygulamayı çalıştırın. Tüm değişikliklerin beklendiği gibi çalıştığını göz atın.

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>Alıştırma 2: WebForms projelerinde sayfa denetçisini kullanma

Bu alıştırmada, sayfa denetçisi 'ni kullanarak bir WebForms çözümünü nasıl önizleyeceğinizi ve ayıklayacağınızı öğreneceksiniz. Web hata ayıklama işlemini kolaylaştıran sayfa denetçisi özelliklerini öğrenmek için ilk olarak araç etrafında kısa bir lap gerçekleştirirsiniz. Daha sonra, stil sorunları içeren bir Web sayfasında çalışacaksınız. Sorunu oluşturan kaynak kodunu bulmak ve onarmak için sayfa denetçisi 'ni nasıl kullanacağınızı öğreneceksiniz.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>Görev 1-sayfa denetçisini keşfetme

Bu görevde, sayfa denetçisi özelliklerini fotoğraf galerisini gösteren bir WebForms projesi bağlamında nasıl kullanacağınızı öğreneceksiniz.

1. **Kaynak/EX2-WebForms/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın.

   1. Devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. Çözüm Gezgini, **default. aspx** sayfasını bulun, sağ tıklayın ve **sayfa denetçisinde görüntüle**' yi seçin.

    ![Default. aspx 'i sayfa denetçisi ile açma](using-page-inspector-in-visual-studio-2012/_static/image24.png "Default. aspx 'i sayfa denetçisi ile açma")

    *Default. aspx 'i sayfa denetçisi ile açma*
3. Sayfa denetçisi penceresinde default. aspx görüntülenir.

    ![Sayfa denetçisinde default. aspx görüntüleme](using-page-inspector-in-visual-studio-2012/_static/image25.png "Sayfa denetçisinde default. aspx görüntüleme")

    *Sayfa denetçisinde default. aspx görüntüleme*

    Sayfa denetçisi Aracı, Visual Studio ortamınızda tümleşiktir. Inspector, seçilen kodu gösteren güçlü bir HTML Profil Oluşturucusu ile birlikte gömülü bir tarayıcı içerir. Sayfalarınızın nasıl göründüğünü görmek için çözümü çalıştırmanız gerekmediğine dikkat edin.

    > [!NOTE]
    > Sayfa denetçisi tarayıcısının genişliği, açılan sayfanın genişliğinden az olduğunda, sayfayı düzgün bir şekilde görmezsiniz. Bu durumda, sayfa denetçisinin genişliğini ayarlayın.
4. Sayfa denetçisi ' nde **dosyalar** sekmesine tıklayın.

    İşlenmiş varsayılan sayfayı oluşturan tüm kaynak dosyaları görüntülenir. Bu, özellikle Kullanıcı denetimleri ve ana sayfalarla çalışırken, tüm öğeleri bir bakışta tanımlamak için yararlı bir özelliktir. Her bir dosyanın da gezindiğine dikkat edin.

    ![Dosyalar sekmesi](using-page-inspector-in-visual-studio-2012/_static/image26.png "Dosyalar sekmesi")

    *Dosyalar sekmesi*
5. Sekmelerin solunda bulunan **Inceleme modunu aç** düğmesine tıklayın.

    Bu araç, sayfanın herhangi bir öğesini seçmenizi ve HTML kodunu ve. aspx kaynağını görmenizi sağlar.

    ![Inceleme modunu değiştirme düğmesi](using-page-inspector-in-visual-studio-2012/_static/image27.png "Inceleme modunu değiştirme düğmesi")

    *Inceleme modunu değiştirme düğmesi*
6. Sayfa denetçisi tarayıcısında, fareyi sayfa öğelerinin üzerine taşıyın. Fare işaretçisini işlenmiş sayfanın herhangi bir bölümünde taşıdığınızda, öğe türü görüntülenir ve ilgili kaynak biçimlendirme veya kod Visual Studio Düzenleyicisi 'nde vurgulanır.

    ![İnceleme modu, eylemde](using-page-inspector-in-visual-studio-2012/_static/image28.png "İnceleme modu, eylemde")

    *İnceleme modu, eylemde*

    > [!NOTE]
    > Sayfa denetçisi penceresini en üst düzeye çıkarmayın veya kaynak kodu gösteren önizleme sekmesini göremezsiniz. Sayfa denetçisinde öğeyi ekranı kapladıktan sonra seçerseniz, seçimin kaynak kodu görüntülenir, ancak sayfa denetçisi penceresini gizleyecek.

    **Default. aspx** dosyasına dikkat etmeniz durumunda, seçili öğeyi üreten kaynak kodu bölümünün vurgulandığını fark edeceksiniz. Bu özellik, koda erişmenin doğrudan ve hızlı bir yolunu sağlayan uzun kaynak dosyalarının sürümünü kolaylaştırır.

    ![Öğeleri İnceleme](using-page-inspector-in-visual-studio-2012/_static/image29.png "Öğeleri İnceleme")

    *Öğeleri İnceleme*
7. **Inceleme modunu değiştirme** düğmesine tıklayın (--![HTML-Tab](using-page-inspector-in-visual-studio-2012/_static/image30.png "-----------------------------------") -------------------------------- ) imleci devre dışı bırakmak için sayfa denetçisi sekmelerinde bulunur.
8. Sayfa denetçisi tarayıcısında işlenen HTML kodunu göstermek için **HTML** sekmesini seçin.
9. HTML kodunda, Koala bağlantısı olan liste öğesini bulun ve seçin.

    Kodu seçtiğinizde ilgili çıktının otomatik olarak vurgulandığını unutmayın. Bu özellik, sayfada bir HTML bloğunun nasıl oluşturulduğunu görmek için yararlıdır.

    ![Sayfada HTML öğesi seçme](using-page-inspector-in-visual-studio-2012/_static/image31.png "Sayfada HTML öğesi seçme")

    *Sayfada HTML öğesi seçme*
10. İnceleme modunu etkinleştirmek için **Inceleme modunu aç** düğmesine *tıklayın ve gezinti* çubuğuna tıklayın. HTML kodunun sağında, stiller bölmesinde, seçili öğeye CSS stillerinin uygulandığını içeren bir liste görürsünüz.

    > [!NOTE]
    > üst bilgi site düzeninin bir parçası olduğundan, sayfa denetçisi site. Master dosyasını da açar ve etkilenen kod segmentini vurgulayacaktır.

    ![Stilleri keşfetme WebForms](using-page-inspector-in-visual-studio-2012/_static/image32.png "Seçili bir öğenin stilleri ve kaynak dosyaları bulunuyor")

    *Seçili bir öğenin stilleri ve kaynak dosyaları bulunuyor*
11. Değiştirme denetimi işaretçisi etkinken, fare işaretçisini menü çubuğunun altına taşıyın ve boş yarı daireyi tıklatın.

    ![Öğe seçme](using-page-inspector-in-visual-studio-2012/_static/image33.png "Öğe seçme")

    *Öğe seçme*
12. Stiller bölmesinde, **. Main-Content** grubunun altındaki **Background-Image** öğesini bulun. **Arka plan resminin** **işaretini kaldırın** ve neler olduğunu görün. Tarayıcının değişiklikleri hemen yansıtmasını ve dairenin gizli olduğunu fark edeceksiniz.

    > [!NOTE]
    > Sayfa denetçisi stilleri sekmesinde uyguladığınız değişiklikler özgün stil sayfasını etkilemez. Stillerin işaretini kaldırabilir veya değerlerini istediğiniz kadar değiştirebilirsiniz, ancak sayfa yenilendikten sonra geri yüklenir.

    ![CSS styles2 etkinleştirme ve devre dışı bırakma](using-page-inspector-in-visual-studio-2012/_static/image34.png "CSS stillerini etkinleştirme ve devre dışı bırakma")

    *CSS stillerini etkinleştirme ve devre dışı bırakma*
13. İnceleme modunu kullanarak**başlıktaki '** **buraya logonuz '** düğmesine tıklayın.
14. **Stiller** sekmesinde, **. site-title** grubu altında **yazı tipi-boyutu** CSS özniteliğini bulun. Değerini düzenlemek için özniteliğe bir kez çift tıklayın. 2\.3 em değerini **3EM**ile değiştirin ve ardından ENTER tuşuna basın. Başlığın daha büyük göründüğünü unutmayın.

    ![Sayfadaki CSS değerlerini değiştirme Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Sayfa denetçisindeki CSS değerlerini değiştirme")

    *Sayfa denetçisindeki CSS değerlerini değiştirme*
15. Sayfa denetçisinin sağ bölmesinde bulunan **Izleme stilleri** sekmesine tıklayın. Bu, seçime uygulanan tüm stilleri, öznitelik adına göre sıralanmış olarak görmeniz için alternatif bir yoldur.

    ![Seçili öğenin CSS stilleri izleniyor](using-page-inspector-in-visual-studio-2012/_static/image36.png "Seçili öğenin CSS stilleri izleniyor")

    *Seçili öğenin CSS stilleri izleniyor*
16. Sayfa denetçisinin başka bir özelliği de düzen bölmesidir. İnceleme modunu kullanarak, gezinti çubuğunu seçin ve sağ bölmedeki **Düzen** sekmesine tıklayın. Seçilen öğenin tam boyutunu, bunun yanı sıra onun sapmasını, kenar boşluğunu, doldurmasını ve kenarlık boyutunu görürsünüz. Bu görünümden değerleri de değiştirebildiğinize dikkat edin.

    ![Sayfa denetçisindeki öğe düzeni](using-page-inspector-in-visual-studio-2012/_static/image37.png "Sayfa denetçisindeki öğe düzeni")

    *Sayfa denetçisindeki öğe düzeni*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>Görev 2-Fotoğraf galerisindeki stil sorunlarını bulma ve düzeltme

Visual Studio 'nun önceki sürümleriyle Web sayfaları sorunlarını nasıl tanılıyorsunuz? Internet Explorer Geliştirici Araçları veya Firebug gibi Visual Studio IDE dışında çalışan Web hata ayıklama araçları hakkında bilginiz olabilir. Tarayıcılar yalnızca HTML, komut dosyası ve stilleri anladıktan sonra, temel alınan bir çerçeve işlenecek HTML 'yi oluşturur. Bu nedenle, Web sayfalarının nasıl göründüğünü görmek için genellikle tüm siteyi dağıtmanız gerekir.

Web sitenizdeki bir sorunu tespit etmek ve onarmak istediğinizde muhtemelen bu adımları takip etmiş olursunuz:

1. Çözümü Visual Studio 'dan çalıştırın veya sayfayı Web sunucusuna dağıtın.
2. Tarayıcıda, kullandığınız geliştirici araçlarını açın veya yalnızca kaynak kodu ve stilleri açıp sorunu eşleştirmeye çalışın. Dahil edilen dosyaları bulmak için, &quot;arama&quot; veya &quot;dosyalarda, stil sınıflarının adı ile&quot; Özellikler ' i kullandınız.
3. Hata algılandıktan sonra, Web tarayıcısını ve sunucuyu durdurun.
4. Tarayıcı önbelleğini temizleyin.
5. Bir çözüm uygulamak için Visual Studio 'ya dönün. Test etmek için tüm adımları tekrarlayın.

ASP.NET WebForms 'de gerçek bir WYSıWYG olmadığından, daha sonraki bir aşamada, çalıştırıldıktan veya dağıttıktan sonra bazı stil sorunları algılanır. Artık sayfa denetçisi ile, çözümü çalıştırmadan herhangi bir sayfanın önizlemesini yapmak mümkündür.

Bu görevde, Fotoğraf Galerisi uygulamasının bazı sorunlarını gidermek için sayfa denetçisini kullanacaksınız. Aşağıdaki adımlarda, üst bilgide bazı basit stil oluşturma sorununu saptayabilir ve hızlı bir şekilde düzelolursunuz.

1. Sayfa denetimini kullanarak üstbilginin sol tarafındaki **kayıt** ve **oturum açma** bağlantılarında bulun.

    Bağlantının sağdaki beklenen yerde gösterilmediğine dikkat edin. Artık bağlantıyı doğru ve yeniden stile göre hizalacaksınız.

    ![Sol tarafta konumlandırılmış oturum açma bağlantısı](using-page-inspector-in-visual-studio-2012/_static/image38.png "Sol tarafta konumlandırılmış oturum açma bağlantısı")

    *Sol tarafta konumlandırılmış oturum açma bağlantısı*
2. Değiştirme Inceleme modu seçiliyken, kodunu açmak için oturum aç bağlantısını seçin.

    Bağlantı kaynak kodunun, ilk yerde görünebileceğiniz yer olan Default. aspx sayfasında değil, **site. Master** dosyasında bulunduğundan emin olun; doğru kaynak dosyasına doğrudan yerleştirdiniz.
3. **Stiller** sekmesinde, bu bağlantıların HTML kapsayıcısı olan **#login öğesi&gt;&lt;bölümünü** bulun ve tıklayın.

    **#Login** stilin, ' a tıkladıktan sonra **site. css** ' de otomatik olarak bulunduğuna dikkat edin. Ayrıca, kod artık vurgulanmıştır.

    ![CSS stillerini seçme](using-page-inspector-in-visual-studio-2012/_static/image39.png "CSS stillerini seçme")

    *CSS stillerini seçme*
4. Açılan ve kapanış karakterlerini kaldırarak ve **site. css** dosyasını kaydettikten sonra vurgulanan koddaki **metin hizalama** özniteliğinin açıklamasını kaldırın.

    Sayfa denetçisi, geçerli sayfayı oluşturan tüm farklı dosyaların farkındadır ve bu dosyalardan herhangi birinin değiştiğini tespit edebilir. Tarayıcıdaki geçerli sayfa kaynak dosyalarla eşitlendiğinde sizi uyarır.
5. Sayfa denetçisi tarayıcısında, değişiklikleri kaydetmek ve sayfayı yeniden yüklemek için adres çubuğunun altında bulunan çubuğa tıklayın.

    ![Sayfayı yeniden yükleme](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *Sayfayı yeniden yükleme*

    Bağlantılar artık doğru, ancak yine de madde işaretli bir liste gibi görünüyor. Şimdi, madde işaretlerini kaldıracak ve bağlantıları yatay olarak hizalacaksınız.

    ![Güncelleştirilmiş sayfa](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *Güncelleştirilmiş sayfa*
6. İnceleme modunu kullanarak, &quot;kaydet&quot; ve &quot;oturum&quot; bağlantılarını içeren **&lt;li&gt;** öğelerinden herhangi birini seçin. Ardından, **&gt;&lt;bölümüne tıklayarak #login** öğe **stilleri. css** koduna erişin.

    ![Stili bulma](using-page-inspector-in-visual-studio-2012/_static/image42.png "Stili bulma")

    *Stili bulma*
7. **Style. css**' de **#login li** öğeler için kodun açıklamasını kaldırın. Eklediğiniz stil, madde işaretini gizler ve öğeleri yatay olarak görüntüler.

    ![Oturum açma bağlantılarını yeniden Stillendirme](using-page-inspector-in-visual-studio-2012/_static/image43.png "Oturum açma bağlantılarını yeniden Stillendirme")

    *Oturum açma bağlantılarını yeniden Stillendirme*
8. **Style. css** dosyasını kaydedin ve sayfayı yeniden yüklemek için adresin altında bulunan çubukta bir kez tıklayın. Bağlantıların doğru şekilde göründüğünden emin olun.

    ![Sağ tarafa hizalanmış bağlantılar](using-page-inspector-in-visual-studio-2012/_static/image44.png "Sağ tarafa hizalanmış bağlantılar")

    *Sağ tarafa hizalanmış bağlantılar*
9. Son olarak, üst bilgi başlığını değiştirirsiniz. Tüm dosyalardaki '**logonuzu buraya yazın '** metnini aramak yerine, metni tıklatıp oluşturan kaynak koduna ulaşmak için İnceleme modunu kullanın.

    ![Site başlığını bulma](using-page-inspector-in-visual-studio-2012/_static/image45.png "Site başlığını bulma")

    *Site başlığını bulma*
10. Artık **site. Master**' de yer alır, '**logonuz**' metninizi '**Fotoğraf Galerisi**' ile değiştirin. Sayfa denetçisi tarayıcısını kaydedin ve güncelleştirin.

    ![Fotoğraf Galerisi sayfası güncelleştirildi](using-page-inspector-in-visual-studio-2012/_static/image46.png "Fotoğraf Galerisi sayfası güncelleştirildi")

    *Fotoğraf Galerisi sayfası güncelleştirildi*
11. Son olarak **F5** tuşuna basarak uygulamayı çalıştırın ve tüm değişikliklerin beklendiği gibi çalıştığını göz atın.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı Laboratuvarı tamamlayarak Web sitesini bir tarayıcıda yeniden oluşturmak ve çalıştırmak zorunda kalmadan Web uygulamanızı önizlemek için sayfa denetçisi 'ni nasıl kullanacağınızı öğrenirsiniz. Ayrıca, işlenen çıktıdan kaynak koda doğrudan erişerek hataları hızlı bir şekilde bulmayı ve düzeltmenizi öğrenirsiniz.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Ek A: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, <em>Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012</em> &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](using-page-inspector-in-visual-studio-2012/_static/image47.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *Web için VS Express kutucuğu*
