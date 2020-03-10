---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: ASP.NET Web sayfalarına giriş-formları kullanarak veritabanı verileri girme | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide bir giriş formu oluşturma ve ASP.NET Web sayfalarını (...) kullandığınızda formdan aldığınız verileri bir veritabanı tablosuna nasıl girebileceğiniz gösterilmektedir.
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624539"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>ASP.NET Web sayfalarına giriş-formları kullanarak veritabanı verileri girme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, bir giriş formu oluşturma ve ASP.NET Web Pages (Razor) kullandığınızda formdan bir veritabanı tablosuna alacağınız verileri girme işlemlerinin nasıl yapılacağı gösterilmektedir. [ASP.NET Web SAYFALARıNDAKI HTML formlarının temelleri](https://go.microsoft.com/fwlink/?LinkId=251581)aracılığıyla seriyi tamamlamış olduğunu varsayar.
> 
> Öğrenecekleriniz:
> 
> - Giriş formlarını işleme hakkında daha fazla bilgi.
> - Veritabanına veri ekleme (ekleme).
> - Kullanıcıların bir formda gerekli bir değeri girdiğinden emin olma (Kullanıcı girişini doğrulama).
> - Doğrulama hatalarını görüntüleme.
> - Geçerli sayfadan başka bir sayfaya nasıl geçeirsiniz.
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - `Database.Execute` yöntemi.
> - SQL `Insert Into` ekstresi
> - `Validation` Yardımcısı.
> - `Response.Redirect` yöntemi.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Daha önce bir veritabanı oluşturmayı belirten öğreticide, **veritabanı çalışma alanında çalışarak veritabanını doğrudan** WebMatrix 'te düzenleyerek veritabanı verileri girdiniz. Çoğu uygulamada, verileri veritabanına koymanın pratik bir yolu değildir, ancak. Bu öğreticide, sizin veya herkesin veri girmesine ve veritabanına kaydetmesine imkan tanıyan bir Web tabanlı arabirim oluşturacaksınız.

Yeni filmler girebileceğiniz bir sayfa oluşturacaksınız. Sayfada, bir film başlığı, tarzı ve yılı girebileceğiniz alanlar (metin kutuları) bulunan bir giriş formu bulunur. Bu sayfa şöyle görünür:

![' Film Ekle ' sayfası tarayıcıda](entering-data/_static/image1.png)

Metin kutuları, bu biçimlendirme gibi görünecek HTML `<input>` öğeleri olacaktır:

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>Temel giriş formu oluşturma

*Addmovie. cshtml*adlı bir sayfa oluşturun.

Dosyada bulunan ve aşağıdaki işaretlerle değiştirin. Her şeyin üzerine yaz; kısa bir süre içinde bir kod bloğu ekleyeceksiniz.

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

Bu örnekte form oluşturmak için tipik HTML gösterilmektedir. Metin kutuları ve Gönder düğmesi için `<input>` öğelerini kullanır. Metin kutularının açıklamalı alt yazıları standart `<label>` öğeleri kullanılarak oluşturulur. `<fieldset>` ve `<legend>` öğeleri formun etrafına iyi bir kutu koyar.

Bu sayfada, `<form>` öğesinin `method` özniteliği için değer olarak `post` kullandığını unutmayın. Önceki öğreticide `get` yöntemini kullanan bir form oluşturdunuz. Bu, formun değerleri sunucuya gönderdiği halde istek hiçbir değişiklik yapmadığından doğrudur. Tüm BT verileri farklı yollarla getiremedi. Bununla birlikte, bu sayfada değişiklikler *yaparsınız —* yeni veritabanı kayıtları ekleyeceksiniz. Bu nedenle, bu form `post` yöntemini kullanmalıdır. (`GET` ve `POST` işlemleri arasındaki fark hakkında daha fazla bilgi için önceki öğreticideki[Get, post ve http fiil güvenliği](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) kenar çubuğu bölümüne bakın.)

Her metin kutusunun `name` öğesi olduğunu unutmayın (`title`, `genre`, `year`). Önceki öğreticide gördüğünüz gibi, bu adlara sahip olmanız gerektiğinden, kullanıcının girişini daha sonra alabilmeniz için bu adlar önemlidir. Herhangi bir ad kullanabilirsiniz. Hangi verileri kullandığınızı anımsamanıza yardımcı olacak anlamlı adlar kullanmak yararlı olacaktır.

Her bir `<input>` öğesinin `value` özniteliği Razor kodu bir bit kodu içerir (örneğin, `Request.Form["title"]`). Form gönderildikten sonra (varsa) metin kutusuna girilen değeri korumak için önceki öğreticide bu elin bir sürümünü öğrendiniz.

## <a name="getting-the-form-values"></a>Form değerlerini alma

Daha sonra, formunu işleyen kodu eklersiniz. Ana hat ' de şunları yapabilirsiniz:

1. Sayfanın nakledilip nakledilmediğini (gönderildi) denetleyin. Kodunuzda yalnızca kullanıcılar düğme tıkladıklarında, sayfa ilk çalıştırıldığında değil, çalıştırmak istediğiniz zaman.
2. Kullanıcının metin kutularına girdiği değerleri alın. Bu durumda, form `POST` fiilini kullandığından, `Request.Form` koleksiyonundan form değerlerini alırsınız.
3. Değerleri, *filmler* veritabanı tablosuna yeni bir kayıt olarak ekleyin.

Dosyanın en üstüne aşağıdaki kodu ekleyin:

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

İlk birkaç satır, metin kutularından değerleri tutmak için değişkenler (`title`, `genre`ve `year`) oluşturur. Satır `if(IsPost)`, değişkenlerin *yalnızca* Kullanıcı **Film Ekle** düğmesine tıklaması durumunda ayarlanmış olduğundan emin olur. diğer bir deyişle, form ne zaman gönderilir.

Önceki bir öğreticide gördüğünüz gibi, `Request.Form["name"]`gibi bir ifade kullanarak bir metin kutusunun değerini alır, burada *name* `<input>` öğesinin adıdır.

Değişkenlerin adları (`title`, `genre`ve `year`) rastgele. `<input>` öğelerine atadığınız adlar gibi bunları dilediğiniz şekilde çağırabilirsiniz. (Değişkenlerin adları, formdaki `<input>` öğelerinin ad öznitelikleriyle eşleşmek zorunda değildir.) `<input>` öğelerinde olduğu gibi, içerdikleri verileri yansıtan değişken adlarını kullanmak iyi bir fikirdir. Kod yazdığınızda, tutarlı adlar hangi verileri kullandığınızı hatırlamanıza daha kolay hale getirir.

## <a name="adding-data-to-the-database"></a>Veritabanına veri ekleme

Az önce eklediğiniz kod bloğunda, `if` bloğunun (yalnızca kod bloğunun içinde değil) kapanış ayracı *içinde* (`}`), aşağıdaki kodu ekleyin:

[!code-csharp[Main](entering-data/samples/sample3.cs)]

Bu örnek, verileri getirmek ve göstermek için önceki bir öğreticide kullandığınız koda benzer. `db =` ile başlayan çizgi, daha önce olduğu gibi veritabanını açar ve sonraki satır bir SQL ifadesini daha önce gördüğünüz şekilde tanımlar. Ancak, bu kez bir SQL `Insert Into` bildirisini tanımlar. Aşağıdaki örnek `Insert Into` deyimin genel sözdizimini göstermektedir:

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

Diğer bir deyişle, eklenecek tabloyu belirtin, sonra eklenecek sütunları listeleyin ve ardından eklenecek değerleri listeleyin. (Daha önce belirtildiği gibi, SQL büyük küçük harfe duyarlı değildir ancak bazı kullanıcılar, komutu okumayı kolaylaştırmak için anahtar sözcüklerini büyük harfle okur.)

İçine eklediğiniz sütunlar zaten komutta listelenmiştir — `(Title, Genre, Year)`. İlgi çekici olan bölüm, metin kutularından gelen değerleri komutun `VALUES` bölümüne alma. Gerçek değerler yerine, kurs yer tutucuları olan `@0`, `@1`ve `@2`görürsünüz. Komutunu çalıştırdığınızda (`db.Execute` satırında), metin kutularından aldığınız değerleri geçirirsiniz.

**Önemli!** Bir SQL deyimindeki bir kullanıcı tarafından çevrimiçi olarak girilen verileri her zaman içeren tek bir şekilde, burada gördüğünüz gibi (`VALUES(@0, @1, @2)`) yer tutucuları kullanacağınızı unutmayın. Kullanıcı girişini bir SQL ifadesine eklerseniz, [ASP.NET Web sayfalarında](https://go.microsoft.com/fwlink/?LinkId=251581) (önceki öğreticide) form temelleri bölümünde açıklandığı gibi, kendınızı bir SQL ekleme saldırısında açarsınız.

Hala `if` bloğunun içinde, `db.Execute` satırından sonra aşağıdaki satırı ekleyin:

[!code-css[Main](entering-data/samples/sample4.css)]

Yeni film veritabanına eklendikten sonra, bu çizgi sizi (yeniden yönlendirmeleri) *filmler* sayfasına atlar, böylece yeni girdiğiniz filmi görebilirsiniz. `~` işleci "Web sitesinin kökü" anlamına gelir. (`~` işleci yalnızca HTML biçiminde değil, yalnızca ASP.NET sayfalarında kullanılabilir.)

Kod bloğu tamamı şu örneğe benzer şekilde görünür:

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>INSERT komutunu test etme (Şu ana kadar)

Henüz bitmedi, ancak şimdi test etmek iyi bir zaman.

WebMatrix 'teki dosyaların ağaç görünümünde, *Addmovie. cshtml* sayfasına sağ tıklayın ve ardından **tarayıcıda Başlat**' a tıklayın.

![' Film Ekle ' sayfası tarayıcıda](entering-data/_static/image2.png)

(Tarayıcıda farklı bir sayfa ile karşılaşırsanız, URL 'nin `http://localhost:nnnnn/AddMovie`) olduğundan emin olun *, burada,* bu, kullandığınız bağlantı noktası numarasıdır.)

Bir hata sayfası mı alıyorsunuz? Bu durumda, dikkatlice okuyun ve kodun tam olarak daha önce listelenmiş şekilde göründüğünden emin olun.

Forma bir film girin &mdash; Örneğin, "vatandaşlık Kane", "drama" ve "1941" kullanın. (Veya herhangi bir.) Ardından **Film Ekle**' ye tıklayın.

Hepsi iyi gitiyorsa, *filmler* sayfasına yönlendirilirsiniz. Yeni filminizin listelendiğinden emin olun.

![Yeni eklenen filmi gösteren filmler sayfası](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>Kullanıcı girişini doğrulama

*Addmovie* sayfasına dönün veya yeniden çalıştırın. Başka bir film girin, ancak bu kez yalnızca başlık &mdash; girin, örneğin "Singın' yazın". Ardından **Film Ekle**' ye tıklayın.

*Filmler* sayfasına yeniden yönlendirilirsiniz. Yeni filmi bulabilirsiniz, ancak bu, tamamlanmamış olabilir.

![Bazı değerler eksik olan yeni filmi gösteren filmler sayfası](entering-data/_static/image4.png)

*Filmler* tablosunu oluşturduğunuz zaman, alanlardan hiçbirinin null olduğunu açıkça belirttik. Burada yeni filmler için bir giriş formunuz vardır ve alanları boş bırakın. Bu bir hatadır.

Bu durumda veritabanı aslında bir hata yükseltmedi (veya *oluşturmaz*). Bir tarz veya yıl belirtmediniz, bu nedenle *Addmovie* sayfasındaki kod bu değerleri, *boş dizeler*olarak kabul ediyor. SQL `Insert Into` komutu çalıştırıldığında, tarz ve yıl alanlarında bu alanlarda faydalı veriler yoktu, ancak bunlar null değil.

Kuşkusuz, kullanıcıların veritabanına yarı boş film bilgileri girmesini sağlamak istemezsiniz. Çözüm, kullanıcının girişini doğrulamaktır. İlk olarak, doğrulama yalnızca kullanıcının tüm alanlar için bir değer girdiğinden emin olur (yani, hiçbirinin boş bir dize içermediği).

> [!TIP]
> 
> **Null ve boş dizeler**
> 
> Programlamada, "değer yok" gibi farklı düşünceler arasında bir ayrım vardır. Genel olarak, hiçbir şekilde hiçbir şekilde ayarlanmadıysa veya başlatılamıyorsa bir değer *null* olur. Buna karşılık, karakter verisi (dizeler) bekleyen bir değişken *boş bir dizeye*ayarlanabilir. Bu durumda, değer null değildir; yalnızca uzunluğu sıfır olan bir karakter dizesi olarak ayarlanmıştır. Bu iki deyim farkı göstermektedir:
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> Bu çok daha karmaşıktır, ancak önemli nokta, `null` belirlenmeyen bir durum sıralamasını temsil etmektedir.
> 
> Şimdi bir değer null olduğunda ve yalnızca boş bir dize olduğunda tam olarak anlaşılması önemlidir. *Addfilm* sayfasında, `Request.Form["title"]` kullanarak metin kutularının değerlerini alır ve bu şekilde devam eder. Sayfa ilk çalıştırıldığında (düğmeye tıklamadan önce) `Request.Form["title"]` değeri null olur. Ancak formu gönderdiğinizde, `Request.Form["title"]` `title` metin kutusunun değerini alır. Açık değil, ancak boş bir metin kutusu null değil; yalnızca içinde boş bir dize vardır. Bu nedenle, kod düğme tıklamasından yanıt olarak çalıştığında `Request.Form["title"]` öğesinde boş bir dize vardır.
> 
> Bu ayrım neden önemlidir? *Filmler* tablosunu oluşturduğunuz zaman, alanlardan hiçbirinin null olduğunu açıkça belirttik. Ancak burada yeni filmler için bir giriş formunuz vardır ve alanları boş bırakın. Tarz veya yıl için değer olmayan yeni filmleri kaydetmeye çalıştığınızda, veritabanının şikayetini makul bir şekilde beklemeniz gerekir. Ancak, bu metin kutularını boş bıraksanız bile bu nokta &mdash;, değerler null değildir; Bunlar boş dizelerdir. Sonuç olarak, bu sütunlar boş &mdash; ancak null olamaz. bu sütunlara yeni filmleri veritabanına kaydedebilirsiniz! &mdash; değerleri. Bu nedenle, kullanıcıların girişini doğrulayarak yapabileceğiniz, kullanıcıların boş bir dize göndermezler olduğundan emin olmanız gerekir.

### <a name="the-validation-helper"></a>Doğrulama Yardımcısı

ASP.NET Web sayfaları, kullanıcıların gereksinimlerinizi karşılayan verileri girdiğinden emin olmak için kullanabileceğiniz `Validation` Yardımcısı &mdash; &mdash; yardımcı içerir. `Validation` Yardımcısı, ASP.NET Web sayfalarına yerleşik olarak bulunan Yardımcılarınızdan biridir. bu nedenle, önceki bir öğreticide Gravatar Yardımcısı 'nı yüklediğiniz şekilde NuGet kullanarak bir paket olarak yüklemek zorunda kalmazsınız.

Kullanıcının girişini doğrulamak için aşağıdakileri yapmanız gerekir:

- Sayfadaki metin kutularında değer gerektirmek istediğinizi belirtmek için kodu kullanın.
- Filmi yalnızca her şey düzgün şekilde doğrulanırsa, film bilgilerinin veritabanına eklenmesi için koda bir test koyun.
- Hata iletilerini göstermek için biçimlendirmeye kod ekleyin.

*Addmovie* sayfasındaki kod bloğunda, değişken bildirimlerinin önüne sağ üstteki olarak, aşağıdaki kodu ekleyin:

[!code-csharp[Main](entering-data/samples/sample7.cs)]

Giriş gerektirmek istediğiniz her alan (`<input>` öğesi) için `Validation.RequireField` bir kez çağrı yapabilirsiniz. Ayrıca, burada gördüğünüz gibi her bir çağrı için özel bir hata iletisi ekleyebilirsiniz. (İletileri, istediğiniz herhangi bir şeyi koyabileceğiniz göstermek için de farklılıyoruz.)

Bir sorun varsa, yeni film bilgilerinin veritabanına eklenmesini engellemek isteyebilirsiniz. `if(IsPost)` bloğunda, `Validation.IsValid()`test eden başka bir koşul eklemek için `&&` (mantıksal ve) kullanın. İşiniz bittiğinde `if(IsPost)` bloğunun tamamı şu kod gibi görünür:

[!code-csharp[Main](entering-data/samples/sample8.cs)]

`Validation` Yardımcısını kullanarak kaydettiğiniz alanlarla ilgili bir doğrulama hatası varsa, `Validation.IsValid` yöntemi false döndürür. Bu durumda, bu bloktaki kodların hiçbiri çalıştırılamayacak, bu nedenle veritabanına geçersiz bir film girişi eklenemeyecektir. *Filmler* sayfasına yönlendirilmezseniz, tabii olursunuz.

Doğrulama kodu da dahil olmak üzere tüm kod blokları Şu örneğe benzer şekilde görünür:

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>Doğrulama hatalarını görüntüleme

Son adım hata iletilerini görüntülemektir. Her doğrulama hatası için tek tek iletileri görüntüleyebilir veya bir özet veya her ikisini de görüntüleyebilirsiniz. Bu öğreticide, her ikisini de nasıl çalıştığını görebileceğiniz şekilde yapacaksınız.

Doğrulamadığınızı her bir `<input>` öğesinin yanında, `Html.ValidationMessage` yöntemini çağırın ve bu dosyayı doğrulamadığınızdan `<input>` öğenin adına geçirin. `Html.ValidationMessage` yöntemini, hata iletisinin görünmesini istediğiniz yere yerleştirebilirsiniz. Sayfa çalıştırıldığında `Html.ValidationMessage` yöntemi, doğrulama hatasının gideceği bir `<span>` öğesi işler. (Hata yoksa `<span>` öğesi işlenir, ancak içinde hiç metin yoktur.)

Sayfadaki biçimlendirmeyi, sayfadaki üç `<input>` öğenin her biri için bir `Html.ValidationMessage` Yöntemi içerecek şekilde değiştirin, örneğin:

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

Özetin nasıl çalıştığını görmek için, sayfadaki `<h1>Add a Movie</h1>` öğeden hemen sonra aşağıdaki biçimlendirmeyi ve kodu ekleyin:

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

`Html.ValidationSummary` yöntemi, varsayılan olarak tüm doğrulama mesajlarını bir liste içinde (bir `<div>` öğesi içindeki bir `<ul>` öğesi) görüntüler. `Html.ValidationMessage` yönteminde olduğu gibi, doğrulama özeti için biçimlendirme her zaman işlenir; hata yoksa, hiçbir liste öğesi işlenmez.

Özet, alana özgü her hatayı göstermek için `Html.ValidationMessage` yöntemi kullanılarak yerine doğrulama iletilerini görüntülemenin alternatif bir yolu olabilir. Ya da hem Özet hem de Ayrıntılar kullanabilirsiniz. Ya da genel bir hata göstermek için `Html.ValidationSummary` yöntemini kullanabilir ve sonra, ayrıntıları göstermek için tek `Html.ValidationMessage` çağrılarını kullanabilirsiniz.

Tüm sayfa şu örneğe benzer şekilde görünür:

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

İşte bu kadar. Artık bir filmi ekleyerek ve bir veya daha fazla alandan bırakarak sayfayı test edebilirsiniz. Bunu yaptığınızda, aşağıdaki hata ekranını görürsünüz:

![Doğrulama hata iletilerini gösteren film sayfası ekle](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>Doğrulama hata Iletilerini Stillendirme

Hata iletileri olduğunu, ancak gerçekten çok iyi bir şekilde görmemenizi görebilirsiniz. Yine de hata iletilerini stillemenin kolay bir yolu vardır.

`Html.ValidationMessage`tarafından görüntülenen ayrı hata iletilerine stil eklemek için `field-validation-error`adlı bir CSS stil sınıfı oluşturun. Doğrulama özetinin görünümünü tanımlamak için `validation-summary-errors`adlı bir CSS stil sınıfı oluşturun.

Bu tekniğin nasıl çalıştığını görmek için, sayfanın `<head>` bölümünün içine bir `<style>` öğesi ekleyin. Ardından aşağıdaki kuralları içeren `field-validation-error` ve `validation-summary-errors` adlı stil sınıflarını tanımlayın:

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

Genellikle stil bilgilerini ayrı bir *. css* dosyasına koyabilirsiniz, ancak kolaylık sağlaması için bunları sayfaya şimdi ekleyebilirsiniz. (Bu öğretici kümesinde daha sonra CSS kurallarını ayrı bir *. css* dosyasına taşıyacaksınız.)

Bir doğrulama hatası varsa `Html.ValidationMessage` yöntemi `class="field-validation-error"`içeren bir `<span>` öğesi işler. Bu sınıfa bir stil tanımı ekleyerek iletinin nasıl göründüğünü yapılandırabilirsiniz. Hatalar varsa `ValidationSummary` yöntemi aynı şekilde özniteliği `class="validation-summary-errors"`dinamik olarak işler.

Sayfayı yeniden çalıştırın ve bir dizi alanın bir kısmını bırakın. Hatalar artık daha belirgin. (Aslında bunlar fazla yapılır, ancak yapabileceklerinizi göstermek yeterlidir.)

![Stil eklenmiş doğrulama hatalarını gösteren film sayfası ekle](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>Filmler sayfasına bağlantı ekleme

Son bir adım, ilk film listesinden *addmovie* sayfasına ulaşmak için uygun hale getirme.

*Filmler* sayfasını yeniden açın. `WebGrid` yardımcısını izleyen kapatma `</div>` etiketinden sonra, aşağıdaki biçimlendirmeyi ekleyin:

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

Daha önce gördüğünüz gibi, ASP.NET `~` işlecini Web sitesinin kökü olarak yorumlar. `~` işlecini kullanmanız gerekmez; biçimlendirme `<a href="./AddMovie">Add a movie</a>` veya HTML 'nin anladığı yolu tanımlamak için başka bir yol kullanabilirsiniz. Ancak `~` işleci, Razor sayfaları için bağlantılar oluşturduğunuzda, siteyi daha esnek hale getiren iyi bir genel yaklaşımdır. geçerli sayfayı bir alt klasöre taşırsanız bağlantı yine de *Addmovie* sayfasına gider. (`~` işlecinin yalnızca *. cshtml* sayfalarında çalışıp çalışmadığını unutmayın. ASP.NET anlamıştır, ancak standart HTML değildir.)

İşiniz bittiğinde, *filmler* sayfasını çalıştırın. Bu sayfa şöyle görünür:

![' Film Ekle ' sayfasına bağlantısı olan filmler sayfası](entering-data/_static/image7.png)

*Addmovie* sayfasına gittiğinden emin olmak Için **Film Ekle** bağlantısına tıklayın.

## <a name="coming-up-next"></a>Sonraki adımda

Sonraki öğreticide, kullanıcıların veritabanında zaten bulunan verileri düzenlemesine nasıl izin vereceğinizi öğreneceksiniz.

## <a name="complete-listing-for-addmovie-page"></a>AddMovie sayfası için listeyi tamamlar

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools sitesinde [SQL INSERT INTO bildirisi](http://www.w3schools.com/sql/sql_insert.asp)
- [ASP.NET Web sayfaları sitelerinde Kullanıcı girişi doğrulanıyor](https://go.microsoft.com/fwlink/?LinkId=253002). `Validation` Yardımcısı ile çalışma hakkında daha fazla bilgi.

> [!div class="step-by-step"]
> [Önceki](form-basics.md)
> [İleri](updating-data.md)
