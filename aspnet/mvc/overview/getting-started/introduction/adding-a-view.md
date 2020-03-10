---
title: MVC uygulamasına görünüm ekleme
author: Rick-Anderson
description: MVC uygulamasına görünüm ekleme
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: 0bc6ac06d12aaee4b2a11c1bf246f9f20f0be017
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582721"
---
# <a name="adding-a-view"></a>Görünüm Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [Tutorial Note](index.md)]

Bu bölümde, bir istemciye HTML yanıtları oluşturma işlemini düzgün bir şekilde kapsüllemek için `HelloWorldController` sınıfını görünüm şablonu dosyalarını kullanacak şekilde değiştirirsiniz. 

[Razor görünüm altyapısını](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md)kullanarak bir görünüm şablonu dosyası oluşturacaksınız. Razor tabanlı görünüm şablonlarının *. cshtml* dosya uzantısı vardır ve kullanarak C#HTML çıkışı oluşturmak için zarif bir yol sağlar. Razor, bir görünüm şablonu yazarken gereken karakter ve tuş vuruşlarının sayısını en aza indirir ve hızlı, akıcı bir kodlama iş akışını mümkün bir şekilde sunar.

Şu anda `Index` yöntemi, denetleyici sınıfında sabit kodlanmış bir ileti içeren bir dize döndürür. Aşağıdaki kodda gösterildiği gibi, `Index` yöntemini, Controllers [Görünüm](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) yöntemini çağırmak için değiştirin:

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

Yukarıdaki `Index` yöntemi, tarayıcıya HTML yanıtı oluşturmak için bir görünüm şablonu kullanır. Yukarıdaki `Index` yöntemi gibi denetleyici Yöntemleri ( [eylem yöntemleri](http://rachelappel.com/asp.net-mvc-actionresults-explained)olarak da bilinir), genellikle dize gibi basit türler değil bir [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (veya [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)öğesinden türetilmiş bir sınıf) döndürür.

*Views\helloworld* klasörüne sağ tıklayın ve **Ekle**' ye ve ardından **MVC 5 görünüm sayfası düzen (Razor)** seçeneğine tıklayın.
  
![](adding-a-view/_static/image1.png)   
  
**Öğe Için ad belirtin** Iletişim kutusunda *Dizin*girin ve ardından **Tamam**' a tıklayın.  
  
![](adding-a-view/_static/image2.png)  
  
**Düzen sayfası seçin** iletişim kutusunda, varsayılan **\_Layout. cshtml** dosyasını kabul edin ve **Tamam**' a tıklayın.  
  
![](adding-a-view/_static/image3.png)  
  
Yukarıdaki iletişim kutusunda, *Görünüm \ paylaşılan* klasörü sol bölmede seçilidir. Başka bir klasörde özel bir düzen dosyanız varsa, bunu seçebilirsiniz. Daha sonra öğreticide düzen dosyası hakkında konuşacağız

*Mvcmovie\views\helloworld\ındex.cshtml* dosyası oluşturulur.

![](adding-a-view/_static/image4.png)

Aşağıdaki Vurgulanan biçimlendirmeyi ekleyin.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

*Index. cshtml* dosyasına sağ tıklayın ve **Tarayıcıda görüntüle**' yi seçin.

![PI](adding-a-view/_static/image5.png)

Ayrıca *Index. cshtml* dosyasına sağ tıklayıp **sayfa denetçisinde görüntüle** ' yi seçebilirsiniz. Daha fazla bilgi için bkz. [sayfa denetçisi öğreticisi](../../views/using-page-inspector-in-aspnet-mvc.md) .

Alternatif olarak, uygulamayı çalıştırın ve `HelloWorld` denetleyicisine (`http://localhost:xxxx/HelloWorld`) gidin. Denetleyicinizdeki `Index` yöntemi çok işe yaramadı; yalnızca `return View()`, yöntemin tarayıcıya yanıt işlemek için bir görünüm şablonu dosyası kullanması gerektiğini belirten ifadesini çalıştırmaktır. Kullanılacak görünüm şablonu dosyasının adını açıkça belirtmediğinizden, ASP.NET MVC, *\Views\helloworld* klasöründeki *Index. cshtml* görünüm dosyasını kullanacak şekilde varsayılan olarak ' ı kullanır. Aşağıdaki görüntüde, görünüm Şablonumuzdan Merhaba &quot;dize gösterilmektedir! görünümde sabit kodlanmış&quot;.

![](adding-a-view/_static/image6.png)

Oldukça iyi bir şekilde görünür. Ancak, tarayıcının başlık çubuğunda "Index-My ASP.NET Application" ifadesinin görüntülendiğine ve sayfanın en üstündeki büyük bağlantının "uygulama adı" olduğunu fark edeceksiniz. Tarayıcı pencerenizi ne kadar küçük olduğunuza bağlı olarak, **giriş**, **hakkında**, **Iletişim**, **kayıt** ve **oturum açma bağlantılarında oturum** açmak için sağ üst köşedeki üç çubuğu tıklamanızı gerekebilir.

## <a name="changing-views-and-layout-pages"></a>Görünümleri ve düzen sayfalarını değiştirme

İlk olarak, sayfanın üst kısmındaki &quot;uygulama adı&quot; bağlantısını değiştirmek istersiniz. Bu metin her sayfada ortaktır. Aslında uygulamada her sayfada görünse de, projede yalnızca bir yerde uygulanır. **Çözüm Gezgini** */views/Shared* klasörüne gidin ve *\_Layout. cshtml* dosyasını açın. Bu dosyaya bir *Düzen sayfası* denir ve diğer tüm sayfaların kullandığı paylaşılan klasörde bulunur.

![_LayoutCshtml](adding-a-view/_static/image7.png)

Düzen şablonları, sitenizin HTML kapsayıcı yerleşimini tek bir yerde belirtmenize ve sonra sitenizdeki birden çok sayfaya uygulamanıza olanak tanır. `@RenderBody()` satırını bulun. `RenderBody`, oluşturduğunuz tüm görünüme özgü sayfaların gösterileceği, &quot;kaydırılan&quot; Düzen sayfasında yer tutucudur. Örneğin, **hakkında** bağlantısını seçerseniz, *Views\home\about.exe* görünümü `RenderBody` yöntemi içinde işlenir.

Title öğesinin içeriğini değiştirin. Düzen şablonundaki [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) &quot;uygulama adı&quot; &quot;MVC filmi&quot; ve denetleyiciyi `Home` ile `Movies`arasında değiştirin. Tüm düzen dosyası aşağıda gösterilmiştir:

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

Uygulamayı çalıştırın ve şimdi MVC filmi &quot;&quot;olduğunu fark edin. **Hakkında** ' ya tıklayın ve bu SAYFANıN &quot;MVC filmi&quot;nasıl gösterdiğini görürsünüz. Düzen şablonunda değişikliği bir kez yapabildik ve sitedeki tüm sayfalar yeni başlığı yansıtmaktadır.

![](adding-a-view/_static/image8.png)

İlk olarak *Views\helloworld\ındex.cshtml* dosyasını oluşturduğumuz zaman aşağıdaki kodu içerir:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Yukarıdaki Razor kodu, düzen sayfasını açıkça ayarlıyor. *Görünümler\\_ViewStart. cshtml* dosyasını inceleyin, tam olarak aynı Razor işaretlemesini içerir. *[_ViewStart. cshtml dosyası\\görünümler](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* , tüm görünümlerin kullanacağı ortak düzeni tanımlar, bu nedenle bu kodu *Views\helloworld\ındex.cshtml* dosyasından açıklama ekleyebilir veya kaldırabilirsiniz.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

Farklı bir düzen görünümü ayarlamak için `Layout` özelliğini kullanabilir veya bir düzen dosyası kullanılmayacak şekilde `null` ayarlayabilirsiniz.

Şimdi Dizin görünümünün başlığını değiştirelim.

*Mvcmovie\views\helloworld\ındex.cshtml*dosyasını açın. Değişiklik yapmak için iki yer vardır: ilk olarak, tarayıcının başlığında görünen metin ve ardından ikincil üst bilgi (`<h2>` öğesi). Uygulamanın parçası olan hangi kod bitini değiştireceğiz için bunları biraz farklı hale getirebilirsiniz.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

Görüntülenecek HTML başlığını göstermek için, yukarıdaki kod `ViewBag` nesnesinin ( *Index. cshtml* görünüm şablonunda bulunan) bir `Title` özelliğini ayarlar. Düzen şablonunun ( *Views\shared\\_Layout. cshtml* ) bu değeri, daha önce DEĞIŞTIRILMEKTE olan HTML 'nin `<head>` bölümünün bir parçası olarak `<title>` öğesinde kullandığını unutmayın.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

Bu `ViewBag` yaklaşımı kullanarak, görünüm şablonunuz ve düzen dosyanız arasında kolayca başka parametreler geçirebilirsiniz.

Uygulamayı çalıştırın. Tarayıcı başlığı, birincil başlık ve ikincil başlıkların değiştirildiğini unutmayın. (Tarayıcıda değişiklik görmüyorsanız, önbelleğe alınmış içeriği görüntülüyor olabilirsiniz. Sunucudan gelen yanıtı zorlamak için tarayıcınızda CTRL + F5 tuşlarına basın.) Tarayıcı başlığı *Index. cshtml* görünüm şablonunda belirlediğimiz `ViewBag.Title` ve düzen dosyasına eklenen ek &quot;-film uygulaması&quot; ile oluşturulur.

Ayrıca, *Index. cshtml* görünüm şablonundaki Içeriğin *\_düzeni. cshtml* görünüm şablonuyla nasıl birleştirildiğini ve tarayıcıya tek bir HTML yanıtı gönderildiğini de unutmayın. Düzen şablonları, uygulamanızdaki tüm sayfalara uygulanan değişiklikler yapmayı gerçekten kolaylaştırır.

![](adding-a-view/_static/image9.png)

&quot;veri&quot; çok kısa bir süre (Bu durumda, görüntüleme şablonumuzdaki &quot;Merhaba!&quot; iletisi) sabit kodlanmış, ancak. MVC uygulamasında bir &quot;V&quot; (görünüm) var ve bir &quot;C&quot; (denetleyici) var, ancak henüz &quot;M&quot; (model) yok. Kısa süre içinde, bir veritabanının nasıl oluşturulduğunu ve model verilerinin nasıl alınacağını adım adım inceleyeceğiz.

## <a name="passing-data-from-the-controller-to-the-view"></a>Denetleyiciden görünüme veri geçirme

Bir veritabanına gitmekten ve modeller hakkında konuşmadan önce, ilk olarak denetleyiciden bir görünüme bilgi geçirme konusunda konuşalım. Denetleyici sınıfları gelen bir URL isteğine yanıt olarak çağrılır. Bir denetleyici sınıfı, gelen tarayıcı isteklerini işleyen, veritabanından veri alan ve son olarak tarayıcıya ne tür bir yanıt gönderileceğini karar veren kodu yazdığınız yerdir. Daha sonra Görünüm şablonları, tarayıcıya HTML yanıtı oluşturmak ve biçimlendirmek için bir denetleyiciden kullanılabilir.

Bir görünüm şablonunun tarayıcıya yanıt oluşturması için gereken verilerin veya nesnelerin sağlanmasından denetleyiciler sorumludur. En iyi yöntem: **bir görünüm şablonu asla iş mantığı gerçekleştirmemelidir veya doğrudan bir veritabanıyla etkileşime sahip olmalıdır**. Bunun yerine, bir görünüm şablonu yalnızca denetleyici tarafından sunulan verilerle birlikte çalışmalıdır. Bu &quot;ayrımının sürdürülmesi&quot;, kodunuzun temiz, test edilebilir ve daha sürdürülebilir olmasını sağlar.

Şu anda, `HelloWorldController` sınıfındaki `Welcome` Action yöntemi bir `name` ve `numTimes` parametresi alır ve sonra değerleri doğrudan tarayıcıya çıkarır. Denetleyicinin bu yanıtı bir dize olarak işlemesini sağlamak yerine, denetleyiciyi bir görünüm şablonu kullanacak şekilde değiştirelim. Görünüm şablonu dinamik bir yanıt oluşturur, bu, yanıtı oluşturmak için denetleyiciden uygun veri bitlerini görünüme geçirmeniz gerektiği anlamına gelir. Bunu, denetleyicinin görünüm şablonunun erişebileceği bir `ViewBag` nesnesinde gerektirdiği dinamik verileri (parametreler) yerleştirerek yapabilirsiniz.

*HelloWorldController.cs* dosyasına dönün ve `ViewBag` nesnesine bir `Message` ve `NumTimes` değeri eklemek için `Welcome` yöntemini değiştirin. `ViewBag` dinamik bir nesnedir, bu, içine istediğiniz her şeyi koyabileceğiniz anlamına gelir; `ViewBag` nesnenin içine bir öğe yerleştirene kadar tanımlanmış özellikleri yok. [ASP.NET MVC model bağlama sistemi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) , adlandırılmış parametreleri (`name` ve `numTimes`) adres çubuğundaki sorgu dizesinden yöntemdeki parametrelere otomatik olarak eşler. Tüm *HelloWorldController.cs* dosyası şuna benzer:

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

Artık `ViewBag` nesnesi, otomatik olarak görünüme geçirilecek verileri içerir. Daha sonra bir hoş geldiniz görünüm şablonunuz olması gerekir! Projenin derlendiğinden emin olmak için Build **(veya** Ctrl + Shift + B) öğesini seçin. *Views\helloworld* klasörüne sağ tıklayın ve **Ekle**' ye ve ardından **MVC 5 görünüm sayfası düzen (Razor)** seçeneğine tıklayın.
  
![](adding-a-view/_static/image10.png)   
  
**Öğe Için ad belirtin** Iletişim kutusunda *hoş geldiniz*yazın ve ardından **Tamam**' a tıklayın.   
  
**Düzen sayfası seçin** iletişim kutusunda, varsayılan **\_Layout. cshtml** dosyasını kabul edin ve **Tamam**' a tıklayın.  
  
![](adding-a-view/_static/image11.png)   

*Mvcmovie\views\helloworld\welcome.cshtml* dosyası oluşturulur.

*Welcome. cshtml* dosyasındaki biçimlendirmeyi değiştirin. Kullanıcının &quot;Hello&quot; belirten bir döngü oluşturacaksınız. Tüm *Welcome. cshtml* dosyası aşağıda gösterilmiştir.

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

Uygulamayı çalıştırın ve aşağıdaki URL 'ye gidin:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Artık veriler URL 'den alınır ve [model cildi](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)kullanılarak denetleyiciye geçirilir. Denetleyici, verileri bir `ViewBag` nesnesine paketler ve bu nesneyi görünüme geçirir. Daha sonra Görünüm, verileri kullanıcıya HTML olarak görüntüler.

![](adding-a-view/_static/image12.png)

Yukarıdaki örnekte, denetleyicideki verileri bir görünüme geçirmek için bir `ViewBag` nesnesi kullandık. Öğreticide daha sonra, bir denetleyicideki verileri bir görünüme geçirmek için bir görünüm modeli kullanacağız. Veri geçirme yaklaşımını görüntüleme yaklaşımı, görünüm paketi yaklaşımına göre genellikle çok tercih edilir. Daha fazla bilgi için bkz. blog girdisi [dinamik türü kesin belirlenmiş görünümler](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) . 

Bu, model için bir &quot;d&quot; türüdür, ancak veritabanı türü değildir. Öğrendiklerimizi ve bir film veritabanı oluşturmamızı görelim.

> [!div class="step-by-step"]
> [Önceki](adding-a-controller.md)
> [İleri](adding-a-model.md)
