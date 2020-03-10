---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: ViewData kullanma ve ViewModel sınıfları uygulama | Microsoft Docs
author: microsoft
description: 6\. adım, daha zengin form düzenlemesi senaryolarına yönelik desteğin nasıl etkinleştirileceğini gösterir ve ayrıca denetleyicilerden görünümlere veri aktarmak için kullanılabilecek iki yaklaşım da anlatılmaktadır:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541610"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>ViewData Kullanma ve ViewModel Sınıfları Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) adım 6 ' dır.
> 
> 6\. adım, daha zengin form düzenlemesi senaryolarına yönelik desteğin nasıl etkinleştirileceğini gösterir ve ayrıca denetleyicilerden görünümlere veri aktarmak için kullanılabilecek iki yaklaşım da anlatmaktadır: ViewData ve ViewModel.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>Nerdakşam yemeği adım 6: ViewData ve ViewModel

Birkaç form gönderi senaryosu ekledik ve Create, Update ve Delete (CRUD) desteğinin nasıl uygulanacağı açıklanmaktadır. Artık DinnersController uygulamamızı daha fazla inceleyeceğiz ve daha zengin form düzenlemesi senaryolarına yönelik destek sağlar. Bunu yaparken, denetleyicilerden görünümlere veri aktarmak için kullanılabilecek iki yaklaşım ele alınacaktır: ViewData ve ViewModel.

### <a name="passing-data-from-controllers-to-view-templates"></a>Denetleyicilerden görüntülemek için verileri geçirme-Şablonlar

MVC deseninin tanımlayıcı özelliklerinden biri, bir uygulamanın farklı bileşenleri arasında zorlamaya yardımcı olur. Modeller, denetleyiciler ve görünümlerin her biri iyi tanımlanmış rollere ve sorumluluklara sahiptir ve her ikisi arasında iyi tanımlanmış yollarla iletişim kurar. Bu, test edilebilirlik ve kod yeniden kullanımını yükseltir.

Bir denetleyici sınıfı bir istemciye geri HTML yanıtı işlemeye karar verdiğinde, yanıtı işlemek için gereken tüm verilerin görünüm şablonuna açıkça geçirilmesinden sorumludur. Görünüm şablonları hiçbir şekilde hiçbir veri alımı veya uygulama mantığını gerçekleştirmemelidir; bunun yerine, denetleyici tarafından yalnızca modelin/verilerin üzerinde çalışan işleme koduna sahip olması gerekir.

Artık DinnersController sınıfımızda bulunan model verileri görünüm şablonlarımızla, basit ve düz ileri sarma: Dizin () durumunda akşam yemeği nesnelerinin bir listesi ve ayrıntılar (), düzenleme (), oluşturma () ve silme () durumunda tek bir akşam yemeği nesnesi. Uygulamamıza daha fazla UI özelliği eklediğimiz için genellikle görünüm Şablonlarımızda HTML yanıtlarını işlemek üzere yalnızca bu verilerden daha fazla bilgi iletmemiz gerekir. Örneğin, düzenleme ve görüntüleme görünümlerinde "Country" alanını, bir HTML TextBox iken bir DropDownList 'e değiştirmek isteyebilir. Görünüm şablonunda ülke adlarının açılan listesini sabit koda eklemek yerine, dinamik olarak doldurduğumuz desteklenen ülkelerin listesinden oluşturmak isteyebilirsiniz. Yalnızca akşam yemeği nesnesini *ve* denetleyicimizden desteklenen ülkelerin listesini Görünüm Şablonlarımıza geçirmek için bir yol gerekir.

Bunu gerçekleştirebilmemiz için iki yola bakalım.

### <a name="using-the-viewdata-dictionary"></a>ViewData sözlüğünü kullanma

Denetleyici temel sınıfı, denetleyicilerden görünümlere ek veri öğeleri geçirmek için kullanılabilen bir "ViewData" Sözlük özelliği sunar.

Örneğin, düzenleme görünümümüzdeki "Country" metin kutusunu bir DropDownList olarak değiştirmek istediğimiz senaryoyu desteklemek için, düzenlenecek düzenleme () eylem yöntemini (bir akşam yemeği nesnesine ek olarak) e-posta olarak kullanılabilecek bir SelectList nesnesi olarak güncelleştirebiliriz. bir ülkelerin DropDownList 'i.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

Yukarıdaki SelectList 'in Oluşturucusu, aşağı açılan listeyi ve şu anda seçili değeri doldurmak için ilçelerin bir listesini kabul ediyor.

Daha sonra, daha önce kullandığımız HTML. TextBox () yardımcı yöntemi yerine HTML. DropDownList () yardımcı yöntemini kullanmak için Edit. aspx görünüm şablonunuzu güncelleştirebiliriz:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

Yukarıdaki HTML. DropDownList () yardımcı yöntemi iki parametre alır. İlki çıktının HTML form öğesinin adıdır. İkincisi, ViewData sözlüğü aracılığıyla geçirdiğimiz "SelectList" modelidir. Sözlük içindeki türü SelectList olarak dönüştürmek için C# "as" anahtar sözcüğünü kullanıyoruz.

Şimdi uygulamamızı çalıştırdığımızda ve tarayıcımızda */Dinners/Edit/1* URL 'sine erişirken, düzenleme Kullanıcı arabirimimizin metin kutusu yerine ülkelerin bir DropDownList 'i görüntülemesi için güncelleştirildiğini görüyoruz:

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

Ayrıca, HTTP-POST düzenleme yönteminden (hata oluştuğunda senaryolar) düzenleme görünümü şablonunu da işlediğimiz için, görünüm şablonu hata senaryolarında işlendiğinde, bu yöntemi de ViewData öğesine eklemek için de güncelleştirdiğimiz emin olmak istiyoruz:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

Artık DinnersController düzenleme senaryomız bir DropDownList 'i destekliyor.

### <a name="using-a-viewmodel-pattern"></a>ViewModel deseninin kullanımı

ViewData sözlüğü yaklaşımının uygulanması oldukça hızlı ve kolay bir avantajdır. Bazı geliştiriciler, derleme zamanında yakalanmayacak hatalara yol açacağından, bazı geliştiriciler dize tabanlı sözlükleri kullanmaktan daha da benzer. Türsüz ViewData sözlüğü Ayrıca bir görünüm şablonunda olduğu gibi C# kesin olarak belirlenmiş bir dil kullanırken "as" işlecinin veya atama için kullanılması gerekir.

Kullandığımız alternatif bir yaklaşım, "ViewModel" modeli olarak adlandırılır. Bu model kullanılırken, belirli görünüm senaryolarımız için optimize edilmiş ve görünüm şablonlarımız tarafından gerek duyulan dinamik değerler/içerik özelliklerini sunan kesin türü belirtilmiş sınıflar oluşturuyoruz. Denetleyici sınıflarımız daha sonra bu görünümün en iyi duruma getirilmiş sınıflarını, kullanılacak görünüm şablonumuza yerleştirebilir ve geçirebilir. Bu, Görünüm şablonları içinde tür güvenliği, derleme zamanı denetimi ve düzenleyici IntelliSense 'i sunar.

Örneğin, akşam yemeği form düzenlemesini etkinleştirmek için aşağıdaki iki tür özelliği sunan bir "DinnerFormViewModel" sınıfı oluştururuz: bir akşam yemeği nesnesi ve DropDownList 'i doldurmak için gereken SelectList modeli:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

Sonra, depomızdan aldığımız akşam yemeği nesnesini kullanarak DinnerFormViewModel oluşturmak ve ardından bunu görünüm şablonumuza geçirmek için düzenleme () eylem yönteminizi güncelleştirebiliriz:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

Daha sonra, Edit. aspx sayfasının en üstündeki "Inherits" özniteliğini değiştirerek "akşam yemeği" nesnesi yerine "DinnerFormViewModel" öğesini bekletireceğiz:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

Bunu yaptıktan sonra, görünüm şablonumuz içindeki "model" özelliğinin IntelliSense, DinnerFormViewModel türünün nesne modelini gösterecek şekilde güncelleştirilecektir:

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

Daha sonra Görünüm kodumuzu, bu durumda çalışacak şekilde güncelleştirebiliriz. Oluşturduğumuz giriş öğelerinin adlarını değiştirmizin (form öğeleri "başlık", "ülke" olarak adlandırılıyordu), ancak DinnerFormViewModel sınıfını kullanarak değerleri almak için HTML Yardımcısı yöntemlerini güncelleştiriyoruz.

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

Ayrıca, hataları işlerken DinnerFormViewModel sınıfını kullanmak için düzenleme gönderi yönteminizi güncelleştireceğiz:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

Ayrıca, aynı *DinnerFormViewModel* sınıfını yeniden kullanmak için oluşturma () eylem yöntemlerinizi de güncelleştirebilir. HTTP-GET uygulamasının aşağıda verilmiştir:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

HTTP-POST oluşturma yönteminin uygulanması aşağıda verilmiştir:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

Artık düzenleme ve oluşturma ekranlarımız, ülkeyi çekmeye yönelik aşağı açılan listeleri destekliyor.

### <a name="custom-shaped-viewmodel-classes"></a>Özel şekillendirilmiş ViewModel sınıfları

Yukarıdaki senaryoda, DinnerFormViewModel sınıfımız, bir özellik olarak akşam yemeği model nesnesini, bir destekleme SelectList model özelliği ile birlikte kullanıma sunar. Bu yaklaşım, görünüm şablonumuzdan oluşturmak istediğimiz HTML Kullanıcı arabiriminin, etki alanı modeli nesnelerimize görece yakından karşılık geldiği senaryolarda sorunsuz bir şekilde çalışmaktadır.

Bunun durum olmadığı senaryolar için kullanabileceğiniz bir seçenek, nesne modeli görünüm tarafından tüketimine daha iyileştirilmiş olan ve temel alınan etki alanı model nesnesinden tamamen farklı görünebilen özel şekillendirilmiş bir ViewModel sınıfı oluşturmaktır. Örneğin, birden çok model nesnesinden toplanan farklı özellik adlarını ve/veya toplama özelliklerini açığa çıkarmak mümkündür.

Özel şekillendirilmiş ViewModel sınıfları, denetleyicilerden görünümlere veri geçirmek için ve bir denetleyicinin eylem yöntemine geri gönderilen form verilerinin işlenmesine yardımcı olmak için kullanılabilir. Bu sonraki senaryo için, bir ViewModel nesnesini form ile gönderilen verilerle güncelleştirme yöntemine sahip olabilir ve ardından ViewModel örneğini kullanarak gerçek bir etki alanı modeli nesnesini eşleştirir veya alabilirsiniz.

Özel şekillendirilmiş ViewModel sınıfları harika bir esneklik sağlayabilir ve işleme kodunu görünüm şablonlarınızda veya eylem yöntemlerinizin içindeki form-Posting kodunda, çok karmaşık alınmaya başlayan bir şekilde araştırmanız için bir şey olabilir. Bu genellikle etki alanı modellerinizin, oluşturduğunuz Kullanıcı arabirimine düzgün şekilde karşılık gelmediyse ve bir ara özel şekillendirilmiş ViewModel sınıfının yardım edebilir.

### <a name="next-step"></a>Sonraki adım

Şimdi, uygulama genelinde Kullanıcı arabirimini yeniden kullanmak ve paylaşmak için partileri ve ana sayfaları nasıl kullanabileceğimizi inceleyelim.

> [!div class="step-by-step"]
> [Önceki](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [İleri](re-use-ui-using-master-pages-and-partials.md)
