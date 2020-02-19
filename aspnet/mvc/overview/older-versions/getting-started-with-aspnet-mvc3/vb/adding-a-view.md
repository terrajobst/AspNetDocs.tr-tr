---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: Görünüm ekleme (VB) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457380"
---
# <a name="adding-a-view-vb"></a>Görünüm Ekleme (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Bu konuyla birlikte VB.NET kaynak koduna sahip bir Visual Web Developer projesi mevcuttur. [Vb.NET sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). İsterseniz C#, Bu öğreticinin [ C# sürümüne](../cs/adding-a-view.md) geçin.

Bu bölümde, bir istemciye HTML yanıtları oluşturma işlemini düzgün bir şekilde kapsüllemek için `HelloWorldController` sınıfını bir görünüm şablonu dosyası kullanacak şekilde değiştirirsiniz.

`HelloWorldController` sınıfında `Index` yöntemiyle bir görünüm şablonu kullanarak başlayalım. Şu anda `Index` yöntemi, denetleyici sınıfı içinde sabit kodlanmış bir ileti içeren bir dize döndürür. `Index` yöntemini, aşağıda gösterildiği gibi bir `View` nesnesini döndürecek şekilde değiştirin:

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

Şimdi de `Index` yöntemiyle çağırabilmemiz için projenize bir görünüm şablonu ekleyelim. Bunu yapmak için `Index` yönteminin içine sağ tıklayın ve **Görünüm Ekle**' ye tıklayın.

[![Indexaddview](adding-a-view/_static/image2.png "Indexaddview")](adding-a-view/_static/image1.png)

**Görünüm Ekle** iletişim kutusu görüntülenir. Varsayılan girişleri bırakın ve **Ekle** düğmesine tıklayın.

[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)

*Mvcmovie\views\helloworld* klasörü ve *Mvcmovie\views\helloworld\ındex.vbhtml* dosyası oluşturulur. Bunları **Çözüm Gezgini**görebilirsiniz:

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

`<h2>` etiketinin altına bazı HTML ekleyin. Değiştirilen *Mvcmovie\views\helloworld\ındex.vbhtml* dosyası aşağıda gösterilmiştir.

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

Uygulamayı çalıştırın ve &quot;Hello World&quot; denetleyicisine (`http://localhost:xxxx/HelloWorld`) gidin. Denetleyicinizdeki `Index` yöntemi çok işe yaramadı; yalnızca, istemciye yanıt işlemek için bir görünüm şablonu dosyası kullanmak istediğimiz `return View()`ifadesini çalıştırdık. Kullanılacak görünüm şablonu dosyasının adını açık bir şekilde belirttiğimiz için, ASP.NET MVC, *\Views\helloworld* klasörü içinde *Index. vbhtml* görünüm dosyasını kullanmaya varsayılan olarak belirttik. Aşağıdaki görüntüde, görünümde sabit kodlanmış dize gösterilmektedir.

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

Oldukça iyi bir şekilde görünür. Ancak, tarayıcının başlık çubuğunun &quot;Dizin&quot; ve sayfadaki büyük başlığın MVC uygulamamın &quot;göründüğünü unutmayın.&quot; bunları değiştirelim.

## <a name="changing-views-and-layout-pages"></a>Görünümleri ve düzen sayfalarını değiştirme

İlk olarak, MVC uygulamamın &quot;metni değiştirelim. metnin paylaşıldığını ve her sayfada göründüğünü&quot;. Aslında uygulamamızda her sayfada olsa bile, projemizdeki yalnızca bir yerde görünür. **Çözüm Gezgini** */views/Shared* klasörüne gidin ve *\_Layout. vbhtml* dosyasını açın. Bu dosyaya bir düzen sayfası denir ve diğer tüm sayfaların kullandığı&quot; paylaşılan &quot;kabuğu olur.

Dosyanın alt kısmındaki `@RenderBody()` kodun satırına göz önünde tutun. `RenderBody`, oluşturduğunuz tüm sayfaların, Düzen sayfasında Sarmalanan &quot;&quot; gösteren bir yer tutucudur. `<h1>` başlığını **&quot;** MVC uygulamamın&quot; &quot;MVC film uygulaması&quot;olarak değiştirin.

[!code-html[Main](adding-a-view/samples/sample3.html)]

Uygulamayı çalıştırın ve şimdi MVC &quot;MVC film uygulaması&quot;diyor. **Hakkında** ' ya tıklayın ve bu sayfada &quot;MVC film uygulaması&quot;de gösterilmektedir.

Tüm *\_Layout. vbhtml* dosyası aşağıda gösterilmektedir:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Şimdi dizin sayfasının başlığını değiştirelim (görünüm).

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

*Mvcmovie\views\helloworld\ındex.vbhtml*dosyasını açın. Değişiklik yapmak için iki yer vardır: ilk olarak, tarayıcının başlığında görünen metin ve ardından ikincil üst bilgi (`<h2>` öğesi). Uygulamanın parçası olan kodun hangi bitini değiştirtireceğiz için bunları biraz farklı hale getireceğiz.

Uygulamayı çalıştırın ve`http://localhost:xx/HelloWorld`gidin. Tarayıcı başlığı, birincil başlık ve ikincil başlıkların değiştirildiğini unutmayın. Bir görünümde küçük değişikliklerle uygulamanızda büyük değişiklikler yapmak kolaydır. (Tarayıcıda değişiklik görmüyorsanız, önbelleğe alınmış içeriği görüntülüyor olabilirsiniz. Sunucudan gelen yanıtı zorlamak için tarayıcınızda CTRL + F5 tuşlarına basın.)

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

&quot;veri&quot; çok kısa bir süre (Bu durumda &quot;Merhaba Dünya!&quot; ileti) sabit kodludur, ancak. MVC uygulamamız V (views) ve C (Controller), ancak henüz M (model) yok. Kısa süre içinde, bir veritabanı oluşturma ve modelden model verilerini alma işlemlerinin nasıl yapılacağını adım adım inceleyeceğiz.

## <a name="passing-data-from-the-controller-to-the-view"></a>Denetleyiciden görünüme veri geçirme

Bir veritabanına gitmekten ve modeller hakkında konuşmadan önce, ilk olarak denetleyiciden bir görünüme bilgi geçirme konusunda konuşalım. Bir istemciye HTML yanıtı işlemek için bir görünüm şablonu gerektirdiğini geçirmek istiyoruz. Bu nesneler tipik olarak bir denetleyici sınıfı tarafından oluşturulup bir görünüm şablonuna geçirilir ve yalnızca görünüm şablonunun gerektirdiği verileri içermesi gerekir.

Daha önce `HelloWorldController` sınıfıyla, `Welcome` eylemi yöntemi bir `name` ve `numTimes` parametresi sürdü ve sonra parametre değerlerini tarayıcıya çıktı. Denetleyicinin bu yanıtı doğrudan işlemeye devam etmesine izin vermek yerine, bu verileri görünüm için bir pakette koyacağız. Denetleyiciler ve görünümler, verileri tutmak için bir `ViewBag` nesnesi kullanabilir. Bu, otomatik olarak bir görünüm şablonuna geçirilir ve veri olarak paket içeriğini kullanarak HTML yanıtını işlemek için kullanılır. Bu şekilde, denetleyicide bir işlemle ilgilenme ve diğer bir deyişle görünüm şablonuyla ilgili bu şekilde, uygulama içinde&quot; endişeler &quot;ayrımı sürdürmemize olanak tanıyor.

Alternatif olarak, özel bir sınıf tanımlayabiliriz, ardından bu nesnenin bir örneğini kendi kendinize oluşturabilir, verileri verilerle doldurup görünüme geçirebilirsiniz. Bu, görünüm için özel bir model olduğundan, genellikle ViewModel olarak adlandırılır. Ancak, küçük miktarlarda veri için ViewBag harika bir şekilde çalışmaktadır.

*HelloWorldController. vb* dosyasına geri dönmek için denetleyicinin içindeki `Welcome` yöntemini değiştirerek Iletiyi ve Numtimes ViewBag 'e koyun ViewBag dinamik bir nesnedir. Bu, içinde istediğiniz her şeyi koyabileceğiniz anlamına gelir. Görünüm paketine, içine bir öğe yerleştirene kadar tanımlı özellikler yoktur.

Tüm `HelloWorldController.vb` aynı dosyadaki yeni sınıfla.

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

Şimdi ViewBag, otomatik olarak görünüme geçirilecek verileri içerir. Alternatif olarak, beğendiğimiz gibi kendi nesnemizi şöyle geçirdik:

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

Şimdi bir `WelcomeView` şablonuna ihtiyacımız var! Yeni kodun derlenmesi için uygulamayı çalıştırın. Tarayıcıyı kapatın, `Welcome` yönteminin içine sağ tıklayın ve ardından **Görünüm Ekle**' ye tıklayın.

**Görünüm Ekle** iletişim kutusu şöyle görünür.

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

Yeni <em>hoş geldiniz</em> içinde `<h2>` öğesinin altına aşağıdaki kodu ekleyin. vbhtml dosyası. Bir döngü oluşturacağız ve kullanıcının söylediğimiz &quot;Hello&quot; söyleiriz!

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

Uygulamayı çalıştırın ve `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` gidin

Artık veriler URL 'den alınır ve denetleyiciye otomatik olarak geçirilir. Denetleyici, verileri bir `Model` nesnesine paketler ve bu nesneyi görünüme geçirir. Görünüm, verileri kullanıcıya HTML olarak görüntülüyor.

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

Bu, model için bir &quot;d&quot; türüdür, ancak veritabanı türü değildir. Öğrendiklerimizi ve bir film veritabanı oluşturmamızı görelim.

> [!div class="step-by-step"]
> [Önceki](adding-a-controller.md)
> [İleri](adding-a-model.md)
