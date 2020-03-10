---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: ASP.NET Web sayfalarına giriş-HTML form temelleri | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda bir giriş formu oluşturma ve kullanıcının girişini işleme hakkında temel bilgiler gösterilmektedir. Şimdi...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574286"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>ASP.NET Web sayfalarına giriş-HTML form temelleri

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda bir giriş formu oluşturma ve kullanıcının girişini işleme hakkında temel bilgiler gösterilmektedir. Artık bir veritabanınız olduğuna göre, kullanıcıların veritabanında belirli filmleri bulmasına izin vermek için form becerilerinizi kullanacaksınız. [ASP.NET Web sayfalarını kullanarak verileri görüntülemeye giriş](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data)ile seriyi tamamlamış olduğunu varsayar.
> 
> Öğrenecekleriniz:
> 
> - Standart HTML öğelerini kullanarak form oluşturma.
> - Kullanıcının bir formdaki girişini okuma.
> - Kullanıcının sağladığı bir arama terimini kullanarak verileri seçmeli olarak alan bir SQL sorgusu oluşturma.
> - "Kullanıcının ne girdiği" konusunda "hatırlama" sayfasında alan
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - `Request` nesnesi.
> - SQL `Where` yan tümcesi.

## <a name="what-youll-build"></a>Ne oluşturacağız?

Önceki öğreticide, bir veritabanı oluşturdunuz, ona veri ekledi ve sonra verileri göstermek için `WebGrid` yardımcısını kullandınız. Bu öğreticide, belirli bir tarzın filmlerini bulmanıza veya başlığında girdiğiniz herhangi bir sözcük içeren bir arama kutusu ekleyeceksiniz. (Örneğin, tarzı "Action" olan veya başlığı "Harry" veya "Adventure" içeren tüm filmleri bulabilirsiniz.

Bu öğreticiyi tamamladığınızda, şöyle bir sayfanız olacaktır:

![Tarz ve başlık arama içeren filmler sayfası](form-basics/_static/image1.png)

Sayfanın listeleme bölümü, kılavuz &mdash; son öğreticideki ile aynıdır. Fark, kılavuzun yalnızca aradığınız filmleri gösterecektir.

## <a name="about-html-forms"></a>HTML formları hakkında

(HTML formları oluşturma konusunda deneyiminiz varsa ve `GET` ve `POST`arasındaki farklılığı varsa, bu bölümü atlayabilirsiniz.)

Bir formda, metin kutuları, düğmeler, radyo düğmeleri, onay kutuları, açılan listeler ve benzeri Kullanıcı giriş öğeleri &mdash; vardır. Kullanıcılar bu denetimleri doldurur veya seçimler yapar ve ardından bir düğmeye tıklayarak formu gönderir.

Bir formun temel HTML sözdizimi bu örneğe göre gösterilmiştir:

[!code-html[Main](form-basics/samples/sample1.html)]

Bu biçimlendirme bir sayfada çalıştığında, bu çizimi şöyle görünen basit bir form oluşturur:

![Tarayıcıda işlenmiş şekilde temel HTML formu](form-basics/_static/image2.png)

`<form>` öğesi gönderilecek HTML öğelerini barındırır. (Oluşturmanın kolay bir hata olması, sayfaya öğe eklemek ve ardından bunları bir `<form>` öğesinin içine koymayı unutmak olur. Bu durumda hiçbir şey gönderilmez.) `method` özniteliği, tarayıcıya Kullanıcı girişinin nasıl göndereceklerini söyler. Sunucuda bir güncelleştirme gerçekleştirmeniz `get` veya sunucudan yalnızca veri getirmeniz durumunda bu `post` olarak ayarlanır.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **GET, POST ve HTTP fiil güvenliği**
> 
> Tarayıcı ve sunucuların bilgi alışverişi için kullandığı protokol olan HTTP, temel işlemlerinde daha basit bir işlemdir. Tarayıcılar, sunuculara istek yapmak için yalnızca birkaç fiil kullanır. Web için kod yazdığınızda, bu yüklemleri ve tarayıcının ve sunucunun bunları nasıl kullandığını anlamanız yararlı olur. En yaygın olarak kullanılan fiiller şunlardır:
> 
> - `GET`. Tarayıcı, sunucudan bir şeyi getirmek için bu fiili kullanır. Örneğin, tarayıcınıza bir URL yazdığınızda, tarayıcı istediğiniz sayfayı istemek için `GET` bir işlem gerçekleştirir. Sayfa grafik içeriyorsa, tarayıcı görüntüleri almak için ek `GET` işlemler gerçekleştirir. `GET` işlemin sunucuya bilgi geçirmesi gerekiyorsa, bilgiler sorgu dizesinde URL 'nin bir parçası olarak geçirilir.
> - `POST`. Tarayıcı, sunucuda eklenecek veya değiştirilecek verileri göndermek için bir `POST` isteği gönderir. Örneğin, `POST` fiil, bir veritabanındaki kayıtları oluşturmak veya var olanları değiştirmek için kullanılır. Çoğu zaman, bir formu doldururken ve Gönder düğmesine tıkladığınızda, tarayıcı `POST` bir işlem gerçekleştirir. `POST` işleminde sunucuya geçirilmekte olan veriler sayfanın gövdesinden olur.
> 
> Bu fiiller arasındaki önemli bir ayrım, `GET` bir işlemin sunucu üzerinde herhangi bir şeyi değiştirmesi veya biraz daha soyut bir şekilde yerine koymalarıdır; bir `GET` işlem, sunucuda durumunda bir değişikliğe neden olmaz. Aynı kaynaklarda, istediğiniz sayıda `GET` işlemi gerçekleştirebilirsiniz ve bu kaynaklar değişmez. (`GET` bir işlem genellikle "güvenli" olarak veya teknik bir dönem kullanmak için *ıdempotent*.) Bunun aksine, bir `POST` isteği, işlemi her gerçekleştirişinizde sunucuda bir şeyi değiştirir.
> 
> Bu ayrımı göstermeye yardımcı olacak iki örnek vardır. Bing veya Google gibi bir altyapıyı kullanarak arama gerçekleştirdiğinizde, tek bir metin kutusundan oluşan bir formu doldurup Ara düğmesine tıklayabilirsiniz. Tarayıcı, URL 'nin bir parçası olarak geçirilen kutuya girdiğiniz değeri içeren `GET` bir işlem gerçekleştirir. Bu tür bir form için `GET` işlemi kullanmak iyidir, çünkü bir arama işlemi sunucudaki kaynakları değiştirmez, yalnızca bilgi getirir.
> 
> Şimdi bir şeyi çevrimiçi olarak sıralama sürecini göz önünde bulundurun. Sipariş Ayrıntıları ' nı doldurup Gönder düğmesine tıklayabilirsiniz. Bu işlem bir `POST` isteği olur, çünkü işlem yeni bir sipariş kaydı, hesap bilgilerinde bir değişiklik ve belki de birçok başka değişiklik gibi sunucuda değişiklikler oluşmasına neden olur. `GET` işleminden farklı olarak, `POST` isteğinizi yinelenemez — siz isteği her yeniden başlattığınızda, sunucuda yeni bir sıra oluşturmanız gerekir. (Bu gibi durumlarda, Web siteleri genellikle bir Gönder düğmesine birden çok kez tıklamamanızı veya formu yanlışlıkla yeniden gönderemeyecek şekilde Gönder düğmesini devre dışı bırakacağını uyarır.)
> 
> Bu öğreticide, HTML formlarıyla çalışmak için hem `GET` işlemini hem de bir `POST` işlemini kullanacaksınız. Kullandığınız fiilin her durumda uygun bir durum olduğunu açıklayacağız.
> 
> (HTTP fiilleri hakkında daha fazla bilgi için bkz. W3C sitesindeki [Yöntem tanımları](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) makalesi.)

Birçok kullanıcı girişi öğesi HTML `<input>` öğeleridir. `<input type="type" name="name">,` şöyle görünür; burada *tür* , istediğiniz kullanıcı giriş denetimi türünü gösterir. Bu öğeler yaygın olanlardır:

- Metin kutusu: `<input type="text">`
- Onay kutusu: `<input type="check">`
- Radyo düğmesi: `<input type="radio">`
- Düğme: `<input type="button">`
- Gönder düğmesi: `<input type="submit">`

Ayrıca, bir çoklu metin kutusu oluşturmak için `<textarea>` öğesini ve bir açılan liste veya kaydırılabilir liste oluşturmak için `<select>` öğesini de kullanabilirsiniz. (HTML form öğeleri hakkında daha fazla bilgi için, bkz. W3Schools sitesinde [HTML Forms and Input](http://www.w3schools.com/html/html_forms.asp) .)

`name` özniteliği çok önemlidir, çünkü ad daha sonra göreceğiniz gibi, daha sonra bir öğenin değerini alabilir.

İlginç olan bölüm, sayfa geliştiricisi, kullanıcının girişi ile yapılır. Bu öğelerle ilişkili yerleşik davranış yok. Bunun yerine, kullanıcının girdiği veya seçtiği değerleri almanız ve bunlarla ilgili bir şey yapmanız gerekir. Bu öğreticide öğrenirsiniz.

> [!TIP] 
> 
> **HTML5 ve giriş formları**
> 
> Bildiğiniz gibi, HTML geçiştir ve en son sürüm (HTML5), kullanıcıların bilgi girmesi için daha sezgisel yollar desteği içerir. Örneğin, HTML5 'de, sizin (sayfa geliştiricisi), sayfanın bir tarih girmesini istediğinizi söyleyebilir. Tarayıcı, kullanıcının el ile tarih girmesini gerektirmek yerine otomatik olarak bir takvim görüntüleyebilir. Ancak HTML5 yenidir ve henüz tüm tarayıcılarda desteklenmez.
> 
> ASP.NET Web sayfaları, kullanıcı tarayıcısının bulunduğu ölçüde HTML5 girişini destekler. HTML5 içindeki `<input>` öğesi için yeni öznitelikler hakkında fikir için, bkz. W3Schools sitesinde [HTML &lt;ınput&gt; Type özniteliği](http://www.w3schools.com/html/html_form_input_types.asp) .

## <a name="creating-the-form"></a>Form Oluşturma

WebMatrix 'te **dosyalar** çalışma alanında, *filmler. cshtml* sayfasını açın.

Kapanış `</h1>` etiketinden sonra ve `grid.GetHtml` çağrısının açılış `<div>` etiketinden önce, aşağıdaki biçimlendirmeyi ekleyin:

[!code-html[Main](form-basics/samples/sample2.html)]

Bu biçimlendirme `searchGenre` ve Gönder düğmesi adlı bir metin kutusu içeren bir form oluşturur. Metin kutusu ve Gönder düğmesi, `method` özniteliği `get`olarak ayarlanmış bir `<form>` öğesi içine alınmıştır. (Metin kutusunu ve Gönder düğmesini bir `<form>` öğesinin içine yerleştirmezseniz, düğmeye tıkladığınızda hiçbir şey gönderilemeyecektir.) Sunucuda herhangi bir değişiklik yapmayan bir form oluşturduğunuz için burada `GET` fiilini kullanırsınız; yalnızca bir aramaya neden olur. (Önceki öğreticide, değişiklikleri sunucuya gönderdiğinizde bir `post` yöntemi kullandınız. Sonraki öğreticide bir daha görürsünüz.)

Sayfayı çalıştırın. Form için herhangi bir davranış tanımlamamış olsanız da, neye benzebileceğinize bakabilirsiniz:

![Tarz için arama kutusu içeren filmler sayfası](form-basics/_static/image3.png)

Metin kutusuna "komedi" gibi bir değer girin. Ardından **Ara tarzı**' ne tıklayın.

Sayfanın URL 'sini bir yere göz atın. `<form>` öğenin `method` özniteliğini `get`olarak ayarladığınız için, girdiğiniz değer şu şekilde URL 'deki sorgu dizesinin bir parçasıdır:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Form değerlerini okuma

Sayfa, veritabanı verilerini alan ve sonuçları bir kılavuzda görüntüleyen bazı kodları zaten içeriyor. Artık, arama terimini içeren bir SQL sorgusunu çalıştırabilmeniz için metin kutusunun değerini okuyan bazı kodlar eklemeniz gerekir.

Formun yöntemini `get`olarak ayarladığınız için, aşağıdaki gibi bir kod kullanarak metin kutusuna girilen değeri okuyabilirsiniz:

`var searchTerm = Request.QueryString["searchGenre"];`

`Request.QueryString` nesnesi (`Request` nesnesinin `QueryString` özelliği) `GET` işlemin bir parçası olarak gönderilen öğelerin değerlerini içerir. `Request.QueryString` özelliği, formda gönderilen değerlerin bir *koleksiyonunu* (bir listesini) içerir. Tek bir değer almak için istediğiniz öğenin adını belirtirsiniz. Bu nedenle, metin kutusunu oluşturan `<input>` öğesi (`searchTerm`) üzerinde `name` bir özniteliğe sahip olmanız gerekir. (`Request` nesnesi hakkında daha fazla bilgi için [kenar çubuğuna](#BKMK_TheRequestObject) daha sonra bakın.)

Metin kutusunun değerini okumak yeterince basittir. Ancak Kullanıcı, metin kutusuna hiç bir şey girmediyse ancak **Ara** ' yı tıklamadığında, arama yapmak için hiçbir şey olmadığından, tıklamayı yoksayabilirsiniz.

Aşağıdaki kod, bu koşulların nasıl uygulanacağını gösteren bir örnektir. (Bu kodu henüz eklemeniz gerekmez; bunu bir süre sonra yapmanız gerekir.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

Test şu şekilde aşağı doğru bir şekilde kesilir:

- `Request.QueryString["searchGenre"]`değerini alır, yani `searchGenre`adlı `<input>` öğeye girilen değer.
- `IsEmpty` yöntemi kullanılarak boş olup olmadığını öğrenin. Bu yöntem, bir şeyin (örneğin, form öğesi) bir değer içerip içermediğini belirlemenin standart yoludur. Ancak aslında yalnızca boş *değil* , bu nedenle...
- `IsEmpty` testinin önüne `!` işlecini ekleyin. (`!` işleci mantıksal DEĞIL anlamına gelir).

Düz Ingilizce olarak, tüm `if` koşulu şu şekilde çevirir: *formun Searchtarz öğesi boş değilse.* ..

Bu blok arama terimini kullanan bir sorgu oluşturmak için aşamayı belirler. Bunu bir sonraki bölümde yapacaksınız.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Istek nesnesi**
> 
> `Request` nesnesi, bir sayfa istendiğinde veya gönderildiğinde tarayıcının uygulamanıza gönderdiği tüm bilgileri içerir. Bu nesne, kullanıcının sağladığı, metin kutusu değerleri veya karşıya yüklenecek bir dosya gibi tüm bilgileri içerir. Ayrıca, tanımlama bilgileri, URL sorgu dizesindeki (varsa), çalışan sayfanın dosya yolu, kullanıcının kullandığı tarayıcı türü, tarayıcıda ayarlanan dillerin listesi gibi tüm ek bilgileri de içerir. ve çok daha fazlası.
> 
> `Request` nesnesi, değerlerin bir *koleksiyonudur* (listesidir). Adını belirterek koleksiyondan tek bir değer alırsınız:
> 
> `var someValue = Request["name"];`
> 
> `Request` nesnesi aslında çeşitli alt kümeler sunar. Örneğin:
> 
> - `Request.Form`, istek bir `POST` isteği ise, gönderilen `<form>` öğesi içindeki öğelerden değerler verir.
> - `Request.QueryString`, URL 'nin sorgu dizesindeki yalnızca değerleri verir. (`http://mysite/myapp/page?searchGenre=action&page=2`gibi bir URL 'de, URL 'nin `?searchGenre=action&page=2` bölümü sorgu dizesidir.)
> - `Request.Cookies` koleksiyon, tarayıcının gönderdiği tanımlama bilgilerine erişmenizi sağlar.
> 
> Gönderilen formda olduğunu bildiğiniz bir değer almak için `Request["name"]`kullanabilirsiniz. Alternatif olarak, `Request.Form["name"]` daha belirli sürümleri (`POST` istekleri için) veya `Request.QueryString["name"]` (`GET` istekleri için) kullanabilirsiniz. Kuşkusuz, *ad* alınacak öğenin adıdır.
> 
> Almak istediğiniz öğenin adı, kullanmakta olduğunuz koleksiyon içinde benzersiz olmalıdır. `Request` nesnesi, `Request.Form` ve `Request.QueryString`gibi alt kümeleri sağlar. Sayfanızın `userName` adlı bir form öğesi içerdiğini ve *ayrıca* `userName`adlı bir tanımlama bilgisi içerdiğini varsayalım. `Request["userName"]`alırsanız, form değerinin mi yoksa tanımlama bilgisinin mi olmasını istediğinize belirsizdir. Ancak, `Request.Form["userName"]` veya `Request.Cookie["userName"]`alırsanız hangi değerin alınacağı açıktır.
> 
> `Request.Form` veya `Request.QueryString`gibi ilgilendiğiniz `Request` alt kümesini kullanmak iyi bir uygulamadır. Bu öğreticide oluşturmakta olduğunuz basit sayfalar için büyük olasılıkla herhangi bir farklılık yapmaz. Ancak, daha karmaşık sayfalar oluştururken, açık sürüm `Request.Form` veya `Request.QueryString` kullanmak, sayfada form (veya birden çok form), tanımlama bilgileri, sorgu dizesi değerleri vb. içerdiğinde oluşabilecek sorunlardan kaçınmanıza yardımcı olabilir.

## <a name="creating-a-query-by-using-a-search-term"></a>Arama terimi kullanarak sorgu oluşturma

Artık kullanıcının girdiği arama teriminin nasıl alınacağını öğrenmiş olduğunuza göre, onu kullanan bir sorgu oluşturabilirsiniz. Tüm film öğelerini veritabanından almak için, bu ifadeye benzeyen bir SQL sorgusu kullandığınızı unutmayın:

`SELECT * FROM Movies`

Yalnızca belirli filmleri almak için, bir `Where` yan tümcesi içeren bir sorgu kullanmanız gerekir. Bu yan tümce, sorgu tarafından döndürülen satırları ayarlamanıza olanak sağlar. Örnek buradadır:

`SELECT * FROM Movies WHERE Genre = 'Action'`

Temel biçim `WHERE column = value`. `=`, `>` (büyüktür), `<` (küçüktür), `<>` (eşit değildir), `<=` (küçüktür veya eşittir), vb. gibi farklı işleçleri kullanabilirsiniz.

Merak ediyorsanız SQL deyimleri büyük/küçük harfe duyarlı değildir &mdash; `SELECT` `Select` (veya hatta `select`) aynıdır. Ancak insanlar, daha kolay okunmasını sağlamak için `SELECT` ve `WHERE`gibi bir SQL deyimindeki anahtar kelimeleri genellikle büyük harfle okur.

### <a name="passing-the-search-term-as-a-parameter"></a>Arama terimi parametre olarak geçiliyor

Belirli bir tarzı aramak yeterince kolay (`WHERE Genre = 'Action'`), ancak kullanıcının girdiği tarz için arama yapmak isteyebilirsiniz. Bunu yapmak için, Aranacak değer için bir yer tutucu içeren bir SQL sorgusu oluşturun. Bu komut şöyle görünür:

`SELECT * FROM Movies WHERE Genre = @0`

Yer tutucu, `@` karakteri ve ardından sıfırdır. Tahmin edebildiği gibi, bir sorgu birden fazla yer tutucu içerebilir ve `@0`, `@1`, `@2`vb. olarak adlandırırlar.

Sorguyu ayarlamak ve bunu gerçekten değeri geçirmek için, aşağıdaki gibi bir kod kullanın:

[!code-sql[Main](form-basics/samples/sample4.sql)]

Bu kod, kılavuzda verileri göstermek için yapmış olduğunuz verilere benzer. Tek farklar şunlardır:

- Sorgu bir yer tutucu (`WHERE Genre = @0"`) içeriyor.
- Sorgu bir değişkene konur (`selectCommand`); önce, sorguyu doğrudan `db.Query` yöntemine geçirtiniz.
- `db.Query` yöntemini çağırdığınızda, hem sorguyu hem de yer tutucu için kullanılacak değeri geçitirsiniz. (Sorguda birden fazla yer tutucu varsa, bunları yönteme ayrı değerler olarak geçirirsiniz.)

Tüm bu öğeleri birlikte yerleştirirseniz, aşağıdaki kodu alırsınız:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Önemli!** SQL komutuna değer geçirmek için yer tutucuları (`@0`gibi) kullanmak, güvenlik açısından *son derece önemlidir* . Burada gördüğünüz gibi, değişken veri yertutucuları ile birlikte SQL komutları oluşturmanız gereken tek yoldur.
> 
> Değişmez değer metin ve kullanıcıdan aldığınız değerleri birlikte koyarak bir SQL ifadesini hiçbir şekilde oluşturun. Kullanıcı girişini bir SQL ifadesine bitiştirme, sitenizi kötü niyetli bir kullanıcının sayfanıza bir değer gönderdiği bir *SQL ekleme saldırısında* açar. (MSDN Web sitesini [ekleme](https://msdn.microsoft.com/library/ms161953.aspx) başlıklı makalede daha fazla bilgi edinebilirsiniz.)

## <a name="updating-the-movies-page-with-search-code"></a>Filmler sayfasını arama koduyla güncelleştirme

Artık *film. cshtml* dosyasındaki kodu güncelleştirebilirsiniz. Başlamak için, sayfanın üst kısmındaki kod bloğundaki kodu şu kodla değiştirin:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

Buradaki fark, sorguyu daha sonra `db.Query` geçirilecek `selectCommand` değişkenine yerleştirmektir. SQL ifadesini bir değişkene koymak, aramayı gerçekleştirmek için yapmanız gereken ifadeyi değiştirmenize olanak sağlar.

Ayrıca, daha sonra geri yerleştirilecek bu iki satırı da kaldırmış olursunuz:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Sorguyu henüz çalıştırmak istemezsiniz (yani, `db.Query`çağırın) ve `WebGrid` yardımcısını henüz başlatmak istemezsiniz. Bu şeyleri, SQL deyimin çalıştırılacağı iletişime aldıktan sonra gerçekleştirirsiniz.

Bu yeniden yazan bloğundan sonra, aramayı işlemeye yönelik yeni mantığı ekleyebilirsiniz. Tamamlanan kod aşağıdaki gibi görünür. Sayfanızdaki kodu, bu örnekle eşleşecek şekilde güncelleştirin:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

Sayfa artık bunun gibi çalışmaktadır. Sayfa her çalıştığında, kod veritabanını açar ve `selectCommand` değişkeni, `Movies` tablosundan tüm kayıtları alan SQL ifadesine ayarlanır. Kod `searchTerm` değişkenini de başlatır.

Ancak, geçerli istek `searchGenre` öğesi için bir değer içeriyorsa, kod, `selectCommand` farklı bir sorguya (yani, bir tarz aramak için `Where` yan tümcesini içeren bir) ayarlar. Ayrıca, arama kutusu için geçirilmiş olarak `searchTerm` ayarlar (hiçbir şey olmayabilir).

`selectCommand`SQL deyiminizden bağımsız olarak, kod daha sonra sorguyu çalıştırmak için `db.Query` çağırır, bu da `searchTerm`herhangi bir şey geçiyor. `searchTerm`hiçbir şey yoksa, bu durum büyük değildir, çünkü bu durumda değeri `selectCommand` geçirilecek hiçbir parametre yoktur.

Son olarak, kod, daha önce olduğu gibi sorgu sonuçlarını kullanarak `WebGrid` yardımcısını başlatır.

SQL ifadesini ve arama terimini değişkenlere koyarak koda esneklik eklemişseniz bunu görebilirsiniz. Bu öğreticide daha sonra göreceğiniz gibi, bu temel çerçeveyi kullanabilir ve farklı arama türleri için mantık eklemeyi koruyabilirsiniz.

## <a name="testing-the-search-by-genre-feature"></a>Türe göre arama özelliğini test etme

WebMatrix 'te, *filmler. cshtml* sayfasını çalıştırın. Sayfayı tarz için metin kutusuyla görürsünüz.

Test kayıtlarınız için girmiş olduğunuz bir tarz girin ve **Ara**' ya tıklayın. Bu zaman, yalnızca bu tarz ile eşleşen filmlerle ilgili bir liste görürsünüz:

![' Comedies ' tarzı aranırken filmlere sayfa listeleme](form-basics/_static/image4.png)

Farklı bir tarz girin ve tekrar arama yapın. Aramanın büyük/küçük harfe duyarlı olmadığını görebilmeniz için tüm küçük harfleri veya tüm büyük harfleri kullanarak tarzı girmeyi deneyin.

## <a name="remembering-what-the-user-entered"></a>Kullanıcının girdiği "hatırlama"

Bir tarz girdikten ve **arama tarzında**tıklandıktan sonra, bu tarz için bir liste gördünüz. Ancak, arama metin kutusu boş &mdash; başka bir deyişle, ne girdiğinizi hatıraramamıştı.

Bu davranışın neden oluştuğunu anlamak önemlidir. Bir sayfa gönderdiğinizde, tarayıcı Web sunucusuna bir istek gönderir. ASP.NET isteği aldığında, sayfanın marka-yeni bir örneğini oluşturur, kod içinde çalıştırır ve sonra sayfayı tarayıcıda yeniden oluşturur. Aslında, sayfa yalnızca önceki bir sürümü ile çalıştıbildiğinizi bilmez. Tüm BT, içinde bazı form verileri bulunan bir istek olduğunu bilir.

İlk kez veya göndererek &mdash; her sayfa istediğinizde yeni bir sayfa alıyorsunuz &mdash;. Web sunucusunda son isteğiniz bellek yok. , ASP.NET yapmaz ve hiçbir ikisini de yapmaz. Sayfanın bu ayrı örnekleri arasındaki tek bağlantı, aralarında iletim yaptığınız herhangi bir veri olur. Örneğin, yeni sayfa örneği, bir sayfa gönderirseniz, önceki örnek tarafından gönderilen form verileri alabilir. (Sayfalar arasında veri geçirmenin diğer bir yolu tanımlama bilgilerini kullanmaktır.)

Bu durumu tanımlamanın resmi bir yolu, Web sayfalarının *durum bilgisiz*olduğu söydir. Web sunucuları ve sayfaları ve sayfadaki öğeler, sayfanın önceki durumu hakkında herhangi bir bilgi bulundurmaz. Web bu şekilde tasarlanmıştır çünkü bireysel isteklerin bakım durumu, genellikle binlerce, hatta yüzlerce binlerce istek (saniyede) işleyen Web sunucularının kaynaklarını hızla tüketti.

Bu nedenle metin kutusunun boş olması neden oldu. Sayfayı gönderdikten sonra, ASP.NET sayfanın yeni bir örneğini oluşturdu ve kod ve biçimlendirme üzerinden çalışır. Bu kodda, metin kutusuna bir değer ASP.NET söylenecek bir şey yok. Bu nedenle ASP.NET hiçbir şey yapmamıştı ve metin kutusu bu değerde bir değer olmadan işlenmiştir.

Bu sorunu geçici olarak yapmanın kolay bir yolu vardır. Metin *kutusuna girdiğiniz tarz, `Request.QueryString["searchGenre"]`* &mdash; kodda bulunabilir.

Metin kutusu için biçimlendirmeyi güncelleştirin, böylece `value` özniteliği, bu örnekte olduğu gibi `searchTerm`değerini alır:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

Bu sayfada Ayrıca, girmiş olduğunuz tarz de içerdiğinden `value` özniteliğini `searchTerm` değişkenine ayarlamış olabilirsiniz. Ancak, bu görevi gerçekleştirmenin standart yolu aşağıda gösterildiği gibi, `value` özniteliğini ayarlamak için `Request` nesnesini kullanmaktır. (Bu &mdash;, bazı durumlarda bile yapmak istediğiniz varsayılarak, bu sayfayı alanlarda değerler *olmadan* işlemek isteyebilirsiniz. Hepsi, uygulamanızla ilgili olan yeniliklere bağlıdır.)

> [!NOTE]
> Parolalar için kullanılan bir metin kutusunun değerini "hatırlayamıyorum". Bu, kullanıcıların kod kullanarak bir parola alanını doldurmasına izin veren bir güvenlik deliği olacaktır.

Sayfayı yeniden çalıştırın, bir tarz girin ve **tarz ara**' yı tıklatın. Bu süre yalnızca aramanın sonuçlarını görmemiş, ancak metin kutusu son kez girdiklerinizi anımsar:

![Metin kutusunun önceki girişin ' hatırlanan ' olduğunu gösteren sayfa](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Başlıktaki herhangi bir sözcük aranıyor

Artık herhangi bir tarz için arama yapabilirsiniz, ancak bir başlık aramak da isteyebilirsiniz. Arama yaptığınızda bir başlık tam olarak doğru bir şekilde almak zordur. bunun yerine başlık içinde herhangi bir yerde görünen bir sözcük arayabilirsiniz. SQL 'de bunu yapmak için, aşağıdaki gibi `LIKE` işlecini ve sözdizimini kullanın:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Bu komut, başlıkları "Adventure" içeren tüm filmleri alır. `LIKE` işlecini kullandığınızda, arama teriminin bir parçası olarak `%` joker karakterini dahil edersiniz. Arama `LIKE 'adventure%'` "Adventure ' ile başlayan" anlamına gelir. (Teknik olarak, "Adventure" dizesinin ardından herhangi bir şey olduğu anlamına gelir. ") Benzer şekilde, arama terimi `LIKE '%adventure'`, "Adventure ' ile biten" ve "Adventure ' ile biten" gibi başka bir yol olan "Adventure" dizesi tarafından izlenen bir şey anlamına gelir.

Bu nedenle `LIKE '%adventure%'` arama terimi, "Adventure" başlığında her yerde "Adventure" anlamına gelir. (Teknik olarak, başlıktaki her şey, ' Adventure ' ve ardından herhangi bir şey). ")

`<form>` öğesinin içinde, aşağıdaki biçimlendirmeyi, tarzı arama için sağ `</div>` etiketinin altına ekleyin (kapanış `</form>` öğesinden hemen önce):

[!code-html[Main](form-basics/samples/sample10.html)]

Bu aramayı işleme kodu, `LIKE` aramasını birleştirmek zorunda olmanız dışında, tarz arama koduna benzer. Sayfanın üst kısmındaki kod bloğunun içinde, bu `if` bloğunu, tarz araması için `if` bloğundan hemen sonra ekleyin:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Bu kod, daha önce gördüğünüz mantığı kullanır, ancak arama bir `LIKE` operatörü kullanır ve kod, arama teriminden önce ve sonra "`%`" koyar.

Sayfada başka bir aramanın nasıl daha kolay bir şekilde ekleneceğini fark edin. Yapmanız gerekdik:

- İlgili arama kutusunun bir değere sahip olup olmadığını görmek için test edilen bir `if` bloğu oluşturun.
- `selectCommand` değişkenini yeni bir SQL ifadesine ayarlayın.
- `searchTerm` değişkenini sorguya geçirilecek değere ayarlayın.

Aşağıda bir başlık araması için yeni mantığı içeren tüm kod bloğu verilmiştir:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Bu kodun ne işe yönelik bir özet aşağıda verilmiştir:

- `searchTerm` ve `selectCommand` değişkenleri en üstte başlatılır. Bu değişkenleri, kullanıcının sayfada ne yaptığını temel alarak uygun arama terimine (varsa) ve uygun SQL komutuna göre ayarlayacağız. Varsayılan arama, tüm filmlerden veritabanından alınması için basit bir durumdur.
- `searchGenre` ve `searchTitle`testlerinde, kod kümeleri `searchTerm` aramak istediğiniz değere ayarlanır. Bu kod blokları Ayrıca, bu arama için uygun bir SQL komutuna `selectCommand` de ayarlanır.
- `db.Query` yöntemi yalnızca bir kez çağrılır, her türlü SQL komutu `selectedCommand` ve `searchTerm`herhangi bir değer kullanılır. Arama terimi (tarz yok ve başlık sözcüğü yoksa) yoksa `searchTerm` değeri boş bir dizedir. Ancak, bu nedenle sorgu bir parametre gerektirmediğinden bu durum değildir.

## <a name="testing-the-title-search-feature"></a>Başlık arama özelliğini test etme

Artık tamamlanan arama sayfanızı test edebilirsiniz. *Filmleri. cshtml*'yi çalıştırın.

Bir tarz girin ve **Ara türe**tıklayın. Kılavuz, daha önce olduğu gibi bu tarzın filmlerini görüntüler.

Bir başlık sözcüğü girin ve **başlık ara**' yı tıklatın. Kılavuz, başlığında bu sözcüğe sahip olan filmleri görüntüler.

![Başlıkta ' The ' aranırken filmlere sayfa listeleme](form-basics/_static/image6.png)

Her iki metin kutusunu da boş bırakın ve düğmeye tıklayın. Kılavuzda tüm filmler görüntülenir.

## <a name="combining-the-queries"></a>Sorguları birleştirme

Gerçekleştirebileceğiniz aramaların dışlamalı olduğunu fark edebilirsiniz. Her iki arama kutusunda de değerler olsa bile başlık ve tarzda aynı anda arama yapamazsınız. Örneğin, başlığı "Adventure" içeren tüm eylem filmlerini araymıyorsunuz. (Sayfa şu anda kodlandığında, hem tarz hem de başlık için değer girerseniz, başlık araması önceliklidir.) Koşulları birleştiren bir arama oluşturmak için, aşağıdaki gibi bir sözdizimi içeren bir SQL sorgusu oluşturmanız gerekir:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

Ve aşağıdaki gibi bir ifade kullanarak (kabaca konuşulur) sorguyu çalıştırmanız gerekir:

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Birçok permütasyon arama ölçütünden izin vermek için mantık oluşturma, görebileceğiniz gibi bir bit dahil olabilir. Bu nedenle, burada duracağız.

## <a name="coming-up-next"></a>Sonraki adımda

Sonraki öğreticide, kullanıcıların veritabanına film eklemesine izin vermek için form kullanan bir sayfa oluşturacaksınız.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Film sayfası listesinin tamamını listeleme (aramayla güncelleştirildi)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](https://go.microsoft.com/fwlink/?LinkID=202890)
- W3Schools sitesinde [SQL WHERE yan tümcesi](http://www.w3schools.com/sql/sql_where.asp)
- W3C sitesindeki [Yöntem tanımları](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) makalesi

> [!div class="step-by-step"]
> [Önceki](displaying-data.md)
> [İleri](entering-data.md)
