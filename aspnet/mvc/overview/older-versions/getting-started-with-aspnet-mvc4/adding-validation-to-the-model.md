---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
title: Modele doğrulama ekleme | Microsoft Docs
author: Rick-Anderson
description: 'Note: ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, izleme ve tanıtım için çok daha kolay...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 5d9a2999-fcc4-4c45-a018-271fddf74a3b
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-validation-to-the-model
msc.type: authoredcontent
ms.openlocfilehash: c9f6699c5d3500d4c1fcade9252aeb9dd92983da
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455964"
---
# <a name="adding-validation-to-the-model"></a>Modele Doğrulama Ekleme

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> > [!NOTE]
> > [Burada](../../getting-started/introduction/getting-started.md) ASP.NET MVC 5 ve Visual Studio 2013 kullanan Bu öğreticinin güncelleştirilmiş bir sürümü mevcuttur. Daha güvenlidir, daha kolay hale gelir ve daha fazla özellik gösterir.

Bu bölümde `Movie` modeline doğrulama mantığı ekleyeceksiniz ve bir kullanıcının uygulamayı kullanarak bir filmi oluşturma veya düzenleme girişiminde bulunduğu her seferinde doğrulama kurallarının uygulanmasını sağlayabilirsiniz.

## <a name="keeping-things-dry"></a>Işleri güncel tutma

ASP.NET MVC 'nin çekirdek tasarımdan biri kuru (&quot;Kendini Tekrarlama&quot;). ASP.NET MVC, işlevselliği veya davranışı yalnızca bir kez belirtmenizi ve sonra bir uygulamada her yerde yansıtıldığını teşvik eder. Bu, yazmanız gereken kod miktarını azaltır ve daha az hata yazmanızı ve bakımını daha kolay hale getirir.

ASP.NET MVC ve Entity Framework Code First tarafından sağlanan doğrulama desteği, işlem içindeki kuru ilkeye yönelik harika bir örnektir. Doğrulama kurallarını tek bir yerde (model sınıfında) bildirimli olarak belirtebilir ve kurallar uygulamada her yerde zorlanır.

Film uygulamasındaki bu doğrulama desteğinden nasıl yararlanabilmenizi görelim.

## <a name="adding-validation-rules-to-the-movie-model"></a>Film modeline doğrulama kuralları ekleme

`Movie` sınıfına bazı doğrulama mantığı ekleyerek başlayacaksınız.

*Movie.cs* dosyasını açın. Dosyanın üst kısmına [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanına başvuran `using` bir ifade ekleyin:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample1.cs)]

Ad alanının `System.Web`içermediğini unutmayın. Dataaçıklamalarda, herhangi bir sınıfa veya özelliğe bildirimli olarak uygulayabileceğiniz yerleşik bir doğrulama öznitelikleri kümesi sağlar.

Şimdi yerleşik [`Required`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx), [`StringLength`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx)ve [`Range`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.rangeattribute.aspx) doğrulama özniteliklerinden yararlanmak için `Movie` sınıfını güncelleştirin. Özniteliklerin nereye uygulanacağını bir örnek olarak aşağıdaki kodu kullanın.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample2.cs?highlight=4,10,13,17)]

Uygulamayı çalıştırın ve aşağıdaki çalışma zamanı hatasını alırsınız:

***' MovieDBContext ' bağlamını destekleyen model veritabanı oluşturulduktan sonra değiştirildi. Veritabanını güncelleştirmek için Code First Migrations kullanmayı düşünün ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).***

Şemayı güncelleştirmek için geçişleri kullanacağız. Çözümü oluşturun ve ardından **Paket Yöneticisi konsol** penceresini açın ve aşağıdaki komutları girin:

[!code-console[Main](adding-validation-to-the-model/samples/sample3.cmd)]

Bu komut tamamlandığında, Visual Studio, yeni `DbMigration` türetilen sınıfı tanımlayan sınıf dosyasını (*Adddataannotationsmg*) açar ve `Up` yönteminde şema kısıtlamalarını güncelleştiren kodu görebilirsiniz. `Title` ve `Genre` alanları artık null olamaz (yani bir değer girmeniz gerekir) ve `Rating` alanı en fazla 5 uzunluğunda olmalıdır.

Doğrulama öznitelikleri, uygulanan model özellikleri üzerinde zorlamak istediğiniz davranışı belirtir. `Required` özniteliği bir özelliğin bir değere sahip olması gerektiğini belirtir; Bu örnekte, bir filmin geçerli olması için `Title`, `ReleaseDate`, `Genre`ve `Price` özellikleri için değerler olması gerekir. `Range` özniteliği bir değeri belirtilen bir Aralık içinde kısıtlar. `StringLength` özniteliği, bir dize özelliğinin en büyük uzunluğunu ve isteğe bağlı olarak en düşük uzunluğunu ayarlamanıza olanak sağlar. İç türler (örneğin `decimal, int, float, DateTime`) varsayılan olarak gereklidir ve `Required` özniteliğine gerek kalmaz.

Code First, bir model sınıfında belirttiğiniz doğrulama kurallarının, uygulama değişiklikleri veritabanına kaydedilmeden önce uygulanmasını sağlar. Örneğin, aşağıdaki kod `SaveChanges` yöntemi çağrıldığında bir özel durum oluşturur, çünkü gerekli birkaç `Movie` Özellik değeri eksik ve fiyat sıfır (geçerli aralığın dışında).

[!code-csharp[Main](adding-validation-to-the-model/samples/sample4.cs?highlight=7-8)]

Doğrulama kurallarının .NET Framework tarafından otomatik olarak uygulanmasını sağlamak, uygulamanızın daha sağlam olmasına yardımcı olur. Ayrıca, bir şeyi doğrulamayı unutmanızı ve veritabanına yanlışlıkla veri vermemesini de sağlar.

Güncelleştirilmiş *Movie.cs* dosyası için bir kod listesi aşağıda verilmiştir:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample5.cs)]

## <a name="validation-error-ui-in-aspnet-mvc"></a>ASP.NET MVC 'de doğrulama hatası Kullanıcı arabirimi

Uygulamayı yeniden çalıştırın ve */filmler* URL 'sine gidin.

Yeni bir film eklemek için **Yeni oluştur** bağlantısına tıklayın. Formu, bazı geçersiz değerlerle doldurun ve ardından **Oluştur** düğmesine tıklayın.

![8_validationErrors](adding-validation-to-the-model/_static/image1.png)

> [!NOTE]
> ondalık bir nokta için virgül (&quot;,&quot;) kullanan Ingilizce olmayan yerel ayarlarda jQuery doğrulamasını desteklemek için, `Globalize.parseFloat`kullanmak üzere *globalize. js* ve belirli *kültürleri/globalize. kültürleri. js* dosyanızı ( [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) ve JavaScript 'i dahil etmeniz gerekir. Aşağıdaki kod, &quot;fr-FR&quot; kültürüyle çalışmak üzere Views\Movies\Edit.cshtml dosyasındaki değişiklikleri gösterir:

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample6.cshtml)]

Formun, geçersiz veriler içeren metin kutularını vurgulamak için otomatik olarak kırmızı kenarlık rengini nasıl kullandığını ve her birinin yanında uygun bir doğrulama hata iletisi oluşturmuş olduğunu unutmayın. Hatalar hem istemci tarafında (JavaScript ve jQuery kullanılarak) hem de sunucu tarafında (kullanıcının JavaScript devre dışı bırakılmış olması durumunda) zorlanır.

Gerçek bir avantaj, bu doğrulama kullanıcı arabirimini etkinleştirmek için `MoviesController` sınıfında veya *Create. cshtml* görünümündeki tek bir kod satırını değiştirmeniz gerekmez. Bu öğreticide daha önce oluşturduğunuz denetleyici ve görünümler, `Movie` model sınıfının özelliklerinde doğrulama özniteliklerini kullanarak belirttiğiniz doğrulama kurallarını otomatik olarak çekti.

`Title` ve `Genre`özellikler olduğunu fark etmiş olabilirsiniz ( **Oluştur** düğmesine basın) veya giriş alanına metin girip onu kaldırmış kadar gerekli öznitelik zorlanmaz. Başlangıçta boş olan ve yalnızca gerekli özniteliğe ve diğer doğrulama özniteliklerine sahip olmayan bir alan için, doğrulamayı tetiklemek için aşağıdakileri yapabilirsiniz:

1. Sekmesine ekleyin.
2. Biraz metin girin.
3. Çıkış sekmesi.
4. Sekmesini alana geri dönün.
5. Metni kaldırın.
6. Çıkış sekmesi.

Yukarıdaki sıra, Gönder düğmesine vurmadan gerekli doğrulamayı tetikler. Herhangi bir alandan birine girmeden Gönder düğmesine vurmak, istemci tarafı doğrulamayı tetikleyecektir. Form verileri, istemci tarafı doğrulama hatası kalmayana kadar sunucuya gönderilmez. Bunu, HTTP POST yöntemine bir kesme noktası koyarak veya [Fiddler aracını](http://fiddler2.com/fiddler2/) ya da IE 9 [F12 geliştirici araçlarını](https://msdn.microsoft.com/ie/aa740478)kullanarak test edebilirsiniz.

![](adding-validation-to-the-model/_static/image2.png)

## <a name="how-validation-occurs-in-the-create-view-and-create-action-method"></a>Oluşturma görüntüleme ve eylem oluşturma yönteminde doğrulama nasıl gerçekleşir

Doğrulama Kullanıcı arabiriminin denetleyici veya görünümlerde kodda herhangi bir güncelleştirme yapmadan nasıl oluşturulduğunu merak edebilirsiniz. Sonraki liste, `MovieController` sınıfındaki `Create` yöntemlerinin nasıl göründüğünü gösterir. Bunlar, bu öğreticide daha önce oluşturduğunuz şekilde değiştirilmez.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample7.cs?highlight=12,15)]

İlk (HTTP GET) `Create` Action yöntemi ilk oluşturma formunu görüntüler. İkinci (`[HttpPost]`) sürüm, form gönderisini işler. İkinci `Create` yöntemi (`HttpPost` sürümü), filmin herhangi bir doğrulama hatası olup olmadığını denetlemek için `ModelState.IsValid` çağırır. Bu yöntemi çağırmak, nesnesine uygulanmış olan tüm doğrulama özniteliklerini değerlendirir. Nesnede doğrulama hataları varsa `Create` yöntemi formu yeniden görüntüler. Hata yoksa, yöntemi yeni filmi veritabanına kaydeder. Kullanmakta olduğumuz film örneğimizde, **istemci tarafında algılanan doğrulama hataları olduğunda form sunucuya nakledilmez; ikinci** `Create`**yöntemi hiçbir zaman çağrılmaz**. Tarayıcınızda JavaScript 'i devre dışı bırakırsanız, istemci doğrulaması devre dışı bırakılır ve HTTP POST `Create` yöntemi, filmin herhangi bir doğrulama hatası olup olmadığını denetlemek için `ModelState.IsValid` çağırır.

`HttpPost Create` yönteminde bir kesme noktası ayarlayabilir ve yöntemin hiçbir zaman çağrılmadığını doğrulayabilirsiniz, doğrulama hataları algılandığında istemci tarafı doğrulaması form verilerini göndermez. Tarayıcınızda JavaScript 'i devre dışı bırakır, ardından formu hatalarla gönderirseniz, kesme noktası isabet eder. JavaScript olmadan tam doğrulama almaya devam edersiniz. Aşağıdaki görüntüde, Internet Explorer 'da JavaScript 'In nasıl devre dışı bırakılacağı gösterilmektedir.

![](adding-validation-to-the-model/_static/image3.png)

![](adding-validation-to-the-model/_static/image4.png)

Aşağıdaki görüntüde, FireFox tarayıcısında JavaScript 'In nasıl devre dışı bırakılacağı gösterilmektedir.

![](adding-validation-to-the-model/_static/image5.png)

Aşağıdaki görüntüde, Chrome tarayıcısı ile JavaScript 'In nasıl devre dışı bırakılacağı gösterilmektedir.

![](adding-validation-to-the-model/_static/image6.png)

Öğreticide daha önce iskele aldığınız *Create. cshtml* görünüm şablonu aşağıda verilmiştir. İlk formu görüntülemek ve bir hata durumunda onu yeniden görüntülemek için yukarıda gösterilen eylem yöntemleri tarafından kullanılır.

[!code-cshtml[Main](adding-validation-to-the-model/samples/sample8.cshtml?highlight=22-23,30-31,38-39,46-47)]

Kodun, her bir `Movie` özelliği için `<input>` öğesinin çıktısını almak üzere bir `Html.EditorFor` Yardımcısı kullandığını fark edin. Bu yardımcının yanında `Html.ValidationMessageFor` Yardımcısı yöntemine yapılan bir çağrıdır. Bu iki yardımcı yöntem, denetleyici tarafından görünüme geçirilen model nesnesiyle (Bu durumda bir `Movie` nesnesi) çalışır. Model üzerinde belirtilen doğrulama özniteliklerini otomatik olarak arar ve hata iletilerini uygun şekilde görüntüler.

Bu yaklaşım ne kadar iyi bir şeydir, denetleyicinin veya oluşturma görünüm şablonunun zorlanmakta olan gerçek doğrulama kuralları ya da görüntülenen belirli hata iletileri hakkında herhangi bir şeyi biliyor olması önemlidir. Doğrulama kuralları ve hata dizeleri yalnızca `Movie` sınıfında belirtilmiştir. Bu aynı doğrulama kuralları, düzenleme görünümüne ve modelinizi düzenleyebilecek oluşturabileceğiniz diğer tüm görünümler şablonlarına otomatik olarak uygulanır.

Daha sonra doğrulama mantığını değiştirmek istiyorsanız, modele doğrulama öznitelikleri ekleyerek tam olarak bir yerde bunu yapabilirsiniz (Bu örnekte, `movie` sınıfı). Kuralların nasıl zorlandığından, uygulamanın farklı bölümlerinin tutarsız olması konusunda endişelenmeniz gerekmez; tüm doğrulama mantığı tek bir yerde tanımlanır ve her yerde kullanılır. Bu, kodun temiz kalmasını sağlar ve bakımını ve gelişmesini kolaylaştırır. Ayrıca, KURULAMA ilkesini tam olarak sunabileceksiniz anlamına gelir.

## <a name="adding-formatting-to-the-movie-model"></a>Film modeline biçimlendirme ekleme

*Movie.cs* dosyasını açın ve `Movie` sınıfını inceleyin. [`System.ComponentModel.DataAnnotations`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) ad alanı, yerleşik doğrulama öznitelikleri kümesine ek olarak biçimlendirme öznitelikleri sağlar. Yayın tarihine ve fiyat alanlarına [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) bir numaralandırma değeri zaten uyguladık. Aşağıdaki kod, uygun [`DisplayFormat`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğiyle `ReleaseDate` ve `Price` özelliklerini gösterir.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample9.cs)]

[`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) öznitelikleri doğrulama öznitelikleri değildir, görünüm altyapısına HTML 'yi nasıl işleneceğini söylemek için kullanılırlar. Yukarıdaki örnekte, `DataType.Date` özniteliği, film tarihlerini zaman içinde yalnızca tarih olarak görüntüler. Örneğin, aşağıdaki [`DataType`](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) öznitelikleri verilerin biçimini doğrulamaz:

[!code-csharp[Main](adding-validation-to-the-model/samples/sample10.cs)]

Yukarıda listelenen öznitelikler yalnızca görünüm altyapısının verileri biçimlendirmek için ipuçları sağlar (ve URL 'SI için bir&gt; &lt;gibi öznitelikleri ve e-posta için bir href =&quot;mailto: Emadresi. com&quot;&gt; &lt;. Verilerin biçimini doğrulamak için [cevap içerisinde RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) özniteliğini kullanabilirsiniz.

`DataType` özniteliklerinin kullanılmasına alternatif bir yaklaşım olan, açıkça bir [`DataFormatString`](https://msdn.microsoft.com/library/system.string.format.aspx) değeri ayarlayabilirsiniz. Aşağıdaki kod, bir tarih biçimi dizesiyle (yani, &quot;d&quot;) Yayın tarihi özelliğini gösterir. Bunu, sürüm tarihinin bir parçası olarak zaman istemediğinizi belirtmek için kullanacaksınız.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample11.cs)]

Tüm `Movie` sınıfı aşağıda gösterilmiştir.

[!code-csharp[Main](adding-validation-to-the-model/samples/sample12.cs)]

Uygulamayı çalıştırın ve `Movies` denetleyicisine gidin. Yayın tarihi ve fiyatı tamamen biçimlendirilir. Aşağıdaki görüntüde, kültür olarak &quot;fr-FR&quot; kullanan yayın tarihi ve fiyatı gösterilmektedir.

![8_format_SM](adding-validation-to-the-model/_static/image7.png)

Aşağıdaki görüntüde varsayılan kültür (Ingilizce ABD) ile birlikte gösterilen veriler gösterilmektedir.

![](adding-validation-to-the-model/_static/image8.png)

Serinin bir sonraki bölümünde, uygulamayı gözden geçireceğiz ve otomatik olarak oluşturulan `Details` ve `Delete` yöntemlerinde bazı geliştirmeler yapacağız.

> [!div class="step-by-step"]
> [Önceki](adding-a-new-field-to-the-movie-model-and-table.md)
> [İleri](examining-the-details-and-delete-methods.md)
