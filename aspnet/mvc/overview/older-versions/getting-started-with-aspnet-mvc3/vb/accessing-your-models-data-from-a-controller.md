---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: Bir denetleyiciden modelinizin verilerine erişme (VB) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 37f45d8f12e3ab5c485718bcf2c59934ad272118
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458028"
---
# <a name="accessing-your-models-data-from-a-controller-vb"></a>Bir Denetleyiciden Modelinizin Verilerine Erişme (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Bu konuyla birlikte VB.NET kaynak koduna sahip bir Visual Web Developer projesi mevcuttur. [Vb.NET sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). İsterseniz C#, Bu öğreticinin [ C# sürümüne](../cs/accessing-your-models-data-from-a-controller.md) geçin.

Bu bölümde, yeni bir `MoviesController` sınıfı oluşturacak ve film verilerini alan ve bir görünüm şablonu kullanarak tarayıcıda görüntüleyen kodu yazılacak. Devam etmeden önce uygulamanızı derlediğinizden emin olun.

*Denetleyiciler* klasörüne sağ tıklayın ve yeni bir `MoviesController` denetleyicisi oluşturun. Aşağıdaki seçenekleri belirleyin:

- Denetleyici adı: **MoviesController**. (Bu varsayılandır.)
- Şablon: **Entity Framework kullanarak okuma/yazma eylemleri ve görünümleri olan denetleyici**.
- Model Sınıfı: **Film (MvcMovie. modeller)** .
- Veri bağlamı sınıfı: **Moviedbcontext (MvcMovie. modeller)** .
- Görünümler: **Razor (cshtml)** . (Varsayılan.)

[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)

**Ekle**'ye tıklayın. Visual Web Developer aşağıdaki dosyaları ve klasörleri oluşturur:

- Projenin *denetleyiciler* klasöründe *bir MoviesController. vb* dosyası.
- Projenin *Görünümler* klasöründeki *filmler* klasörü.
- Yeni *Views\filmler* klasöründe *. vbhtml, delete. vbhtml, details. vbhtml, Edit. vbhtml*ve *Index. vbhtml* oluşturun.

[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)

ASP.NET MVC 3 yapı iskelesi mekanizması, sizin için CRUD (oluşturma, okuma, güncelleştirme ve silme) eylem yöntemlerini ve görünümlerini otomatik olarak oluşturdu. Artık, film girişleri oluşturmanızı, listelemenizi, düzenlemenizi ve silmenizi sağlayan tam işlevli bir Web uygulamanız vardır.

Uygulamayı çalıştırın ve tarayıcınızın adres çubuğundaki URL 'ye */filmler* ekleyerek `Movies` denetleyiciye gidin. Uygulama varsayılan yönlendirmeye bağlı olduğundan ( *Global. asax* dosyasında tanımlı), tarayıcı isteği `http://localhost:xxxxx/Movies`, `Movies` denetleyicisinin varsayılan `Index` eylem yöntemine yönlendirilir. Diğer bir deyişle, tarayıcı istek `http://localhost:xxxxx/Movies` `http://localhost:xxxxx/Movies/Index`tarayıcı isteğiyle aynı şekilde aynıdır. Henüz hiç eklemediğiniz için sonuç, filmlerin boş bir listesidir.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a>Film oluşturma

**Yeni oluştur** bağlantısını seçin. Bir film hakkındaki ayrıntıları girin ve ardından **Oluştur** düğmesine tıklayın.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

**Oluştur** düğmesine tıkladığınızda form, film bilgilerinin veritabanına kaydedildiği sunucuya gönderilmesini sağlar. Daha sonra, yeni oluşturulan filmi listede görebileceğiniz */filmler* URL 'sine yönlendirilirsiniz.

[![ındexwhenharrykarşılandığından](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)

Birkaç film girişi oluşturun. Tüm işlevsel olan **düzenleme**, **Ayrıntılar**ve **silme** bağlantılarını deneyin.

## <a name="examining-the-generated-code"></a>Oluşturulan kodu İnceleme

*Controllers\MoviesController.vb* dosyasını açın ve oluşturulan `Index` yöntemini inceleyin. `Index` yöntemi ile birlikte film denetleyicisi 'nin bir bölümü aşağıda gösterilmiştir.

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

`MoviesController` sınıfından aşağıdaki satır, daha önce açıklandığı gibi bir film veritabanı bağlamını başlatır. Film veritabanı bağlamını kullanarak filmleri sorgulayabilir, düzenleyebilir ve silebilirsiniz.

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

`Movies` denetleyicisine yapılan bir istek, film veritabanının `Movies` tablosundaki tüm girişleri döndürür ve sonra sonuçları `Index` görünümüne geçirir.

## <a name="strongly-typed-models-and-the-model-keyword"></a>Türü kesin belirlenmiş modeller ve @model anahtar sözcüğü

Bu öğreticide daha önce, bir denetleyicinin `ViewBag` nesnesini kullanarak bir görünüm şablonuna nasıl veri veya nesne geçirekullanabileceğinizi gördünüz. `ViewBag`, bir görünüme bilgi geçirmek için uygun, geç bağlanan bir yol sağlayan dinamik bir nesnedir.

ASP.NET MVC, kesin olarak belirlenmiş verileri veya nesneleri bir görünüm şablonuna geçirme özelliği de sağlar. Bu kesin türü belirtilmiş yaklaşım, Visual Web Developer Editor 'da kodunuzun ve daha zengin IntelliSense 'in derleme zamanı denetimini daha iyi bir şekilde sunar. Bu yaklaşımı `MoviesController` Class ve *Index. vbhtml* görünüm şablonuyla kullanıyoruz.

[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) , `Index` eylem yönteminde `View` Helper metodunu çağırdığında kodun bir nesne nasıl oluşturduğunu göreceksiniz. Kod daha sonra bu `Movies` listesini denetleyiciden görünüme geçirir:

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

Görünüm şablonu dosyasının üst kısmına bir `@ModelType` ifadesini ekleyerek, görünümün beklediği nesne türünü belirtebilirsiniz. Film denetleyicisini oluştururken, Visual Web Developer *Dizin. vbhtml* dosyasının en üstüne aşağıdaki `@model` ifadesini otomatik olarak dahil edin:

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

Bu `@ModelType` yönergesi, kesin olarak belirlenmiş bir `Model` nesnesi kullanarak denetleyicinin görünüme geçirildiği film listesine erişmenizi sağlar. Örneğin, *Index. vbhtml* şablonunda, kod, türü kesin belirlenmiş `Model` nesnesi üzerinde `foreach` bir bildiri gerçekleştirerek filmlerde döngü yapılır:

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

`Model` nesne kesin olarak yazıldığı için (bir `IEnumerable<Movie>` nesnesi olarak), döngüdeki her bir `item` nesnesi `Movie`olarak yazılır. Diğer avantajlar arasında bu, kod Düzenleyicisi 'nde kodun derleme zamanı denetimini ve tam IntelliSense desteğini elde ettiğiniz anlamına gelir:

[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>SQL Server Compact çalışma

Entity Framework Code First, belirtilen veritabanı bağlantı dizesinin henüz mevcut olmayan bir `Movies` veritabanına işaret ettiği algılandı, bu nedenle veritabanını otomatik olarak oluşturdu Code First. Uygulamasının oluşturulduğunu, *uygulama\_veri* klasörüne bakarak doğrulayabilirsiniz. *Filmler. sdf* dosyasını görmüyorsanız, **Çözüm Gezgini** araç çubuğunda **tüm dosyaları göster** düğmesine tıklayın, **Yenile** düğmesine tıklayın ve ardından *uygulama\_verileri* klasörünü genişletin.

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)

**Sunucu Gezgini**açmak için *filmler. sdf* öğesine çift tıklayın. Ardından, veritabanında oluşturulmuş tabloları görmek için **Tablolar** klasörünü genişletin.

> [!NOTE]
> *Filmler. sdf*öğesine çift tıkladığınızda bir hata alırsanız, **SQL Server Compact 4,0 için VISUAL Studio 2010 SP1 araçları**'nı yüklediğinizden emin olun. (Yazılımın bağlantıları için, bu öğretici serisinin 1. bölümünde Önkoşullar listesine bakın.) Yayını Şimdi yüklerseniz, Visual Web Developer 'ı kapatıp yeniden açmanız gerekir.

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)

Biri `Movie` varlık kümesi ve sonra `EdmMetadata` tablo olmak üzere iki tablo vardır. `EdmMetadata` tablosu, modelin ve veritabanının ne zaman eşitlenmemiş olduğunu anlamak için Entity Framework tarafından kullanılır.

`Movies` tabloya sağ tıklayıp **tablo verilerini göster** ' i seçerek oluşturduğunuz verileri görüntüleyin.

[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)

`Movies` tabloya sağ tıklayıp **tablo şemasını Düzenle**' yi seçin.

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)

![Tablodüzeni](accessing-your-models-data-from-a-controller/_static/image19.png)

`Movies` tablosu şemasının, daha önce oluşturduğunuz `Movie` sınıfa nasıl eşlendiğini fark edin. Entity Framework Code First, bu şemayı `Movie` sınıfınızı temel alarak sizin için otomatik olarak oluşturdu.

İşiniz bittiğinde bağlantıyı kapatın. (Bağlantıyı kapatmazsanız, projeyi bir sonraki çalıştırışınızda bir hata alabilirsiniz).

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)

Artık veritabanını ve bir basit liste sayfasını, içeriği görüntüleme sayfasına sahipsiniz. Sonraki öğreticide, iskele eklenen kodun geri kalanını inceleyeceğiz ve bu veritabanında film aramanızı sağlayan bir `SearchIndex` yöntemi ve bir `SearchIndex` görünümü ekleyeceğiz.

> [!div class="step-by-step"]
> [Önceki](adding-a-model.md)
> [İleri](examining-the-edit-methods-and-edit-view.md)
