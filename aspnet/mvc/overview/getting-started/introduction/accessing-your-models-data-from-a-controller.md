---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Bir denetleyiciden modelinizin verilerine erişme | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: e01953dcfb2abf2db53a8aa869aa75b40485daca
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519095"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Bir Denetleyiciden Modelinizin Verilerine Erişme

[Rick Anderson]((https://twitter.com/RickAndMSFT)) tarafından

[!INCLUDE [Tutorial Note](index.md)]

Bu bölümde, yeni bir `MoviesController` sınıfı oluşturacak ve film verilerini alan ve bir görünüm şablonu kullanarak tarayıcıda görüntüleyen kodu yazılacak.

Sonraki adıma geçmeden önce **uygulamayı derleyin** . Uygulamayı dermezseniz, denetleyici eklenirken bir hata alırsınız.

Çözüm Gezgini, *denetleyiciler* klasörüne sağ tıklayın ve ardından **Ekle**' ye ve ardından **Denetleyici**' ye tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

**Yapı Iskelesi Ekle** iletişim kutusunda, **Entity Framework kullanarak, görünümler Içeren MVC 5 denetleyici**' ye tıklayın ve ardından **Ekle**' ye tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- Model sınıfı için **filmi (MvcMovie. modeller)** seçin.
- Veri bağlamı sınıfı için **Moviedbcontext (MvcMovie. modeller)** öğesini seçin.
- Denetleyici adı için **MoviesController**girin.

  Aşağıdaki görüntüde tamamlanan iletişim kutusu gösterilmektedir.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

**Ekle**'yi tıklatın. (Bir hata alırsanız, denetleyiciyi eklemeye başlamadan önce uygulamayı derlemeniz olasıdır.) Visual Studio aşağıdaki dosyaları ve klasörleri oluşturur:

- *Controllers* klasöründeki *bir MoviesController.cs* dosyası.
- *Views\filmler* klasörü.
- Yeni *Views\filmlerini* klasöründeki *. cshtml, delete. cshtml, details. cshtml, Edit. cshtml*ve *Index. cshtml* oluşturun.

Visual Studio [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (oluşturma, okuma, güncelleştirme ve silme) eylem yöntemlerini ve görünümlerini sizin için otomatik olarak oluşturdu (CRUD eylem yöntemlerinin ve görünümlerinin otomatik olarak oluşturulması, yapı iskelesi olarak bilinir). Artık, film girişleri oluşturmanızı, listelemenizi, düzenlemenizi ve silmenizi sağlayan tam işlevli bir Web uygulamanız vardır.

Uygulamayı çalıştırın ve **MVC film** bağlantısına tıklayın (veya tarayıcınızın adres çubuğundaki URL 'ye */filmler* ekleyerek `Movies` denetleyiciye gidin). Uygulama varsayılan yönlendirmeye bağlı olduğundan ( *uygulama\_Start\RouteConfig.cs* dosyasında tanımlanan), tarayıcı isteği `http://localhost:xxxxx/Movies`, `Movies` denetleyicisinin varsayılan `Index` eylem yöntemine yönlendirilir. Diğer bir deyişle, tarayıcı istek `http://localhost:xxxxx/Movies` `http://localhost:xxxxx/Movies/Index`tarayıcı isteğiyle aynı şekilde aynıdır. Henüz hiç eklemediğiniz için sonuç, filmlerin boş bir listesidir.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>Film oluşturma

**Yeni oluştur** bağlantısını seçin. Bir film hakkındaki ayrıntıları girin ve ardından **Oluştur** düğmesine tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> Fiyat alanına ondalık nokta veya virgül giremeyebilirsiniz. ondalık bir nokta ve ABD Ingilizcesi olmayan tarih biçimleri için virgül (&quot;,&quot;) kullanan Ingilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için, *globalize. js* ve belirli *kültürleri/globalize. kültürleri. js* dosyanızı ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve JavaScript 'i `Globalize.parseFloat` kullanacak şekilde eklemeniz gerekir. Bunu bir sonraki öğreticide nasıl yapacağım. Şimdilik, yalnızca 10 gibi tüm sayıları girmeniz yeterlidir.

**Oluştur** düğmesine tıkladığınızda form, film bilgilerinin veritabanına kaydedildiği sunucuya gönderilmesini sağlar. Daha sonra, yeni oluşturulan filmi listede görebileceğiniz */filmler* URL 'sine yönlendirilirsiniz.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Birkaç film girişi oluşturun. Tüm işlevsel olan **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarını deneyin.

## <a name="examining-the-generated-code"></a>Oluşturulan kodu İnceleme

*Controllers\MoviesController.cs* dosyasını açın ve oluşturulan `Index` yöntemini inceleyin. `Index` yöntemi ile birlikte film denetleyicisi 'nin bir bölümü aşağıda gösterilmiştir.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

`Movies` denetleyicisine yapılan bir istek, `Movies` tablosundaki tüm girdileri döndürür ve sonra sonuçları `Index` görünümüne geçirir. `MoviesController` sınıfından aşağıdaki satır, daha önce açıklandığı gibi bir film veritabanı bağlamını başlatır. Film veritabanı bağlamını kullanarak filmleri sorgulayabilir, düzenleyebilir ve silebilirsiniz.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>Türü kesin belirlenmiş modeller ve @model anahtar sözcüğü

Bu öğreticide daha önce, bir denetleyicinin `ViewBag` nesnesini kullanarak bir görünüm şablonuna nasıl veri veya nesne geçirekullanabileceğinizi gördünüz. `ViewBag`, bir görünüme bilgi geçirmek için uygun, geç bağlanan bir yol sağlayan dinamik bir nesnedir.

MVC Ayrıca, *türü kesin* belirlenmiş nesneleri bir görünüm şablonuna geçirebilme olanağı da sağlar. Bu kesin türü belirtilmiş yaklaşım, Visual Studio düzenleyicisinde kodunuzun ve daha zengin [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) 'in derleme zamanı denetimini daha iyi bir şekilde sunar. Visual Studio 'daki scafkatlama mekanizması, bu yaklaşımı (yani, *türü kesin* belirlenmiş bir model geçirerek) `MoviesController` sınıfıyla kullandı ve yöntemleri ve görünümleri oluştururken şablonları görüntüleyebilir.

*Controllers\MoviesController.cs* dosyasında, oluşturulan `Details` yöntemini inceleyin. `Details` yöntemi aşağıda gösterilmiştir.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

`id` parametresi genellikle rota verileri olarak geçirilir, örneğin `http://localhost:1234/movies/details/1` denetleyiciyi film denetleyicisine, `details` eylemini ve `id` 1 olarak ayarlar. Ayrıca kimliği bir sorgu dizesi ile aşağıdaki gibi geçirebilirsiniz:

`http://localhost:1234/movies/details?id=1`

Bir `Movie` bulunursa, `Details` görünümüne `Movie` modelinin bir örneği geçirilir:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

*Views\Movies\Details.cshtml* dosyasının içeriğini inceleyin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

Görünüm şablonu dosyasının üst kısmına bir `@model` ifadesini ekleyerek, görünümün beklediği nesne türünü belirtebilirsiniz. Film denetleyicisini oluştururken, Visual Studio *details. cshtml* dosyasının en üstüne aşağıdaki `@model` ifadesini otomatik olarak dahil edin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Bu `@model` yönergesi, kesin olarak belirlenmiş bir `Model` nesnesi kullanarak denetleyicinin görünüme geçirildiği filme erişmenizi sağlar. Örneğin, *details. cshtml* şablonunda, kod her bir film alanını `DisplayNameFor` geçirir ve türü kesin belirlenmiş `Model` nesnesi olan HTML Yardımcıları [için Display.](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) `Create` ve `Edit` yöntemleri ve Görünüm şablonları bir film modeli nesnesi de iletir.

*Index. cshtml* görünüm şablonunu ve *MoviesController.cs* dosyasındaki `Index` yöntemini inceleyin. [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) , `Index` eylem yönteminde `View` Helper metodunu çağırdığında kodun bir nesne nasıl oluşturduğunu göreceksiniz. Kod daha sonra bu `Movies` listesini `Index` eylem yönteminden görünüme geçirir:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

Film denetleyicisini oluştururken, Visual Studio *Index. cshtml* dosyasının en üstüne aşağıdaki `@model` ifadesini otomatik olarak dahil edin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

Bu `@model` yönergesi, kesin olarak belirlenmiş bir `Model` nesnesi kullanarak denetleyicinin görünüme geçirildiği film listesine erişmenizi sağlar. Örneğin, *Index. cshtml* şablonunda kod, türü kesin belirlenmiş `Model` nesnesi üzerinde `foreach` bir bildiri gerçekleştirerek filmlerde döngü yapılır:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

`Model` nesne kesin olarak yazıldığı için (bir `IEnumerable<Movie>` nesnesi olarak), döngüdeki her bir `item` nesnesi `Movie`olarak yazılır. Diğer avantajlar arasında bu, kod Düzenleyicisi 'nde kodun derleme zamanı denetimini ve tam IntelliSense desteğini elde ettiğiniz anlamına gelir:

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB ile çalışma

Entity Framework Code First, belirtilen veritabanı bağlantı dizesinin henüz mevcut olmayan bir `Movies` veritabanına işaret ettiği algılandı, bu nedenle veritabanını otomatik olarak oluşturdu Code First. Uygulamasının oluşturulduğunu, *uygulama\_veri* klasörüne bakarak doğrulayabilirsiniz. *Filmler. mdf* dosyasını görmüyorsanız, **Çözüm Gezgini** araç çubuğunda **tüm dosyaları göster** düğmesine tıklayın, **Yenile** düğmesine tıklayın ve ardından *uygulama\_verileri* klasörünü genişletin.

![](accessing-your-models-data-from-a-controller/_static/image9.png)

*Film. mdf* ' ye çift TıKLAYARAK **Sunucu Gezgini**'Ni açın ve ardından Filmler tablosunu görmek için **Tablolar** klasörünü genişletin. ID ' ın yanındaki anahtar simgesine göz önünde. Varsayılan olarak, EF, birincil anahtar adlı bir özellik oluşturacak. EF ve MVC hakkında daha fazla bilgi için, bkz. Tom Dykstra 'ın [MVC ve EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)hakkında harika bir öğreticisi.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

`Movies` tabloya sağ tıklayıp **tablo verilerini göster** ' i seçerek oluşturduğunuz verileri görüntüleyin.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

`Movies` tabloya sağ tıklayıp **tablo tanımını aç** ' ı seçerek Entity Framework Code First sizin için oluşturduğu tablo yapısını görüntüleyin.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

`Movies` tablosu şemasının, daha önce oluşturduğunuz `Movie` sınıfa nasıl eşlendiğini fark edin. Entity Framework Code First, bu şemayı `Movie` sınıfınızı temel alarak sizin için otomatik olarak oluşturdu.

İşiniz bittiğinde, *Moviedbcontext* ' i sağ tıklatıp **Bağlantıyı kapat**' ı seçerek bağlantıyı kapatın. (Bağlantıyı kapatmazsanız, projeyi bir sonraki çalıştırışınızda bir hata alabilirsiniz).

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

Artık veri görüntüleme, düzenleme, güncelleştirme ve silme için bir veritabanınız ve sayfalarınız vardır. Sonraki öğreticide, iskele eklenen kodun geri kalanını inceleyeceğiz ve bu veritabanında film aramanızı sağlayan bir `SearchIndex` yöntemi ve bir `SearchIndex` görünümü ekleyeceğiz. MVC ile Entity Framework kullanma hakkında daha fazla bilgi için, bkz. [ASP.NET MVC uygulaması için Entity Framework veri modeli oluşturma](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

> [!div class="step-by-step"]
> [Önceki](creating-a-connection-string.md)
> [İleri](examining-the-edit-methods-and-edit-view.md)
