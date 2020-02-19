---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: Görünüm ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457641"
---
# <a name="adding-a-view"></a>Görünüm Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.

Bu bölümde, bir istemciye HTML yanıtları oluşturma işlemini düzgün bir şekilde kapsüllemek için `HelloWorldController` sınıfını görünüm şablonu dosyalarını kullanacak şekilde değiştirirsiniz.

ASP.NET MVC 3 ile tanıtılan [Razor görüntüleme altyapısını](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) kullanarak bir görünüm şablonu dosyası oluşturacaksınız. Razor tabanlı görünüm şablonlarının *. cshtml* dosya uzantısı vardır ve kullanarak C#HTML çıkışı oluşturmak için zarif bir yol sağlar. Razor, bir görünüm şablonu yazarken gereken karakter ve tuş vuruşlarının sayısını en aza indirir ve hızlı, akıcı bir kodlama iş akışını mümkün bir şekilde sunar.

Şu anda `Index` yöntemi, denetleyici sınıfında sabit kodlanmış bir ileti içeren bir dize döndürür. `Index` yöntemini, aşağıdaki kodda gösterildiği gibi bir `View` nesnesi döndürecek şekilde değiştirin:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

Yukarıdaki `Index` yöntemi, tarayıcıya HTML yanıtı oluşturmak için bir görünüm şablonu kullanır. Yukarıdaki `Index` yöntemi gibi denetleyici Yöntemleri ( [eylem yöntemleri](http://rachelappel.com/asp.net-mvc-actionresults-explained)olarak da bilinir), genellikle dize gibi basit türler değil bir [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (veya [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)öğesinden türetilmiş bir sınıf) döndürür.

Projesinde `Index` yöntemiyle kullanabileceğiniz bir görünüm şablonu ekleyin. Bunu yapmak için `Index` yönteminin içine sağ tıklayın ve **Görünüm Ekle**' ye tıklayın.

![](adding-a-view/_static/image1.png)

**Görünüm Ekle** iletişim kutusu görüntülenir. Varsayılan değerleri olduğu gibi bırakın ve **Ekle** düğmesine tıklayın:

![](adding-a-view/_static/image2.png)

*Mvcmovie\views\helloworld* klasörü ve *Mvcmovie\views\helloworld\ındex.cshtml* dosyası oluşturulur. Bunları **Çözüm Gezgini**görebilirsiniz:

![](adding-a-view/_static/image3.png)

Aşağıda, oluşturulan *Index. cshtml* dosyası gösterilmektedir:

![HelloWorldIndex](adding-a-view/_static/image4.png)

`<h2>` etiketinin altına aşağıdaki HTML 'yi ekleyin.

[!code-html[Main](adding-a-view/samples/sample2.html)]

Tüm *Mvcmovie\views\helloworld\ındex.cshtml* dosyası aşağıda gösterilmiştir.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

Visual Studio 2012 kullanıyorsanız, Çözüm Gezgini ' nde *Index. cshtml* dosyasına sağ tıklayın ve **sayfa denetçisinde görüntüle**' yi seçin.

![PI](adding-a-view/_static/image5.png)

[Sayfa denetçisi öğreticisinde](../../views/using-page-inspector-in-aspnet-mvc.md) bu yeni araç hakkında daha fazla bilgi bulunur.

Alternatif olarak, uygulamayı çalıştırın ve `HelloWorld` denetleyicisine (`http://localhost:xxxx/HelloWorld`) gidin. Denetleyicinizdeki `Index` yöntemi çok işe yaramadı; yalnızca `return View()`, yöntemin tarayıcıya yanıt işlemek için bir görünüm şablonu dosyası kullanması gerektiğini belirten ifadesini çalıştırmaktır. Kullanılacak görünüm şablonu dosyasının adını açıkça belirtmediğinizden, ASP.NET MVC, *\Views\helloworld* klasöründeki *Index. cshtml* görünüm dosyasını kullanacak şekilde varsayılan olarak ' ı kullanır. Aşağıdaki görüntüde, görünüm Şablonumuzdan Merhaba &quot;dize gösterilmektedir! görünümde sabit kodlanmış&quot;.

![](adding-a-view/_static/image6.png)

Oldukça iyi bir şekilde görünür. Ancak, tarayıcının başlık çubuğunun ASP.NET A&quot; &quot;Dizin gösterdiğine ve sayfanın üst kısmındaki büyük bağlantının buraya &quot;göründüğünü görürsünüz. logonuzu &quot;altına&quot;.&quot; bağlantı, bağlantılar ve bağlantı bağlantıları ile Ilgili bağlantıların, hakkında ve ilgili sayfaların ayrıntılarını sağlar. Bunlardan bazılarını değiştirelim.

## <a name="changing-views-and-layout-pages"></a>Görünümleri ve düzen sayfalarını değiştirme

İlk olarak, logonuzu &quot;burada değiştirmek istersiniz. sayfanın üst kısmında&quot; başlık. Bu metin her sayfada ortaktır. Aslında uygulamada her sayfada görünse de, projede yalnızca bir yerde uygulanır. **Çözüm Gezgini** */views/Shared* klasörüne gidin ve *\_Layout. cshtml* dosyasını açın. Bu dosyaya bir *Düzen sayfası* denir ve diğer tüm sayfaların kullandığı&quot; paylaşılan &quot;kabuğu olur.

![_LayoutCshtml](adding-a-view/_static/image7.png)

Düzen şablonları, sitenizin HTML kapsayıcı yerleşimini tek bir yerde belirtmenize ve sonra sitenizdeki birden çok sayfaya uygulamanıza olanak tanır. `@RenderBody()` satırını bulun. `RenderBody`, oluşturduğunuz tüm görünüme özgü sayfaların gösterileceği, &quot;kaydırılan&quot; Düzen sayfasında yer tutucudur. Örneğin, hakkında bağlantısını seçerseniz, *Views\home\about.exe* görünümü `RenderBody` yöntemi içinde işlenir.

Düzen şablonundaki site başlığı başlığını buradan &quot;&quot; logonuzu &quot;MVC filmi&quot;' e değiştirin.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Title öğesinin içeriğini aşağıdaki biçimlendirme ile değiştirin:

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

Uygulamayı çalıştırın ve şimdi MVC filmi &quot;&quot;olduğunu fark edin. **Hakkında** ' ya tıklayın ve bu SAYFANıN &quot;MVC filmi&quot;nasıl gösterdiğini görürsünüz. Düzen şablonunda değişikliği bir kez yapabildik ve sitedeki tüm sayfalar yeni başlığı yansıtmaktadır.

![](adding-a-view/_static/image8.png)

Şimdi Dizin görünümünün başlığını değiştirelim.

*Mvcmovie\views\helloworld\ındex.cshtml*dosyasını açın. Değişiklik yapmak için iki yer vardır: ilk olarak, tarayıcının başlığında görünen metin ve ardından ikincil üst bilgi (`<h2>` öğesi). Uygulamanın parçası olan hangi kod bitini değiştireceğiz için bunları biraz farklı hale getirebilirsiniz.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

Görüntülenecek HTML başlığını göstermek için, yukarıdaki kod `ViewBag` nesnesinin ( *Index. cshtml* görünüm şablonunda bulunan) bir `Title` özelliğini ayarlar. Düzen şablonunun kaynak kodunda geri bakarsanız, şablonun bu değeri, daha önce değiştirilmekte olan HTML 'nin `<head>` bölümünün bir parçası olarak `<title>` öğesinde kullandığını fark edersiniz. Bu `ViewBag` yaklaşımı kullanarak, görünüm şablonunuz ve düzen dosyanız arasında kolayca başka parametreler geçirebilirsiniz.

Uygulamayı çalıştırın ve `http://localhost:xx/HelloWorld`gidin. Tarayıcı başlığı, birincil başlık ve ikincil başlıkların değiştirildiğini unutmayın. (Tarayıcıda değişiklik görmüyorsanız, önbelleğe alınmış içeriği görüntülüyor olabilirsiniz. Sunucudan gelen yanıtı zorlamak için tarayıcınızda CTRL + F5 tuşlarına basın.) Tarayıcı başlığı *Index. cshtml* görünüm şablonunda belirlediğimiz `ViewBag.Title` ve düzen dosyasına eklenen ek &quot;-film uygulaması&quot; ile oluşturulur.

Ayrıca, *Index. cshtml* görünüm şablonundaki Içeriğin *\_düzeni. cshtml* görünüm şablonuyla nasıl birleştirildiğini ve tarayıcıya tek bir HTML yanıtı gönderildiğini de unutmayın. Düzen şablonları, uygulamanızdaki tüm sayfalara uygulanan değişiklikler yapmayı gerçekten kolaylaştırır.

![](adding-a-view/_static/image9.png)

&quot;veri&quot; çok kısa bir süre (Bu durumda, görüntüleme şablonumuzdaki &quot;Merhaba!&quot; iletisi) sabit kodlanmış, ancak. MVC uygulamasında bir &quot;V&quot; (görünüm) var ve bir &quot;C&quot; (denetleyici) var, ancak henüz &quot;M&quot; (model) yok. Kısa süre içinde, bir veritabanı oluşturma ve modelden model verilerini alma işlemlerinin nasıl yapılacağını adım adım inceleyeceğiz.

## <a name="passing-data-from-the-controller-to-the-view"></a>Denetleyiciden görünüme veri geçirme

Bir veritabanına gitmekten ve modeller hakkında konuşmadan önce, ilk olarak denetleyiciden bir görünüme bilgi geçirme konusunda konuşalım. Denetleyici sınıfları gelen bir URL isteğine yanıt olarak çağrılır. Bir denetleyici sınıfı, gelen tarayıcı isteklerini işleyen, veritabanından veri alan ve son olarak tarayıcıya ne tür bir yanıt gönderileceğini karar veren kodu yazdığınız yerdir. Daha sonra Görünüm şablonları, tarayıcıya HTML yanıtı oluşturmak ve biçimlendirmek için bir denetleyiciden kullanılabilir.

Bir görünüm şablonunun tarayıcıya yanıt oluşturması için gereken verilerin veya nesnelerin sağlanmasından denetleyiciler sorumludur. En iyi yöntem: **bir görünüm şablonu asla iş mantığı gerçekleştirmemelidir veya doğrudan bir veritabanıyla etkileşime sahip olmalıdır**. Bunun yerine, bir görünüm şablonu yalnızca denetleyici tarafından sunulan verilerle birlikte çalışmalıdır. Bu &quot;ayrımının sürdürülmesi&quot;, kodunuzun temiz, test edilebilir ve daha sürdürülebilir olmasını sağlar.

Şu anda, `HelloWorldController` sınıfındaki `Welcome` Action yöntemi bir `name` ve `numTimes` parametresi alır ve sonra değerleri doğrudan tarayıcıya çıkarır. Denetleyicinin bu yanıtı bir dize olarak işlemesini sağlamak yerine, denetleyiciyi bir görünüm şablonu kullanacak şekilde değiştirelim. Görünüm şablonu dinamik bir yanıt oluşturur, bu, yanıtı oluşturmak için denetleyiciden uygun veri bitlerini görünüme geçirmeniz gerektiği anlamına gelir. Bunu, denetleyicinin görünüm şablonunun erişebileceği bir `ViewBag` nesnesinde gerektirdiği dinamik verileri (parametreler) yerleştirerek yapabilirsiniz.

*HelloWorldController.cs* dosyasına dönün ve `ViewBag` nesnesine bir `Message` ve `NumTimes` değeri eklemek için `Welcome` yöntemini değiştirin. `ViewBag` dinamik bir nesnedir, bu, içine istediğiniz her şeyi koyabileceğiniz anlamına gelir; `ViewBag` nesnenin içine bir öğe yerleştirene kadar tanımlanmış özellikleri yok. [ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri (`name` ve `numTimes`) adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler. Tüm *HelloWorldController.cs* dosyası şuna benzer:

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

Artık `ViewBag` nesnesi, otomatik olarak görünüme geçirilecek verileri içerir.

Daha sonra bir hoş geldiniz görünüm şablonunuz olması gerekir! Projenin derlendiğinden emin olmak için **Build (oluştur** ) menüsünde **mvcfilmi oluştur** ' u seçin.

Sonra `Welcome` yönteminin içine sağ tıklayıp **Görünüm Ekle**' ye tıklayın.

![](adding-a-view/_static/image10.png)

**Görünüm Ekle** iletişim kutusu şöyle görünür:

![](adding-a-view/_static/image11.png)

**Ekle**' ye tıklayın ve ardından yeni *hoş geldiniz. cshtml* dosyasındaki `<h2>` öğesinin altına aşağıdaki kodu ekleyin. Kullanıcının &quot;Hello&quot; belirten bir döngü oluşturacaksınız. Tüm *Welcome. cshtml* dosyası aşağıda gösterilmiştir.

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

Uygulamayı çalıştırın ve aşağıdaki URL 'ye gidin:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Artık veriler URL 'den alınır ve [model cildi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)kullanılarak denetleyiciye geçirilir. Denetleyici, verileri bir `ViewBag` nesnesine paketler ve bu nesneyi görünüme geçirir. Daha sonra Görünüm, verileri kullanıcıya HTML olarak görüntüler.

![](adding-a-view/_static/image12.png)

Yukarıdaki örnekte, denetleyicideki verileri bir görünüme geçirmek için bir `ViewBag` nesnesi kullandık. İkinci öğreticide, bir denetleyicideki verileri bir görünüme geçirmek için bir görünüm modeli kullanacağız. Veri geçirme yaklaşımını görüntüleme yaklaşımı, görünüm paketi yaklaşımına göre genellikle çok tercih edilir. Daha fazla bilgi için bkz. blog girdisi [dinamik türü kesin belirlenmiş görünümler](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) .

Bu, model için bir &quot;d&quot; türüdür, ancak veritabanı türü değildir. Öğrendiklerimizi ve bir film veritabanı oluşturmamızı görelim.

> [!div class="step-by-step"]
> [Önceki](adding-a-controller.md)
> [İleri](adding-a-model.md)
