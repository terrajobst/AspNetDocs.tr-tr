---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: Görünüm ekleme (C#) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: b4a1316feb8d9b7f3ef5ca4755bf1cc5b23e6ef9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458226"
---
# <a name="adding-a-view-c"></a>Görünüm Ekleme (C#)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.
> 
> 
> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Kaynak koduna sahip bir Visual Web C# Developer projesi, bu konuyla birlikte kullanılabilecek. [Sürümü C# indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Visual Basic tercih ediyorsanız, Bu öğreticinin [Visual Basic sürümüne](../vb/intro-to-aspnet-mvc-3.md) geçin.

Bu bölümde, bir istemciye HTML yanıtları oluşturma işlemini düzgün bir şekilde kapsüllemek için `HelloWorldController` sınıfını görünüm şablonu dosyalarını kullanacak şekilde değiştirirsiniz.

ASP.NET MVC 3 ile tanıtılan yeni [Razor görünümü altyapısını](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) kullanarak bir görünüm şablonu dosyası oluşturacaksınız. Razor tabanlı görünüm şablonlarının *. cshtml* dosya uzantısı vardır ve kullanarak C#HTML çıkışı oluşturmak için zarif bir yol sağlar. Razor, bir görünüm şablonu yazarken gereken karakter ve tuş vuruşlarının sayısını en aza indirir ve hızlı, akıcı bir kodlama iş akışını mümkün bir şekilde sunar.

`HelloWorldController` sınıfında `Index` yöntemiyle bir görünüm şablonu kullanarak başlayın. Şu anda `Index` yöntemi, denetleyici sınıfında sabit kodlanmış bir ileti içeren bir dize döndürür. `Index` yöntemini, aşağıda gösterildiği gibi bir `View` nesnesini döndürecek şekilde değiştirin:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

Bu kod, tarayıcıya HTML yanıtı oluşturmak için bir görünüm şablonu kullanır. Projesinde `Index` yöntemiyle kullanabileceğiniz bir görünüm şablonu ekleyin. Bunu yapmak için `Index` yönteminin içine sağ tıklayın ve **Görünüm Ekle**' ye tıklayın.

![](adding-a-view/_static/image1.png)

**Görünüm Ekle** iletişim kutusu görüntülenir. Varsayılan değerleri olduğu gibi bırakın ve **Ekle** düğmesine tıklayın:

![](adding-a-view/_static/image2.png)

*Mvcmovie\views\helloworld* klasörü ve *Mvcmovie\views\helloworld\ındex.cshtml* dosyası oluşturulur. Bunları **Çözüm Gezgini**görebilirsiniz:

![](adding-a-view/_static/image3.png)

Aşağıda, oluşturulan *Index. cshtml* dosyası gösterilmektedir:

[Merhaba Dünya dizinini ![](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

`<h2>` etiketinin altına bazı HTML ekleyin. Değiştirilen *Mvcmovie\views\helloworld\ındex.cshtml* dosyası aşağıda gösterilmiştir.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

Uygulamayı çalıştırın ve `HelloWorld` denetleyicisine (`http://localhost:xxxx/HelloWorld`) gidin. Denetleyicinizdeki `Index` yöntemi çok işe yaramadı; yalnızca `return View()`, yöntemin tarayıcıya yanıt işlemek için bir görünüm şablonu dosyası kullanması gerektiğini belirten ifadesini çalıştırmaktır. Kullanılacak görünüm şablonu dosyasının adını açıkça belirtmediğinizden, ASP.NET MVC, *\Views\helloworld* klasöründeki *Index. cshtml* görünüm dosyasını kullanacak şekilde varsayılan olarak ' ı kullanır. Aşağıdaki görüntüde, görünümde sabit kodlanmış dize gösterilmektedir.

![](adding-a-view/_static/image6.png)

Oldukça iyi bir şekilde görünür. Ancak, tarayıcının başlık çubuğunun "Dizin" ve sayfadaki büyük başlık "MVC Uygulamam" diyor olduğuna dikkat edin. Bunları değiştirelim.

## <a name="changing-views-and-layout-pages"></a>Görünümleri ve düzen sayfalarını değiştirme

İlk olarak, sayfanın en üstündeki "MVC uygulamamın" başlığını değiştirmek istiyorsunuz. Bu metin her sayfada ortaktır. Aslında uygulamada her sayfada görünse de, projede yalnızca bir yerde uygulanır. **Çözüm Gezgini** */views/Shared* klasörüne gidin ve *\_Layout. cshtml* dosyasını açın. Bu dosyaya bir *Düzen sayfası* denir ve diğer tüm sayfaların kullandığı paylaşılan "kabuk" budur.

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

Düzen şablonları, sitenizin HTML kapsayıcı yerleşimini tek bir yerde belirtmenize ve sonra sitenizdeki birden çok sayfaya uygulamanıza olanak tanır. Dosyanın alt kısmındaki `@RenderBody()` satırına göz önünde tutun. `RenderBody`, oluşturduğunuz tüm görünüme özgü sayfaların, Düzen sayfasında "sarmalanmış" olduğunu gösteren bir yer tutucudur. "MVC Uygulamam" olan düzen şablonundaki başlık başlığını "MVC film uygulaması" olarak değiştirin.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

Uygulamayı çalıştırın ve şimdi "MVC film uygulaması" ifadesinin olduğuna dikkat edin. **Hakkında** ' ya tıklayın ve bu SAYFANıN "MVC film uygulaması" nı nasıl gösterdiğini görürsünüz. Düzen şablonunda değişikliği bir kez yapabildik ve sitedeki tüm sayfalar yeni başlığı yansıtmaktadır.

![](adding-a-view/_static/image9.png)

Tüm *\_Layout. cshtml* dosyası aşağıda gösterilmektedir:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Şimdi dizin sayfasının başlığını değiştirelim (görünüm).

*Mvcmovie\views\helloworld\ındex.cshtml*dosyasını açın. Değişiklik yapmak için iki yer vardır: ilk olarak, tarayıcının başlığında görünen metin ve ardından ikincil üst bilgi (`<h2>` öğesi). Uygulamanın parçası olan hangi kod bitini değiştireceğiz için bunları biraz farklı hale getirebilirsiniz.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

Görüntülenecek HTML başlığını göstermek için, yukarıdaki kod `ViewBag` nesnesinin ( *Index. cshtml* görünüm şablonunda bulunan) bir `Title` özelliğini ayarlar. Düzen şablonunun kaynak kodunda geri bakarsanız, şablonun bu değeri, HTML 'nin `<head>` bölümünün bir parçası olarak `<title>` öğesinde kullandığını fark edersiniz. Bu yaklaşımı kullanarak, görünüm şablonunuz ve düzen dosyanız arasında kolayca başka parametreler geçirebilirsiniz.

Uygulamayı çalıştırın ve `http://localhost:xx/HelloWorld`gidin. Tarayıcı başlığı, birincil başlık ve ikincil başlıkların değiştirildiğini unutmayın. (Tarayıcıda değişiklik görmüyorsanız, önbelleğe alınmış içeriği görüntülüyor olabilirsiniz. Sunucudan gelen yanıtı zorlamak için tarayıcınızda CTRL + F5 tuşlarına basın.)

Ayrıca, *Index. cshtml* görünüm şablonundaki Içeriğin *\_düzeni. cshtml* görünüm şablonuyla nasıl birleştirildiğini ve tarayıcıya tek bir HTML yanıtı gönderildiğini de unutmayın. Düzen şablonları, uygulamanızdaki tüm sayfalara uygulanan değişiklikler yapmayı gerçekten kolaylaştırır.

![](adding-a-view/_static/image10.png)

"Data" (Bu durumda "Görünümümüzden Merhaba!") çok az. ileti) sabit kodludur, ancak. MVC uygulamasında bir "V" (görünüm) var ve bir "C" (denetleyici) var, ancak henüz "M" (model) yok. Kısa süre içinde, bir veritabanı oluşturma ve modelden model verilerini alma işlemlerinin nasıl yapılacağını adım adım inceleyeceğiz.

## <a name="passing-data-from-the-controller-to-the-view"></a>Denetleyiciden görünüme veri geçirme

Bir veritabanına gitmekten ve modeller hakkında konuşmadan önce, ilk olarak denetleyiciden bir görünüme bilgi geçirme konusunda konuşalım. Denetleyici sınıfları gelen bir URL isteğine yanıt olarak çağrılır. Bir denetleyici sınıfı, gelen parametreleri işleyen, veritabanından veri alan ve son olarak tarayıcıya ne tür bir yanıt gönderileceğini karar veren kodu yazdığınız yerdir. Daha sonra Görünüm şablonları, tarayıcıya HTML yanıtı oluşturmak ve biçimlendirmek için bir denetleyiciden kullanılabilir.

Bir görünüm şablonunun tarayıcıya yanıt oluşturması için gereken verilerin veya nesnelerin sağlanmasından denetleyiciler sorumludur. Bir görünüm şablonu asla iş mantığı gerçekleştirmemelidir veya doğrudan bir veritabanıyla etkileşime sahip olmalıdır. Bunun yerine, yalnızca denetleyici tarafından kendisine sunulan verilerle çalışır. Bu "kaygıları ayrımı", kodunuzun temiz ve daha sürdürülebilir kalmasına yardımcı olur.

Şu anda, `HelloWorldController` sınıfındaki `Welcome` Action yöntemi bir `name` ve `numTimes` parametresi alır ve sonra değerleri doğrudan tarayıcıya çıkarır. Denetleyicinin bu yanıtı bir dize olarak işlemesini sağlamak yerine, denetleyiciyi bir görünüm şablonu kullanacak şekilde değiştirelim. Görünüm şablonu dinamik bir yanıt oluşturur, bu, yanıtı oluşturmak için denetleyiciden uygun veri bitlerini görünüme geçirmeniz gerektiği anlamına gelir. Bunu, denetleyicinin görünüm şablonunun erişebileceği dinamik verileri görünüm şablonunun erişebileceği bir `ViewBag` nesnesinde yerleştirerek yapabilirsiniz.

*HelloWorldController.cs* dosyasına dönün ve `ViewBag` nesnesine bir `Message` ve `NumTimes` değeri eklemek için `Welcome` yöntemini değiştirin. `ViewBag` dinamik bir nesnedir, bu, içine istediğiniz her şeyi koyabileceğiniz anlamına gelir; `ViewBag` nesnenin içine bir öğe yerleştirene kadar tanımlanmış özellikleri yok. Tüm *HelloWorldController.cs* dosyası şuna benzer:

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

Artık `ViewBag` nesnesi, otomatik olarak görünüme geçirilecek verileri içerir.

Daha sonra bir hoş geldiniz görünüm şablonunuz olması gerekir! Projenin derlendiğinden emin olmak için **Hata Ayıkla** menüsünde **Mvcfilmi oluştur** ' u seçin.

[BuildHelloWorld ![](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

Sonra `Welcome` yönteminin içine sağ tıklayıp **Görünüm Ekle**' ye tıklayın. **Görünüm Ekle** iletişim kutusu şöyle görünür:

![](adding-a-view/_static/image13.png)

**Ekle**' ye tıklayın ve ardından yeni *hoş geldiniz. cshtml* dosyasındaki `<h2>` öğesinin altına aşağıdaki kodu ekleyin. "Hello" ifadesini gösteren ve kullanıcının bunu belirten bir döngü oluşturacaksınız. Tüm *Welcome. cshtml* dosyası aşağıda gösterilmiştir.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

Uygulamayı çalıştırın ve aşağıdaki URL 'ye gidin:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Artık veriler URL 'den alınır ve denetleyiciye otomatik olarak geçirilir. Denetleyici, verileri bir `ViewBag` nesnesine paketler ve bu nesneyi görünüme geçirir. Daha sonra Görünüm, verileri kullanıcıya HTML olarak görüntüler.

![](adding-a-view/_static/image14.png)

Bu, model için bir "a" türüdür ancak veritabanı türü değildir. Öğrendiklerimizi ve bir film veritabanı oluşturmamızı görelim.

> [!div class="step-by-step"]
> [Önceki](adding-a-controller.md)
> [İleri](adding-a-model.md)
