---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: Bir denetleyiciden modelinizin verilerine erişme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456172"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Bir Denetleyiciden Modelinizin Verilerine Erişme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.

Bu bölümde, yeni bir `MoviesController` sınıfı oluşturacak ve film verilerini alan ve bir görünüm şablonu kullanarak tarayıcıda görüntüleyen kodu yazılacak.

Sonraki adıma geçmeden önce **uygulamayı derleyin** .

*Denetleyiciler* klasörüne sağ tıklayın ve yeni bir `MoviesController` denetleyicisi oluşturun. Aşağıdaki seçenekler, uygulamanızı derlene kadar görünmez. Aşağıdaki seçenekleri belirleyin:

- Denetleyici adı: **MoviesController**. (Bu varsayılandır. )
- Şablon: **Entity Framework kullanarak okuma/yazma eylemleri ve görünümleri olan MVC denetleyicisi**.
- Model Sınıfı: **Film (MvcMovie. modeller)** .
- Veri bağlamı sınıfı: **Moviedbcontext (MvcMovie. modeller)** .
- Görünümler: **Razor (cshtml)** . (Varsayılan.)

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

**Ekle**'ye tıklayın. Visual Studio Express aşağıdaki dosya ve klasörleri oluşturur:

- Projenin *Controllers* klasöründeki *bir MoviesController.cs* dosyası.
- Projenin *Görünümler* klasöründeki *filmler* klasörü.
- Yeni *Views\filmlerini* klasöründeki *. cshtml, delete. cshtml, details. cshtml, Edit. cshtml*ve *Index. cshtml* oluşturun.

ASP.NET MVC 4, sizin için CRUD (oluşturma, okuma, güncelleştirme ve silme) eylem yöntemlerini ve görünümlerini otomatik olarak oluşturdu (CRUD eylem yöntemlerinin ve görünümlerinin otomatik olarak oluşturulması yapı iskelesi olarak bilinir). Artık, film girişleri oluşturmanızı, listelemenizi, düzenlemenizi ve silmenizi sağlayan tam işlevli bir Web uygulamanız vardır.

Uygulamayı çalıştırın ve tarayıcınızın adres çubuğundaki URL 'ye */filmler* ekleyerek `Movies` denetleyiciye gidin. Uygulama varsayılan yönlendirmeye bağlı olduğundan ( *Global. asax* dosyasında tanımlı), tarayıcı isteği `http://localhost:xxxxx/Movies`, `Movies` denetleyicisinin varsayılan `Index` eylem yöntemine yönlendirilir. Diğer bir deyişle, tarayıcı istek `http://localhost:xxxxx/Movies` `http://localhost:xxxxx/Movies/Index`tarayıcı isteğiyle aynı şekilde aynıdır. Henüz hiç eklemediğiniz için sonuç, filmlerin boş bir listesidir.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>Film oluşturma

**Yeni oluştur** bağlantısını seçin. Bir film hakkındaki ayrıntıları girin ve ardından **Oluştur** düğmesine tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image3.png)

**Oluştur** düğmesine tıkladığınızda form, film bilgilerinin veritabanına kaydedildiği sunucuya gönderilmesini sağlar. Daha sonra, yeni oluşturulan filmi listede görebileceğiniz */filmler* URL 'sine yönlendirilirsiniz.

![Indexwhenharrymet](accessing-your-models-data-from-a-controller/_static/image4.png "Indexwhenharrymet")

Birkaç film girişi oluşturun. Tüm işlevsel olan **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarını deneyin.

## <a name="examining-the-generated-code"></a>Oluşturulan kodu İnceleme

*Controllers\MoviesController.cs* dosyasını açın ve oluşturulan `Index` yöntemini inceleyin. `Index` yöntemi ile birlikte film denetleyicisi 'nin bir bölümü aşağıda gösterilmiştir.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

`MoviesController` sınıfından aşağıdaki satır, daha önce açıklandığı gibi bir film veritabanı bağlamını başlatır. Film veritabanı bağlamını kullanarak filmleri sorgulayabilir, düzenleyebilir ve silebilirsiniz.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

`Movies` denetleyicisine yapılan bir istek, film veritabanının `Movies` tablosundaki tüm girişleri döndürür ve sonra sonuçları `Index` görünümüne geçirir.

## <a name="strongly-typed-models-and-the-model-keyword"></a>Türü kesin belirlenmiş modeller ve @model anahtar sözcüğü

Bu öğreticide daha önce, bir denetleyicinin `ViewBag` nesnesini kullanarak bir görünüm şablonuna nasıl veri veya nesne geçirekullanabileceğinizi gördünüz. `ViewBag`, bir görünüme bilgi geçirmek için uygun, geç bağlanan bir yol sağlayan dinamik bir nesnedir.

ASP.NET MVC, kesin olarak belirlenmiş verileri veya nesneleri bir görünüm şablonuna geçirme özelliği de sağlar. Bu kesin türü belirtilmiş yaklaşım, Visual Studio düzenleyicisinde kodunuzun ve daha zengin IntelliSense 'in derleme zamanı denetimini daha iyi bir şekilde sunar. Visual Studio 'daki scafkatlama mekanizması, `MoviesController` sınıfıyla bu yaklaşımı kullandı ve yöntem ve görünümleri oluştururken şablonları görüntüleyebilir.

*Controllers\MoviesController.cs* dosyasında, oluşturulan `Details` yöntemini inceleyin. `Details` yöntemi ile birlikte film denetleyicisi 'nin bir bölümü aşağıda gösterilmiştir.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

Bir `Movie` bulunursa, Ayrıntılar görünümüne `Movie` modelinin bir örneği geçirilir. *Views\Movies\Details.cshtml* dosyasının içeriğini inceleyin.

Görünüm şablonu dosyasının üst kısmına bir `@model` ifadesini ekleyerek, görünümün beklediği nesne türünü belirtebilirsiniz. Film denetleyicisini oluştururken, Visual Studio *details. cshtml* dosyasının en üstüne aşağıdaki `@model` ifadesini otomatik olarak dahil edin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

Bu `@model` yönergesi, kesin olarak belirlenmiş bir `Model` nesnesi kullanarak denetleyicinin görünüme geçirildiği filme erişmenizi sağlar. Örneğin, *details. cshtml* şablonunda, kod her bir film alanını `DisplayNameFor` geçirir ve türü kesin belirlenmiş `Model` nesnesi olan HTML Yardımcıları [için Display.](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) Oluşturma ve düzenleme yöntemleri ve Görünüm şablonları da bir film modeli nesnesi iletir.

*Index. cshtml* görünüm şablonunu ve *MoviesController.cs* dosyasındaki `Index` yöntemini inceleyin. [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) , `Index` eylem yönteminde `View` Helper metodunu çağırdığında kodun bir nesne nasıl oluşturduğunu göreceksiniz. Kod daha sonra bu `Movies` listesini denetleyiciden görünüme geçirir:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

Film denetleyicisini oluştururken, Visual Studio Express *Index. cshtml* dosyasının en üstüne aşağıdaki `@model` ifadesini otomatik olarak dahil edin:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Bu `@model` yönergesi, kesin olarak belirlenmiş bir `Model` nesnesi kullanarak denetleyicinin görünüme geçirildiği film listesine erişmenizi sağlar. Örneğin, *Index. cshtml* şablonunda kod, türü kesin belirlenmiş `Model` nesnesi üzerinde `foreach` bir bildiri gerçekleştirerek filmlerde döngü yapılır:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

`Model` nesne kesin olarak yazıldığı için (bir `IEnumerable<Movie>` nesnesi olarak), döngüdeki her bir `item` nesnesi `Movie`olarak yazılır. Diğer avantajlar arasında bu, kod Düzenleyicisi 'nde kodun derleme zamanı denetimini ve tam IntelliSense desteğini elde ettiğiniz anlamına gelir:

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>SQL Server LocalDB ile çalışma

Entity Framework Code First, belirtilen veritabanı bağlantı dizesinin henüz mevcut olmayan bir `Movies` veritabanına işaret ettiği algılandı, bu nedenle veritabanını otomatik olarak oluşturdu Code First. Uygulamasının oluşturulduğunu, *uygulama\_veri* klasörüne bakarak doğrulayabilirsiniz. *Filmler. mdf* dosyasını görmüyorsanız, **Çözüm Gezgini** araç çubuğunda **tüm dosyaları göster** düğmesine tıklayın, **Yenile** düğmesine tıklayın ve ardından *uygulama\_verileri* klasörünü genişletin.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

*Film. mdf* ' ye çift TıKLAYARAK **veritabanı Gezginini**açın ve ardından Filmler tablosunu görmek için **Tablolar** klasörünü genişletin.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> Veritabanı Gezgini görünmezse, **Araçlar** menüsünde **veritabanına Bağlan**' ı seçin ve ardından **veri kaynağı seç** iletişim kutusunu iptal edin. Bu, veritabanı Gezginini açmaya zorlanır.

> [!NOTE]
> VWD veya Visual Studio 2010 kullanıyorsanız ve aşağıdakilerden birine benzer bir hata alırsanız:
> 
> - ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES. veritabanı Sürüm 706 olduğundan, MDF açılamıyor. Bu sunucu sürüm 655 ve öncesini destekler. Düşürme yolu desteklenmiyor.
> - &quot;InvalidOperation özel durumu, Kullanıcı kodu tarafından yakalanmıştı&quot; sağlanan SqlConnection bir ilk katalog belirtmiyor.
> 
> [SQL Server veri araçları](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) ve [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)'yi yüklemeniz gerekir. Önceki sayfada belirtilen `MovieDBContext` bağlantı dizesini doğrulayın.

`Movies` tabloya sağ tıklayıp **tablo verilerini göster** ' i seçerek oluşturduğunuz verileri görüntüleyin.

![](accessing-your-models-data-from-a-controller/_static/image8.png)

`Movies` tabloya sağ tıklayıp **tablo tanımını aç** ' ı seçerek Entity Framework Code First sizin için oluşturduğu tablo yapısını görüntüleyin.

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

`Movies` tablosu şemasının, daha önce oluşturduğunuz `Movie` sınıfa nasıl eşlendiğini fark edin. Entity Framework Code First, bu şemayı `Movie` sınıfınızı temel alarak sizin için otomatik olarak oluşturdu.

İşiniz bittiğinde, *Moviedbcontext* ' i sağ tıklatıp **Bağlantıyı kapat**' ı seçerek bağlantıyı kapatın. (Bağlantıyı kapatmazsanız, projeyi bir sonraki çalıştırışınızda bir hata alabilirsiniz).

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

Artık veritabanını ve bir basit liste sayfasını, içeriği görüntüleme sayfasına sahipsiniz. Sonraki öğreticide, iskele eklenen kodun geri kalanını inceleyeceğiz ve bu veritabanında film aramanızı sağlayan bir `SearchIndex` yöntemi ve bir `SearchIndex` görünümü ekleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](adding-a-model.md)
> [İleri](examining-the-edit-methods-and-edit-view.md)
