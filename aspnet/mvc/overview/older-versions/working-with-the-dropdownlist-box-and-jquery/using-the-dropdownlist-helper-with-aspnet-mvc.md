---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: ASP.NET MVC ile DropDownList Yardımcısını kullanma | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6375bb2be158cea18309ffa71c71ac3e67bc91ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538747"
---
# <a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>ASP.NET MVC ile DropDownList Yardımcısını Kullanma

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

Bu öğretici, bir ASP.NET MVC web uygulamasındaki [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) Yardımcısı ve [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) Yardımcısı ile çalışma hakkında temel bilgileri öğretir. Öğreticiyi izlemek için Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanabilirsiniz. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:

- [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)

Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack). Bu öğreticide, [ASP.NET MVC](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) öğreticisi veya[ASP.NET MVC müzik mağazası](../mvc-music-store/mvc-music-store-part-1.md) öğreticisini tamamlayan veya ASP.NET MVC geliştirme hakkında bilgi sahibi olduğunuz varsayılır. Bu öğretici, [ASP.NET MVC müzik deposu](../mvc-music-store/mvc-music-store-part-1.md) öğreticisindeki değiştirilmiş bir projeyle başlar. Başlangıç projesini aşağıdaki bağlantıyla indirebilirsiniz [ C# sürümü indirebilirsiniz](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829).

Tamamlanmış öğretici C# kaynak koduna sahip bir Visual Web Developer projesi, bu konuyla birlikte kullanılabilecek. [İndirin](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d).

### <a name="what-youll-build"></a>Ne oluşturacağız?

Bir kategori seçmek için [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) yardımcısını kullanan eylem yöntemleri ve görünümleri oluşturacaksınız. Ayrıca, yeni bir kategori (örn. tarz veya sanatçı) gerektiğinde kullanılabilecek bir kategori ekle iletişim kutusu eklemek için **jQuery** ' i de kullanacaksınız. Aşağıda yeni bir tarz eklemek ve yeni bir sanatçı eklemek için bağlantıları gösteren oluştur görünümünün ekran görüntüsü verilmiştir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>Öğrenmeniz gereken yetenekler

Öğrenirsiniz:

- Kategori verilerini seçmek için [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) Yardımcısını kullanma.
- Yeni kategoriler eklemek için **jQuery** iletişim kutusu ekleme.

### <a name="getting-started"></a>Başlarken

Aşağıdaki bağlantıyla birlikte Başlatıcı projesini indirerek başlayın, [indirin](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829). Windows Gezgini 'nde, *DDL\_Starter. zip* dosyasına sağ tıklayın ve Özellikler ' i seçin. **DDL\_Starter. zip özellikleri** Iletişim kutusunda Engellemeyi kaldır ' ı seçin.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

DDL\_Starter. zip dosyasına sağ tıklayın ve dosyayı sıkıştırmayı açmak için **Tümünü Ayıkla** ' yı seçin. Visual Web Developer 2010 Express ("Visual Web Developer" veya "VWD" for short) veya Visual Studio 2010 ile *Startmusicstore. sln* dosyasını açın.

Uygulamayı çalıştırmak için CTRL + F5 tuşlarına basın ve **Test** bağlantısına tıklayın.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

**Film kategorisi seçin (basit)** bağlantısını seçin. Seçili değeri komedi bir film türü seçme listesi görüntülenir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

Tarayıcıya sağ tıklayın ve kaynağı görüntüle ' yi seçin. Sayfa için HTML görüntülenir. Aşağıdaki kodda select öğesi için HTML gösterilmektedir.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

Seçim listesindeki her bir öğenin bir değere sahip olduğunu görebilirsiniz (eylem için 0, Drama için 1, komedi için 2 ve bilimi için 3) ve bir görünen ad (eylem, Drama, komedi ve bilim kurgu). Yukarıdaki kod, bir seçim listesi için standart HTML 'dir.

Seçim listesini Drama olarak değiştirin ve **Gönder** düğmesine basın. Tarayıcıdaki URL `http://localhost:2468/Home/CategoryChosen?MovieType=1` ve sayfa seçtiğiniz sayfada görüntülenir **: 1**.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

*Controllers\homecontroller.cs* dosyasını açın ve `SelectCategory` metodunu inceleyin.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

HTML seçme listesi oluşturmak için kullanılan [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) Yardımcısı, açıkça veya örtük olarak bir **IEnumerable&lt;SelectListItem &gt;** gerektirir. Diğer bir deyişle, **ıenumerable&lt;selectlistıtem &gt;** açıkça [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) Yardımcısı 'na geçirebilir veya **IEnumerable&lt;SelectListItem &gt;** öğesini, **SelectListItem** Için model özelliği olarak aynı adı kullanarak [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 'e ekleyebilirsiniz. **SelectListItem** 'ın örtük ve açık olarak bir sonraki bölümünde ele geçirilmesi önerilir. Yukarıdaki kod, bir **ıenumerable&lt;SelectListItem &gt;** oluşturmak için mümkün olan en basit yolu gösterir ve metin ve değerlerle doldurmaktır. `Comedy`[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) 'ın [Seçili](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx) özelliği **true** olarak ayarlandığını aklınızda, bu, işlenen seçim listesinin listedeki seçili öğe olarak **komedi** görüntülemesine neden olur.

Yukarıda oluşturulan **ıenumerable&lt;SelectListItem &gt;** , [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) 'e MovieType adıyla eklenir. **Ienumerable&lt;SelectListItem &gt;** aşağıda gösterilen [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) Yardımcısı 'na örtük olarak geçiririz.

*Views\home\selectcategory.exe* dosyasını açın ve biçimlendirmeyi inceleyin.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

Üçüncü satırda, düzeni/paylaşılan/\_basit\_Layout. cshtml olarak ayarlayacağız. Bu, Standart Düzen dosyasının basitleştirilmiş bir sürümüdür. Bunu, görüntüleme ve işlenmiş HTML 'in basit tutulması için yaptık.

Bu örnekte, uygulamanın durumunu değiştirmedik, bu nedenle verileri http **Al**, **http post**değil kullanarak gönderecağız. [Http get veya post ' i seçmek IÇIN W3C bölümüne hızlı denetim listesi](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)' ne bakın. Uygulamayı değiştirmedik ve formu gönderdiğimiz için, eylem yöntemini, denetleyiciyi ve form yöntemini (**http post** veya **http get**) belirtmemizi sağlayan [HTML. BeginForm](https://msdn.microsoft.com/library/dd460344.aspx) aşırı yüklemesini kullanıyoruz. Genellikle görünümler, hiçbir parametre alan [HTML. BeginForm](https://msdn.microsoft.com/library/dd505244.aspx) aşırı yüklemesini içerir. Hiçbir parametre sürümü varsayılan olarak form verilerini aynı eylem yönteminin ve denetleyicinin GÖNDERI sürümüne nakletmez.

Aşağıdaki satır

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

**DropDownList** Yardımcısı 'na bir dize bağımsız değişkeni geçirir. Örneğimizde "MovieType" dizesi şu iki şeyi yapar:

- **ViewBag**Içinde bir **IEnumerable&lt;SelectListItem &gt;** bulmak için **DropDownList** Yardımcısı için anahtar sağlar.
- MovieType form öğesine veri bağımlıdır. Gönderme yöntemi **http get**ise, `MovieType` bir sorgu dizesi olacaktır. Gönderme yöntemi **http post**ise, ileti gövdesine `MovieType` eklenecektir. Aşağıdaki görüntüde, değeri 1 olan sorgu dizesi gösterilmektedir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

Aşağıdaki kod, formun gönderildiği `CategoryChosen` yöntemini gösterir.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

Sınama sayfasına geri gidin ve **HTML SelectList** bağlantısını seçin. HTML sayfası, basit ASP.NET MVC test sayfasına benzer bir select öğesi oluşturur. Tarayıcı penceresine sağ tıklayın ve **kaynağı görüntüle**' yi seçin. Seçim listesi için HTML biçimlendirmesi temelde aynıdır. HTML sayfasını test edin, ASP.NET MVC eylem yöntemi ve daha önce sınadığımız görünüm gibi çalışacaktır.

### <a name="improving-the-movie-select-list-with-enums"></a>Numaralandırmalar içeren film seçme listesini geliştirme

Uygulamanızdaki Kategoriler düzeltildiğinde ve değişmeyecektir, kodunuzun daha sağlam ve daha basit olması için Numaralandırmaların avantajlarından faydalanabilirsiniz. Yeni bir kategori eklediğinizde, doğru kategori değeri oluşturulur. Yeni bir kategori eklediğinizde kopyalama ve yapıştırma hatalarını önler, ancak Kategori değerini güncelleştirmeyi unutabilirsiniz.

*Controllers\homecontroller.cs* dosyasını açın ve aşağıdaki kodu inceleyin:

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[Enum](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories` dört film türünü yakalar. `SetViewBagMovieType` yöntemi `eMovieCategories`**numaralandırmasından** **IEnumerable&lt;SelectListItem &gt;** oluşturur ve `Selected` özelliğini `selectedMovie` parametresinden ayarlar. `SelectCategoryEnum` Action yöntemi, `SelectCategory` Action yöntemiyle aynı görünümü kullanır.

Sınama sayfasına gidin ve `Select Movie Category (Enum)` bağlantısına tıklayın. Bu kez, bir değer (sayı) yerine, sabit listesini temsil eden bir dize görüntülenir.

### <a name="posting-enum-values"></a>Enum değerlerini postalama

HTML formları genellikle sunucuya veri göndermek için kullanılır. Aşağıdaki kod `SelectCategoryEnumPost` yönteminin `HTTP GET` ve `HTTP POST` sürümlerini gösterir.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

`eMovieCategories` numaralandırması `POST` yöntemine geçirerek hem enum değerini hem de sabit listesi dizesini ayıklayabiliriz. Örneği çalıştırın ve test sayfasına gidin. `Select Movie Category(Enum Post)` bağlantısına tıklayın. Bir film türü seçip Gönder düğmesine basın. Görüntü hem değeri hem de film türünün adını gösterir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>Birden çok bölüm Seç öğe oluşturma

[ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) HTML Yardımcısı, HTML `<select>` öğesini, kullanıcıların birden çok seçim yapmasına izin veren `multiple` özniteliğiyle işler. Test bağlantısına gidin ve **Çoklu ülke seç** bağlantısını seçin. İşlenmiş Kullanıcı arabirimi birden çok ülke seçmenizi sağlar. Aşağıdaki görüntüde Kanada ve Çin seçilidir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>MultiSelectCountry kodunu inceleme

*Controllers\homecontroller.cs* dosyasından aşağıdaki kodu inceleyin.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

`GetCountries` yöntemi, ülkelerin bir listesini oluşturur ve sonra bunu `MultiSelectList` oluşturucusuna geçirir. Yukarıdaki `GetCountries` yönteminde kullanılan `MultiSelectList` Oluşturucu aşırı yüklemesi dört parametre alır:

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *Items*: listedeki öğeleri Içeren bir [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) . Yukarıdaki örnekte, ülkelerin listesi.
2. *DataValueField*: değeri içeren **IEnumerable** listesindeki özelliğin adı. Yukarıdaki örnekte `ID` özelliği.
3. *DataTextField*: görüntülenecek bilgileri içeren **IEnumerable** listesindeki özelliğin adı. Yukarıdaki örnekte `name` özelliği.
4. *SelectedValues*: seçili değerlerin listesi.

Yukarıdaki örnekte `MultiSelectCountry` yöntemi seçili ülkeler için bir `null` değeri geçirir, bu yüzden Kullanıcı arabirimi görüntülenirken hiçbir ülke seçilmezler. Aşağıdaki kod `MultiSelectCountry` görünümünü işlemek için kullanılan Razor işaretlemesini gösterir.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

Yukarıda kullanılan HTML yardımcı [ListBox](https://msdn.microsoft.com/library/dd470200.aspx) yöntemi iki parametre alır, model bağlama özelliğinin adı ve Select seçeneklerini ve değerlerini Içeren [MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) . Yukarıdaki `ViewBag.YouSelected` kodu, formu gönderdiğinizde seçtiğiniz ülkelerin değerlerini göstermek için kullanılır. `MultiSelectCountry` yönteminin HTTP POST yüklemesini inceleyin.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected` Dynamic özelliği, form koleksiyonundaki `Countries` girdisi için edinilen Seçili ülkeleri içerir. Bu sürümde, Getülkeler yöntemine seçili ülkelerin bir listesi geçirilir, bu nedenle `MultiSelectCountry` görünümü görüntülendiğinde, seçilen ülkeler Kullanıcı arabiriminde seçilir.

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>Seçili jQuery eklentisi ile bir select öğesi kullanımı kolay yapılıyor

[Seçili](https://harvesthq.github.com/chosen/) jQuery EKLENTISI bir HTML &lt;eklenebilir ve Kullanıcı dostu BIR kullanıcı arabirimi oluşturmak için&gt; öğesini seçin. Aşağıdaki görüntüler, `MultiSelectCountry` görünümü ile [Seçili](https://harvesthq.github.com/chosen/) jQuery eklentisini gösterir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

Aşağıdaki iki görüntüde **Kanada** seçilidir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

Yukarıdaki görüntüde Kanada seçilidir ve bir **x** içerir ve seçimi kaldırmak için tıklayabilirsiniz. Aşağıdaki görüntüde Kanada, Çin ve Japonya seçili gösterilmektedir.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>Seçili jQuery eklentisinin takılarak

JQuery ile ilgili bazı deneyiminiz varsa aşağıdaki bölüm daha kolay olur. Daha önce jQuery kullanmadıysanız, aşağıdaki jQuery öğreticilerden birini denemek isteyebilirsiniz.

- JQuery, [John Resg](http://ejohn.org/) tarafından [nasıl çalışmaktadır](http://docs.jquery.com/Tutorials:How_jQuery_Works)
- [Jörn Zaefftole](http://bassistance.de/) [jQuery ile çalışmaya](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery) başlama
- [Cody Lindley](http://codylindley.com/) tarafından [gerçek jQuery örnekleri](http://codylindley.com/blogstuff/js/jquery/#)

Seçilen eklenti, Bu öğreticiye eşlik eden başlatıcı ve tamamlanmış örnek projelere dahildir. Bu öğreticide, yalnızca Kullanıcı arabirimine bağlamak için jQuery kullanmanız gerekir. Seçili jQuery eklentisini bir ASP.NET MVC projesinde kullanmak için şunları yapmanız gerekir:

1. Seçili eklentiyi [GitHub](https://github.com/harvesthq/chosen/)'dan indirin. Bu adım sizin için gerçekleştirildi.
2. Seçilen klasörü ASP.NET MVC projenize ekleyin. Önceki adımda indirdiğiniz seçili olan eklentiden varlıkları seçili klasöre ekleyin. Bu adım sizin için gerçekleştirildi.
3. Seçili eklentiyi **DropDownList** veya **ListBox** HTML Yardımcısı 'na bağlama.

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>Seçili eklenti MultiSelectCountry görünümüne yerleştirdim.

*Views\home\multiselectcountry.exe* dosyasını açın ve `Html.ListBox`bir `htmlAttributes` parametresi ekleyin. Ekleyeceğiniz parametre seçim listesi için bir sınıf adı içerir (`@class = "chzn-select"`). Tamamlanan kod aşağıda gösterilmektedir:

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

Yukarıdaki kodda, `class = "chzn-select"`HTML özniteliğini ve öznitelik değerini ekliyoruz. Önceki \@ karakteri Razor görünüm altyapısıyla hiçbir şey yapmaz. `class` bir [ C# anahtar sözcüktür](https://msdn.microsoft.com/library/x53a06bb.aspx). C#anahtar sözcükler, \@ önek olarak içermedikleri sürece tanımlayıcı olarak kullanılamaz. Yukarıdaki örnekte, `@class` geçerli bir tanımlayıcıdır **, ancak sınıf** bir anahtar sözcüktür.

*Seçili/seçili. jQuery. js* ve *Seçili/seçili. css* dosyalarına başvuruları ekleyin. *Seçili/seçili. jQuery. js* ve seçilen eklentinin işlev düzeyini uygular. *Seçili/seçili. css* dosyası stili sağlar. Bu başvuruları *Views\home\multiselectcountry.exe. cshtml* dosyasının altına ekleyin. Aşağıdaki kod, seçilen eklentiye nasıl başvurulacağını gösterir.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

**HTML. ListBox** kodunda kullanılan sınıf adını kullanarak seçili eklentiyi etkinleştirin. Yukarıdaki örnekte, sınıf adı `chzn-select`. *Views\home\multiselectcountry.exe. cshtml* görünüm dosyasının altına aşağıdaki satırı ekleyin. Bu satır seçili eklentiyi etkinleştirir.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

Aşağıdaki satır, sınıf adı `chzn-select`DOM öğesini seçen jQuery Ready işlevini çağırma sözdizimidir.

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

Yukarıdaki çağrıdan döndürülen sarmalanmış küme, seçilen eklentiyi bağlayan seçili yöntemi (`.chosen();`) uygular.

Aşağıdaki kod, tamamlanan *Views\home\multiselectcountry.exe. cshtml* görünüm dosyasını gösterir.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

Uygulamayı çalıştırın ve `MultiSelectCountry` görünümüne gidin. Ülke eklemeyi ve silmeyi deneyin. Örnek yükleme, Ayrıca, **ViewBag**yerine bir görünüm modeli kullanarak MultiSelectCountry işlevlerini uygulayan bir `MultiCountryVM` yöntemi ve görünümü içerir.

Sonraki bölümde, ASP.NET MVC scafkatlama mekanizmasının **DropDownList** Yardımcısı ile nasıl çalıştığını göreceksiniz.

> [!div class="step-by-step"]
> [Next](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)
