---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
title: Modele doğrulama ekleme (VB) | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 878f6c31-972d-45f4-8849-5c633b511409
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: 7f3f195bc30ed23a637b59f15e6fc8431e39e217
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457212"
---
# <a name="adding-validation-to-the-model-vb"></a>Modele Doğrulama Ekleme (VB)

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğretici, Microsoft Visual Studio ücretsiz bir sürümü olan Microsoft Visual Web Developer 2010 Express Service Pack 1 ' i kullanarak bir ASP.NET MVC web uygulaması oluşturmaya ilişkin temel bilgileri öğretir. Başlamadan önce, aşağıda listelenen önkoşulları yüklediğinizden emin olun. Şu bağlantıya tıklayarak hepsini yükleyebilirsiniz: [Web Platformu Yükleyicisi](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Alternatif olarak, aşağıdaki bağlantıları kullanarak önkoşulları ayrı ayrı yükleyebilirsiniz:
> 
> - [Visual Studio Web Developer Express SP1 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [ASP.NET MVC 3 Araçlar güncelleştirmesi](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(çalışma zamanı + araçlar desteği)
> 
> Visual Web Developer 2010 yerine Visual Studio 2010 kullanıyorsanız, aşağıdaki bağlantıya tıklayarak önkoşulları yükleyebilirsiniz: [Visual studio 2010 önkoşulları](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Bu konuyla birlikte VB.NET kaynak koduna sahip bir Visual Web Developer projesi mevcuttur. [Vb.NET sürümünü indirin](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). İsterseniz C#, Bu öğreticinin [ C# sürümüne](../cs/adding-validation-to-the-model.md) geçin.

Bu bölümde `Movie` modeline doğrulama mantığı ekleyeceksiniz ve bir kullanıcının uygulamayı kullanarak bir filmi oluşturma veya düzenleme girişiminde bulunduğu her seferinde doğrulama kurallarının uygulanmasını sağlayabilirsiniz.

## <a name="keeping-things-dry"></a>Işleri güncel tutma

ASP.NET MVC 'nin çekirdek tasarımdan biri kuru ("Kendini Tekrarlama"). ASP.NET MVC, işlevselliği veya davranışı yalnızca bir kez belirtmenizi ve sonra bir uygulamada her yerde yansıtıldığını teşvik eder. Bu, yazmanız gereken kod miktarını azaltır ve daha fazla bakım yapmak için yazdığınız kodu daha kolay hale getirir.

ASP.NET MVC ve Entity Framework Code First tarafından sağlanan doğrulama desteği, işlem içindeki kuru ilkeye yönelik harika bir örnektir. Doğrulama kurallarını tek bir yerde (model sınıfında) bildirimli olarak belirtebilir ve ardından bu kurallar uygulamada her yerde zorlanır.

Film uygulamasındaki bu doğrulama desteğinden nasıl yararlanabilmenizi görelim.

## <a name="adding-validation-rules-to-the-movie-model"></a>Film modeline doğrulama kuralları ekleme

`Movie` sınıfına bazı doğrulama mantığı ekleyerek başlayacaksınız.

*Movie. vb* dosyasını açın. Dosyanın üst kısmına [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanına başvuran `Imports` bir ifade ekleyin:

[!code-vb[Main](adding-validation-to-the-model/samples/sample1.vb)]

Ad alanı .NET Framework bir parçasıdır. Herhangi bir sınıfa veya özelliğe bildirimli olarak uygulayabileceğiniz, yerleşik bir doğrulama öznitelikleri kümesi sağlar.

Şimdi yerleşik [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)ve [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) doğrulama özniteliklerinden yararlanmak için `Movie` sınıfını güncelleştirin. Özniteliklerin nereye uygulanacağını bir örnek olarak aşağıdaki kodu kullanın.

[!code-vb[Main](adding-validation-to-the-model/samples/sample2.vb)]

Doğrulama öznitelikleri, uygulanan model özellikleri üzerinde zorlamak istediğiniz davranışı belirtir. `Required` özniteliği bir özelliğin bir değere sahip olması gerektiğini belirtir; Bu örnekte, bir filmin geçerli olması için `Title`, `ReleaseDate`, `Genre`ve `Price` özellikleri için değerler olması gerekir. `Range` özniteliği bir değeri belirtilen bir Aralık içinde kısıtlar. `StringLength` özniteliği, bir dize özelliğinin en büyük uzunluğunu ve isteğe bağlı olarak en düşük uzunluğunu ayarlamanıza olanak sağlar.

Code First, bir model sınıfında belirttiğiniz doğrulama kurallarının, uygulama değişiklikleri veritabanına kaydedilmeden önce uygulanmasını sağlar. Örneğin, aşağıdaki kod `SaveChanges` yöntemi çağrıldığında bir özel durum oluşturur, çünkü gerekli birkaç `Movie` Özellik değeri eksik ve fiyat sıfır (geçerli aralığın dışında).

[!code-vb[Main](adding-validation-to-the-model/samples/sample3.vb)]

Doğrulama kurallarının .NET Framework tarafından otomatik olarak uygulanmasını sağlamak, uygulamanızın daha sağlam olmasına yardımcı olur. Ayrıca, bir şeyi doğrulamayı unutmanızı ve veritabanına yanlışlıkla veri vermemesini de sağlar.

Güncelleştirilmiş *film. vb* dosyası için bir kod listesi aşağıda verilmiştir:

[!code-vb[Main](adding-validation-to-the-model/samples/sample4.vb)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 'de doğrulama hatası Kullanıcı arabirimi

Uygulamayı yeniden çalıştırın ve */filmler* URL 'sine gidin.

Yeni bir film eklemek için **Film Oluştur** bağlantısına tıklayın. Formu, bazı geçersiz değerlerle doldurun ve ardından **Oluştur** düğmesine tıklayın.

[![8_validationErrors](adding-validation-to-the-model/_static/image2.png)](adding-validation-to-the-model/_static/image1.png)

Formun, geçersiz veriler içeren metin kutularını vurgulamak için otomatik olarak bir arka plan rengi nasıl kullandığını ve her birinin yanında uygun bir doğrulama hata mesajı oluşturmuş olduğunu unutmayın. Hata iletileri, `Movie` sınıfının açıklandığında belirttiğiniz hata dizeleriyle eşleşir. Hatalar hem istemci tarafında (JavaScript kullanılarak) hem de sunucu tarafında zorlanır (bir kullanıcının JavaScript devre dışı olması durumunda).

Gerçek bir avantaj, bu doğrulama kullanıcı arabirimini etkinleştirmek için `MoviesController` sınıfında veya *Create. vbhtml* görünümündeki tek bir kod satırını değiştirmeniz gerekmez. Bu öğreticide daha önce oluşturduğunuz denetleyici ve görünümler, `Movie` model sınıfında öznitelikleri kullanarak belirttiğiniz doğrulama kurallarını otomatik olarak çekti.

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Oluşturma görüntüleme ve eylem oluşturma yönteminde doğrulama nasıl gerçekleşir

Doğrulama Kullanıcı arabiriminin denetleyici veya görünümlerde kodda herhangi bir güncelleştirme yapmadan nasıl oluşturulduğunu merak edebilirsiniz. Sonraki liste, `MovieController` sınıfındaki `Create` yöntemlerinin nasıl göründüğünü gösterir. Bunlar, bu öğreticide daha önce oluşturduğunuz şekilde değiştirilmez.

[!code-vb[Main](adding-validation-to-the-model/samples/sample5.vb)]

İlk eylem yöntemi ilk oluşturma formunu görüntüler. İkinci, form gönderisini işler. İkinci `Create` yöntemi, filmin herhangi bir doğrulama hatası olup olmadığını denetlemek için `ModelState.IsValid` çağırır. Bu yöntemi çağırmak, nesnesine uygulanmış olan tüm doğrulama özniteliklerini değerlendirir. Nesnede doğrulama hataları varsa `Create` yöntemi formu yeniden görüntüler. Hata yoksa, yöntemi yeni filmi veritabanına kaydeder.

Öğreticide daha önce iskele aldığınız *Create. vbhtml* görünüm şablonu aşağıda verilmiştir. İlk formu görüntülemek ve bir hata durumunda onu yeniden görüntülemek için yukarıda gösterilen eylem yöntemleri tarafından kullanılır.

[!code-vbhtml[Main](adding-validation-to-the-model/samples/sample6.vbhtml)]

Kodun, her bir `Movie` özelliği için `<input>` öğesinin çıktısını almak üzere bir `Html.EditorFor` Yardımcısı kullandığını fark edin. Bu yardımcının yanında `Html.ValidationMessageFor` Yardımcısı yöntemine yapılan bir çağrıdır. Bu iki yardımcı yöntem, denetleyici tarafından görünüme geçirilen model nesnesiyle (Bu durumda bir `Movie` nesnesi) çalışır. Model üzerinde belirtilen doğrulama özniteliklerini otomatik olarak arar ve hata iletilerini uygun şekilde görüntüler.

Bu yaklaşım ne kadar iyi bir şeydir, denetleyicinin veya oluşturma görünüm şablonunun zorlanmakta olan gerçek doğrulama kuralları ya da görüntülenen belirli hata iletileri hakkında herhangi bir şeyi biliyor olması önemlidir. Doğrulama kuralları ve hata dizeleri yalnızca `Movie` sınıfında belirtilmiştir.

Daha sonra doğrulama mantığını değiştirmek istiyorsanız, bunu tam olarak bir yerde yapabilirsiniz. Kuralların nasıl zorlandığından, uygulamanın farklı bölümlerinin tutarsız olması konusunda endişelenmeniz gerekmez; tüm doğrulama mantığı tek bir yerde tanımlanır ve her yerde kullanılır. Bu, kodun temiz kalmasını sağlar ve bakımını ve gelişmesini kolaylaştırır. Ayrıca, KURULAMA ilkesini tam olarak sunabileceksiniz anlamına gelir.

## <a name="adding-formatting-to-the-movie-model"></a>Film modeline biçimlendirme ekleme

*Movie. vb* dosyasını açın. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanı, yerleşik doğrulama öznitelikleri kümesine ek olarak biçimlendirme öznitelikleri sağlar. [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğini ve bir [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) numaralandırma değerini, yayın tarihine ve fiyat alanlarına uygularsınız. Aşağıdaki kod, uygun [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğiyle `ReleaseDate` ve `Price` özelliklerini gösterir.

[!code-vb[Main](adding-validation-to-the-model/samples/sample7.vb)]

Alternatif olarak, açıkça bir [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) değeri ayarlayabilirsiniz. Aşağıdaki kod, bir tarih biçimi dizesiyle (yani, "d") sürüm tarihi özelliğini gösterir. Bunu, sürüm tarihinin bir parçası olarak zaman istemediğinizi belirtmek için kullanacaksınız.

[!code-vb[Main](adding-validation-to-the-model/samples/sample8.vb)]

Aşağıdaki kod `Price` özelliğini para birimi olarak biçimlendirir.

[!code-vb[Main](adding-validation-to-the-model/samples/sample9.vb)]

Tüm `Movie` sınıfı aşağıda gösterilmiştir.

[!code-vb[Main](adding-validation-to-the-model/samples/sample10.vb)]

Uygulamayı çalıştırın ve `Movies` denetleyicisine gidin.

![8_format_SM](adding-validation-to-the-model/_static/image3.png)

Serinin bir sonraki bölümünde, uygulamayı gözden geçireceğiz ve otomatik olarak oluşturulan `Details` ve `Delete` yöntemlerinde bazı geliştirmeler yapacağız.

> [!div class="step-by-step"]
> [Önceki](adding-a-new-field.md)
> [İleri](improving-the-details-and-delete-methods.md)
