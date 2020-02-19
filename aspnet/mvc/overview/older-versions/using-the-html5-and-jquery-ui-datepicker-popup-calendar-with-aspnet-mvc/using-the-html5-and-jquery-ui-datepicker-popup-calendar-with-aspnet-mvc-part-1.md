---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 1 | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvimini bir ASP.NET MV içinde nasıl çalışabileceğiniz hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: c1c2380f24c72f6aabaaacaf975e95288a384ff1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457628"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-1. Bölüm

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, bir ASP.NET MVC web uygulamasında düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvim ile çalışma hakkında temel bilgiler verilir.

Bu öğreticide, bir ASP.NET MVC web uygulamasında düzenleyici şablonları, görüntüleme şablonları ve jQuery [UI DatePicker açılan takvim](http://plugins.jquery.com/project/datepicker) ile çalışma hakkında temel bilgiler verilir. Bu öğreticide, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i (&quot;Visual Web Developer&quot;) kullanabilir veya zaten varsa Visual Studio 2010 SP1 'i kullanabilirsiniz.

Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak gerekli yazılımları tek tek yükleyebilirsiniz:

- [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)

Visual Web Developer yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).

Bu öğreticide, [MVC 3 ' ü kullanmaya başlama](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) öğreticisini tamamlamış veya ASP.NET MVC geliştirme hakkında bilgi sahibi olduğunuz varsayılır. Bu öğretici, [MVC 3 Ile çalışmaya başlama](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) öğreticisindeki tamamlanmış projeyle başlar.

Bu öğreticide kodu gösterir C#. Ancak, [Başlatıcı proje](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) ve tamamlanmış proje de Visual Basic de mevcuttur.

Ve Visual Basic kaynak kodu içeren C# bir Visual Studio projesi, bu konu başlığına eşlik etmek için kullanılabilir: [Download](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800).

### <a name="what-youll-build"></a>Ne oluşturacağız?

[MVC 3 Ile çalışmaya](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) başlama öğreticisinde oluşturulan basit film listeleme uygulamasına şablonlar (özellikle, düzenleme ve görüntüleme şablonları) ekleyebilirsiniz. Ayrıca, tarih girme işlemini basitleştirmek için bir [jQuery UI DatePicker](http://jqueryui.com/demos/datepicker/) açılan takvimi ekleyeceksiniz. Aşağıdaki ekran görüntüsünde, jQuery UI DatePicker açılan takviminin gösterildiği değiştirilmiş uygulama gösterilmektedir.

![bitmiş jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>Öğrenmeniz gereken yetenekler

Öğrenirsiniz:

- Veri açıklamalarını, görüntülendiği zaman ve düzenleme modunda olduğunda denetlemek için [datanot](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanındaki öznitelikleri kullanma.
- Verilerin biçimlendirilmesini denetlemek için şablon oluşturma (düzenleme ve görüntüleme şablonları).
- Veri alanlarını girmeye bir yol olarak [jQuery UI DatePicker](http://jqueryui.com/demos/datepicker/) ekleme.

### <a name="getting-started"></a>Başlarken

Zaten başlangıç projesinden film listeleme uygulamanız yoksa, indirin: 

* [İndirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).
* Windows Gezgini 'nde, *Mvcmovie. zip* dosyasına sağ tıklayın ve **Özellikler**' i seçin. 
* **Mvcmovie. zip özellikleri** Iletişim kutusunda **Engellemeyi kaldır**' ı seçin. (Engellemeyi kaldırma, Web 'den indirdiğiniz bir *. zip* dosyasını kullanmaya çalıştığınızda oluşan bir güvenlik uyarısını önler.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

*Mvcmovie. zip* dosyasına sağ tıklayın ve dosyayı sıkıştırmayı açmak Için **Tümünü Ayıkla** ' yı seçin. Visual Web Developer veya Visual Studio 2010 ' de *MvcMovieCS\_tu. sln* dosyasını açın.

**Çözüm Gezgini**içinde, *views\shared\\_Layout. cshtml* öğesine çift tıklayarak açın. **MVC film uygulamasındaki** `H1` üst bilgisini **film jQuery**olarak değiştirin. Uygulamayı çalıştırmak için CTRL + F5 tuşlarına basın ve bunu film denetleyicisinin `Index` yöntemine götüren **giriş** sekmesine tıklayın. Uygulamayı denemek için filmden biri için **Düzenle** bağlantısını ve **Ayrıntılar** bağlantısını seçin. Dizin, düzenleme ve Ayrıntılar görünümlerinde, Yayın tarihi ve fiyatının düzgün biçimlendirildiğine dikkat edin:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

Tarih ve fiyat için biçimlendirme, `Movie` sınıfının özelliklerinde [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğini kullanmanın sonucudur.

*Movie.cs* dosyasını açın ve `ReleaseDate` ve `Price` özelliklerine `DisplayFormat` özniteliğini açıklama olarak ekleyin. Elde edilen `Movie` sınıfı şöyle görünür:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

Uygulamayı çalıştırmak için CTRL + F5 tuşlarına basın ve film listesini görüntülemek için **giriş** sekmesini seçin. Bu kez Yayımlanma tarihi tarihi ve saati gösterir ve fiyat alanı artık para birimi simgesini göstermez. `Movie` sınıfında yaptığınız değişiklik, daha önce gördüğünüz iyi biçimlendirmeyi geri aldı, ancak bu işlemi bir süre sonra çözeceksiniz.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>Veri türünü belirtmek için Dataaçıklamalarda DataType özniteliğini kullanma

`Date` sabit listesini kullanarak `ReleaseDate` özelliğinin açıklamalı `DisplayFormat` özniteliğini [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) özniteliğiyle değiştirin. `Price` özelliği için `DisplayFormat` özniteliğini, bu kez `Currency` numaralandırmayı kullanarak yeniden [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) özniteliğiyle değiştirin. Tamamlanan kod şöyle görünür:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

Uygulamayı çalıştırın. Artık Yayın tarihi ve fiyat özellikleri doğru biçimlendirilir (yani, uygun tarih ve para birimi biçimlerini kullanarak). [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) özniteliği, YERLEŞIK ASP.NET MVC şablonlarının tür meta verilerini sağlar, böylece alanlar doğru biçimde işlenir. `DataType` özniteliğinin kullanılması `DisplayFormat` tercih edilir, çünkü `DataType` özniteliği model temizleyici ve uluslararası duruma getirme gibi amaçlarla daha esnek hale gelir.

Sonraki bölümde, tarih alanlarını görüntülemek için nasıl özel şablonlar yapılacağını öğreneceksiniz.

> [!div class="step-by-step"]
> [Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
