---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: CRUD (oluşturma, okuma, güncelleştirme, silme) veri formu girişi desteği | Microsoft Docs
author: microsoft
description: 5\. adım, DinnersController sınıfınızı daha fazla alma, oluşturma ve bunları silme desteğini etkinleştirme konusunda nasıl yapılacağını gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580558"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>CRUD (Oluşturma, Okuma, Güncelleştirme, Silme) Veri Formu Giriş Desteği Sağlama

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) 5. adımıdır.
> 
> 5\. adım, DinnersController sınıfınızı daha fazla alma, oluşturma ve bunları silme desteğini etkinleştirme konusunda nasıl yapılacağını gösterir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>Nerdakşam yemeği 5. Adım: oluşturma, güncelleştirme, form senaryoları silme

Denetleyicileri ve görünümleri geliştirdik ve bunların site/ayrıntı deneyimi için nasıl kullanılacağını ele aldık. Sonraki adımınız, DinnersController sınıfınızı daha fazla almak ve ayrıca, bu da ile ilgili olarak düzenlemenizi, oluşturmayı ve silmeyi destekler.

### <a name="urls-handled-by-dinnerscontroller"></a>DinnersController tarafından işlenen URL 'Ler

Daha önce DinnersController 'e iki URL için destek uygulayan eylem yöntemleri ekledik: */Dıntik* ve */Dinners/details/[ID]* .

| **URL** | **Ü** | **Amaç** |
| --- | --- | --- |
| */Dinners/* | GET | Yaklaşan dinlerlerin HTML listesini görüntüleyin. |
| */Dinners/Details/[kimlik]* | GET | Belirli bir akşam yemeği hakkındaki ayrıntıları görüntüleyin. |

Şimdi üç ek URL uygulamak için eylem yöntemleri ekleyeceğiz: */Dinners/Edit/[ID]* , */Dinners/Create*ve */Dinners/delete/[ID]* . Bu URL 'Ler, var olan Dinlayıcıları düzenlemeyle, yeni yemek oluşturanlar ve Dinlayıcıları silmenin desteğini etkinleştirir.

Bu yeni URL 'Ler ile HTTP GET ve HTTP POST fiili etkileşimlerini destekliyoruz. Bu URL 'lere HTTP GET istekleri, verilerin ilk HTML görünümünü ("Düzenle", "Oluştur" durumunda boş bir form ve "Sil" durumunda bir silme onayı ekranı) görüntüler. Bu URL 'lere HTTP POST istekleri, DinnerRepository sitemizdeki (ve veritabanına) akşam yemeği verilerini kaydeder/güncelleştirir/siler.

| **URL** | **Ü** | **Amaç** |
| --- | --- | --- |
| */Dinners/Edit/[kimlik]* | GET | Akşam yemeği verileriyle doldurulmuş düzenlenebilir bir HTML formu görüntüleyin. |
| POST | Veritabanına belirli bir akşam yemeği için form değişikliklerini kaydedin. |
| */Dinners/Create* | GET | Kullanıcıların yeni Dinlayıcıları tanımlamasına olanak sağlayan boş bir HTML formu görüntüler. |
| POST | Yeni bir akşam yemeği oluşturun ve veritabanına kaydedin. |
| */Dinners/Delete/[kimlik]* | GET | Silme onayını görüntüleme ekranı. |
| POST | Belirtilen akşam yemeği veritabanından siler. |

### <a name="edit-support"></a>Desteği Düzenle

"Düzenle" senaryosunu uygulayarak başlayalım.

#### <a name="the-http-get-edit-action-method"></a>HTTP-GET düzenleme eylemi yöntemi

Düzenleme eylemi yönteminizin HTTP "GET" davranışını uygulayarak başlayacağız. Bu yöntem, */Dinners/Edit/[ID]* URL 'si istendiğinde çağrılacaktır. Uygulamamız şöyle görünür:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

Yukarıdaki kod, DinnerRepository kullanarak bir akşam yemeği nesnesi alır. Daha sonra akşam yemeği nesnesini kullanarak bir görünüm şablonu oluşturur. *Görüntüleme ()* yardımcı yöntemine açıkça bir şablon adı geçirdiğimiz için, görünüm şablonunu çözümlemek için kural tabanlı varsayılan yolu kullanır:/views/Dinners/Edit.aspx.

Şimdi bu görünüm şablonunu oluşturalım. Bunu, düzenleme yöntemi içinde sağ tıklayıp "Görünüm Ekle" bağlam menüsü komutunu seçerek yapacağız:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

"Görünüm Ekle" iletişim kutusunda, bir akşam yemeği nesnesini, model olarak görüntüleme şablonumuza geçirdiğimiz ve "düzenleme" şablonunu otomatik olarak yeniden oluşturma ' yı seçtiğimiz anlamına belirteceğiz.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

"Ekle" düğmesine tıkladığımızda, Visual Studio "\Views\dınanlar" dizininde bize yönelik yeni bir "Edit. aspx" görünüm şablonu dosyası ekler. Ayrıca, aşağıdaki gibi ilk "Düzenle" İskele uygulamasıyla doldurulan, kod Düzenleyicisi içindeki yeni "Düzenle. aspx" görünüm şablonunu açar:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

Varsayılan "Düzenle" scafkatı ' nin oluşturulması için birkaç değişiklik yapalim ve düzenleme görünümü şablonunu aşağıdaki içeriğe sahip olacak şekilde güncelleştirin (Bu, göstermek istediğimiz özelliklerden birkaçını kaldırır):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

Uygulamayı çalıştırdığımızda ve *"/Dinners/Edit/1"* URL 'sini isteytiğimiz zaman şu sayfayı görüyoruz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

Görünümümüzden üretilen HTML biçimlendirmesi aşağıdaki gibi görünür. "Save" &lt;Input Type = "Gönder"/&gt; düğmesi gönderildiğinde */Dinners/Edit/1* URL 'SINE http post gerçekleştiren bir &lt;form&gt; öğesi Ile standart HTML 'dir. Bir HTML &lt;giriş türü = "Text"/&gt; öğesi her düzenlenebilir özellik için çıktı:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>HTML. BeginForm () ve HTML. TextBox () HTML yardımcı yöntemleri

"Edit. aspx" görünüm şablonunuz birkaç "HTML Yardımcısı" yöntemini kullanıyor: HTML. ValidationSummary (), HTML. BeginForm (), HTML. TextBox () ve HTML. ValidationMessage (). Bu yardımcı yöntemler, bizim için HTML biçimlendirmesi oluşturmaya ek olarak yerleşik hata işleme ve doğrulama desteği sağlar.

##### <a name="htmlbeginform-helper-method"></a>HTML. BeginForm () yardımcı yöntemi

HTML. BeginForm () yardımcı yöntemi, biçimlendirme içindeki HTML &lt;form&gt; öğesi çıktı. Edit. aspx görünüm şablonumuza bu yöntemi kullanırken bir C# "Using" ifadesini uygulayacağız fark edeceksiniz. Açık süslü ayraç, &lt;form&gt; içeriğin başlangıcını gösterir ve sağ küme ayracı &lt;formu&gt; öğesinin sonunu belirtir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

Alternatif olarak, bunun gibi bir senaryo için doğal olmayan "Using" ifadesini görürseniz, bir HTML. BeginForm () ve HTML. EndForm () bileşimini kullanabilirsiniz (aynı şeyi yapar):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

HTML. BeginForm () parametresini parametre olmadan çağırmak, geçerli isteğin URL 'SI için HTTP-POST olan bir form öğesinin çıkışının oluşmasına neden olur. Bu nedenle, düzenleme görünümümüzde bir *&lt;form Action = "/Dinners/Edit/1" method = "Post"&gt;* öğesi oluşturulur. Farklı bir URL 'ye gönderi yapmak istiyorsam, alternatif olarak HTML. BeginForm 'a () açık parametreler geçiririz.

##### <a name="htmltextbox-helper-method"></a>HTML. TextBox () yardımcı yöntemi

Edit. aspx görünümümüzde, &lt;giriş türü = "Text"/&gt; öğelerinden çıkış yapmak için HTML. TextBox () yardımcı yöntemi kullanılır:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

Yukarıdaki HTML. TextBox () yöntemi tek bir parametre alır. &lt;giriş türü = "Text"/&gt; öğesi için ID/name özniteliklerini ve metin kutusu değerini doldurmak için model özelliğini belirtmek için kullanılır. Örneğin, düzenleme görünümüne geçirdiğimiz akşam yemeği nesnesi ".NET Futures" öğesinin bir "title" özelliği değerine sahipti ve bu nedenle HTML. TextBox ("title") yöntem çağrısı çıkışı: *&lt;giriş kimliği = "title" ad = "title" Type = "metin" değeri = ". NET Futures"/&gt;* .

Alternatif olarak, ilk HTML. TextBox () parametresini kullanarak öğenin kimliğini/adını belirtebilir ve ardından ikinci bir parametre olarak kullanılacak değerde açıkça geçiş yapabilirsiniz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

Genellikle çıktı olan değer üzerinde özel biçimlendirme gerçekleştirmek istiyoruz. String. Format () statik yöntemi bu senaryolar için yerleşik .NET ' tir. Edit. aspx görünüm şablonumuz, EventDate değerini (DateTime türünde olan) biçimlendirmek için bunu kullanarak sürenin saniye cinsinden gösterilmemesi için kullanılır:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

HTML. TextBox () için üçüncü bir parametre, isteğe bağlı olarak ek HTML özniteliklerinin çıkışını almak için kullanılabilir. Aşağıdaki kod parçacığı, ek bir boyut = "30" özniteliği ve bir Class = "mycssclass" özniteliğinin &lt;giriş türü = "metin"/&gt; öğesi üzerinde nasıl işleneceğini gösterir. "@" character because "sınıfı" kullanılarak sınıf özniteliğinin adının nasıl kaçışımız, içindeki C#ayrılmış bir anahtar sözcüktür.

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>HTTP-POST düzenleme eylem yöntemini uygulama

Şimdi düzenleme eylemi yönteminizin HTTP-Al sürümü uygulandı. Bir Kullanıcı */Dinners/Edit/1* URL 'sini istediğinde, aşağıdaki gıbı bir HTML sayfası alırlar:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

"Kaydet" düğmesine basıldığında form */Dinners/Edit/1* URL 'si için bir form göndermesine neden olur ve http post FIILINI kullanarak HTML &lt;girişi&gt; form değerlerini gönderir. Şimdi, bir akşam yemeği 'nin kaydedilmesini işleyecek olan düzenleme eylemi yönteminizin HTTP POST davranışını uygulayalim.

Bir "AcceptVerbs" özniteliği olan DinnersController için HTTP POST senaryolarını işlediğini belirten, daha fazla yüklenmiş bir "düzenleme" eylemi yöntemi ekleyerek başlayacağız:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

{AcceptVerbs] özniteliği aşırı yüklenmiş eylem yöntemlerine uygulandığında, ASP.NET MVC gelen HTTP fiiline bağlı olarak uygun eylem yöntemine gönderilen istekleri otomatik olarak işler. */Dinners/Edit/[ID]* URL 'LERINE http post Istekleri Yukarıdaki düzenleme yöntemine gider, ancak */Dinners/Edit/[ID]* URL 'lerine yönelik diğer http fiili Istekleri uyguladığımız ilk düzenleme yöntemine (`[AcceptVerbs]` özniteliği olmayan) gidecektir.

| **Kenar konusu: neden HTTP fiilleri farklılaştırsın?** |
| --- |
| Sorun: neden tek bir URL kullanıyorum ve HTTP fiili aracılığıyla davranışını farklılaştırıyor musunuz? Düzenleme değişikliklerini yüklemeyi ve kaydetmeyi işlemek için yalnızca iki ayrı URL 'Si yok mu? Örneğin:/Dinners/Edit/[ID] başlangıç formunu ve/Dinners/Save/[ID] öğesini kaydetmek için form gönderisini işleyecek şekilde görüntüleyin. İki ayrı URL yayımlamanın yanı sıra,/Dinners/Save/2 ' a gönderdiğimiz ve ardından bir giriş hatası nedeniyle HTML formunu yeniden görüntüleytiğimiz durumlarda Son Kullanıcı, tarayıcının adres çubuğunda (Bu URL 'nin gönderildiği URL olduğundan)/Dinners/Save/2 URL 'sini alacak. Son Kullanıcı bu sayfayı tarayıcı sık kullanılanlar listesine ekler veya URL 'YI kopyalayıp yapıştırır ve bir arkadaşınıza e-posta ile gönderirse, gelecekte çalışmayan bir URL 'YI kaydederek (Bu URL, post değerlerine bağlı olduğundan) sona acaktır. Tek bir URL 'YI (örneğin,/Dinners/Edit/[ID]) açarak ve işleme HTTP fiili tarafından farklılaştırarak, son kullanıcıların düzenleme sayfasına yer işareti koymak ve/veya URL 'YI başkalarına göndermek güvenlidir. |

#### <a name="retrieving-form-post-values"></a>Form Gönderi değerlerini alma

HTTP POST "düzenleme" yöntemimiz içindeki postalanan form parametrelerine erişebildiğimiz çeşitli yollar vardır. Tek bir basit yaklaşım, form koleksiyonuna erişmek ve gönderilen değerleri doğrudan almak için denetleyici temel sınıfındaki Request özelliğini kullanmaktır:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

Yukarıdaki yaklaşım biraz ayrıntılıdır, ancak özellikle hata işleme mantığı ekliyoruz.

Bu senaryoya daha iyi bir yaklaşım, denetleyici temel sınıfındaki yerleşik *UpdateModel ()* yardımcı yönteminden faydalanır. Bu, gelen form parametrelerini kullanarak geçirdiğimiz bir nesnenin özelliklerinin güncelleştirilmesini destekler. Nesne üzerindeki özellik adlarını belirlemede yansıma kullanır ve ardından, istemci tarafından gönderilen girdi değerlerine göre değerleri otomatik olarak dönüştürür ve bunlara atar.

Bu kodu kullanarak HTTP-POST düzenleme eyleminizi basitleştirmek için UpdateModel () yöntemini kullanabiliriz:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

Artık */Dinners/Edit/1* URL 'sini ziyaret edebiliyoruz ve akşam yemeği 'nin başlığını değiştirebiliriz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

"Kaydet" düğmesine tıkladığımızda, düzenleme eylemmize bir form gönderisi gerçekleştiririz ve güncelleştirilmiş değerler veritabanında kalıcı olacak. Bundan sonra akşam yemeği için Ayrıntılar URL 'sine yönlendirilecektir (yeni kaydedilen değerleri görüntüler):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>Düzenleme hatalarını işleme

Geçerli HTTP-POST uygulamamız, hatalar olduğu durumlar dışında iyi şekilde çalışıyor.

Bir Kullanıcı bir formu düzenlemede bir hata yaptığında, formu düzeltmeye yönelik bir bilgilendirici hata iletisiyle formun yeniden görüntülendiğinden emin olmanız gerekir. Bu, bir son kullanıcının yanlış giriş (örneğin, hatalı biçimlendirilmiş bir tarih dizesi) naklettiği ve giriş biçiminin geçerli olduğu, ancak bir iş kuralı ihlali olduğu durumlarda oluşan durumları içerir. Hata oluştuğunda form, kullanıcının yaptığı değişiklikleri el ile yeniden doldurmak zorunda kalmayacak şekilde, kullanıcının ilk girdiği giriş verilerini korumalıdır. Bu işlem, form başarıyla tamamlanana kadar gerektiği kadar yinelenir.

ASP.NET MVC, hata işleme ve form yeniden görüntüleme işlemlerini kolaylaştıran bazı iyi yerleşik özellikler içerir. Bu özellikleri, şu kodla düzenleme eylemi sitemizi güncelleştirelim ' de görmek için:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

Yukarıdaki kod, şimdi çalışmamıza bir try/catch hata işleme bloğunu sarmalıyoruz, ancak bu, önceki uygulamanıza benzer. UpdateModel () çağrılırken bir özel durum oluşursa veya DinnerRepository (bir özel durum oluşturacak ve kaydetmeye çalıştığınız akşam yemeği nesnesi modelimizin içindeki bir kural ihlali nedeniyle geçerli değilse) yürütme. Bunun içinde, akşam yemeği nesnesinde var olan tüm kural ihlallerinin üzerinde döngü gerçekleştirin ve bunları bir ModelState nesnesine (kısa süre içinde tartışacağız) ekleyin. Daha sonra görünümü yeniden görüntüyoruz.

Bu çalışma için uygulamayı yeniden çalıştırın, bir akşam yemeği düzenleyin ve boş bir başlığa, bir EventDate "yapay" adına sahip olacak şekilde değiştirin ve ABD ülke değeriyle Birleşik Krallık telefon numarası kullanın. "Kaydet" düğmesine bastığımızda, HTTP POST düzenleme yönteminiz akşam yemeği (hatalar nedeniyle) kaydedemeyecek ve formu yeniden görüntüleyeceğiz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

Uygulamamız bir hata deneyimine sahiptir. Geçersiz girişi olan metin öğeleri kırmızı renkle vurgulanır ve doğrulama hatası iletileri son kullanıcıya bunlarla ilgili olarak görüntülenir. Form Ayrıca kullanıcının ilk girdiği giriş verilerini de korur. böylece, herhangi bir şeyi yeniden doldurmak zorunda kalmazsınız.

Nasıl sorabilirsiniz, bu durum ortaya çıkabilir mi? Başlık, EventDate ve ContactPhone metin kutularının kendilerini kırmızıyla nasıl vurguladığına ve özgün olarak girilen Kullanıcı değerlerinin çıkışını nasıl anlayabilirim? En üstteki listede hata iletileri nasıl görüntüleniyor? İyi haber, bu bunun yerine, giriş doğrulama ve hata işleme senaryolarını kolay hale getirmek için yerleşik ASP.NET MVC özelliklerinden bazılarını kullandığımız için, bunun yerine Magic tarafından gerçekleşmiyordu.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>ModelState ve doğrulama HTML Yardımcısı yöntemlerini anlama

Denetleyici sınıfları, bir görünüme geçirilmekte olan bir model nesnesiyle ilgili hataların mevcut olduğunu belirtmek için bir yol sağlayan bir "ModelState" özellik koleksiyonuna sahiptir. ModelState koleksiyonundaki hata girdileri, sorun ile model özelliğinin adını (örneğin, "title", "EventDate" veya "ContactPhone") belirler ve insana kolay bir hata iletisi belirtilmesine izin verir (örneğin: "başlık gereklidir").

*UpdateModel ()* yardımcı yöntemi, model nesnesindeki özelliklere form değerleri atamaya çalışırken hata ile karşılaştığında otomatik olarak ModelState koleksiyonunu doldurur. Örneğin, akşam yemeği nesnenizin EventDate özelliği DateTime türündedir. UpdateModel () yöntemi, yukarıdaki senaryoda "yapay" dize değerini atayamamıştı. UpdateModel () yöntemi, bu özellik ile bir atama hatası oluştuğunu gösteren ModelState koleksiyonuna bir giriş ekledi.

Geliştiriciler, ModelState koleksiyonunu doğrudan "Catch" hata işleme bloğundan aşağıda yaptığımız gibi ModelState koleksiyonuna eklemek için de kod yazabilir ve bu, Akşam yemeği nesnesi:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>ModelState ile HTML Yardımcısı tümleştirmesi

HTML yardımcı yöntemleri-HTML. TextBox () gibi-çıktı işlenirken ModelState koleksiyonunu kontrol edin. Öğe için bir hata varsa, Kullanıcı tarafından girilen değeri ve bir CSS hata sınıfını işler.

Örneğin, "Düzenle" görünümümüzde, akşam yemeği nesnemizin EventDate öğesini işlemek için HTML. TextBox () yardımcı yöntemini kullanıyoruz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

Görünüm hata senaryosunda işlendiğinde, HTML. TextBox () yöntemi, akşam yemeği nesnenizin "EventDate" özelliği ile ilişkili herhangi bir hata olup olmadığını görmek için ModelState koleksiyonunu denetledi. Değer olarak gönderilen Kullanıcı girişini ("sahte") işlendiğinde bir hata olduğunu tespit edildiğinde ve &lt;giriş türü = "TextBox"/&gt; işaretleme için bir CSS hata sınıfı ekledi:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

CSS hatası sınıfının görünümünü, ancak istediğiniz gibi özelleştirebilirsiniz. Varsayılan CSS hata sınıfı – "giriş-doğrulama-hatası" – *\content\site.exe* stil sayfasında tanımlanmıştır ve aşağıdaki gibi görünür:

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

Bu CSS kuralı, geçersiz giriş öğelerimizin aşağıdaki gibi vurgulanmasının nedeni olan şeydir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>HTML. ValidationMessage () yardımcı yöntemi

HTML. ValidationMessage () yardımcı yöntemi, belirli bir model özelliği ile ilişkili ModelState hata iletisinin çıktısını almak için kullanılabilir:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

Yukarıdaki kod çıktıları: *&lt;span class = "alan-doğrulama-hatası"&gt; ' yapay ' değeri geçersiz&lt;/span&gt;*

HTML. ValidationMessage () yardımcı yöntemi, geliştiricilerin görüntülenen hata SMS iletisini geçersiz kılmasını sağlayan ikinci bir parametreyi de destekler:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

Yukarıdaki kod çıktıları: *&lt;span class = "alan-doğrulama-hatası"&gt;\** eventdate özelliği için bir hata mevcut olduğunda varsayılan hata metni yerine &lt;/span&gt;.

##### <a name="htmlvalidationsummary-helper-method"></a>HTML. ValidationSummary () yardımcı yöntemi

HTML. ValidationSummary () yardımcı yöntemi, ModelState koleksiyonundaki tüm ayrıntılı hata iletilerinin bir &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; listesi tarafından eşlik eden bir Özet hata iletisi oluşturmak için kullanılabilir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

HTML. ValidationSummary () yardımcı yöntemi, ayrıntılı hataların listesinin üstünde görüntülenecek bir Özet hata iletisi tanımlayan bir isteğe bağlı dize parametresi alır:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

İsteğe bağlı olarak, hata listesinin ne gibi göründüğünü geçersiz kılmak için CSS kullanabilirsiniz.

#### <a name="using-a-addruleviolations-helper-method"></a>Addruleihlalleri yardımcı yöntemi kullanma

İlk HTTP-POST düzenleme uygulamamız, bir catch bloğu içinde akşam yemeği nesnesinin kural Ihlallerinin üzerine döngüsü için bir foreach ifadesi kullandı ve bunları denetleyicinin ModelState koleksiyonuna ekler:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

Nerdakşam yemeği projesine bir "Controllerhelper" sınıfı ekleyerek ve bunun içinde ASP.NET MVC ModelStateDictionary sınıfına bir yardımcı yöntem ekleyen bir "Addruleihlalleri" genişletme yöntemi uygulayarak bu kodu küçük bir temizleyici hale getirebilirsiniz. Bu genişletme yöntemi, ModelStateDictionary öğesini Ruleihlal hatalarının bir listesiyle doldurmak için gereken mantığı kapsülleyebilirsiniz:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

Daha sonra, ModelState koleksiyonunu akşam yemeği kural Ihlalleri ile doldurmak için bu genişletme yöntemini kullanmak üzere HTTP-POST düzenleme eylem yönteminizi güncelleştirebiliriz.

#### <a name="complete-edit-action-method-implementations"></a>Eylem yöntemi uygulamalarını tamamen Düzenle

Aşağıdaki kod, düzenleme senaryomız için gereken tüm denetleyici mantığını uygular:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

Düzenleme uygulamamız hakkında iyi şeyler, denetleyici sınıfınız veya görünüm şablonumuz, akşam yemeği modelimiz tarafından zorlanan belirli doğrulama veya iş kuralları hakkında herhangi bir şeyi bilmelidir. Daha sonra modelinize ek kurallar ekleyebiliriz ve bunların desteklenmesi için denetleyicimizde veya görünümümüzde herhangi bir kod değişikliği yapmak zorunda değilsiniz. Bu, en az kod değişikliği ile gelecekte uygulama gereksinimlerimizi kolayca geliştirme esnekliği sağlar.

### <a name="create-support"></a>Destek oluştur

DinnersController sınıfımızın "düzenleme" davranışını uygulamayı tamamladık. Şimdi "Oluştur" desteğini uygulamaya geçelim. Bu, kullanıcıların yeni Dinlayıcıları eklemesine olanak tanır.

#### <a name="the-http-get-create-action-method"></a>HTTP-GET oluşturma eylemi yöntemi

Oluşturma eylemi yönteminizin HTTP "GET" davranışını uygulayarak başlayacağız. Bu yöntem, birisi */Dinners/Create* URL 'sini ziyaret ettiğinde çağrılacaktır. Uygulamamız şöyle görünür:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

Yukarıdaki kod yeni bir akşam yemeği nesnesi oluşturur ve EventDate özelliğini gelecekte bir hafta olacak şekilde atar. Daha sonra yeni akşam yemeği nesnesine dayalı bir görünüm oluşturur. *Görüntüleme ()* yardımcı yöntemine açıkça bir ad geçirdiğimiz için, görünüm şablonunu çözümlemek için kural tabanlı varsayılan yolu kullanır:/views/Dinners/Create.aspx.

Şimdi bu görünüm şablonunu oluşturalım. Bunu, oluşturma eylemi yöntemi içinde sağ tıklayıp "Görünüm Ekle" bağlam menüsü komutunu seçerek yapabiliriz. "Görünüm Ekle" iletişim kutusunda, bir akşam yemeği nesnesini görünüm şablonuna geçirdiğimiz ve "oluşturma" şablonunu otomatik olarak oluşturmayı tercih ettiğimiz belirteceğiz.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

"Ekle" düğmesine tıkladığımızda, Visual Studio "\Views\dıntik" dizinine yeni bir Scaffold tabanlı "Create. aspx" görünümü kaydeder ve IDE içinde açar:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Aşağıda, bizim için oluşturulan varsayılan "oluşturma" scafkatlama dosyasında birkaç değişiklik yapmam ve aşağıdaki gibi görünmesi için değiştirin:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

Bundan sonra uygulamamızı çalıştırdığımızda ve *"/Dinners/Create"* URL 'sine erişirken, Create ACTION uygulamamızda aşağıdaki gibi kullanıcı arabirimini işleyecek.

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>HTTP-POST oluşturma eylemi yöntemi uygulama

Oluşturma eylemi yönteminizin HTTP-GET sürümü uygulandı. Kullanıcı "Kaydet" düğmesine tıkladığında, */Dinners/Create* URL 'sine bir form gönderisini uygular ve http post FIILINI kullanarak HTML &lt;girişi&gt; form değerlerini gönderir.

Şimdi Create ACTION yönteminizin HTTP POST davranışını uygulayalim. Bir "AcceptVerbs" özniteliği olan DinnersController için HTTP POST senaryolarını işlediğini belirten, daha fazla yüklenmiş bir "Create" eylem yöntemi ekleyerek başlayacağız:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

HTTP-POST özellikli "Create" yöntemimiz içindeki postalanan form parametrelerine erişebildiğimiz çeşitli yollar vardır.

Bir yaklaşım, yeni bir akşam yemeği nesnesi oluşturmak ve ardından *UpdateModel ()* yardımcı yöntemini (düzenleme eylemiyle yaptığımız gibi) kullanarak, postalanan form değerleriyle doldurmaktır. Daha sonra bunu DinnerRepository 'e ekleyebiliriz, veritabanında kalıcı hale getirebiliyoruz ve aşağıdaki kodu kullanarak yeni oluşturulan akşam yemeği 'yi göstermek için kullanıcıyı Ayrıntılar eylemmize yönlendirebilir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

Alternatif olarak, Create () eylem yönteminizin bir yöntem parametresi olarak akşam yemeği nesnesini aldığı bir yaklaşım kullanabiliriz. ASP.NET MVC daha sonra otomatik olarak yeni bir akşam yemeği nesnesi oluşturacak, form girişlerini kullanarak özelliklerini dolduracaktır ve eylem yönteimize iletmektir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

Yukarıdaki eylem yönteminiz, bir akşam yemeği nesnesinin ModelState. IsValid özelliğini denetleyerek form post değerleriyle başarıyla doldurulduğunu doğrular. Bu, giriş dönüştürme sorunları varsa (örneğin, EventDate özelliği için "yapay" bir dize) ve eylem yöntemizdeki herhangi bir sorun varsa, formu yeniden görüntülediğinde false döndürür.

Giriş değerleri geçerliyse, eylem yöntemi yeni akşam yemeği 'ni eklemeye ve DinnerRepository 'e kaydetmeye çalışır. Bu çalışmayı bir try/catch bloğu içinde kaydırır ve herhangi bir iş kuralı ihlali varsa (bir özel durum oluşturmak için dinnerRepository. Save () yönteminin oluşmasına neden olacak) formu yeniden görüntüler.

Bu hata işleme davranışını eylemde görmek için, */Dinners/Create* URL 'sini isteyebiliriz ve yeni bir akşam yemeği hakkındaki ayrıntıları dolduracağız. Yanlış giriş veya değerler, oluşturma formunun aşağıdaki gibi vurgulanan hatalarla yeniden görüntülenmesine neden olur:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

Oluşturma formumuza, düzenleme formumuzdan aynı doğrulama ve iş kurallarını nasıl sunduğuna dikkat edin. Bunun nedeni, doğrulama ve iş kurallarımızın modelde tanımlanması ve uygulamanın kullanıcı arabirimi ya da denetleyicisi içinde katıştırılmasından kaynaklanır. Bu, daha sonra doğrulama veya iş kurallarımızı tek bir yerde değiştirebiliyoruz/geliştirebilir ve uygulamamız genelinde uygulanabileceksiniz. Var olan yeni kuralları veya değişiklikleri otomatik olarak kabul etmek için düzenleme veya oluşturma eylemi yöntemlerimizin içindeki herhangi bir kodu değiştirmek zorunda değilsiniz.

Giriş değerlerini düzeltireceğimizde ve "Kaydet" düğmesine tıkladığınızda, DinnerRepository ekleme işlemi başarılı olur ve veritabanına yeni bir akşam yemeği eklenecektir. Daha sonra, yeni oluşturulan akşam yemeği hakkındaki ayrıntılarla sunulacak olan */Dinners/details/[ID]* URL 'sine yönlendirilirsiniz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Desteği Sil

Şimdi DinnersController ' ye "Sil" desteği ekleyelim.

#### <a name="the-http-get-delete-action-method"></a>HTTP-GET silme eylemi yöntemi

Silme eylemi yönteminizin HTTP GET davranışını uygulayarak başlayacağız. Bu yöntem, birisi */Dinners/delete/[ID]* URL 'sini ziyaret ettiğinde çağırılır. Uygulama aşağıda verilmiştir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

Eylem yöntemi, silinecek akşam yemeği 'ni almaya çalışır. Akşam yemeği varsa akşam yemeği nesnesine göre bir görünüm oluşturur. Nesne yoksa (veya zaten silinmişse), daha önce "Ayrıntılar" eylem yöntemi için oluşturduğumuz "NotFound" görünüm şablonunu işleyen bir görünüm döndürür.

"Sil" görünüm şablonunu, silme eylemi yöntemi içinde sağ tıklayıp "Görünüm Ekle" bağlam menüsü komutunu seçerek oluşturuyoruz. "Görünüm Ekle" iletişim kutusunda, bir akşam yemeği nesnesini, modeli olarak görüntüleme şablonumuza geçirdiğimiz ve boş bir şablon oluşturmayı seçtiğimiz belirteceğiz:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

"Ekle" düğmesine tıkladığımızda, Visual Studio "\Views\dıntik" dizininiz dahilinde bize yönelik yeni bir "delete. aspx" görünüm şablonu dosyası ekler. Aşağıdaki gibi bir silme onayı ekranı uygulamak için şablona bazı HTML ve kod ekleyeceğiz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

Yukarıdaki kod, silinecek akşam yemeği 'nin başlığını görüntüler ve son kullanıcı onun içindeki "Sil" düğmesine tıkladığında,/Dinners/Delete/[ID] URL 'sine GÖNDERI yapan bir &lt;form&gt; öğesi verir.

Uygulamamızı çalıştırdığımızda ve geçerli bir akşam yemeği nesnesi için *"/Dinners/delete/[ID]"* URL 'sine erişirken, aşağıdaki gibi kullanıcı arabirimini işler:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **Kenar konusu: neden bir GÖNDERI yapıyoruz?** |
| --- |
| Sorun, neden silme onayı ekranımızda&gt; &lt;formu oluşturma çabasında gitemiz? Gerçek silme işlemini yapan bir eylem yöntemine bağlanmak için neden yalnızca standart köprü kullanılmalı? Bunun nedeni, URL 'lerimizi bulan web gezginlerine ve arama altyapılarımıza karşı koruma konusunda dikkatli olmak istiyoruz ve bağlantıları izlediklerinde verilerin silinmesine neden oluyordu. HTTP-GET tabanlı URL 'Ler, bunlara erişim/gezinme için "güvenli" olarak değerlendirilir ve HTTP-POST ' ı takip edilmemelidir. HTTP-POST isteklerinin arkasında bozucu veya veri değiştirme işlemlerini her zaman yerleştirdiğinizden emin olmak iyi bir kuraldır. |

#### <a name="implementing-the-http-post-delete-action-method"></a>HTTP-POST silme eylemini uygulama yöntemi

Artık bir silme onayı ekranını görüntüleyen, silme eylemi yönteminizin uygulandığı HTTP-Al sürümüne sahipsiniz. Son Kullanıcı "Sil" düğmesine tıkladığında, */Dinners/Dinner/[ID]* URL 'si için bir form gönderisini yapar.

Şimdi aşağıdaki kodu kullanarak silme eylemi yönteminin HTTP "POST" davranışını uygulayalim:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

Silme eylemi yönteminizin HTTP-POST sürümü, silinecek akşam yemeği nesnesini almaya çalışır. Bulamazsa, "NotFound" şablonumuzu işler. Akşam yemeği bulunursa, DinnerRepository öğesinden siler. Daha sonra bir "silinmiş" şablon oluşturur.

"Silinen" şablonu uygulamak için eylem yöntemine sağ tıklayıp "Görünüm Ekle" bağlam menüsünü seçmeniz gerekir. "Silinmiş" görünümümüzü adlandıracağız ve boş bir şablon (ve kesin türü belirtilmiş bir model nesnesi almaz) olacaktır. Daha sonra buna bir HTML içeriği ekleyeceğiz:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

Şimdi uygulamamızı çalıştırdığımızda ve geçerli bir akşam yemeği nesnesi için *"/Dinners/delete/[ID]"* URL 'sine erişirken, aşağıdaki gibi akşam yemeği silme onayı ekranımızı işleyecek:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

"Sil" düğmesine tıkladığımızda, */Dinners/delete/[ID]* URL 'SINE bir HTTP-POST işlemi gerçekleştirecek ve bu, veritabanımızdan akşam yemeği silinecek ve "silinen" görünüm şablonumuzu görüntüleyecektir:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>Model bağlama güvenliği

ASP.NET MVC 'nin yerleşik model bağlama özelliklerini kullanmanın iki farklı yolunu tartıştık. İlk olarak, var olan bir model nesnesindeki özellikleri güncellemek için UpdateModel () yöntemi ve ikincisi, ASP.NET MVC 'nin model nesnelerini eylem yöntemi parametresi olarak geçirme desteğini kullanarak kullanın. Bu tekniklerin her ikisi de çok güçlü ve son derece yararlı olur.

Bu güç, BT sorumluluğu da sunar. Herhangi bir kullanıcı girişi kabul edilirken her zaman güvenlik hakkında her zaman bir bilgi olması önemlidir ve bu da nesneleri form girişine bağlarken de geçerlidir. HTML ve JavaScript ekleme saldırılarına karşı, her zaman bir HTML kodlamasına dikkat etmeniz ve SQL ekleme saldırılarına karşı dikkatli olmanız gerekir (Note: uygulamamız için LINQ to SQL kullanıyoruz ve bu sayede bunları önlemek için parametreleri otomatik olarak kodlar saldırı türleri). Hiçbir zaman istemci tarafı doğrulamaya güvenmelisiniz ve size sahte değerler gönderilmeye çalışan korsanlara karşı koruma için her zaman sunucu tarafı doğrulama kullanın.

ASP.NET MVC 'nin bağlama özelliklerini kullanmanın, bağladığınız nesnelerin kapsamı olduğunu düşündüğünüzden emin olmak için bir ek güvenlik öğesi. Özellikle, bağlanmasına izin verdiğiniz özelliklerin güvenlik etkilerine ilişkin etkilerini anladığınızdan emin olmak ve yalnızca son kullanıcı tarafından güncelleştirilemeyen özelliklerin yalnızca gerçekten güncelleştirilmesini sağlamak için emin olmanız gerekir.

Varsayılan olarak, UpdateModel () yöntemi, model nesnesindeki, gelen form parametre değerleriyle eşleşen tüm özellikleri güncelleştirmeye çalışır. Benzer şekilde, eylem yöntemi parametreleri olarak geçirilen nesneler, varsayılan olarak, form parametreleri aracılığıyla ayarlanmış tüm özelliklerine sahip olabilir.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>Bağlamayı kullanım bazında kilitleme

Güncelleştirilebilen özelliklerin açık bir "dahil listesini" sağlayarak, bağlama ilkesini kullanım başına bir şekilde kilitleyebilir. Bu, aşağıdaki gibi UpdateModel () yöntemine fazladan bir dize dizisi parametresi geçirilerek yapılabilir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

Eylem yöntemi parametreleri olarak geçirilen nesneler, aşağıda gösterildiği gibi, izin verilen özelliklerin "içerme listesini" sağlayan bir [bind] özniteliğini de destekler:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>Bir tür temelinde bağlamayı kilitleme

Ayrıca, bağlama kurallarını bir tür temelinde de kilitlersiniz. Bu, bağlama kurallarını bir kez belirtmenizi sağlar ve sonra tüm denetleyiciler ve eylem yöntemleri genelinde tüm senaryolarda (UpdateModel ve eylem yöntemi parametre senaryoları dahil) uygulanmasını sağlar.

Türe bir [bind] özniteliği ekleyerek veya bunu uygulamanın Global. asax dosyasına kaydederek tür başına bağlama kurallarını özelleştirebilirsiniz (türü sahip olmadığınız senaryolar için yararlıdır). Daha sonra, belirli bir sınıf veya arabirim için hangi özelliklerin bağlanabilir olduğunu denetlemek için bağlama özniteliğinin Içerme ve dışlama özelliklerini kullanabilirsiniz.

Nerdakşam yemeği uygulamamızda akşam yemeği sınıfı için bu tekniği kullanacağız ve bağlanabilir Özellikler listesini şu şekilde sınırlandıran bir [bind] özniteliği ekleyin:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

RSVPs koleksiyonunun bağlama yoluyla yükseltilmesine izin vermedik, ya da DinnerID veya HostedBy özelliklerinin bağlama yoluyla ayarlanmalarına izin verdik. Bunun yerine, yalnızca eylem yöntemlerimiz içinde açık kod kullanarak bu belirli özellikleri kullanacağız.

### <a name="crud-wrap-up"></a>CRUD kaydırması

ASP.NET MVC, form gönderme senaryolarını uygulamaya yardımcı olan çeşitli yerleşik özellikler içerir. DinnerRepository en üstünde CRUD UI desteği sağlamak için bu özelliklerden birini kullandık.

Uygulamamızı uygulamak için model odaklı bir yaklaşım kullandık. Bu, tüm doğrulama ve iş kuralı mantığımız model katmanımızda tanımlanmış ve denetleyicilerimizin veya görünümlerimiz dahilinde olmadığı anlamına gelir. Denetleyici sınıfınız veya görüntüleme şablonlarımız, akşam yemeği model sınıfımız tarafından zorlanan belirli iş kuralları hakkında herhangi bir şey bilmez.

Bu, uygulama mimarimizi temizleyecektir ve test etmek daha kolay hale getirir. Daha sonra model katmanımız daha fazla iş kuralı ekleyebiliriz ve bunların desteklenmesi için Denetleyicimizde veya görünümümüzde *herhangi bir kod değişikliği yapmak zorunda değilsiniz* . Bu, gelecekte uygulamamızı geliştikçe ve değiştirebilmeniz için harika bir çeviklik sunmamıza olanak sağlıyor.

DinnersController şimdi akşam yemeği listelerinin/ayrıntılarının yanı sıra destek oluşturma, düzenleme ve silme desteği sunar. Sınıf için kodun tamamı aşağıda bulunabilir:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>Sonraki adım

Artık temel CRUD (oluşturma, okuma, güncelleştirme ve silme) desteği, DinnersController sınıfımızın içinde uygulanır.

Artık formlarımızda daha zengin Kullanıcı arabirimi sağlamak için ViewData ve ViewModel sınıflarını nasıl kullanabileceğimizi inceleyelim.

> [!div class="step-by-step"]
> [Önceki](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [İleri](use-viewdata-and-implement-viewmodel-classes.md)
