---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-Bölüm 2 | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici, düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvimini bir ASP.NET MV içinde nasıl çalışabileceğiniz hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455899"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>ASP.NET MVC ile HTML5 ve jQuery kullanıcı arabirimi DatePicker açılan takvimini kullanma-2. Bölüm

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu öğreticide, bir ASP.NET MVC web uygulamasında düzenleyici şablonları, görüntüleme şablonları ve jQuery UI DatePicker açılan takvim ile çalışma hakkında temel bilgiler verilir.

## <a name="adding-an-automatic-datetime-template"></a>Otomatik DateTime şablonu ekleme

Bu öğreticinin ilk bölümünde, açıkça biçimlendirmeyi belirtmek için modele nasıl öznitelik ekleyekullanabileceğinizi ve modeli oluşturmak için kullanılan şablonu açıkça nasıl belirtebileceğiniz gördünüz. Örneğin, aşağıdaki koddaki [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliği `ReleaseDate` özelliği için biçimlendirmeyi açıkça belirtir.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

Aşağıdaki örnekte, `Date` numaralandırmayı kullanan [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) özniteliği, modeli işlemek için tarih şablonunun kullanılması gerektiğini belirtir. Projenizde bir tarih şablonu yoksa, yerleşik tarih şablonu kullanılır.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

Ancak, ASP. MVC, bir tür adıyla eşleşen bir şablonu arayarak, yapılandırma üzerinden kural kullanarak tür eşleştirmeyi gerçekleştirebilir. Bu, herhangi bir özniteliği veya kodu kullanmadan verileri otomatik olarak biçimlendiren bir şablon oluşturmanıza olanak sağlar. Öğreticinin bu bölümü için, [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)türünde model özelliklerine otomatik olarak uygulanan bir şablon oluşturacaksınız. Şablonun [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx)türünde tüm model özelliklerini işlemek için kullanılması gerektiğini belirtmek için bir öznitelik veya başka bir yapılandırma kullanmanız gerekmez.

Ayrıca tek tek özelliklerin ve hatta ayrı alanların görüntülenmesini özelleştirmenin bir yolunu öğreneceksiniz.

Başlamak için, var olan biçimlendirme bilgilerini kaldıralım ve uygulamadaki tüm tarihleri görüntüleriz.

*Movie.cs* dosyasını açın ve `ReleaseDate` özelliğindeki `DataType` özniteliğini açıklama olarak ekleyin:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

Uygulamayı çalıştırmak için CTRL+F5'e basın.

`ReleaseDate` özelliği artık hem tarih hem de saati görüntülediğine dikkat edin, çünkü bu varsayılan değer hiçbir biçimlendirme bilgisi sağlanmaz.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>Yeni şablonların test edilmesi için CSS stilleri ekleme

Biçimlendirme tarihleri için bir şablon oluşturmadan önce, yeni şablonlara uygulayabileceğiniz birkaç CSS stil kuralı ekleyebilirsiniz. Bunlar, işlenmiş sayfanın yeni şablonu kullandığını doğrulamanıza yardımcı olur.

*Content\site.cs*dosyasını açın ve dosyanın sonuna aşağıdaki CSS kurallarını ekleyin:

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>Tarih saat görüntüleme şablonları ekleme

Artık yeni şablonu oluşturabilirsiniz. *Views\filmler* klasöründe bir *DisplayTemplates* klasörü oluşturun.

*Views\shared* klasöründe bir *DisplayTemplates* klasörü ve bir *EditorTemplates* klasörü oluşturun.

*Views\shared\displaytemplates* klasöründeki görüntüleme şablonları tüm denetleyiciler tarafından kullanılır. *Views\movie\displaytemplates* klasöründeki görüntüleme şablonları yalnızca `Movie` denetleyicisi tarafından kullanılır. (Her iki klasörde da aynı ada sahip bir şablon görüntülenirse, *Views\movie\displaytemplates* klasöründeki şablon — diğer bir deyişle, `Movie` denetleyicisi tarafından döndürülen görünümler için öncelik kazanır.)

**Çözüm Gezgini**, *Görünümler* klasörünü genişletin, *paylaşılan* klasörünü genişletin ve ardından *Views\Shared\DisplayTemplates* klasörüne sağ tıklayın.

**Ekle** ' ye tıklayın ve ardından **görüntüle**' ye tıklayın. **Görünüm Ekle** iletişim kutusu görüntülenir.

**Görünüm adı** kutusuna `DateTime`yazın. (Bu adı, türün adıyla eşleşecek şekilde kullanmanız gerekir.)

**Kısmi görünüm olarak oluştur** onay kutusunu seçin. **Düzen veya ana sayfa kullan** ve **kesin türü belirtilmiş bir görünüm oluştur** onay kutularının seçili olmadığından emin olun.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

**Ekle**'ye tıklayın. *Views\shared\displaytemplates*Içinde bir *DateTime. cshtml* şablonu oluşturulur.

Aşağıdaki görüntüde, `DateTime` görüntüleme ve düzenleyici şablonları oluşturulduktan sonra **Çözüm Gezgini** *görünümleri* klasörü gösterilmektedir.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

*Views\shared\displaytemplates\datetime.exe* dosyasını açın ve aşağıdaki biçimlendirmeyi ekleyerek, özelliği saat olmadan bir tarih olarak biçimlendirmek için [String. Format](https://msdn.microsoft.com/library/system.string.format.aspx) yöntemini kullanır. (`{0:d}` biçimi kısa tarih biçimini belirtir.)

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

*Views\movie\displaytemplates* klasöründe bir `DateTime` şablonu oluşturmak için bu adımı tekrarlayın. *Views\movie\displaytemplates\datetime.cshtml* dosyasında aşağıdaki kodu kullanın.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` CSS sınıfı, tarihin kalın kırmızı metinle görüntülenmesine neden olur. Bu belirli şablonun kullanıldığı zaman kolayca görebilmeniz için `loud-1` CSS sınıfını geçici bir ölçü olarak eklediniz.

İşiniz tamamlandı ve ASP.NET 'in tarihleri görüntülemesi için kullanacağı özelleştirilmiş şablonlar. Daha genel şablon ( *Views\shared\displaytemplates* klasöründe) basit bir kısa tarih görüntüler. Özellikle `Movie` denetleyicisi ( *Views\Movies\DisplayTemplates* klasöründe) için olan şablon, kalın kırmızı metin olarak biçimlendirilen kısa bir tarih görüntüler.

Uygulamayı çalıştırmak için CTRL+F5'e basın. Tarayıcı, uygulama için Dizin görünümünü işler.

`ReleaseDate` özelliği artık tarihi olmayan kalın kırmızı bir yazı tipinde görüntüler. Bu, *Views\Movies\DisplayTemplates* klasöründe şablonlu `DateTime` Yardımcısı ' nın, paylaşılan klasördeki `DateTime` şablonlu yardımcı üzerinden (*Views\shared\displaytemplates*) seçili olduğunu doğrulamanıza yardımcı olur.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

Şimdi *Views\Movies\DisplayTemplates\DateTime.cshtml* dosyasını *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*olarak yeniden adlandırın.

Uygulamayı çalıştırmak için CTRL+F5'e basın.

Bu kez `ReleaseDate` özelliği, zaman içinde ve kalın kırmızı yazı tipi olmadan bir tarih görüntüler. Bu, veri türü adı olan bir şablonun (Bu durumda `DateTime`) bu türün tüm model özelliklerini göstermek için otomatik olarak kullanıldığını gösterir. *DateTime. cshtml* dosyasını iksındatetime *. cshtml*olarak yeniden adlandırdıktan sonra, ASP.net artık *Views\Movies\DisplayTemplates* klasöründe bir şablon bulmadığından, bu nedenle * Views\Movies\Shared\* klasöründen *DateTime. cshtml* şablonunu kullandı.

(Şablon eşleştirmesi büyük/küçük harfe duyarlıdır, bu nedenle şablon dosya adını herhangi bir büyük harf ile oluşturmuş olabilirsiniz. Örneğin, *DateTime. cshtml, DateTime. cshtml*ve *datetime. cshtml* `DateTime` türüyle eşleşir.)

Gözden geçirmek için: Bu noktada, `ReleaseDate` alanı, verileri kısa tarih biçimi kullanılarak görüntüleyen *Views\Movies\DisplayTemplates\DateTime.cshtml* şablonu kullanılarak görüntülenir, aksi takdirde özel biçim yoktur.

### <a name="using-uihint-to-specify-a-display-template"></a>Bir görüntüleme şablonu belirtmek için Uııınt kullanma

Web uygulamanızın birçok `DateTime` alanı varsa ve varsayılan olarak bunların tümünü veya çoğunu tarih biçiminde bir biçimde göstermek istiyorsanız, *DateTime. cshtml* şablonu iyi bir yaklaşımdır. Ancak tarih ve saati tam olarak göstermek istediğiniz birkaç tarih varsa ne olacak? Sorun değil. Ek bir şablon oluşturabilir ve tam tarih ve saat için biçimlendirme belirtmek üzere [Uihınt](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) özniteliğini kullanabilirsiniz. Daha sonra, bu şablonu seçmeli olarak uygulayabilirsiniz. [Uıihınt](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) özniteliğini model düzeyinde kullanabilir veya şablonu bir görünüm içinde belirtebilirsiniz. Bu bölümde, bazı tarih-saat alan örneklerinin biçimlendirmesini seçmeli olarak değiştirmek için `UIHint` özniteliğini nasıl kullanacağınızı göreceksiniz.

*Views\Movies\DisplayTemplates\LoudDateTime.cshtml* dosyasını açın ve mevcut kodu şu kodla değiştirin:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

Bu, tam tarih ve saatin görüntülenmesine ve metnin yeşil ve büyük olmasını sağlayan CSS sınıfını eklemesine neden olur.

*Movie.cs* dosyasını açın ve aşağıdaki örnekte gösterildiği gibi [uihınt](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) özniteliğini `ReleaseDate` özelliğine ekleyin:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

Bu, ASP.NET MVC 'nin `ReleaseDate` özelliğini (özellikle de yalnızca herhangi bir `DateTime` nesnesi değil) gösterdiği zaman, bu, *Ses DateTime. cshtml* şablonunu kullanması gerektiğini söyler.

Uygulamayı çalıştırmak için CTRL+F5'e basın.

`ReleaseDate` özelliğinin artık büyük bir yeşil yazı tipinde tarih ve saati görüntülediğini görürsünüz.

*Movie.cs* dosyasındaki `UIHint` özniteliğine dönün ve bu öğeyi, *Ses tarihi. cshtml* şablonu kullanılmayacak şekilde not edin. Uygulamayı yeniden çalıştırın. Yayın tarihi büyük ve yeşil bir şekilde gösterilmez. Bu, *Views\shared\displaytemplates\datetime.exe* şablonunun dizin ve Ayrıntılar görünümlerinde kullanıldığını doğrular.

Daha önce belirtildiği gibi, şablonu bazı verilerin tek bir örneğine uygulamanızı sağlayan bir görünümde de şablon uygulayabilirsiniz. *Views\Movies\Details.cshtml* görünümünü açın. `ReleaseDate` alanı için bir [HTML. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) çağrısının ikinci parametresi olarak `"LoudDateTime"` ekleyin. Tamamlanan kod şöyle görünür:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

Bu, modele uygulanan özniteliklerin ne olursa olsun model özelliğini göstermek için `LoudDateTime` şablonunun kullanılması gerektiğini belirtir.

Uygulamayı çalıştırmak için CTRL+F5'e basın.

Film dizini sayfasının *Views\shared\displaytemplates\datetime.cshtml* şablonunu (kırmızı kalın) kullandığını ve *Movie\details* sayfasının *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* şablonunu (büyük ve yeşil) kullandığını doğrulayın.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

Sonraki bölümde, karmaşık bir tür için bir şablon oluşturacaksınız.

> [!div class="step-by-step"]
> [Önceki](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [İleri](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)
