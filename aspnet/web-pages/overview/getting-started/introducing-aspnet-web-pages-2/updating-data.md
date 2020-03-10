---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: ASP.NET Web sayfalarına giriş-veritabanı verilerini güncelleştirme | Microsoft Docs
author: Rick-Anderson
description: Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda var olan bir veritabanı girişini güncelleştirme (değiştirme) gösterilmektedir. Seriyi tamamladığınız varsayılır...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 8f8bcfb7d9d2416a2699776cadbdaae8e12415ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574230"
---
# <a name="introducing-aspnet-web-pages---updating-database-data"></a>ASP.NET Web sayfalarına giriş-veritabanı verilerini güncelleştirme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Bu öğreticide, ASP.NET Web Pages (Razor) kullandığınızda var olan bir veritabanı girişini güncelleştirme (değiştirme) gösterilmektedir. [ASP.NET Web sayfalarını kullanarak formları kullanarak seriyi, verileri girerek](entering-data.md)tamamlamış olduğunu varsayar.
> 
> Öğrenecekleriniz:
> 
> - `WebGrid` Yardımcısı 'nda tek bir kayıt seçme.
> - Veritabanından tek bir kayıt okuma.
> - Veritabanı kaydındaki değerlerle bir formu önceden yükleme.
> - Veritabanında var olan bir kaydı güncelleştirme.
> - Bilgiyi sayfada görüntülemeden depolama.
> - Bilgileri depolamak için gizli bir alan kullanma.
>   
> 
> Ele alınan özellikler/teknolojiler:
> 
> - `WebGrid` Yardımcısı.
> - SQL `Update` komutu.
> - `Database.Execute` yöntemi.
> - Gizli alanlar (`<input type="hidden">`).

## <a name="what-youll-build"></a>Ne oluşturacağız?

Önceki öğreticide, bir veritabanına kayıt eklemeyi öğrendiniz. Burada, bir kaydın düzenlenmek üzere nasıl görüntüleneceği hakkında bilgi edineceksiniz. *Filmler* sayfasında, her filmin yanında bir **düzenleme** bağlantısı görüntüleyecek şekilde `WebGrid` Yardımcısı 'nı güncelleştireceksiniz:

![Her film için ' düzenleme ' bağlantısı dahil olmak üzere WebGrid görüntüsü](updating-data/_static/image1.png)

**Düzenleme** bağlantısına tıkladığınızda, sizi film bilgisinin zaten bir biçimde olduğu farklı bir sayfaya götürür:

![Düzenlenecek filmi gösteren film sayfasını düzenleme](updating-data/_static/image2.png)

Değerlerden herhangi birini değiştirebilirsiniz. Değişiklikleri gönderdiğinizde, sayfadaki kod veritabanını güncelleştirir ve sizi film listesine geri götürür.

İşlemin bu bölümü, önceki öğreticide oluşturduğunuz *Addmovie. cshtml* sayfası gibi neredeyse tam olarak çalışır, bu nedenle Bu öğreticinin çoğu tanıdık gelecektir.

Tek bir filmi düzenlemek için bir yol uygulayabileceğiniz çeşitli yollar vardır. Gösterilen yaklaşım, kolayca uygulanması ve anlaşılması kolay olduğundan, seçilir.

## <a name="adding-an-edit-link-to-the-movie-listing"></a>Film listesine düzenleme bağlantısı ekleme

Başlamak için, *filmler* sayfasını her bir film listesinin de bir **düzenleme** bağlantısı içermesi için güncelleştireceksiniz.

*Filmler. cshtml* dosyasını açın.

Sayfanın gövdesinde, `WebGrid` işaretlemesini bir sütun ekleyerek değiştirin. Değiştirilen biçimlendirme şu şekildedir:

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

Yeni sütun budur:

[!code-html[Main](updating-data/samples/sample2.html)]

Bu sütunun noktası, metni "Düzenle" olan bir bağlantı (`<a>` öğesi) göstermek içindir. Ne yaptığımız, sayfa çalıştırıldığında aşağıdaki gibi görünen bir bağlantı oluşturmaktır, her film için `id` değeri farklıdır:

[!code-css[Main](updating-data/samples/sample3.css)]

Bu bağlantı, *Editmovie*adlı bir sayfayı çağırır ve sorgu dizesi `?id=7` bu sayfaya geçilecektir.

Yeni sütunun sözdizimi bir bit karmaşık görünebilir, ancak bu yalnızca birkaç öğe yerleştirdiğinden geçerlidir. Her bireysel öğe basittir. Yalnızca `<a>` öğesi üzerinde odaklandıysanız şu biçimlendirmeyi görürsünüz:

[!code-html[Main](updating-data/samples/sample4.html)]

Kılavuzun nasıl çalıştığı hakkında bazı arka plan: kılavuz, her veritabanı kaydı için bir tane olmak üzere satırları görüntüler ve veritabanı kaydındaki her bir alan için sütunları görüntüler. Her kılavuz satırı oluşturulurken, `item` nesnesi bu satırın veritabanı kaydını (öğe) içerir. Bu düzenleme, bu satır için verilere ulaşmak üzere kodda bir yol sağlar. Burada gördüğünüz gibi: ifadesi `item.ID` geçerli veritabanı öğesinin KIMLIK değerini alıyor. Veritabanı değerlerinden (başlık, tarz veya yıl) herhangi birini, `item.Title`, `item.Genre`veya `item.Year`kullanarak aynı şekilde alabilirsiniz.

İfade `"~/EditMovie?id=@item.ID` hedef URL 'nin (`~/EditMovie?id=`) sabit kodlanmış bölümünü bu dinamik olarak türetilen KIMLIKLE birleştirir. (`~` işlecini önceki öğreticide gördünüz; bu, geçerli Web sitesi kökünü temsil eden bir ASP.NET işleçtir.)

Sonuç olarak sütundaki biçimlendirmenin bu bölümü, çalışma zamanında aşağıdaki biçimlendirme gibi bir şey üretir:

[!code-xml[Main](updating-data/samples/sample5.xml)]

Doğal olarak, `id` gerçek değeri her satır için farklı olacaktır.

## <a name="creating-a-custom-display-for-a-grid-column"></a>Kılavuz sütunu için özel görüntü oluşturma

Şimdi kılavuz sütununa geri dönün. Başlangıçta kılavuzda bulunan üç sütun yalnızca veri değerlerini (başlık, tarz ve yıl) görüntüdi. Bu ekranı, veritabanı sütununun adını geçirerek belirttiniz &mdash; Örneğin, `grid.Column("Title")`.

Bu yeni **düzenleme** bağlantısı sütunu farklı. Bir sütun adı belirtmek yerine bir `format` parametresi geçiriyoruz. Bu parametre, `WebGrid` Yardımcısı 'nın, sütun verilerini kalın veya yeşil ya da istediğiniz biçimde görüntülemek için `item` değeriyle birlikte işleneceğini belirten biçimlendirme tanımlamanızı sağlar. Örneğin, başlığın kalın görünmesini isterseniz, aşağıdaki örnekte olduğu gibi bir sütun oluşturabilirsiniz:

[!code-html[Main](updating-data/samples/sample6.html)]

(`format` özelliğinde gördüğünüz çeşitli `@` karakterleri, biçimlendirme ve bir kod değeri arasındaki geçişi işaret ediyor.)

`format` özelliği hakkında bilgi aldıktan sonra, yeni **düzenleme** bağlantısı sütununun nasıl bir araya yerleştirileceğini anlamak daha kolay olur:

[!code-html[Main](updating-data/samples/sample7.html)]

Sütun *yalnızca* bağlantıyı işleyen biçimlendirmeyi ve satırın veritabanı kaydından ayıklanan bazı BILGILERI (kimliği) içerir.

> [!TIP]
> 
> **Bir yöntem için adlandırılmış parametreler ve Konumsal parametreler**
> 
> Bir yöntemi çağırdığınızda ve ona parametreler geçirdiyseniz, parametre değerleri yalnızca virgülle ayrılmış olarak listelenir. İşte birkaç örnek:
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> Bu kodu ilk kez gördüğünüzde bu sorunla karşılaşmadınız, ancak her durumda, parametreleri belirli bir sırada yöntemlere geçirdiniz &mdash; Bu yöntemde parametrelerin tanımlandığı sıra. `db.Execute` ve `Validation.RequireFields`için, geçirdiğiniz değerlerin sırasını karıştırdıysanız, sayfa çalıştırıldığında bir hata mesajı veya en az bir garip sonuç elde edersiniz. Açık olarak, içindeki parametrelerin iletilmesi sırasını bilmeniz gerekir. (WebMatrix 'te IntelliSense, parametrelerin adını, türünü ve sırasını öğrenmenize yardımcı olabilir.)
> 
> Değerleri sırasıyla geçirme alternatifi olarak *adlandırılmış parametreleri*kullanabilirsiniz. (Parametreleri sırayla geçirme, *Konumsal parametreler*kullanma olarak bilinir.) Adlandırılmış parametreler için, değerini geçirirken parametrenin adını açıkça dahil edersiniz. Adlandırılmış parametreleri bu öğreticilerde zaten birkaç kez kullandınız. Örneğin:
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> and
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> Adlandırılmış parametreler, özellikle bir yöntem birçok parametre alırsa, birkaç durum için kullanışlıdır. Bunlardan biri yalnızca bir veya iki parametre geçirmek istediğinizde, ancak geçirmek istediğiniz değerler parametre listesindeki ilk konumlar arasında değil. Diğer bir durum ise, parametreleri en anlamlı hale getiren sırada, kodunuzu daha okunaklı hale getirmek istediğinizde olur.
> 
> Kuşkusuz, adlandırılmış parametreleri kullanmak için parametrelerin adlarını bilmeniz gerekir. WebMatrix IntelliSense, adları *gösterebilir* , ancak şu anda bunları sizin için dolduramaz.

## <a name="creating-the-edit-page"></a>Düzenleme sayfası oluşturma

Şimdi *Editmovie* sayfasını oluşturabilirsiniz. Kullanıcılar **düzenleme** bağlantısına tıkladıklarında bu sayfada sona abileceksiniz.

*Editmovie. cshtml* adlı bir sayfa oluşturun ve dosyadaki nelerin aşağıdaki biçimlendirmeyle değiştirin:

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

Bu biçimlendirme ve kod, *Addmovie* sayfasında sahip olduğunuz şekilde benzerdir. Gönder düğmesinin metninde küçük bir fark vardır. *Addmovie* sayfasında olduğu gibi, varsa doğrulama hatalarını görüntüleyen bir `Html.ValidationSummary` çağrısı vardır. Bu süre, doğrulama özetinde hatalar görüntüleneceği için `Validation.Message`çağrıları terk ettik. Önceki öğreticide belirtildiği gibi, çeşitli birleşimlerde doğrulama özetini ve bireysel hata iletilerini kullanabilirsiniz.

`<form>` öğesinin `method` özniteliği `post`olarak ayarlandığını unutmayın. *Addmovie. cshtml* sayfasında olduğu gibi, Bu sayfa veritabanında değişiklikler yapar. Bu nedenle, bu form `POST` bir işlem gerçekleştirmelidir. (`GET` ve `POST` işlemleri arasındaki fark hakkında daha fazla bilgi için, HTML formlarında öğreticideki [Get, post ve http fiil güvenliği](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) kenar çubuğu bölümüne bakın.)

Önceki bir öğreticide gördüğünüz gibi, metin kutularının `value` öznitelikleri, bunları önceden yüklemek için Razor kodu ile ayarlanır. Bu kez, `Request.Form["title"]`yerine bu görev için `title` ve `genre` gibi değişkenler kullanıyorsunuz:

`<input type="text" name="title" value="@title" />`

Daha önce olduğu gibi, bu biçimlendirme metin kutusu değerlerini film değerleriyle önyüklenir. `Request` nesnesini kullanmak yerine, bu kez değişkenlerin nasıl kullanılacağı konusunda bir süre daha görürsünüz.

Bu sayfada Ayrıca bir `<input type="hidden">` öğesi vardır. Bu öğe, film KIMLIĞINI sayfada görünür yapmadan depolar. KIMLIK, başlangıçta bir sorgu dizesi değeri (`?id=7` veya URL 'de benzer) kullanılarak sayfaya geçirilir. KIMLIK değerini gizli bir alana yerleştirerek, sayfanın ile birlikte çağrılan özgün URL 'ye artık erişemese de, form gönderildiğinde kullanılabilir olduğundan emin olabilirsiniz.

*Addmovie* sayfasının aksine, *editmovie* sayfasının kodu iki ayrı işleve sahiptir. İlk işlev, sayfa ilk kez görüntülenirken (ve *yalnızca* ), kod sorgu DIZESINDEN film kimliğini alır. Kod daha sonra KIMLIĞI, ilgili filmi veritabanından okumak ve metin kutularında (Önyükle) göstermek için kullanır.

İkinci işlev, Kullanıcı **Değişiklikleri Gönder** düğmesine tıkladığında, kodun metin kutularının değerlerini okuması ve doğrulanması gerekir. Bu kodun Ayrıca, veritabanı öğesini yeni değerlerle güncelleştirmesi gerekir. Bu teknik, *Addfilmi*gördüğünüz gibi bir kayıt eklemeye benzer.

## <a name="adding-code-to-read-a-single-movie"></a>Tek bir filmi okumak için kod ekleme

İlk işlevi gerçekleştirmek için, bu kodu sayfanın en üstüne ekleyin:

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

Bu kodun çoğu `if(!IsPost)`başlayan bir bloğun içindedir. `!` işleci "Not" anlamına gelir; bu nedenle ifade, bu isteğin *Bu sayfa çalıştırıldığında ilk kez bu isteğin çalıştırılmasının*dolaylı bir yolu olan *gönderi gönderimi olmadığı*anlamına gelir. Daha önce belirtildiği gibi, bu kod *yalnızca* sayfanın ilk kez çalıştırılması gerekir. Kodu `if(!IsPost)`içine almadıysanız, sayfa her çağrıldığında, bir düğmeye ilk kez veya yanıt olarak bir düğme tıklamadığınız her seferinde çalıştırılır.

Kodun bu kez `else` bloğunu içerdiğine dikkat edin. `if` blokları tanıdığımızda söylediğimiz gibi, bazen test ettiğiniz koşul doğru değilse alternatif kodu çalıştırmak istersiniz. Burada bu durum söz konusu şekildedir. Koşul geçerse (yani, sayfaya geçirilen KIMLIĞI tamam ise), veritabanından bir satır okur. Ancak, koşul geçmezse `else` bloğu çalışır ve kod bir hata mesajı ayarlar.

## <a name="validating-a-value-passed-to-the-page"></a>Sayfaya geçirilen bir değer doğrulanıyor

Kod, sayfaya geçirilen KIMLIĞI almak için `Request.QueryString["id"]` kullanır. Kod, KIMLIK için bir değerin gerçekten geçirildiğinden emin olmanızı sağlar. Değer geçirilmemişse, kod bir doğrulama hatası ayarlar.

Bu kod, bilgileri doğrulamak için farklı bir yol gösterir. Önceki öğreticide `Validation` Yardımcısı ile çalıştık. Doğrulanacak alanları kaydettiniz ve ASP.NET `Html.ValidationMessage` ve `Html.ValidationSummary`kullanarak doğrulama ve görüntülenme hatalarını otomatik olarak yaptınız. Ancak, bu durumda Kullanıcı girişini gerçekten doğrulamayız. Bunun yerine, başka bir yere sayfaya geçirilmiş bir değeri doğruluyoruz. `Validation` Yardımcısı sizin için bunu yapmaz.

Bu nedenle, değeri `if(!Request.QueryString["ID"].IsEmpty()`) ile test ederek kendiniz kontrol edersiniz. Bir sorun varsa, `Validation` Yardımcısı ile yaptığınız gibi `Html.ValidationSummary`kullanarak hatayı görüntüleyebilirsiniz. Bunu yapmak için `Validation.AddFormError` çağırır ve bunu görüntülenecek bir ileti iletirsiniz. `Validation.AddFormError`, zaten bildiğiniz doğrulama sistemiyle ilgili özel iletiler tanımlamanıza olanak sağlayan yerleşik bir yöntemdir. (Bu öğreticide daha sonra bu doğrulama işlemini biraz daha sağlam hale getirmek için konuşacağız.)

Film için bir KIMLIK olduğundan emin olduktan sonra kod, yalnızca tek bir veritabanı öğesini arayarak veritabanını okur. (Muhtemelen veritabanı işlemleri için genel bir model olduğunu fark etmiş olabilirsiniz: veritabanını açın, bir SQL ifadesini tanımlayın ve ifadesini çalıştırın.) Bu kez, SQL `Select` deyimleri `WHERE ID = @0`içerir. KIMLIK benzersiz olduğundan, yalnızca bir kayıt döndürülebilir.

Sorgu, film listesi için kullandığınız `db.QuerySingle` (`db.Query`değil) kullanılarak gerçekleştirilir ve kod sonucu `row` değişkenine koyar. `row` adı rastgele; değişkenleri istediğiniz herhangi bir şekilde adlandırın. En üstte başlatılan değişkenler, bu değerlerin metin kutularında görüntülenebilmesi için film ayrıntıları ile doldurulur.

## <a name="testing-the-edit-page-so-far"></a>Düzenleme sayfasını test etme (şimdiye kadar)

Sayfanızı test etmek isterseniz, *filmler* sayfasını hemen çalıştırın ve herhangi bir filmin yanındaki bir **düzenleme** bağlantısına tıklayın. Seçtiğiniz filmle ilgili ayrıntıların bulunduğu *Editmovie* sayfasını görürsünüz:

![Düzenlenecek filmi gösteren film sayfasını düzenleme](updating-data/_static/image3.png)

Sayfanın URL 'sinin `?id=10` (veya başka bir sayı) gibi bir şey içerdiğine dikkat edin. Bu nedenle, *film* sayfasındaki bağlantıları **Düzenle** ' yi test ettiğiniz için, sayfanızın sorgu dizesinden kimliği okumasını ve tek bir film kaydı almak için veritabanı sorgusunun çalıştığını test edersiniz.

Film bilgilerini değiştirebilirsiniz, ancak **Değişiklikleri Gönder**' e tıkladığınızda hiçbir şey olmaz.

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>Filmi kullanıcının değişiklikleriyle güncelleştirmek için kod ekleme

*Editmovie. cshtml* dosyasında, ikinci işlevi uygulamak için (değişiklikleri kaydetme), aşağıdaki kodu `@` bloğunun kapatma ayracı içine ekleyin. (Kodu tam olarak nereye koyduğunuzdan emin değilseniz, Bu öğreticinin sonunda görüntülenen [filmi Düzenle sayfası için tam kod listesine](#Complete_Page_Listing_for_EditMovie) bakabilirsiniz.)

[!code-csharp[Main](updating-data/samples/sample12.cs)]

Bu biçimlendirme ve kod, *Addmovie*içindeki koda benzer. Kod `if(IsPost)` bir blokta, bu kod yalnızca Kullanıcı **Değişiklikleri Gönder** düğmesine tıkladığında, (ve yalnızca form nakledildiğinde) &mdash; çalışır. Bu durumda, `if(IsPost && Validation.IsValid())`gibi bir test kullanmadığınızı — Yani, ve kullanarak her iki testi birleştirmediniz. Bu sayfada, önce bir form gönderimi (`if(IsPost)`) olup olmadığını ve yalnızca doğrulama için alanları kaydetmeyi belirlersiniz. Daha sonra doğrulama sonuçlarını (`if(Validation.IsValid()`) test edebilirsiniz. Akış, *Addmovie. cshtml* sayfasından biraz farklıdır, ancak efekt aynıdır.

`Request.Form["title"]` ve diğer `<input>` öğeleri için benzer kodu kullanarak metin kutularının değerlerini alırsınız. Bu zaman, kodun film KIMLIĞINI gizli alandan (`<input type="hidden">`) aldığından emin olun. Sayfa ilk kez çalıştırıldığında, kod sorgu dizesinden KIMLIĞI aldı. Sorgu dizesinin daha sonra bir şekilde değiştirilmiş olması durumunda, başlangıçta görüntülenen filmin KIMLIĞINI aldığınızdan emin olmak için gizli alandan değeri alırsınız.

*Addfilm* kodu ve bu kod arasındaki gerçek önemli fark, bu kodda `Insert Into` DEYIMIN yerine SQL `Update` ifadesini kullanmanızdır. Aşağıdaki örnekte, SQL `Update` ifadesinin sözdizimi gösterilmektedir:

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

Herhangi bir sırada sütun belirtebilir ve bir `Update` işlemi sırasında her sütunu güncelleştirmeniz gerekmez. (KIMLIĞI güncellenemez, çünkü bu, kaydı yeni bir kayıt olarak kaydeder ve bir `Update` işlemi için izin verilmez.)

> [!NOTE] 
> 
> **Önemli** KIMLIĞE sahip `Where` yan tümcesi, veritabanının hangi veritabanı kaydını güncelleştirmek istediğinizi bildiği için çok önemlidir. `Where` yan tümcesini kapatırsanız, veritabanı veritabanındaki *her* kaydı güncelleştirir. Çoğu durumda, bu bir olağanüstü durum olacaktır.

Kodda, güncelleştirilecek değerler yer tutucuları kullanılarak SQL ifadesine geçirilir. Daha önce söylediğimiz öğeleri yinelemek için: güvenlik nedenleriyle, *yalnızca* bir SQL ifadesine değer geçirmek için yer tutucuları kullanın.

Kod, `Update` ifadesini çalıştırmak için `db.Execute` kullandıktan sonra, değişiklikleri görebileceğiniz şekilde liste sayfasına yeniden yönlendirilir.

> [!TIP] 
> 
> **Farklı SQL deyimleri, farklı Yöntemler**
> 
> Farklı SQL deyimlerini çalıştırmak için biraz farklı yöntemler kullanacağınızı fark etmiş olabilirsiniz. Birden çok kayıt döndüren `Select` bir sorgu çalıştırmak için `Query` yöntemini kullanırsınız. Yalnızca bir veritabanı öğesi döndüreceğimizi bildiğiniz bir `Select` sorgusu çalıştırmak için `QuerySingle` yöntemini kullanırsınız. Değişiklik yapan ancak veritabanı öğeleri döndürmeyen komutları çalıştırmak için `Execute` yöntemini kullanırsınız.
> 
> `Query` ve `QuerySingle`arasında zaten gördüğünüz gibi, her biri farklı sonuçlar döndürdüğünden, farklı yöntemlere sahip olmanız gerekir. (`Execute` yöntemi gerçekten &mdash; de bir değer döndürür &mdash; Komutun etkilediği veritabanı satırı sayısı, ancak şu ana kadar yoksayıyorsunuz.)
> 
> Kuşkusuz `Query` yöntemi yalnızca bir veritabanı satırı döndürebilir. Ancak, ASP.NET `Query` yönteminin sonuçlarını her zaman bir koleksiyon olarak değerlendirir. Yöntem yalnızca bir satır döndürürse bile, bu tek satırı koleksiyondan ayıklamanız gerekir. Bu nedenle, yalnızca bir satırın geri alınacağını *bildiğiniz* durumlarda `QuerySingle`kullanımı biraz daha uygundur.
> 
> Belirli veritabanı işlemleri türlerini gerçekleştiren birkaç yöntem vardır. Veritabanı yöntemlerinin bir listesini [ASP.NET Web Pages API hızlı başvurusu](../../api-reference/asp-net-web-pages-api-reference.md#Data)' nda bulabilirsiniz.

## <a name="making-validation-for-the-id-more-robust"></a>KIMLIK doğrulaması daha sağlam yapılıyor

Sayfa ilk kez çalıştığında, filmi veritabanından almak için sorgu dizesinden film KIMLIĞINI alırsınız. Bu kodu kullanarak yaptığınız, gerçekte gidilecek bir değer olduğundan emin olursunuz:

[!code-csharp[Main](updating-data/samples/sample13.cs)]

Bu kodu, bir Kullanıcı *film sayfasında bir* filmi seçmeden *editfilmlerini* sayfasına aldığından emin olmak için kullandınız, sayfada Kullanıcı dostu bir hata iletisi görüntülenir. (Aksi takdirde, kullanıcılar büyük olasılıkla yalnızca onları şaşırtabileceği bir hata görür.)

Ancak, bu doğrulama çok sağlam değildir. Sayfa şu hatalarla de çağrılabilir:

- KIMLIK bir sayı değil. Örneğin, sayfa `http://localhost:nnnnn/EditMovie?id=abc`gibi bir URL ile çağrılabilir.
- KIMLIK bir sayıdır, ancak mevcut olmayan bir filme (örneğin, `http://localhost:nnnnn/EditMovie?id=100934`) başvurur.

Bu URL 'lerden kaynaklanan hataları görmeyi merak ediyorsanız, *filmler* sayfasını çalıştırın. Düzenlenecek filmi seçin ve ardından *Editmovie* sayfasının URL 'sini ALFABETIK bir kimlik veya mevcut olmayan BIR filmin kimliği IÇEREN bir URL 'ye değiştirin.

Ne yapmalısınız? İlk düzeltmeler yalnızca sayfaya geçirilen bir KIMLIK olmadığından ve KIMLIğIN bir tamsayı olduğundan emin olmak içindir. `!IsPost` testin kodunu Şu örneğe benzer şekilde değiştirin:

[!code-csharp[Main](updating-data/samples/sample14.cs)]

`IsEmpty` testine ikinci bir koşul eklediniz, `&&` (mantıksal AND) ile bağlantılandırdınız:

[!code-csharp[Main](updating-data/samples/sample15.cs)]

[ASP.NET Web sayfaları programlama](../introducing-razor-syntax-c.md) öğreticisine giriş `AsBool`, bir karakter dizesini başka bir veri türüne dönüştürdüğünü `AsInt` gibi yöntemler bulabilirsiniz. `IsInt` yöntemi (ve `IsBool` ve `IsDateTime`gibi diğerleri) benzerdir. Ancak, yalnızca dönüştürme işlemini gerçekleştirmeksizin *dizeyi dönüştürüp* dönüştürmeyeceğinizi test ederler. Bu nedenle *, aslında sorgu dizesi değerinin bir tamsayıya dönüştürüledildiğini*söylüyorsunuz....

Diğer olası sorun, mevcut olmayan bir filmi arıyor. Filmi alacağınız kod şu kod gibi görünür:

[!code-csharp[Main](updating-data/samples/sample16.cs)]

Gerçek bir filme karşılık gelen `QuerySingle` yöntemine bir `movieId` değeri geçirirseniz, hiçbir şey döndürülmez ve izleyen deyimler (örneğin, `title=row.Title`) hatalara neden olur.

Daha kolay bir çözüm vardır. `db.QuerySingle` yöntemi sonuç döndürürse, `row` değişkeni null olur. Bu nedenle, bundan sonra değer almayı denemeden önce `row` değişkeninin null olup olmadığını kontrol edebilirsiniz. Aşağıdaki kod, `row` nesnesinden değerleri alan deyimler etrafında bir `if` bloğu ekler:

[!code-csharp[Main](updating-data/samples/sample17.cs)]

Bu iki ek doğrulama testi ile, sayfa daha fazla madde işareti-kanıt haline gelir. `!IsPost` dalı için kodun tamamı şu örneğe benzer şekilde görünür:

[!code-csharp[Main](updating-data/samples/sample18.cs)]

Bu görevin bir `else` bloğu için iyi bir şekilde kullanılması hakkında daha fazla bilgi edineceksiniz. Testler geçmezse `else` blokları hata iletilerini ayarlar.

## <a name="adding-a-link-to-return-to-the-movies-page"></a>Filmler sayfasına dönmek için bağlantı ekleme

Son ve yararlı bir ayrıntı, *filmler* sayfasına geri bir bağlantı eklemektir. Normal olay akışında, kullanıcılar *filmler* sayfasından başlayacaktır ve bir **düzenleme** bağlantısına tıklacaktır. Bu, bunları, filmi düzenleyebilecekleri ve düğmesine tıklatabilecekleri *Editmovie* sayfasına getirir. Kod değişikliği tamamladıktan sonra, *filmler* sayfasına yeniden yönlendirilir.

Ancak

- Kullanıcı herhangi bir şeyi değiştirmemeye karar verebilir.
- Kullanıcı, önce *filmler* sayfasındaki bir **düzenleme** bağlantısına tıklamadan bu sayfayı alabilir.

Her iki durumda da, ana listeye dönmesini kolaylaştırmak istersiniz. Bu kolay bir düzeldir &mdash; biçimlendirme içindeki kapanış `</form>` etiketinden hemen sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-html[Main](updating-data/samples/sample19.html)]

Bu biçimlendirme, başka bir yerde gördüğünüz `<a>` öğesi için aynı sözdizimini kullanır. URL, "Web sitesinin kökünü `~`" içerir.

## <a name="testing-the-movie-update-process"></a>Film güncelleştirme Işlemini test etme

Artık test edebilirsiniz. *Filmler* sayfasını çalıştırın ve filmin yanındaki **Düzenle** ' ye tıklayın. *Editmovie* sayfası göründüğünde, film üzerinde değişiklikler yapın ve **Değişiklikleri Gönder**' e tıklayın. Film listesi göründüğünde değişikliklerinizin gösterildiğinden emin olun.

Doğrulamanın çalıştığından emin olmak için, başka bir film için **Düzenle** ' ye tıklayın. *Editmovie* sayfasına geldiğinizde, **tarz** alanını (veya **yıl** alanını veya her ikisini birden) temizleyin ve değişikliklerinizi göndermeyi deneyin. Beklenen bir hata görürsünüz:

![Doğrulama hatalarını gösteren film sayfasını Düzenle](updating-data/_static/image4.png)

Değişikliklerinizi iptal etmek ve *filmler* sayfasına dönmek için **film dökümüne dön** bağlantısına tıklayın.

## <a name="coming-up-next"></a>Sonraki adımda

Bir sonraki öğreticide, bir film kaydını silme hakkında bilgi edineceksiniz.

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>Film sayfası için komple liste (düzenleme bağlantılarıyla güncelleştirildi)

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>Film düzenleme sayfasının sayfa listesini tamamlar

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>Ek Kaynaklar

- [Razor söz dizimini kullanarak ASP.NET Web programlamaya giriş](../../getting-started/introducing-razor-syntax-c.md)
- W3Schools sitesinde [SQL Update bildirisi](http://www.w3schools.com/sql/sql_update.asp)

> [!div class="step-by-step"]
> [Önceki](entering-data.md)
> [İleri](deleting-data.md)
