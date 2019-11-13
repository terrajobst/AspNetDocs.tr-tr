---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: ASP.NET MVC 4 sürümündeki yenilikler | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4, iyi kurulan tasarım düzenlerini ve ASP.NET ve... gücünü kullanarak ölçeklenebilir, standartlara dayalı Web uygulamaları oluşturmaya yönelik bir çerçevedir.
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057037"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>ASP.NET MVC 4 Sürümündeki Yenilikler

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[Web Camps eğitim setini indirin](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4, iyi kurulan tasarım düzenlerini ve ASP.NET ve .NET Framework 'ün gücünü kullanarak ölçeklenebilir, standartlara dayalı Web uygulamaları oluşturmaya yönelik bir çerçevedir. Framework 'ün bu yeni, dördüncü sürümü mobil Web uygulaması geliştirmeyi kolaylaştırır.

İle başlamak için yeni bir ASP.NET MVC 4 projesi oluşturduğunuzda artık mobil cihazlara özel olarak tek başına uygulama oluşturmak için kullanabileceğiniz bir mobil uygulama proje şablonu vardır. Ayrıca, ASP.NET MVC 4, jQuery. Mobile. MVC NuGet paketi aracılığıyla jQuery Mobile ile tümleşir. jQuery Mobile, Windows Phone, iPhone, Android vb. dahil olmak üzere tüm popüler mobil cihaz platformlarıyla uyumlu Web uygulamaları geliştirmeye yönelik HTML5 tabanlı bir çerçevedir. Ancak, özelleştirmeye ihtiyacınız varsa, ASP.NET MVC 4 farklı cihazlar için farklı görünümlere sunmanızı ve cihaza özgü iyileştirmeler sağlamanıza olanak sağlar.

Bu uygulamalı laboratuvarda, bir fotoğraf galerisi uygulaması oluşturmak için ASP.NET MVC 4 &quot;Internet uygulaması&quot; proje şablonuyla başlayacaksınız. Farklı mobil cihazlarla ve Masaüstü Web tarayıcılarıyla uyumlu hale getirmek için jQuery Mobile ve ASP.NET MVC 4 ' ün yeni özelliklerini kullanarak uygulamayı aşamalı olarak geliştirirsiniz. Ayrıca, kod oluşturma için yeni kod tariflerini ve ASP.NET MVC 4 ' nın görevi&lt;ActionResult&gt; dönüş türlerini destekleyerek zaman uyumsuz eylem yöntemleri yazmanızı nasıl kolaylaştıracağınızı öğreneceksiniz.

> [!NOTE]
> Tüm örnek kod ve kod parçacıkları, [Microsoft-Web/Webkamptraıningkit sürümlerinde](https://aka.ms/webcamps-training-kit)kullanılabilen Web Camps eğitim seti ' ne dahildir. Bu laboratuvara özgü proje, [ASP.NET 4,5 '](https://github.com/Microsoft-Web/HOL-ASPNETWebForms)deki yenilikleri Web Forms.

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- Yeni mobil uygulama projesi şablonu dahil olmak üzere, ASP.NET MVC proje şablonlarına yönelik geliştirmelerden yararlanın
- Mobil cihazlarda ekranı geliştirmek için HTML5 Görünüm penceresi özniteliğini ve CSS medya sorgularını kullanın
- Aşamalı geliştirmeler ve dokunarak iyileştirilmiş Web Kullanıcı arabirimi oluşturmak için jQuery Mobile kullanın
- Mobil 'e özgü görünümler oluşturma
- Uygulamadaki mobil ve Masaüstü görünümleri arasında geçiş yapmak için View-değiştirici bileşenini kullanın
- Görev desteğini kullanarak zaman uyumsuz denetleyiciler oluşturma

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Prerequisites

Bu Laboratuvarı tamamlayabilmeniz için aşağıdaki öğelere sahip olmanız gerekir:

- [Web veya üst için Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (nasıl yükleneceğine ilişkin yönergeler Için [Ek B](#AppendixB) 'yi okuyun).
- [ASP.NET MVC 4](../../../mvc4.md) (Microsoft Visual Studio 2012 yüklemesinde bulunur)
- Windows Phone öykünücü ( [Windows Phone 7.1.1 SDK 'ya](https://www.microsoft.com/download/details.aspx?id=29233)dahil)
- **Elektrik Plum IPhone simülatörü** ile isteğe bağlı- [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) (yalnızca bir iPhone simülatörü ile Web uygulamasına gözatarken kullanılan alıştırma 3 için)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

Laboratuvar belgesi boyunca kod blokları eklemeniz istenir. Kolaylık olması için bu kodun çoğu, Visual Studio içinden kullanarak el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio Code kod parçacıkları olarak sağlanır.

Kod parçacıklarını yüklemek için:

1. Bir Windows Explorer penceresi açın ve laboratuvarın **Source\setup** klasörüne gidin.
2. Visual Studio kod parçacıklarını yüklemek için bu klasördeki **Setup. cmd** dosyasına çift tıklayın.

Visual Studio Code parçacıkları hakkında bilginiz yoksa ve bunları nasıl kullanacağınızı öğrenmek istiyorsanız, [Ek A: Ek A: kod parçacıkları&quot;kullanarak](#AppendixA) bu &quot;belgedeki eke başvurabilirsiniz.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:

1. [Yeni ASP.NET MVC 4 proje şablonları](#Exercise1)
2. [Fotoğraf Galerisi Web uygulaması oluşturma](#Exercise2)
3. [Mobil cihazlar için destek ekleme](#Exercise3)
4. [Zaman uyumsuz denetleyicileri kullanma](#Exercise4)

> [!NOTE]
> Her alıştırma, alıştırmaları tamamladıktan sonra elde etmeniz gereken sonuç çözümünü içeren bir **son** klasör ile birlikte sunulur. Bu çözümü, alýþtýrmalar üzerinden çalışarak daha fazla yardıma ihtiyacınız varsa kılavuz olarak kullanabilirsiniz.

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**.

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>Alıştırma 1: yeni ASP.NET MVC 4 proje şablonları

Bu alıştırmada, ASP.NET MVC 4 proje şablonlarındaki geliştirmeleri araştıracaktır. MVC 3 ' te zaten bulunan Internet uygulaması şablonuna ek olarak, bu sürüm artık mobil uygulamalar için ayrı bir şablon içerir. İlk olarak, her bir şablonun ilgili bazı özelliklerine bakacaksınız. Ardından, doğru yaklaşımı kullanarak, farklı platformlarda sayfanızı doğru bir şekilde işlemeye çalışmanız gerekir.

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>Görev 1-Internet uygulaması şablonunu keşfetme

1. **Visual Studio 'yu**açın.
2. Dosyayı seçin **| Yeni | Proje** menü komutu. **Yeni proje** Iletişim kutusunda **görseli C# seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulaması** ' nı seçin. Projeyi **Photogallery**olarak adlandırın, bir konum seçin (veya varsayılanı bırakın) ve **Tamam**' a tıklayın.

    > [!NOTE]
    > Şimdi oluşturduğunuz PhotoGallery ASP.NET MVC 4 çözümünü daha sonra özelleştirecek.

    ![Yeni bir proje oluşturma](whats-new-in-aspnet-mvc-4/_static/image1.png "Yeni bir proje oluşturma")

    *Yeni bir proje oluşturma*
3. **Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** proje şablonunu seçin ve **Tamam**' a tıklayın. Görünüm altyapısı olarak Razor seçtiğinizden emin olun.

    ![Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma](whats-new-in-aspnet-mvc-4/_static/image2.png "Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma")

    *Yeni bir ASP.NET MVC 4 Internet uygulaması oluşturma*

    > [!NOTE]
    > Razor söz dizimi, ASP.NET MVC 3 ' te tanıtılmıştır. Amacı, bir dosyada gereken karakter ve tuş vuruşlarının sayısını en aza indirmektir ve hızlı ve akıcı bir kodlama iş akışını etkinleştirir. Razor, mevcut C# /vb (veya diğer) dil becerilerini kullanır ve harıka bir HTML oluşturma iş akışı sağlayan bir şablon biçimlendirme sözdizimi sunar.
4. **F5** tuşuna basarak çözümü çalıştırın ve yenilenen şablonları görüntüleyin. Aşağıdaki özelliklere bakabilirsiniz:

    **Modern stil şablonları**

    Şablonlar, daha modern görünümlü daha fazla stil sunarak yenilendi.

    ![ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar](whats-new-in-aspnet-mvc-4/_static/image3.png "MVC 4 yeniden biçimlendirilmiş Şablonlar")

    *ASP.NET MVC 4 yeniden biçimlendirilmiş Şablonlar*

    ![Yeni kişi sayfası](whats-new-in-aspnet-mvc-4/_static/image4.png "Yeni kişi sayfası")

    *Yeni kişi sayfası*

    **Uyarlamalı Işleme**

    Tarayıcı penceresini yeniden boyutlandırın ve sayfa düzeninin yeni pencere boyutuna dinamik olarak nasıl uyum sağlayadığına dikkat edin. Bu şablonlar, hiçbir özelleştirme yapmadan hem masaüstü hem de mobil platformlarda düzgün şekilde işlemek için uyarlamalı işleme tekniğini kullanır.

    ![Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu](whats-new-in-aspnet-mvc-4/_static/image5.png "Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu")

    *Farklı tarayıcı boyutlarında ASP.NET MVC 4 proje şablonu*

    **JavaScript ile daha zengin Kullanıcı arabirimi**

    Varsayılan proje şablonlarına yönelik başka bir geliştirme, JavaScript 'in daha etkileşimli bir JavaScript sağlamak için kullanılması. Şablonda kullanılan oturum açma ve kayıt bağlantıları, giriş alanlarını istemci tarafında doğrulamak için jQuery doğrulamalarının nasıl kullanılacağını muaf tutma.

    ![jQuery doğrulaması](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *jQuery doğrulaması*

    > [!NOTE]
    > İki günlük bölümünde, ilk bölümde siteden kayıtlı bir hesap kullanarak oturum açabildiğiniz ikinci bölümde başka bir şekilde Google (varsayılan olarak devre dışı) gibi başka bir kimlik doğrulama hizmetini kullanarak oturum açabilirsiniz.
5. Hata ayıklayıcıyı durdurmak ve Visual Studio 'ya dönmek için tarayıcıyı kapatın.
6. **Uygulama\_başlangıç** klasörü altında bulunan **AuthConfig.cs** dosyasını açın.
7. *OAuth* kimlik doğrulaması için Google Client 'ı kaydetmek üzere son satırdaki yorumu kaldırın.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > Facebook, Twitter, Microsoft vb. gibi herhangi bir OpenID veya OAuth hizmetini kullanarak kimlik doğrulamasını kolayca etkinleştirebildiğinize dikkat edin.
8. **F5** tuşuna basarak çözümü çalıştırın ve oturum açma sayfasına gidin.
9. Oturum açmak için **Google** hizmetini seçin.

    ![Günlüğü hizmette seçme](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *Günlüğü hizmette seçme*
10. Google hesabınızı kullanarak oturum açın.
11. Sitenin (localhost) Google hesabından bilgi almasına izin verin.
12. Son olarak, Google hesabını ilişkilendirmek için sitesine kaydolmanız gerekir.

   ![Google hesabınızı ilişkilendirin](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *Google hesabınızı ilişkilendirme*
13. Hata ayıklayıcıyı durdurmak ve Visual Studio 'ya dönmek için tarayıcıyı kapatın.
14. Şimdi, ASP.NET MVC 4 tarafından sunulan diğer yeni özellikleri proje şablonunda görmek için çözümü inceleyin.

   ![ASP.NET MVC 4 Internet uygulaması proje şablonu](whats-new-in-aspnet-mvc-4/_static/image9.png "ASP.NET MVC 4 Internet uygulaması proje şablonu")

   *ASP.NET MVC 4 Internet uygulaması proje şablonu*

    - **HTML 5 biçimlendirmesi**

       Yeni Tema işaretlemesini bulmak için şablon görünümlerine gözatamazsınız.

       ![. Cshtml hakkında Razor ve HTML5 biçimlendirmesi kullanan yeni şablon.](whats-new-in-aspnet-mvc-4/_static/image10.png ". Cshtml hakkında Razor ve HTML5 biçimlendirmesi kullanan yeni şablon.")

       *Razor ve HTML5 işaretlemesi (About. cshtml) kullanarak yeni şablon.*
    - **Güncelleştirilmiş JavaScript kitaplıkları**

       ASP.NET MVC 4 varsayılan şablonu artık JavaScript ve HTML kullanarak zengin ve yüksek oranda yanıt veren Web uygulamaları oluşturmanıza olanak tanıyan bir JavaScript MVVM çerçevesi olan altını gizleme özelliği içerir. MVC3 gibi, jQuery ve jQuery kullanıcı arabirimi kitaplıkları da ASP.NET MVC 4 ' de bulunur.

     > [!NOTE]
     > Bu bağlantıdaki altını gizleme ( [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/)) kitaplığı hakkında daha fazla bilgi edinebilirsiniz. Ayrıca, [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/)' de jQuery ve jQuery kullanıcı arabirimi hakkında bilgi edinebilirsiniz.

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>Görev 2-mobil uygulama şablonunu keşfetme

ASP.NET MVC 4, mobil ve tablet tarayıcılarına yönelik Web sitelerinin geliştirilmesini kolaylaştırır. Bu şablon, Internet uygulama şablonuyla aynı uygulama yapısına sahiptir (denetleyici kodunun neredeyse aynı olduğuna dikkat edin), ancak stili dokunmatik tabanlı mobil cihazlarda düzgün şekilde işlenecek şekilde değiştirilmiştir.

1. Dosyayı seçin **| Yeni | Proje** menü komutu. **Yeni proje** Iletişim kutusunda **görseli C# seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulamasını seçin.** Projeyi **Photogallery. Mobile**olarak adlandırın, bir konum seçin (ya da varsayılan olarak bırakın) &quot;çözüme Ekle&quot; ' i seçin ve **Tamam**' a tıklayın.
2. **Yeni ASP.NET MVC 4 projesi** iletişim kutusunda, **mobil uygulama** proje şablonunu seçin ve **Tamam**' a tıklayın. Görünüm altyapısı olarak Razor seçtiğinizden emin olun.

    ![Yeni bir ASP.NET MVC 4 mobil uygulaması oluşturma](whats-new-in-aspnet-mvc-4/_static/image11.png "Yeni bir ASP.NET MVC 4 mobil uygulaması oluşturma")

    *Yeni bir ASP.NET MVC 4 mobil uygulaması oluşturma*
3. Artık çözümü keşfedebiliyor ve mobil için ASP.NET MVC 4 çözüm şablonu tarafından sunulan yeni özelliklerden bazılarını kullanıma sunabileceksiniz:

    - **jQuery mobil kitaplığı**

        Mobil uygulama projesi şablonu, mobil tarayıcı uyumluluğuna yönelik açık bir kaynak kitaplığı olan jQuery mobil kitaplığını içerir. jQuery Mobile, CSS ve JavaScript 'i destekleyen mobil tarayıcılara aşamalı geliştirme uygular. Aşamalı geliştirme tüm tarayıcıların bir Web sayfasının temel içeriğini görüntülemesini sağlar, ancak yalnızca en güçlü tarayıcıların zengin içeriği görüntülemesine olanak sağlar. JQuery Mobile stilinde bulunan JavaScript ve CSS dosyaları, mobil tarayıcıların sayfa biçimlendirmesinde herhangi bir değişiklik yapmadan ekrandaki içeriğe sığması için yardım sağlar.

        ![jQuery-mobil-kitaplık-dahil-şablon](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *şablona dahil olan jQuery mobil kitaplığı*
    - **HTML5 tabanlı biçimlendirme**

        ![Mobil-uygulama-şablon--HTML5-işaretleme kullanma](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *HTML5 işaretlemesini kullanan mobil uygulama şablonu (login. cshtml ve index. cshtml)*
4. Çözümü çalıştırmak için **F5** tuşuna basın.
5. **Windows Phone 7 öykünücüsünü**açın.
6. Telefon başlangıç ekranında Internet Explorer ' ı açın. Masaüstü uygulamasının başlatıldığı URL 'yi gözden geçirin ve telefondan bu URL 'ye göz atın (örneğin, `http://localhost:[PortNumber]/`).
7. Artık oturum açma sayfasını girebilir veya hakkında sayfasına bakabilirsiniz. Web sitesinin stili, mobil için yeni metro uygulamasını temel alır. ASP.NET MVC 4 proje şablonu mobil cihazlarda doğru şekilde görüntülenirken sayfanın tüm öğelerinin görünür ve etkin olmasını sağlayın. Başlıktaki bağlantıların tıklanabileceği veya dokunacak kadar büyük olduğuna dikkat edin.

    ![Mobil cihazdaki proje şablonu sayfaları](whats-new-in-aspnet-mvc-4/_static/image14.png "Mobil cihazdaki proje şablonu sayfaları")

    *Mobil cihazdaki proje şablonu sayfaları*
8. Yeni şablon **Görünüm penceresi meta etiketini**de kullanır. Çoğu mobil tarayıcı, mobil cihazın gerçek genişliğinden daha büyük olan bir sanal tarayıcı penceresi veya &quot;Görünüm penceresi&quot;için bir genişlik tanımlar. Bu, mobil tarayıcıların tüm Web sayfasını sanal görüntü içinde görüntülemesini sağlar. **Görünüm penceresi meta etiketi** , Web geliştiricilerinin mobil cihazlarda tarayıcı alanının genişliğini, yüksekliğini ve ölçeğini ayarlamasına olanak tanır **.** Mobil uygulamalar için ASP.NET MVC 4 şablonu, görünüm penceresinin Görünüm penceresi, cihaz ekranı genişliğine ayarlanmış olacak şekilde Düzen *\_* şablonunda (&quot;Width = cihaz-Width&quot;) Görünüm penceresini ayarlar. Görünüm penceresi meta etiketinin varsayılan tarayıcı görünümünü değiştirmediğine dikkat edin.
9. Görünümlerde bulunan **\_Layout. cshtml**dosyasını açın **| Paylaşılan** klasör ve Görünüm penceresi meta etiketini açıklama. Zaten açılmadıysa uygulamayı çalıştırın ve farklılıkları inceleyin.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![Görünüm penceresi meta etiketini açıklama ekleyerek site](whats-new-in-aspnet-mvc-4/_static/image15.png "Görünüm penceresi meta etiketini açıklama ekleyerek site")

*Görünüm penceresi meta etiketini açıklama ekleyerek site*
10. Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.
11. Görünüm penceresi meta etiketinin açıklamasını kaldırın.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>Görev 3-Uyarlamalı Işleme kullanma

Bu görevde, bir Web sayfasını herhangi bir özelleştirme olmadan aynı anda mobil cihazlarda ve Web tarayıcılarında doğru bir şekilde işlemek için başka bir yöntem öğreneceksiniz. Zaten benzer bir amaçla Görünüm penceresi meta etiketi kullandınız. Artık başka bir güçlü yöntemi karşılamanız gerekir: *Uyarlamalı işleme*.

Uyarlamalı işleme, bir sayfaya uygulanan stili özelleştirmek için **CSS3 medya sorguları** kullanan bir tekniktir. Medya sorguları, bir stil sayfası içindeki koşulları tanımlar ve belirli bir koşulun altına CSS stillerini gruplandırarak. Yalnızca koşul true olduğunda, stil, belirtilen nesnelere uygulanır.

Uyarlamalı işleme tekniği tarafından sağlanan esneklik, siteyi farklı cihazlarda görüntülemek için herhangi bir özelleştirmeyi sağlar. Stili seçmek için mantıksal kod yazmadan tek bir stil sayfasında istediğiniz kadar stil tanımlayabilirsiniz. Bu nedenle, sayfa stillerinin uyarlanmasıyla ilgili olarak, yinelenen kod miktarını ve işleme amaçları için mantığı azaltır. Öte yandan, CSS dosyalarınızın boyutu büyük ölçüde büyürken bant genişliği tüketimi artar.

Uyarlamalı işleme tekniğini kullanarak, **Tarayıcınız ne olursa olsun siteniz düzgün şekilde görüntülenecektir.** Ancak, bant genişliği ekstra yükünün bir sorun olup olmadığını göz önünde bulundurmanız gerekir.

> [!NOTE]
> Bir medya sorgusunun temel biçimi: @media \[kapsamı: ALL | Avuçiçi | Yazdır | projeksiyon | ekran\] ([özellik: değer] ve... [özellik: değer])

Medya sorgularının örnekleri: &gt; **@media All ve (max-width: 1000px) ve (min-width: 700px) {}:** 700px ve 1000px tüm çözünürlükler için.

> **@media Screen ve (min-width: 400px) ve (max-width: 700px) {...}:** Yalnızca ekranlar için. Çözüm 400 ile 700px arasında olmalıdır.
> 
> **@media Portatif ve (min-width: 20em), ekran ve (min-width: 20em) {...}:** Avuçiçi bilgisayarlar (mobil ve cihazlar) ve ekranlar için. En küçük genişlik 20em 'den büyük olmalıdır.
> 
> Bu konuda, [W3C sitesinde](http://www.w3.org/TR/css3-mediaqueries/)hakkında daha fazla bilgi edinebilirsiniz.

Artık, ASP.NET MVC 4 varsayılan Web sitesi şablonunun okunabilirliğini iyileştirmek için uyarlamalı işlemenin nasıl çalıştığını araştıracaktır.

1. Görev 1 ' de oluşturduğunuz **Photogallery. sln** çözümünü açın ve **Photogallery** projesini seçin. Çözümü çalıştırmak için **F5** tuşuna basın.
2. Tarayıcının genişliğini yeniden boyutlandırın, pencereleri yarı veya orijinal boyutunun bir çeyreğinin bir çeyrekten daha az olacak şekilde ayarlar. Başlıktaki öğelerle ne olduğunu fark edin: bazı öğeler üstbilginin görünür alanında görünmez.
3. **İçerik** proje klasöründe bulunan Visual Studio Çözüm Gezgini 'nden **site. css** dosyasını açın. Visual Studio tümleşik arama 'yı açmak için **CTRL + F** tuşlarına basın ve **CSS medya sorgusunu**bulmak için `@media` yazın.

    Bu şablonda tanımlanan medya sorgusu koşulu şu şekilde çalışıyor: tarayıcının pencere boyutu **850 px**altındaysa, uygulanan CSS kuralları bu medya bloğunda tanımlananlardır.

    ![Medya sorgusu bulunuyor](whats-new-in-aspnet-mvc-4/_static/image16.png "Medya sorgusu bulunuyor")

    *Medya sorgusu bulunuyor*
4. Uyarlamalı işlemeyi devre dışı bırakmak için 850 piksel olarak ayarlanan max-width öznitelik değerini **10**piksel ile değiştirin ve değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın. Tarayıcıya dönün ve yaptığınız değişikliklerle sayfayı yenilemek için **CTRL + F5** tuşlarına basın. Pencerenin genişliğini ayarlarken her iki sayfada da farklılıklara dikkat edin.

    ![Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır](whats-new-in-aspnet-mvc-4/_static/image17.png "Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır")

    *Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır*

    Şimdi mobil cihazlarda neler olduğunu göz atalım:

    ![Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır](whats-new-in-aspnet-mvc-4/_static/image18.png "Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır")

    *Solda, sayfa @media stilini uyguluyor ve sağ tarafta stil atlanır*

    Sayfa bir Web tarayıcısında işlendiğinde yapılan değişikliklerin çok önemli olmadığına fark edilse de, bir mobil cihaz kullanırken farklar daha belirgin hale gelir. Görüntünün sol tarafında, özel stilin okunabilirliğini iyileştirildiğini görebiliriz.

    Uyarlamalı işleme, bir Web sitesine koşullu stil uygulamayı ve bir düzenlidir yaklaşımıyla ortak stil sorunlarını çözmeye daha kolay hale getirmek için birçok daha fazla senaryoda kullanılabilir.

    Görünüm penceresi meta etiketi ve CSS medya sorguları ASP.NET MVC 4 ' e özgü değildir, bu sayede herhangi bir Web uygulamasında bu özelliklerden yararlanabilirsiniz.
5. Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>Alıştırma 2: Fotoğraf Galerisi Web uygulaması oluşturma

Bu alıştırmada, fotoğrafları göstermek için bir fotoğraf galerisi uygulaması üzerinde çalışacaksınız. ASP.NET MVC 4 proje şablonuyla başlayacaksınız ve sonra bir hizmetten fotoğraf alıp giriş sayfasında görüntülenecek bir özellik ekleyeceksiniz.

Aşağıdaki alıştırmada, mobil cihazlarda görüntülenme şeklini iyileştirmek için bu çözümü güncelleştirecek olursunuz.

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>Görev 1-bir sahte fotoğraf hizmeti oluşturma

Bu görevde, galeride görüntülenecek içeriği almak için fotoğraf hizmeti 'nin bir türünü oluşturacaksınız. Bunu yapmak için, her fotoğrafın verileriyle yalnızca bir JSON dosyası döndüren yeni bir denetleyici ekleyeceksiniz.

1. Henüz açılmadıysa **Visual Studio 'yu** açın.
2. Dosyayı seçin **| Yeni | Proje** menü komutu. **Yeni proje** Iletişim kutusunda **görseli C# seçin |** Sol bölme ağacındaki Web şablonu ve **ASP.NET MVC 4 Web uygulaması** ' nı seçin. Projeyi **Photogallery**olarak adlandırın, bir konum seçin (veya varsayılanı bırakın) ve **Tamam**' a tıklayın. Alternatif olarak, **alıştırma 1** ' den mevcut ASP.NET MVC 4 **Internet uygulaması** çözümünüzden çalışmaya devam edebilir ve sonraki adımı atlayabilirsiniz.
3. **Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** proje şablonunu seçin ve **Tamam**' a tıklayın. Görünüm altyapısı olarak Razor seçtiğinizden emin olun.
4. **Çözüm Gezgini**, projenizin **uygulama\_veri** klasörüne sağ tıklayın ve Ekle ' yi seçin **| Mevcut öğe**. Bu laboratuvarın **Source\assets\app\_Data** klasörüne göz atın ve **Fotoğraflar. JSON** dosyasını ekleyin.
5. **Photocontroller**adlı yeni bir denetleyici oluşturun. Bunu yapmak için, **denetleyiciler** klasörüne sağ tıklayın, **Ekle** ' ye gidin ve denetleyici ' yi seçin **.** Denetleyicinin adını doldurun, **boş MVC denetleyicisi** şablonunu bırakın ve **Ekle**' ye tıklayın.

    ![PhotoController ekleniyor](whats-new-in-aspnet-mvc-4/_static/image19.png "PhotoController ekleniyor")

    *PhotoController ekleniyor*
6. **Index** metodunu aşağıdaki **Galeri** eylemiyle değiştirin ve son zamanlarda projeye eklemiş olduğunuz JSON dosyasındaki içeriği döndürün.

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex02-Gallery eylemi*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. Çözümü çalıştırmak için **F5** tuşuna basın ve ardından, şu URL 'ye giderek, bu çözümü test etmek IÇIN aşağıdaki URL 'ye gidin: `http://localhost:[port]/photo/gallery` ([port] değeri uygulamanın başlatıldığı geçerli bağlantı noktasına bağlıdır). Bu URL 'ye yönelik isteğin, **Fotoğraflar. JSON** dosyasının içeriğini alması gerekir.

    ![Moclenmiş fotoğraf hizmetini test etme](whats-new-in-aspnet-mvc-4/_static/image20.png "Moclenmiş fotoğraf hizmetini test etme")

    *Moclenmiş fotoğraf hizmetini test etme*

Gerçek bir uygulamada, Fotoğraf Galerisi hizmetini uygulamak için [ASP.NET Web API 'sini](../../../../web-api/index.md) kullanabilirsiniz. ASP.NET Web API 'SI, tarayıcılar ve mobil cihazlar dahil olmak üzere çok çeşitli istemcilere ulaşan HTTP Hizmetleri oluşturmayı kolaylaştıran bir çerçevedir. ASP.NET Web API 'SI, .NET Framework üzerinde yeniden uygulamalar oluşturmaya yönelik ideal bir platformdur.

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>Görev 2-fotoğraf galerisini görüntüleme

Bu görevde, bu alıştırmanın ilk görevinde oluşturduğunuz moclenmiş hizmeti kullanarak fotoğraf galerisini görüntülemek için giriş sayfasını güncelleşceksiniz. Model dosyaları ekleyecek ve Galeri görünümlerini güncellerimize sahip olursunuz.

1. Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.
2. **Modeller** klasöründe **fotoğraf** sınıfını oluşturun. Bunu yapmak için **modeller** klasörüne sağ tıklayın, **Ekle** ' yi seçin ve **sınıf**' a tıklayın. Ardından, adı **Photo.cs** olarak ayarlayın ve **Ekle**' ye tıklayın.
3. Aşağıdaki üyeleri **fotoğraf** sınıfına ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex02-Photo Model*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. **HomeController.cs** dosyasını **denetleyiciler** klasöründen açın.
5. Aşağıdaki using deyimlerini ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 laboratuvar-Ex02-HomeController kullanımlar*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. Galeri verilerini almak için **HttpClient** kullanmak üzere **Dizin** eylemini güncelleştirin ve ardından Görünüm modelinde kaldırmak için **JavaScriptSerializer** kullanın.

    (Kod parçacığı- *ASP.NET MVC 4 laboratuvar-Ex02-Dizin eylemi*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. **Views\home** klasörünün altında bulunan **Index. cshtml** dosyasını açın ve tüm içeriği aşağıdaki kodla değiştirin.

    Bu kod, hizmetten alınan tüm fotoğraflarda döngü gösterir ve sıralanmamış bir liste halinde görüntüler.

    (Kod parçacığı- *ASP.NET MVC 4 laboratuvar-Ex02-fotoğraf listesi*)

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. **Çözüm Gezgini**projenizin **içerik** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Mevcut öğe**. Bu laboratuvarın **Source\assets\content** klasörüne göz atın ve **site. css** dosyasını ekleyin. Onun yerini onaylamanız gerekecektir. **Site. css** dosyası açıksa, dosyayı da yeniden yüklemeyi onaylamanız gerekir.
9. Dosya Gezgini 'ni açın ve bu laboratuvarın **Source\varlıklar** klasörü altında bulunan tüm **Fotoğraflar** klasörünü Çözüm Gezgini ' deki projenizin kök klasörüne kopyalayın.
10. Uygulamayı çalıştırın. Şimdi, galerideki fotoğrafları görüntüleyen giriş sayfasını görmeniz gerekir.

    ![Fotoğraf Galerisi](whats-new-in-aspnet-mvc-4/_static/image21.png "Fotoğraf Galerisi")

    *Fotoğraf Galerisi*
11. Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>Alıştırma 3: mobil cihazlar için destek ekleme

ASP.NET MVC 4 ' teki temel güncelleştirmelerden biri, mobil geliştirme için destedir. Bu alıştırmada, önceki alıştırmada oluşturduğunuz PhotoGallery çözümünü genişleterek mobil uygulamalar için ASP.NET MVC 4 yeni özelliklerini keşfedecektir.

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>Görev 1-ASP.NET MVC 4 uygulamasına jQuery Mobile yükleme

1. **Kaynak/Ex3-MobileSupport/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu** menü seçeneği ' ne tıklayarak **Paket Yöneticisi konsolunu** açın.

    ![NuGet Paket Yöneticisi konsolu açılıyor](whats-new-in-aspnet-mvc-4/_static/image22.png "NuGet Paket Yöneticisi konsolu açılıyor")

    *NuGet Paket Yöneticisi konsolu açılıyor*
3. Paket Yöneticisi konsolunda **jQuery. Mobile. Mvc** paketini yüklemek için aşağıdaki komutu çalıştırın.

    jQuery Mobile, dokunmatik iyileştirilmiş Web Kullanıcı arabirimi oluşturmaya yönelik açık kaynak bir kitaplıktır. JQuery. Mobile. MVC NuGet paketi, ASP.NET MVC 4 uygulamasıyla jQuery Mobile kullanma yardımcıları içerir.

    > [!NOTE]
    > Aşağıdaki komutu çalıştırarak, jQuery. Mobile. MVC kitaplığını NuGet 'den indirilecektir.

    9

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    Bu komut, jQuery Mobile ve bazı yardımcı dosyalarını aşağıdakiler de dahil olmak üzere kurar:

    - **Görünümler/paylaşılan/\_Layout. Mobile. cshtml**: daha küçük bir ekran Için Iyileştirilmiş jQuery Mobile tabanlı bir düzen. Web sitesi bir mobil tarayıcıdan istek aldığında, özgün düzen (\_Layout. cshtml) bu ile değiştirilir.
    - Bir görünüm-değiştirici bileşeni: **Görünümler/paylaşılan/\_Viewdeğiştirici. cshtml** kısmi görünümden ve **ViewSwitcherController.cs** denetleyicisinden oluşur. Bu bileşen, kullanıcıların sayfanın masaüstü sürümüne geçiş kurmasını sağlamak için mobil tarayıcılarda bir bağlantı gösterir.  
        ![Mobil desteğe sahip Fotoğraf Galerisi projesi](whats-new-in-aspnet-mvc-4/_static/image23.png "PhMobil desteğe sahip Me Gallery Projesi ")

        *Mobil desteğe sahip Fotoğraf Galerisi projesi*
4. Mobil paketleri kaydedin. Bunu yapmak için, **Global.asax.cs** dosyasını açın ve aşağıdaki satırı ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex03-mobil paketleri kaydet*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. Bir Masaüstü Web tarayıcısı kullanarak uygulamayı çalıştırın.
6. Başlangıç menüsünde bulunan **Windows Phone 7 öykünücüsünü** açın **| Tüm Programlar | Windows Phone SDK 7,1 | Windows Phone öykünücü.**
7. Telefon başlangıç ekranında Internet Explorer ' ı açın. Uygulamanın başlatıldığı URL 'yi inceleyin ve telefon tarayıcısıyla bu URL 'ye göz atın (örn. `http://localhost:[PortNumber]/`).

    JQuery. Mobile. MVC, projenizde mobil cihazlar için iyileştirilmiş görünümleri gösteren yeni varlıklar oluşturduğu için, uygulamanızın Windows Phone öykünücüsünde farklı görünmeyeceğini fark edeceksiniz.

    Telefonun en üstünde yer alan ve Masaüstü görünümüne geçiş yapan bağlantıyı gösteren iletiyi görürsünüz. Ayrıca, yüklediğiniz paket tarafından oluşturulan **\_Layout. Mobile. cshtml** düzeni, uygulamaya farklı bir düzen de dahil değildir.

    > [!NOTE]
    > Şimdiye kadar, mobil görünüme geri dönmek için bir bağlantı yoktur. Daha sonraki sürümlere dahil edilecek.

    ![Fotoğraf Galerisi giriş sayfasının mobil görünümü](whats-new-in-aspnet-mvc-4/_static/image24.png "Fotoğraf Galerisi giriş sayfasının mobil görünümü")

    *Fotoğraf Galerisi giriş sayfasının mobil görünümü*
8. Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>Görev 2-mobil görünümler oluşturma

Bu görevde, mobil cihazlarda daha iyi bir görünüm için içerik uyarlanmasını içeren dizin görünümünün bir mobil sürümünü oluşturacaksınız.

1. **Views\home\ındex.cshtml** görünümünü kopyalayın ve bir kopya oluşturmak üzere yapıştırın, yeni dosyayı **Index. Mobile. cshtml**olarak yeniden adlandırın.
2. Yeni oluşturulan **Index. Mobile. cshtml** görünümünü açın ve mevcut &lt;ul&gt; etiketini bu kodla değiştirin. Bunu yaparak jQuery 'ten mobil temaları kullanmak için jQuery Mobile Data Not &lt;ul&gt; etiketini güncelleştirirsiniz.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > Dikkat edin:
    > 
    > - **ListView** olarak ayarlanan **veri rolü** özniteliği, ListView stillerini kullanarak listeyi işler.
    > 
    > - **Data-ınmetinözniteliği** true olarak ayarlandığında, listeyi yuvarlatılmış kenarlık ve kenar boşluğu ile gösterir.
    > 
    > - **Data-Filter** özniteliği **true** olarak ayarlanan bir arama kutusu oluşturacaktır.
    > 
    > Proje belgelerindeki jQuery mobil kuralları hakkında daha fazla bilgi edinebilirsiniz: [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.
4. **Windows Phone öykünücüye** geçin ve siteyi yenileyin. Galeri listesinin yeni görünümünü ve en üstte bulunan yeni arama kutusunu fark edin. Ardından, fotoğraf galerisinde bir arama başlatmak için arama kutusuna (örneğin, **TULIP**) bir sözcük yazın.

    ![Filtre ile ListView stili kullanan Galeri](whats-new-in-aspnet-mvc-4/_static/image25.png "Filtre ile ListView stili kullanan Galeri")

    *Filtre ile ListView stili kullanan Galeri*

    Özetlemek gerekirse, mobil&quot; sonekiyle &quot;Dizin görünümünün bir kopyasını oluşturmak için bir görünüm Oluşturucu tarifi kullandınız. Bu sonek, bir mobil cihazdan oluşturulan her isteğin, dizinin bu kopyasını kullanacağını ASP.NET MVC 4 ' ü gösterir. Ayrıca, mobil cihazlarda site görünümünü geliştirmek için, Dizin görünümünün mobil sürümünü jQuery Mobile kullanacak şekilde güncelleştirmiş olursunuz.
5. Visual Studio 'ya geri dönün ve **içerik** klasörünün altında bulunan **site. Mobile. css** ' i açın.
6. Resmin sağ tarafında görünmesini sağlamak için fotoğraf başlığının konumlandırılmasını düzeltir. Bunu yapmak için, aşağıdaki kodu **site. Mobile. css** dosyasına ekleyin.

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.
8. **Windows Phone öykünücüye** dönün ve siteyi yenileyin. Fotoğraf başlığının hemen düzgün şekilde konumlandığına dikkat edin.

    ![Resmin sağ tarafında konumlandırılmış başlık](whats-new-in-aspnet-mvc-4/_static/image26.png "Resmin sağ tarafında konumlandırılmış başlık")

    *Resmin sağ tarafında konumlandırılmış başlık*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>Görev 3-jQuery mobil temaları

JQuery Mobile 'daki her düzen ve pencere öğesi, sitelere ve uygulamalara tam bir birleştirilmiş görsel tasarım teması uygulamayı olanaklı kılan yeni bir nesne odaklı CSS çerçevesi etrafında tasarlanmıştır.

jQuery Mobile 'ın varsayılan teması, hızlı başvuru için harfler verilen (a, b, c, d, e) 5 renk örneğini içerir.

Bu görevde, mobil düzeni varsayılandan farklı bir tema kullanacak şekilde güncelleşitecaksınız.

1. Visual Studio 'ya geri dönün.
2. **Views\shared**konumunda bulunan **\_Layout. Mobile. cshtml** dosyasını açın.
3. Veri-rolü &quot;sayfa&quot; olarak ayarlanan div öğesini bulun ve **veri temasını** &quot;**e**&quot;olarak güncelleştirin.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.
5. **Windows Phone öykünücüsünde** siteyi yenileyin ve yeni renkler düzenine dikkat edin.

    ![Farklı renk düzenine sahip mobil düzen](whats-new-in-aspnet-mvc-4/_static/image27.png "Farklı renk düzenine sahip mobil düzen")

    *Farklı renk düzenine sahip mobil düzen*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>Görev 4-görünüm-değiştirici bileşenini ve tarayıcı geçersiz kılma özelliklerini kullanma

Mobil olarak iyileştirilmiş Web sayfalarına yönelik bir kural, metnin masaüstü görünümü veya tam site modu gibi, kullanıcıların sayfanın masaüstü sürümüne geçmelerini sağlayan bir bağlantı eklemektir. JQuery. Mobile. MVC paketi, bu amaç için **\_Layout. Mobile. cshtml** görünümünde kullanılan bir örnek **Görünüm-değiştirici** bileşeni içerir.

![Masaüstü görünümüne geçiş bağlantısı](whats-new-in-aspnet-mvc-4/_static/image28.png "Masaüstü görünümüne geçiş bağlantısı")

*Masaüstü görünümüne geçiş bağlantısı*

Görünüm değiştirici, **tarayıcı geçersiz kılma**adlı yeni bir özellik kullanır. Bu özellik, uygulamanızın istekleri gerçekten geldiğini farklı bir tarayıcıdan (Kullanıcı Aracısı) geliyormuş gibi işleme sağlar.

Bu görevde, jQuery. Mobile. MVC tarafından eklenen bir görünüm değiştiricisinden örnek uygulama ve ASP.NET MVC 4 ' teki yeni tarayıcı geçersiz kılma özellikleri araştırılacak.

1. Visual Studio 'ya geri dönün.
2. **Views\shared** klasörünün altında bulunan **\_Layout. Mobile. cshtml** görünümünü açın ve görünüm-değiştirici bileşenine kısmi bir görünüm olarak başvurulduğunu unutmayın.

    ![Görünüm-değiştirici bileşeni kullanarak mobil düzen](whats-new-in-aspnet-mvc-4/_static/image29.png "Görünüm-değiştirici bileşeni kullanarak mobil düzen")

    *Görünüm-değiştirici bileşeni kullanarak mobil düzen*
3. **\_Viewdeğiştirici. cshtml** kısmi görünümünü açın.

    Kısmi görünüm, Web isteğinin kaynağını tespit etmek ve masaüstüne ya da mobil görünümlere geçiş yapmak için karşılık gelen bağlantıyı göstermek için **ViewContext. HttpContext. GetOverriddenBrowser ()** yeni yöntemini kullanır.

    **GetOverriddenBrowser** yöntemi, istek için ayarlanmış olan kullanıcı aracısına karşılık gelen bir **HttpBrowserCapabilitiesBase** örneği döndürür (gerçek veya geçersiz kılındı). Bu değeri, **ımobiledevice**gibi özellikleri almak için kullanabilirsiniz.

    ![Viewdeğiştirici kısmi görünümü](whats-new-in-aspnet-mvc-4/_static/image30.png "Viewdeğiştirici kısmi görünümü")

    *Viewdeğiştirici kısmi görünümü*
4. **Denetleyiciler** klasöründe bulunan **ViewSwitcherController.cs** sınıfını açın. Bu SwitchView eyleminin, Viewdeğiştirici bileşenindeki bağlantı tarafından çağrıldığını ve yeni HttpContext yöntemlerine dikkat ettiğini göz atın.

    - **HttpContext. ClearOverriddenBrowser ()** yöntemi, geçerli istek için geçersiz kılınan Kullanıcı aracılarını kaldırır.
    - **HttpContext. SetOverriddenBrowser ()** yöntemi, belirtilen Kullanıcı aracısını kullanarak isteğin gerçek Kullanıcı Aracısı değerini geçersiz kılar.  
        ![Viewdeğiştirici denetleyicisi](whats-new-in-aspnet-mvc-4/_static/image31.png "ViEwdeğiştirici denetleyicisi ")  
*Viewdeğiştirici denetleyicisi*

        Tarayıcı geçersiz kılma, jQuery. Mobile. MVC paketini yüklemeseniz bile bulunan ASP.NET MVC 4 ' ün temel bir özelliğidir. Ancak, bu özellik yalnızca görünüm, düzen ve kısmi görünümü etkiler ve Isteğin. Browser nesnesine bağlı olan özelliklerden hiçbirini etkilemez.

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>5\. görev-masaüstü görünümünde View-değiştirici ekleme

Bu görevde, masaüstü mizanpajını görünüm-değiştirici dahil olacak şekilde güncelleşirsiniz. Bu, mobil kullanıcıların Masaüstü görünümüne gözatarken mobil görünüme geri gitmesini sağlar.

1. **Windows Phone öykünücüsünde**siteyi yenileyin.
2. Galerinin en üstündeki **Masaüstü görünümü** bağlantısına tıklayın. Mobil görünüme geri dönebilmeniz için masaüstü görünümünde bir görünüm değiştirici olmadığına dikkat edin.
3. Visual Studio 'ya geri dönün ve **\_Layout. cshtml** görünümünü açın.
4. Oturum açma bölümünü bulun ve **\_LogOnPartial** kısmi görünümü altında **\_viewdeğiştirici** kısmi görünümünü işlemek için bir çağrı ekleyin. Ardından, değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. Değişiklikleri kaydetmek için **CTRL + S** tuşlarına basın.
6. Windows Phone öykünücüsünde sayfayı yenileyin ve yakınlaştırmak için ekrana çift tıklayın. Giriş sayfasında artık mobil 'den Masaüstü görünümüne geçiş yapan **Mobil görünüm** bağlantısı gösterildiğine dikkat edin.

    ![Masaüstü görünümünde işlenen değiştirici görüntüle](whats-new-in-aspnet-mvc-4/_static/image32.png "Masaüstü görünümünde işlenen değiştirici görüntüle")

    *Masaüstü görünümünde işlenen değiştirici görüntüle*
7. Mobil görünüme yeniden geçin **ve sayfaya gidin** (http://localhost [bağlantı noktası]/Home/About). Bir about. Mobile. cshtml görünümü oluşturmamış olsanız bile, mobil düzen (\_Layout. Mobile. cshtml) kullanılarak hakkında sayfasının görüntülendiğini unutmayın.

    ![Sayfa hakkında](whats-new-in-aspnet-mvc-4/_static/image33.png "Sayfa hakkında")

    *Sayfa hakkında*
8. Son olarak, siteyi bir Masaüstü Web tarayıcısında açın. Önceki güncelleştirmelerden hiçbirinin masaüstü görünümünden etkilenmediğine dikkat edin.

    ![PhotoGallery masaüstü görünümü](whats-new-in-aspnet-mvc-4/_static/image34.png "PhotoGallery masaüstü görünümü")

    *PhotoGallery masaüstü görünümü*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>Görev 6-yeni görüntü modları oluşturma

Yeni görüntü modları özelliği, bir uygulamanın isteği oluşturan tarayıcıya bağlı olarak görünüm seçmesini sağlar. Örneğin, bir masaüstü tarayıcısı giriş sayfasını isterse, uygulama **Views\home\ındex.cshtml** şablonunu döndürür. Daha sonra, bir mobil tarayıcı giriş sayfasını isterse, uygulama **Views\Home\Index.Mobile.cshtml** şablonunu döndürür.

Bu görevde iPhone cihazları için özelleştirilmiş bir düzen oluşturacaksınız ve iPhone cihazlarından gelen isteklerin benzetimini yapmanız gerekir. Bunu yapmak için, bir iPhone öykünücüsü/Simülatörü ( [elektrik mobil simülatörü](http://www.electricplum.com/)gibi) veya Kullanıcı aracısını değiştiren eklentilerle bir tarayıcı kullanabilirsiniz. Bir iPhone tarayıcısı için bir Safari tarayıcısında Kullanıcı Aracısı dizesinin nasıl ayarlanacağı hakkında yönergeler için, bkz. Safari 'nin, David Alison blogundan [IE 'Yi nasıl öngörün](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) .

**Bu görevin isteğe bağlı olduğuna ve bunu yürütmeden laboratuvar genelinde devam edebildiğinize dikkat edin.**

1. Visual Studio 'da, uygulamada hata ayıklamayı durdurmak için **shıft** + **F5** tuşlarına basın.
2. **Global.asax.cs** açın ve aşağıdaki using ifadesini ekleyin.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. Aşağıdaki Vurgulanan kodu uygulama\_start yöntemine ekleyin.

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex03-IPhone DisplayMode*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

**&quot;iPhone&quot;adlı yeni bir Defaultdisplaymode** , her gelen istek için eşleştirilecek statik **displaymodeprovider. Instance. Modes** statik listesi içinde kaydettiniz. Gelen istek iPhone&quot;&quot;dize içeriyorsa, ASP.NET MVC adı &quot;iPhone&quot; sonekini içeren görünümleri bulur. 0 parametresi, belirtilen yeni mod olduğunu gösterir; Örneğin, bu görünüm mobil cihazlardan gelen isteklerle eşleşen genel &quot;. mobil&quot; kuralından daha özeldir.

Bu kod çalıştıktan sonra, bir iPhone tarayıcısı bir istek oluşturduğunda, uygulamanız sonraki adımlarda oluşturacağınız **Views\shared\\_Layout. iPhone. cshtml** mizanpajını kullanacaktır.

> [!NOTE]
> İPhone isteğini test etmenin bu şekilde tanıtım amaçlarıyla basitleştirilmesi ve her iPhone Kullanıcı Aracısı dizesi için beklenen şekilde çalışmayabilir (örneğin, test büyük/küçük harfe duyarlıdır).

4. **Views\shared** klasöründe **\_Layout. Mobile. cshtml** dosyasının bir kopyasını oluşturun ve kopyayı &quot; **\_Layout. iPhone. cshtml**&quot;olarak yeniden adlandırın.
5. Önceki adımda oluşturduğunuz **\_Layout. iPhone. cshtml** dosyasını açın.
6. Data-Role özniteliği **Page** olarak ayarlanan div öğesini bulun ve **veri teması** özniteliğini **bir**&quot;&quot;olarak değiştirin.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

Artık ASP.NET MVC 4 uygulamanızda 3 düzenimize sahipsiniz:

1. **\_Layout. cshtml**: masaüstü tarayıcıları için kullanılan varsayılan düzen.
2. **\_Layout. Mobile. cshtml**: mobil cihazlar için kullanılan varsayılan düzen.
3. **\_Layout. iPhone. cshtml**: \_düzeninden ayırt etmek için farklı bir renk şeması kullanarak iPhone cihazları için özel düzen. Mobile. cshtml.
7. **F5** tuşuna basarak uygulamayı çalıştırın ve **Windows Phone öykünücüsünde**siteye gidin.
8. Bir **iPhone simülatörü** açın (iPhone simülatörü yükleyip yapılandırma hakkında yönergeler için bkz. [Ek C](#AppendixC) ) ve siteye nasıl gözatacağınız. Her telefonun belirli bir şablonu kullandığını fark edebilirsiniz.

    ![---------------Görünümlerini kullanma](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *Her mobil cihaz için farklı görünümler kullanma*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>Alıştırma 4: zaman uyumsuz denetleyicileri kullanma

Microsoft .NET Framework 4,5, .NET programlama 'de zaman uyumsuzluğu için yeni bir temel sağlamak üzere C# ve Visual Basic yeni dil özellikleri sunmaktadır. Bu yeni temel, zaman uyumsuz programlamayı, ve ile benzer şekilde, tamamen zaman uyumlu programlama olarak sunar. Artık **AsyncController** sınıfını kullanarak ASP.NET MVC 4 ' e zaman uyumsuz eylem yöntemleri yazabilirsiniz. Uzun süre çalışan, CPU olmayan istekler için zaman uyumsuz eylem yöntemlerini kullanabilirsiniz. Bu, istek işlenirken Web sunucusunun iş gerçekleştirmesini engellemeyi önler. AsyncController sınıfı genellikle uzun süre çalışan Web hizmeti çağrıları için kullanılır.

Bu alıştırmada, ASP.NET MVC 4 ' te zaman uyumsuz işlemin temelleri açıklanmaktadır. Daha ayrıntılı bilgi edinmek istiyorsanız aşağıdaki makaleye göz atabilirsiniz: [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>Görev 1-zaman uyumsuz denetleyici uygulama

1. **Kaynak/EX4-Async/BEGIN/** Folder konumunda bulunan **Başlangıç** çözümünü açın. Aksi takdirde, önceki Alıştırmayı tamamlayarak elde edilen **son** çözümü kullanmaya devam edebilirsiniz.

   1. Belirtilen **Başlangıç** çözümünü açtıysanız devam etmeden önce bazı eksik NuGet paketlerini indirmeniz gerekir. Bunu yapmak için **Proje** menüsüne tıklayın ve **NuGet Paketlerini Yönet**' i seçin.
   2. **NuGet Paketlerini Yönet** iletişim kutusunda eksik paketleri Indirmek Için **geri yükle** ' ye tıklayın.
   3. Son olarak, **derleme** | **Build Solution**' a tıklayarak Çözümü derleyin.

      > [!NOTE]
      > NuGet kullanmanın avantajlarından biri, projenizdeki tüm kitaplıkları sevk etmek zorunda olmadığınızdan proje boyutunu azaltmanızı sağlar. NuGet güç araçlarıyla, Packages. config dosyasındaki paket sürümlerini belirterek, projeyi ilk kez çalıştırdığınızda gerekli tüm kitaplıkları indirebilirsiniz. Bu laboratuvardan mevcut bir çözümü açtıktan sonra bu adımları çalıştırmanız neden olur.
2. **HomeController.cs** sınıfını **denetleyiciler** klasöründen açın.
3. Aşağıdaki using ifadesini ekleyin.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. Incontroller sınıfını **AsyncController**'dan devralacak şekilde güncelleştirin. AsyncController 'dan türetilen denetleyiciler, zaman uyumsuz istekleri işlemek için ASP.NET özelliğini etkinleştirir ve zaman uyumlu eylem yöntemlerine hala hizmet verebilir.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. **Zaman uyumsuz** anahtar sözcüğünü **Dizin** yöntemine ekleyin ve **&lt;ActionResult&gt;tür görevi** döndürün.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > **Async** anahtar sözcüğü .NET Framework 4,5 'nin sağladığı yeni anahtar sözcüklerden biridir; derleyiciye bu yöntemin zaman uyumsuz kod içerdiğini söyler. Bir **görev** nesnesi, gelecekte bir noktada tamamlayaetkileyebilecek zaman uyumsuz bir işlemi temsil eder.
6. İstemcisini değiştirin **.** Aşağıda gösterildiği gibi await anahtar sözcüğünü kullanan tam zaman uyumsuz sürümle GetAsync () çağrısı.

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-GetAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > Önceki sürümde, sonuç döndürülünceye kadar iş parçacığını engellemek için **görev** nesnesinden **Result** özelliğini kullanıyorsunuz (eşitleme sürümü).
    > 
    > **Await** anahtar sözcüğünü eklemek, derleyiciye yöntem çağrısından döndürülen görevin zaman uyumsuz olarak beklemesini söyler. Bu, kodun geri kalanının yalnızca beklenen Yöntem tamamlandıktan sonra geri çağırma olarak yürütülebileceği anlamına gelir. Başka bir şey, bu işi yapmak için try-catch bloğunu değiştirmeniz gerekmez: arka planda veya ön planda gerçekleşen özel durumlar, çerçeve tarafından sunulan bir işleyici kullanılarak hiçbir ek iş olmadan yakalanacaktır.
7. Satırları aşağıda gösterildiği gibi yeni kodla değiştirerek zaman uyumsuz uygulamayla devam edecek şekilde kodu değiştirin

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. Uygulamayı çalıştırın. Önemli bir değişiklik olmadığını fark edeceksiniz, ancak kodunuz iş parçacığı havuzundan bir iş parçacığını engellemez ve bu da sunucu kaynaklarını daha iyi bir şekilde kullanımını ve performansı geliştirir.

    > [!NOTE]
    > Laboratuvardaki yeni zaman uyumsuz programlama özellikleri hakkında daha fazla bilgi edinebilirsiniz &quot; **.net 4,5 ' de zaman uyumsuz programlama C# ve** Visual Studio eğitim paketine dahil Visual Basic&quot;.

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>Görev 2-Iptal belirteçleriyle zaman aşımlarını Işleme

Görev örnekleri döndüren zaman uyumsuz eylem metotları zaman aşımlarını de destekleyebilir. Bu görevde, bir iptal belirteci kullanarak bir zaman aşımı senaryosunu işlemek için Dizin yöntemi kodunu güncelleşolursunuz.

1. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurmak için **SHIFT + F5** tuşlarına basın.
2. Aşağıdaki using ifadesini **HomeController.cs** dosyasına ekleyin.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. Dizin eylemini bir **CancellationToken** bağımsız değişkeni alacak şekilde güncelleştirin.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. İptal belirtecini geçirmek için **GetAsync** çağrısını güncelleştirin.

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-CancellationToken Ile Sendadsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. *Dizin* yöntemini bir **AsyncTimeout** özniteliğiyle birlikte 500 milisaniyeye ve bir **zaman** aşımı görünümüne yönlendirerek **Taskolaydexception** işleyecek şekilde yapılandırılmış bir **HandleError** özniteliği süsleyin.

    (Kod parçacığı- *ASP.NET MVC 4 Lab-Ex04-Attributes*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. **Photocontroller** sınıfını açın ve uzun süre çalışan bir görevin benzetimini yapmak için yürütme 1000 milisaniyesini (1 saniye) geciktirmek üzere **Galeri** yöntemini güncelleştirin.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. **Web. config** dosyasını açın ve aşağıdaki öğeyi ekleyerek özel hataları etkinleştirin.

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. **Views\shared** adlandırılmış **zaman aşımına uğradı** bölümünde yeni bir görünüm oluşturun ve varsayılan düzeni kullanın. Çözüm Gezgini, **Views\shared** klasörüne sağ tıklayın ve **Ekle | ' yi seçin. Görüntüleyin**.

    ![Her mobil cihaz için farklı görünümler kullanma](whats-new-in-aspnet-mvc-4/_static/image36.png "Her mobil cihaz için farklı görünümler kullanma")

    *Her mobil cihaz için farklı görünümler kullanma*
9. **Zaman aşımına uğradı** görünümü içeriğini aşağıda gösterildiği gibi güncelleştirin.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. Uygulamayı çalıştırın ve kök URL 'ye gidin. Bir **iş 1000 parçacığı** eklediyseniz, **AsyncTimeout** özniteliği tarafından oluşturulan bir zaman aşımı hatası alırsınız ve **HandleError** özniteliğiyle elde edersiniz.

    ![Zaman aşımı özel durumu işlendi](whats-new-in-aspnet-mvc-4/_static/image37.png "Zaman aşımı özel durumu işlendi")

    *Zaman aşımı özel durumu işlendi*

> [!NOTE]
> Ayrıca, [Ek D: Web dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlamak](#AppendixD)için bu uygulamayı Microsoft Azure Web siteleri ' ne de dağıtabilirsiniz.

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı laboratuvarda, ASP.NET MVC 4 ' te yeni özelliklerden bazılarını gözlemlediniz. Aşağıdaki kavramlar tartışılır:

- Yeni mobil uygulama projesi şablonu dahil olmak üzere, ASP.NET MVC proje şablonlarına yönelik geliştirmelerden yararlanın
- Mobil cihazlarda ekranı geliştirmek için HTML5 Görünüm penceresi özniteliğini ve CSS medya sorgularını kullanın
- Aşamalı geliştirmeler ve dokunarak iyileştirilmiş Web Kullanıcı arabirimi oluşturmak için jQuery Mobile kullanın
- Mobil 'e özgü görünümler oluşturma
- Uygulamadaki mobil ve Masaüstü görünümleri arasında geçiş yapmak için View-değiştirici bileşenini kullanın
- Görev desteğini kullanarak zaman uyumsuz denetleyiciler oluşturma

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>Ek A: kod parçacıkları kullanma

Kod parçacıkları ile, ihtiyacınız olan tüm koda parmaklarınızın elinizin altında olmasını sağlayabilirsiniz. Laboratuvar belgesi, aşağıdaki şekilde gösterildiği gibi, bunları yalnızca ne zaman kullanacağınızı söyleyecektir.

![Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma](whats-new-in-aspnet-mvc-4/_static/image38.png "Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma")

*Projenize kod eklemek için Visual Studio kod parçacıklarını kullanma*

***Klavyeyi kullanarak bir kod parçacığı eklemek için (C# yalnızca)***

1. Kodu eklemek istediğiniz yere imleci yerleştirin.
2. Kod parçacığı adını yazmaya başlayın (boşluk veya tire olmadan).
3. IntelliSense, eşleşen kod parçacıklarının adlarını gösterdiği gibi izleyin.
4. Doğru kod parçacığını seçin (veya tüm kod parçacığının adı seçilene kadar yazmaya devam edin).
5. Kod parçacığını imleç konumuna eklemek için SEKME tuşuna iki kez basın.

![Kod parçacığı adını yazmaya başlayın](whats-new-in-aspnet-mvc-4/_static/image39.png "Kod parçacığı adını yazmaya başlayın")

*Kod parçacığı adını yazmaya başlayın*

![Vurgulanan parçacığı seçmek için Tab tuşuna basın](whats-new-in-aspnet-mvc-4/_static/image40.png "Vurgulanan parçacığı seçmek için Tab tuşuna basın")

*Vurgulanan parçacığı seçmek için Tab tuşuna basın*

![Sekmeye tekrar basın ve kod parçacığı genişletilir](whats-new-in-aspnet-mvc-4/_static/image41.png "Sekmeye tekrar basın ve kod parçacığı genişletilir")

*Sekmeye tekrar basın ve kod parçacığı genişletilir*

***Fareyi kullanarak bir kod parçacığı eklemek için (C#, VISUAL BASIC ve XML)***

1. Kod parçacığını eklemek istediğiniz yere sağ tıklayın.
2. Kod **parçacığı Ekle** ' yi ve ardından **kod parçacıklarını**seçin.
3. Listeden tıklatarak ilgili kod parçacığını seçin.

![Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.](whats-new-in-aspnet-mvc-4/_static/image42.png "Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.")

*Kod parçacığını eklemek istediğiniz yere sağ tıklayın ve parçacığı Ekle ' yi seçin.*

![Listeden tıklatarak ilgili kod parçacığını seçin](whats-new-in-aspnet-mvc-4/_static/image43.png "Listeden tıklatarak ilgili kod parçacığını seçin")

*Listeden tıklatarak ilgili kod parçacığını seçin*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>Ek B: Web için Visual Studio Express 2012 yükleme

**[Microsoft Web Platformu Yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx)** kullanarak **Web için Microsoft Visual Studio Express 2012** veya başka bir &quot;Express&quot; sürümü yükleyebilirsiniz. Aşağıdaki yönergeler *Microsoft Web Platformu Yükleyicisi*kullanarak *Web Için Visual Studio Express 2012* ' i yüklemek için gereken adımlarda size yol gösterir.

1. [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, *Microsoft Azure SDK&quot;Ile Web için Visual Studio Express 2012* &quot;ürünü açabilir ve bunu arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![Visual Studio Express yüklensin](whats-new-in-aspnet-mvc-4/_static/image44.png "Visual Studio Express yüklensin")

    *Visual Studio Express yüklensin*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.
8. Web için Visual Studio Express açmak için **Başlangıç** ekranına gidin ve &quot;**vs Express**&quot;yazmaya başlayın ve ardından **Web için vs Express** kutucuğuna tıklayın.

    ![Web için VS Express kutucuğu](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *Web için VS Express kutucuğu*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>Ek C: WebMatrix 2 ve iPhone simülatörü yükleme

Sitenizi sanal bir iPhone cihazında çalıştırmak için, iPhone&quot;için bir elektrik mobil simülasyonu &quot;WebMatrix uzantısını kullanabilirsiniz. Ayrıca, Visual Studio 2012 ' den Benzetici çalıştırmak için aynı uzantıyı yapılandırabilirsiniz.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>Görev 1-WebMatrix yükleme 2

1. [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169)gidin. Alternatif olarak, Web Platformu Yükleyicisi zaten yüklüyse, bunu açıp &quot;*WebMatrix 2*&quot;ürünü arayabilirsiniz.
2. **Şimdi yüklensin**' e tıklayın. **Web platformu yükleyicinizi** yoksa, önce indirmek ve yüklemek üzere yönlendirilirsiniz.
3. **Web Platformu Yükleyicisi** açıkken, kurulum 'u başlatmak için **yükleme** ' ye tıklayın.

    ![WebMatrix 'i yükler 2](whats-new-in-aspnet-mvc-4/_static/image49.png "WebMatrix 'i yükler 2")

    *WebMatrix 'i yükler 2*
4. Tüm ürünlerin lisanslarını ve koşullarını okuyun ve devam etmek için **kabul ediyorum** ' a tıklayın.

    ![Lisans koşullarını kabul etme](whats-new-in-aspnet-mvc-4/_static/image50.png "Lisans koşullarını kabul etme")

    *Lisans koşullarını kabul etme*
5. İndirme ve yükleme işlemi tamamlanana kadar bekleyin.

    ![Yükleme ilerleme durumu](whats-new-in-aspnet-mvc-4/_static/image51.png "Yükleme ilerleme durumu")

    *Yükleme ilerleme durumu*
6. Yükleme tamamlandığında **son**' a tıklayın.

    ![Yükleme tamamlandı](whats-new-in-aspnet-mvc-4/_static/image52.png "Yükleme tamamlandı")

    *Yükleme tamamlandı*
7. Web Platformu Yükleyicisi 'ni kapatmak için **Çıkış** ' a tıklayın.

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>Görev 2-iPhone simülatör uzantısını yükleme

1. **WebMatrix** 'i çalıştırın ve mevcut Web sitesini açın veya yeni bir tane oluşturun.
2. **Giriş** şeridinde **Çalıştır** düğmesine tıklayın ve **Yeni Ekle**' yi seçin.

    ![Yeni WebMatrix uzantısı ekleniyor](whats-new-in-aspnet-mvc-4/_static/image53.png "Yeni WebMatrix uzantısı ekleniyor")

    *Yeni WebMatrix uzantısı ekleniyor*
3. **IPhone simülatörü** ' **ni seçin ve ardından**

    ![WebMatrix uzantılarına göz atma](whats-new-in-aspnet-mvc-4/_static/image54.png "WebMatrix uzantılarına göz atma")

    *WebMatrix uzantılarına göz atma*
4. Paket ayrıntıları ' nda, uzantı yüklemesine devam etmek için **yükleme** ' ye tıklayın.

    ![iPhone simülatörü uzantısı](whats-new-in-aspnet-mvc-4/_static/image55.png "iPhone simülatörü uzantısı")

    *iPhone simülatörü uzantısı*
5. Uzantıyı okuyun ve kabul edin.

    ![WebMatrix uzantısı EULA 'Sı](whats-new-in-aspnet-mvc-4/_static/image56.png "WebMatrix uzantısı EULA 'Sı")

    *WebMatrix uzantısı EULA 'Sı*
6. Şimdi, iPhone simülatörü seçeneğini kullanarak Web sitenizi WebMatrix 'ten çalıştırabilirsiniz.

    ![İPhone kullanarak çalıştırma](whats-new-in-aspnet-mvc-4/_static/image57.png "İPhone kullanarak çalıştırma")

    *İPhone kullanarak çalıştırma*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>Görev 3-Visual Studio 2012 ' i iPhone simülatörü çalıştırmak için yapılandırma

1. **Visual Studio 2012** ' i açın ve herhangi bir Web sitesi açın veya yeni bir proje oluşturun.
2. Çalıştır düğmesinden aşağı oka tıklayın ve **Ile araştır**' ı seçin.

    ![İle araştır](whats-new-in-aspnet-mvc-4/_static/image58.png "İle araştır")

    *İle araştır*
3. &quot;&quot; iletişim kutusunda **Ekle**' ye tıklayın.
4. &quot;Program Ekle&quot; iletişim kutusunda aşağıdaki değerleri kullanın:

   - **Program**: C:\Users\*{CurrentUser} * \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(yolu uygun şekilde güncelleştirin)*
   - **Bağımsız değişkenler**: &quot;1&quot;
   - **Kolay ad**: IPhone simülatörü

     ![Program Ekle](whats-new-in-aspnet-mvc-4/_static/image59.png "Program Ekle")

     *Gezinmek için Program Ekle*
5. **Tamam** ' a tıklayın ve iletişim kutularını kapatın.
6. Artık, Web uygulamalarınızı Visual Studio 2012 ' den iPhone simülatörü ' nden çalıştırabilirsiniz.

    ![İPhone simülatörü ile tarayın](whats-new-in-aspnet-mvc-4/_static/image60.png "İPhone simülatörü ile tarayın")

    *İPhone simülatörü ile tarayın*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Ek D: Web Dağıtımı kullanarak ASP.NET MVC 4 uygulaması yayımlama

Bu ek, Microsoft Azure Yönetim Portalı yeni bir Web sitesi oluşturmayı ve Laboratuvarı izleyerek edindiğiniz uygulamayı yayımlamayı, Microsoft Azure tarafından sunulan Web Dağıtımı yayımlama özelliğinden yararlanarak nasıl yayımlayacağınızı gösterir.

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>Görev 1-Microsoft Azure portalından yeni bir Web sitesi oluşturma

1. [Windows Azure yönetim portalı](https://manage.windowsazure.com/) gidin ve aboneliğinizle ilişkili Microsoft kimlik bilgilerini kullanarak oturum açın.

    > [!NOTE]
    > Windows Azure ile 10 ASP.NET Web sitesini ücretsiz olarak barındırabilir ve ardından trafiğiniz büyüdükçe ölçeklendirebilirsiniz. [Buradan](https://aka.ms/aspnet-hol-azure)kaydolabilirsiniz.

    ![Windows Azure portal oturum açın](whats-new-in-aspnet-mvc-4/_static/image61.png "Windows Azure portal oturum açın")

    *Windows Azure 'da oturum açma Yönetim Portalı*
2. Komut çubuğunda **Yeni** ' ye tıklayın.

    ![Yeni bir Web sitesi oluşturma](whats-new-in-aspnet-mvc-4/_static/image62.png "Yeni bir Web sitesi oluşturma")

    *Yeni bir Web sitesi oluşturma*
3. **İşlem** | **Web sitesi**' ne tıklayın. Sonra **hızlı oluştur** seçeneğini belirleyin. Yeni Web sitesi için kullanılabilir bir URL sağlayın ve **Web sitesi oluştur**' a tıklayın.

    > [!NOTE]
    > Bir Microsoft Azure Web sitesi, bulutta çalışan ve yönetebileceğiniz bir Web uygulaması için ana bilgisayar. Hızlı oluştur seçeneği, tamamlanmış bir Web uygulamasını Portal dışından Windows Azure Web sitesine dağıtmanızı sağlar. Bir veritabanı ayarlamaya yönelik adımları içermez.

    ![Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma](whats-new-in-aspnet-mvc-4/_static/image63.png "Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma")

    *Hızlı oluşturma kullanarak yeni bir Web sitesi oluşturma*
4. Yeni **Web sitesi** oluşturuluncaya kadar bekleyin.
5. Web sitesi oluşturulduktan sonra **URL** sütununun altındaki bağlantıya tıklayın. Yeni Web sitesinin çalışıp çalışmadığını denetleyin.

    ![Yeni Web sitesine göz atma](whats-new-in-aspnet-mvc-4/_static/image64.png "Yeni Web sitesine göz atma")

    *Yeni Web sitesine göz atma*

    ![Web sitesi çalışıyor](whats-new-in-aspnet-mvc-4/_static/image65.png "Web sitesi çalışıyor")

    *Web sitesi çalışıyor*
6. Portala geri dönün ve yönetim sayfalarını göstermek için **ad** sütununun altındaki Web sitesinin adına tıklayın.

    ![Web sitesi yönetim sayfalarını açma](whats-new-in-aspnet-mvc-4/_static/image66.png "Web sitesi yönetim sayfalarını açma")

    *Web sitesi yönetim sayfalarını açma*
7. **Pano** sayfasında, **Hızlı bakış** bölümünde, **Yayımlama profilini indir** bağlantısına tıklayın.

    > [!NOTE]
    > *Yayımlama profili* , bir Web uygulamasını etkin her yayımlama yöntemi Için bir Windows Azure Web sitesinde yayımlamak için gereken tüm bilgileri içerir. Yayımlama profili, bir yayın yönteminin etkinleştirildiği uç noktalara bağlanmak ve kimlik doğrulaması yapmak için gereken URL 'Leri, Kullanıcı kimlik bilgilerini ve veritabanı dizelerini içerir. **Microsoft WebMatrix 2**, **Web için Microsoft Visual Studio Express** ve **Microsoft Visual Studio 2012** , Web uygulamalarını Microsoft Azure Web siteleri 'ne yayımlamak üzere bu programların yapılandırılmasını otomatik hale getirmek için yayımlama profillerinin okunmasını destekler.

    ![Web sitesi yayımlama profili indiriliyor](whats-new-in-aspnet-mvc-4/_static/image67.png "Web sitesi yayımlama profili indiriliyor")

    *Web sitesi yayımlama profili indiriliyor*
8. Yayımlama profili dosyasını bilinen bir konuma indirin. Bu alıştırmada, bir Web uygulamasını Visual Studio 'dan bir Windows Azure Web sitelerinde yayımlamak için bu dosyayı nasıl kullanacağınızı göreceksiniz.

    ![Yayımlama profili dosyası kaydediliyor](whats-new-in-aspnet-mvc-4/_static/image68.png "Yayımlama profili kaydediliyor")

    *Yayımlama profili dosyası kaydediliyor*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Görev 2-veritabanı sunucusunu yapılandırma

Uygulamanız SQL Server veritabanlarını kullanıyorsa, bir SQL veritabanı sunucusu oluşturmanız gerekir. SQL Server kullanmayan basit bir uygulama dağıtmak istiyorsanız bu görevi atlayabilirsiniz.

1. Uygulama veritabanını depolamak için bir SQL veritabanı sunucusuna ihtiyacınız olacaktır. SQL veritabanı sunucularını aboneliğinizden Windows Azure Yönetim Portalı ' nda **SQL veritabanları** | **sunucuları** | **Sunucu panosu**' nda görüntüleyebilirsiniz. Oluşturulmuş bir sunucunuz yoksa, komut çubuğunda **Ekle** düğmesini kullanarak bir tane oluşturabilirsiniz. **Sunucu adını ve URL 'yi, yönetici oturum açma adını ve parolayı**, bunları bir sonraki görevlerde kullanacaksınız gibi bir yere göz atın. Daha sonraki bir aşamada oluşturulacak şekilde veritabanını henüz oluşturmayın.

    ![SQL veritabanı sunucu panosu](whats-new-in-aspnet-mvc-4/_static/image69.png "SQL veritabanı sunucu panosu")

    *SQL veritabanı sunucu panosu*
2. Sonraki görevde, Visual Studio 'dan veritabanı bağlantısını test edersiniz. bu nedenle, yerel IP adresinizi sunucunun **Izin VERILEN IP adresleri**listesine eklemeniz gerekir. Bunu yapmak için, **Yapılandır**' a tıklayın, **geçerli ISTEMCI IP** adresinden IP ADRESINI seçin ve **Başlangıç IP adresi** ve **bitiş IP adresi** metin kutularına yapıştırın ve ![Add-Client-ip-Address-ok-Button](whats-new-in-aspnet-mvc-4/_static/image70.png) düğmesine tıklayın.

    ![Istemci IP adresi ekleniyor](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *Istemci IP adresi ekleniyor*
3. **ISTEMCI IP adresi** ızın verilen IP adresleri listesine eklendikten sonra, değişiklikleri onaylamak için **Kaydet** ' e tıklayın.

    ![Değişiklikleri Onayla](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *Değişiklikleri Onayla*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Görev 3-Web Dağıtımı kullanarak bir ASP.NET MVC 4 uygulaması yayımlama

1. ASP.NET MVC 4 çözümüne geri dönün. **Çözüm Gezgini**Web sitesi projesine sağ tıklayın ve **Yayımla**' yı seçin.

    ![Uygulama yayımlanıyor](whats-new-in-aspnet-mvc-4/_static/image73.png "Uygulamayı Yayımlama")

    *Web sitesi yayımlanıyor*
2. İlk görevde kaydettiğiniz yayımlama profilini içeri aktarın.

    ![Yayımlama profilini içeri aktarma](whats-new-in-aspnet-mvc-4/_static/image74.png "Yayımlama profilini içeri aktarma")

    *Yayımlama profili içeri aktarılıyor*
3. **Bağlantıyı doğrula**' ya tıklayın. Doğrulama tamamlandıktan sonra **İleri**' ye tıklayın.

    > [!NOTE]
    > Bağlantıyı Doğrula düğmesinin yanında yeşil bir onay işareti gördüğünüzde doğrulama tamamlanır.

    ![Bağlantı doğrulanıyor](whats-new-in-aspnet-mvc-4/_static/image75.png "Bağlantı doğrulanıyor")

    *Bağlantı doğrulanıyor*
4. **Ayarlar** sayfasında, **veritabanları** bölümü altında, veritabanı bağlantınızın metin kutusunun yanındaki düğmeye (yani **DefaultConnection**) tıklayın.

    ![Web dağıtımı yapılandırması](whats-new-in-aspnet-mvc-4/_static/image76.png "Web dağıtımı yapılandırması")

    *Web dağıtımı yapılandırması*
5. Veritabanı bağlantısını aşağıdaki şekilde yapılandırın:

   - **Sunucu adı** ' nda, *TCP:* önekini kullanarak SQL veritabanı sunucunuzun URL 'nizi yazın.
   - **Kullanıcı adı** ' nda Sunucu Yöneticisi oturum açma adınızı yazın.
   - **Parola** alanına Sunucu Yöneticisi oturum açma parolanızı yazın.
   - Yeni bir veritabanı adı yazın, örneğin: *MVC4SampleDB*.

     ![Hedef bağlantı dizesi yapılandırılıyor](whats-new-in-aspnet-mvc-4/_static/image77.png "Hedef bağlantı dizesi yapılandırılıyor")

     *Hedef bağlantı dizesi yapılandırılıyor*
6. Sonra **Tamam**'a tıklayın. Veritabanını oluşturmak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

    ![Veritabanı oluşturma](whats-new-in-aspnet-mvc-4/_static/image78.png "Veritabanı dizesi oluşturuluyor")

    *Veritabanı oluşturma*
7. Windows Azure 'da SQL veritabanı 'na bağlanmak için kullanacağınız bağlantı dizesi varsayılan bağlantı metin kutusu içinde gösterilir. Sonra **İleri**'ye tıklayın.

    ![SQL veritabanı 'na işaret eden bağlantı dizesi](whats-new-in-aspnet-mvc-4/_static/image79.png "SQL veritabanı 'na işaret eden bağlantı dizesi")

    *SQL veritabanı 'na işaret eden bağlantı dizesi*
8. **Önizleme** sayfasında **Yayımla**' ya tıklayın.

    ![Web uygulaması yayımlanıyor](whats-new-in-aspnet-mvc-4/_static/image80.png "Web uygulaması yayımlanıyor")

    *Web uygulaması yayımlanıyor*
9. Yayımlama işlemi tamamlandıktan sonra varsayılan tarayıcınız yayınlanan Web sitesini açar.

    ![Windows Azure 'da yayımlanan uygulama](whats-new-in-aspnet-mvc-4/_static/image81.png "Windows Azure 'da yayımlanan uygulama")

    *Windows Azure 'da yayımlanan uygulama*
