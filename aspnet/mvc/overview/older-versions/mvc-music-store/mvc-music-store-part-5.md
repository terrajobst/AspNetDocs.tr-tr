---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: '5\. Bölüm: formları ve şablon oluşturmayı düzenleme | Microsoft Docs'
author: jongalloway
description: Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, formları ve şablon oluşturmayı düzenlemenizi içerir.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559551"
---
# <a name="part-5-edit-forms-and-templating"></a>5\. Bölüm: Formları Düzenleme ve Şablon Oluşturma

[Jon Galloway](https://github.com/jongalloway) tarafından

> MVC müzik deposu, Web geliştirme için ASP.NET MVC ve Visual Studio 'nun nasıl kullanılacağını anlatan bir öğretici uygulamadır.  
>   
> MVC müzik deposu, çevrimiçi olarak müzik albümlerini satan ve temel site yönetimi, Kullanıcı oturum açma ve alışveriş sepeti işlevlerini uygulayan basit bir örnek depolama uygulamasıdır.
> 
> Bu öğretici serisi, ASP.NET MVC müzik deposu örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, formları ve şablon oluşturmayı düzenlemenizi içerir.

Önceki bölümde, veritabanımızdan veri yüklüyor ve görüntüleme yaptık. Bu bölümde, verileri düzenlemenizi de olanaklı yapacağız.

## <a name="creating-the-storemanagercontroller"></a>StoreManagerController oluşturma

**Storemanagercontroller**adlı yeni bir denetleyici oluşturarak başlayacağız. Bu denetleyici için, ASP.NET MVC 3 araçları güncelleştirmesinde bulunan yapı Iskelesi özelliklerinden faydalanacağız. Denetleyici Ekle iletişim kutusu seçeneklerini aşağıda gösterildiği gibi ayarlayın.

![](mvc-music-store-part-5/_static/image1.png)

Ekle düğmesine tıkladığınızda, ASP.NET MVC 3 yapı iskelesi mekanizmasının sizin için iyi bir iş miktarı olduğunu görürsünüz:

- Yerel bir Entity Framework değişkeniyle yeni StoreManagerController oluşturur
- Projenin görünümler klasörüne bir StoreManager klasörü ekler
- Bu, albüm sınıfına kesin olarak yazılan Create. cshtml, delete. cshtml, details. cshtml, Edit. cshtml ve Index. cshtml görünümünü ekler

![](mvc-music-store-part-5/_static/image2.png)

Yeni StoreManager denetleyici sınıfı, albüm model sınıfıyla çalışmayı ve veritabanı erişimi için Entity Framework bağlamımızı kullanmayı bilen CRUD (oluşturma, okuma, güncelleştirme, silme) denetleyicisi eylemlerini içerir.

## <a name="modifying-a-scaffolded-view"></a>Bir yapı Iskelesi görünümünü değiştirme

Bu kod, Bu öğreticinin tamamında yazdığımız gibi standart ASP.NET MVC kodsunurken, bu kodun bizim için oluşturulduğunu unutmamak önemlidir. Ortak denetleyici kodu yazmak ve kesin olarak belirlenmiş görünümleri el ile oluşturmak için harcadığınız zamanı kaydetmek amaçlanmıştır, ancak bu, şu şekilde değişiklik yapma konusunda d uyarılar ile önceden ortaya çıkacak gördüğünüz oluşturulan kod türüdür. kodudur. Bu kodunuzda bu sizin değiştirmeniz beklenmektedir.

Bu nedenle, StoreManager dizin görünümüne hızlı bir düzenleme (/views/storemanager/Index.cshtml) ile başlayalım. Bu görünüm, depolarımızda düzenleme/Ayrıntılar/silme bağlantılarıyla birlikte gelen albümleri listeleyen bir tablo görüntüler ve albümün ortak özelliklerini içerir. Bu ekranda çok faydalı olmadığından Albümlerüorturl alanını kaldıracağız. Görünüm kodunun &lt;tablo&gt; bölümünde, aşağıdaki vurgulanan satırlarda gösterildiği gibi, albümle birlikte bulunan &lt;&gt; ve &lt;TD öğelerini çevreleyen öğeleri&gt; silin:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

Değiştirilen görünüm kodu şu şekilde görünür:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>Mağaza Yöneticisi 'ne ilk bakış

Şimdi uygulamayı çalıştırın ve/Storemanager/dizinine gidin. Bu, yeni değiştirdiğimiz mağaza yöneticisi dizinini görüntüleyerek, Düzenle, Ayrıntılar ve Sil bağlantılarıyla depodaki Albümler listesini gösterir.

![](mvc-music-store-part-5/_static/image3.png)

Düzenle bağlantısına tıkladığınızda, albümün alanları içeren bir düzenleme formu görüntülenir ve bu da, tarz ve sanatçının açılan listeleri dahil değildir.

![](mvc-music-store-part-5/_static/image4.png)

Alttaki "listeye geri dön" bağlantısına tıklayın ve ardından bir albümün Ayrıntılar bağlantısına tıklayın. Bu, tek bir albümün ayrıntı bilgilerini görüntüler.

![](mvc-music-store-part-5/_static/image5.png)

Yeniden, listeye geri dön bağlantısına ve ardından silme bağlantısına tıklayın. Bu, albüm ayrıntılarını gösteren bir onay iletişim kutusu görüntüler ve bunu silmek istediğdiğimiz emin olup olmadığını sorar.

![](mvc-music-store-part-5/_static/image6.png)

Alt kısımdaki Sil düğmesine tıkladığınızda, albüm silinir ve silinen albümün gösterildiği dizin sayfasına dönersiniz.

Mağaza Yöneticisi ile karşılaştık, ancak başlayacağız CRUD işlemleri için çalışma denetleyicisi ve kod görüntüleme yaptık.

## <a name="looking-at-the-store-manager-controller-code"></a>Mağaza Yöneticisi denetleyici koduna bakıyor

Mağaza Yöneticisi denetleyicisi iyi bir kod miktarı içerir. Bunu yukarıdan aşağıya doğru ilerlim. Denetleyici, MVC denetleyicisinin bazı standart ad alanlarını ve modeller ad alanımızın bir başvurusunu içerir. Denetleyicinin, veri erişimi için her bir denetleyici eylemi tarafından kullanılan özel bir MusicStoreEntities örneği vardır.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>Mağaza Yöneticisi Dizin ve ayrıntıları eylemleri

Dizin görünümü, bir albümün başvurulan tarzı ve sanatçı bilgileri de dahil olmak üzere Albümler listesini alır ve daha önce Store Gözatım yönteminde çalışırken gördük. Dizin görünümü, bağlantılı nesnelere yapılan başvuruları izleyerek her bir albümün tarz adını ve sanatçı adını görüntüleyebilir, bu nedenle denetleyicinin etkin ve bu bilgileri özgün istekte sorguladığını unutmayın.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

StoreManager denetleyicisinin Ayrıntılar denetleyicisi eylemi, depolama denetleyicisi ayrıntıları eylemiyle tam olarak aynı şekilde çalışarak Find () yöntemini kullanarak albüm KIMLIĞI için önceden BT sorguları yazdık, sonra da görünüme döndürülür.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>Oluşturma eylemi yöntemleri

Oluşturma eylemi yöntemleri, şimdiye kadar gördüğdiklerden biraz farklıdır, çünkü form girişi işler. Bir Kullanıcı/StoreManager/Create/öğesini ilk kez ziyaret ettiğinde boş bir form görüntülenir. Bu HTML sayfası, albümün ayrıntılarını girebilecekleri açılan menü ve metin kutusu giriş öğelerini içeren bir &lt;form&gt; öğesi içerir.

Kullanıcı albüm form değerlerini doldurduktan sonra, bu değişiklikleri veritabanına kaydetmek için bu değişiklikleri uygulamanıza geri göndermek için "Kaydet" düğmesine basabilir. Kullanıcı "Kaydet" düğmesine bastığında &lt;form&gt;,/StoreManager/Create/URL 'ye bir HTTP-POST işlemi gerçekleştirir ve &lt;formu&gt; değerlerini HTTP-POST 'un bir parçası olarak gönderir.

ASP.NET MVC, StoreManagerController sınıfımızda iki ayrı "Create" eylem yöntemi uygulamamızı sağlayarak bu iki URL çağırma senaryosunun mantığını kolayca bölmemizi sağlar. ilk HTTP-GET-/StoreManager/Create/URL 'sine gidin ve diğer yandan gönderilen değişikliklerin HTTP-POST işlemini idare edin.

### <a name="passing-information-to-a-view-using-viewbag"></a>ViewBag kullanarak bir görünüme bilgi geçirme

Bu öğreticide daha önce olan görünüm paketini kullandık, ancak bunun çok fazla olmadığı için. ViewBag, türü kesin belirlenmiş bir model nesnesi kullanmadan görünüme bilgi iletmemize olanak sağlar. Bu durumda, HTTP-GET denetleyiciyi Düzenle eyleminin, açılan listeleri doldurmak için forma bir tür ve sanatçı listesi geçirmesi gerekir ve bunu yapmanın en kolay yolu, bunları ViewBag öğeleri olarak döndürmektir.

ViewBag, bu özellikleri tanımlamak için kod yazmadan ViewBag. foo veya ViewBag. YourNameHere türünde, dinamik bir nesnedir. Bu durumda, denetleyici kodu ViewBag. Genreıd ve ViewBag. ArtistId ' yi kullanarak, form ile gönderilen aşağı açılan değerlerin Genreıd ve ArtistId olur ve bu da bu ayarların ayartıkları albüm özellikleridir.

Bu açılan değerler, yalnızca bu amaçla oluşturulan SelectList nesnesi kullanılarak forma döndürülür. Bu, aşağıdaki gibi kod kullanılarak yapılır:

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

Eylem yöntemi kodundan görebileceğiniz gibi, bu nesneyi oluşturmak için üç parametre kullanılır:

- DropDown 'ın görüntüleneceği öğelerin listesi. Bunun yalnızca bir dize olmadığını unutmayın; bir tür listesi geçiriyoruz.
- SelectList öğesine geçirilen sonraki parametre seçili değerdir. Bu, SelectList 'in listede bir öğenin nasıl önceden ekleneceğini nasıl öğrendiği. Bu, oldukça benzer olan düzenleme formuna baktığımızda anlaşılması daha kolay olacaktır.
- Son parametre, görüntülenecek özelliktir. Bu durumda, Genre.Name özelliğinin kullanıcıya gösterildiğine işaret eder.

Göz önünde bulundurularak, HTTP-GET oluşturma eylemi oldukça basittir; ViewBag 'e iki SelectLists eklenir ve forma hiçbir model nesnesi geçirilmemiştir (henüz oluşturulmadığından).

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>Oluştur görünümünde açılan listeleri görüntülemek için HTML Yardımcıları

Açılan değerlerin görünüme nasıl geçtiğini ele geçirdiğimiz için, bu değerlerin nasıl görüntülendiğini görmek üzere görünüme hızlı bir göz atalım. Görünüm kodunda (/views/storemanager/Create.exe), tarz açılan ekranını görüntülemek için aşağıdaki çağrının yapıldığını görürsünüz.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

Bu, ortak bir görüntüleme görevi gerçekleştiren bir HTML Yardımcısı-bir yardımcı program yöntemi olarak bilinir. HTML Yardımcıları, görünüm kodumuzu kısa ve okunabilir halde tutmanın çok yararlı olur. HTML. DropDownList Yardımcısı, ASP.NET MVC tarafından sağlanır, ancak daha sonra uygulamamızda yeniden kullanacağımız görünüm kodu için kendi yardımcıları oluşturmak mümkün olacaktır.

HTML. DropDownList çağrısının yalnızca iki şey söyleilmesi gerekir. listenin görüntüleneceği yer, (varsa) bir değer önceden seçilmelidir. Birinci parametre olan Genreıd, DropDownList 'e model veya ViewBag içinde Genreıd adlı bir değer bakmasını söyler. İkinci parametre, açılan listede başlangıçta seçildiği şekilde gösterilecek değeri göstermek için kullanılır. Bu form bir oluşturma formu olduğundan, önceden seçilecek bir değer yok ve String. Empty geçildi.

### <a name="handling-the-posted-form-values"></a>Postalanan form değerlerini işleme

Daha önce anlatıldığı gibi, her formla ilişkili iki eylem yöntemi vardır. İlki HTTP-GET isteğini işler ve formu görüntüler. İkincisi, gönderilen form değerlerini içeren HTTP-POST isteğini işler. Denetleyici eyleminin, ASP.NET MVC 'nin yalnızca HTTP-POST isteklerine yanıt vermesi gerektiğini belirten bir [HttpPost] özniteliği olduğunu fark edersiniz.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

Bu eylem dört sorumluluklara sahiptir:

- 1. Form değerlerini oku
- 2. Form değerlerinin herhangi bir doğrulama kuralını geçmediğinden emin olun
- 3. Form gönderimi geçerliyse, verileri kaydedin ve güncelleştirilmiş listeyi görüntüleyin
- 4. Form gönderimi geçerli değilse, doğrulama hatalarıyla formu yeniden görüntüleyin

#### <a name="reading-form-values-with-model-binding"></a>Model bağlamasıyla form değerlerini okuma

Denetleyici eylemi, Genreıd ve ArtistId (açılan listeden) ve başlık, Fiyat ve albümle ilgili metin kutusu değerlerini içeren bir form gönderimini işliyor. Form değerlerine doğrudan erişmek mümkün olsa da, ASP.NET MVC içinde yerleşik model bağlama özelliklerini kullanmak daha iyi bir yaklaşımdır. Bir denetleyici eylemi bir parametre olarak model türü alırsa, ASP.NET MVC Form girişlerini (Ayrıca Route ve QueryString değerlerini) kullanarak o türdeki bir nesneyi doldurmayı dener. Bu, adları model nesnesinin özellikleriyle eşleşen değerleri arayarak yapar; örneğin, yeni albüm nesnesinin Genreıd değeri ayarlanırken, Genreıd adında bir giriş arar. ASP.NET MVC 'de standart yöntemleri kullanarak görünümler oluşturduğunuzda, formlar her zaman giriş alanı adı olarak özellik adları kullanılarak işlenir, bu nedenle alan adları yalnızca eşleşmeyecektir.

#### <a name="validating-the-model"></a>Model doğrulanıyor

Model, ModelState. IsValid basit çağrısıyla onaylanır. Henüz albüm sınıfınız için herhangi bir doğrulama kuralı eklemediniz. bu şekilde, bu denetim artık bu denetimi çok fazla yapacağız. Bu ModelStat. IsValid denetiminin, modelinize yerleştirdiğimiz doğrulama kurallarına uyarlanmasının önemli olması, bu nedenle Doğrulama kurallarındaki gelecekteki değişikliklerin, denetleyici eylem kodunda herhangi bir güncelleştirme gerektirmemesi gerekir.

#### <a name="saving-the-submitted-values"></a>Gönderilen değerler kaydediliyor

Form gönderimi doğrulamayı geçerse, değerleri veritabanına kaydetmeniz zaman olur. Entity Framework ile, yalnızca bir modelin Albümler koleksiyonuna eklenmesini ve SaveChanges 'in çağrılmasını gerektirir.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework, değeri kalıcı hale getirmek için uygun SQL komutlarını üretir. Verileri kaydettikten sonra, güncelleştirmemizi görebilmemiz için Albümler listesine geri yönlendiriyoruz. Bu işlem, görüntülenmesini istediğimiz denetleyici eyleminin adı ile RedirectToAction döndürülmesiyle yapılır. Bu durumda, Dizin yöntemi budur.

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>Doğrulama hatalarıyla geçersiz form gönderimleri görüntüleme

Geçersiz form girişi durumunda, açılan değerler ViewBag 'e eklenir (HTTP-GET durumunda olduğu gibi) ve bağlantılı model değerleri görüntüleme görünümüne geri geçirilir. Doğrulama hataları @Html.ValidationMessageFor HTML Yardımcısı kullanılarak otomatik olarak görüntülenir.

#### <a name="testing-the-create-form"></a>Oluşturma formunu test etme

Bunu test etmek için uygulamayı çalıştırın ve/StoreManager/Create/adresine gidin. Bu, StoreController Create HTTP-GET yöntemi tarafından döndürülen boş formu gösterir.

Formu göndermek için bazı değerleri girin ve Oluştur düğmesine tıklayın.

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>Düzenlemeleri işleme

Düzenleme eylemi çifti (HTTP-GET ve HTTP-POST), az önce bakdığımız oluşturma eylemi yöntemlerine çok benzer. Düzenleme senaryosu mevcut bir albümle çalışmayı içerdiğinden, Edit HTTP-GET yöntemi, albümü, yol aracılığıyla geçirilen "ID" parametresine göre yükler. Bu kod, Albümno 'a göre bir albümü almaya yönelik bu kod, daha önce ayrıntılar denetleyicisi eyleminde bakdığımız şekilde aynıdır. Create/HTTP-GET yönteminde olduğu gibi, açılan değerler de ViewBag aracılığıyla döndürülür. Bu, model nesnemiz olarak görünüm (örneğin, bir tarzın listesi) ile ViewBag aracılığıyla bir albüm döndürmemize olanak sağlar.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

HTTP-POST işlemini Düzenle eylemi, HTTP-POST oluşturma eylemine çok benzer. Tek fark, veritabanına yeni bir albüm eklemek yerine kullanılır. Albümler koleksiyonu, veritabanı kullanarak albümün geçerli örneğini buluyoruz. Giriş (albüm) ve durumunu değiştirildi olarak ayarlama. Bu, yeni bir albümü oluşturmak yerine var olan bir albümü değiştirmekte olduğumuz Entity Framework söyler.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

Uygulamayı çalıştırıp/StoreManger/adresine giderek ve ardından bir albümün düzenleme bağlantısına tıklayarak bunu test edebilirsiniz.

![](mvc-music-store-part-5/_static/image9.png)

Bu, düzenleme HTTP-GET yöntemi tarafından gösterilen düzenleme formunu görüntüler. Bazı değerleri girin ve Kaydet düğmesine tıklayın.

![](mvc-music-store-part-5/_static/image10.png)

Bu, formu gönderir, değerleri kaydeder ve ABD 'nin güncelleştirildiğini gösteren albüm listesine döndürür.

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>Silme Işlemi işleniyor

Silme, düzenleme ve oluşturma ile aynı kalıbı izler, onay formunu göstermek için bir denetleyici eylemi ve form gönderimini işlemek için başka bir denetleyici eylemi kullanmaktır.

HTTP-GET Delete Controller eylemi, önceki Store Manager ayrıntıları denetleyicisi eylemmizden tamamen aynıdır.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

Görünüm içeriğini sil şablonunu kullanarak bir albüm türüne kesin olarak yazılmış bir form görüntüyoruz.

![](mvc-music-store-part-5/_static/image12.png)

Şablonu Sil, modelin tüm alanlarını gösterir, ancak bu şekilde bir bit ' i basitleştireceğiz. /Views/storemanager/delete.exe ' deki görünüm kodunu aşağıdaki şekilde değiştirin.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

Bu, Basitleştirilmiş bir silme onayı görüntüler.

![](mvc-music-store-part-5/_static/image13.png)

Sil düğmesine tıkladığınızda formun sunucuya geri nakledilmesine neden olur ve bu da Deleteonaylanan eylemi yürütür.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

HTTP-POST silme denetleyici eylemi aşağıdaki eylemleri gerçekleştirir:

- 1. Albümü KIMLIĞE göre yükler
- 2. Albümü siler ve değişiklikleri kaydeder
- 3. Albümün listeden kaldırıldığını gösteren dizine yeniden yönlendirir

Bunu test etmek için uygulamayı çalıştırın ve/Storemanagera gidin. Listeden bir albüm seçin ve Sil bağlantısına tıklayın.

![](mvc-music-store-part-5/_static/image14.png)

Bu, silme onayı ekranımızı görüntüler.

![](mvc-music-store-part-5/_static/image15.png)

Sil düğmesine tıkladığınızda albüm kaldırılır ve bu, albümün silindiğini gösteren mağaza yöneticisi dizin sayfasına döndürülür.

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>Metni kesmek için özel HTML Yardımcısı kullanma

Store Manager Dizin sayfamızda bir olası sorun var. Albüm başlığımız ve sanatçı adı özellikleri, tablo biçimimizi oluşturabilecek kadar uzun olabilir. Görünümlerimizde bu ve diğer özellikleri kolayca kesmemizi sağlamak için özel bir HTML Yardımcısı oluşturacağız.

![](mvc-music-store-part-5/_static/image17.png)

Razor @helper söz dizimi, görünümlerinizin kullanımı için kendi yardımcı işlevlerinizi oluşturmayı oldukça kolay hale yaptı. /Views/storemanager/Index.cshtml görünümünü açın ve @model satırından hemen sonra aşağıdaki kodu ekleyin.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

Bu yardımcı yöntem, izin vermek için bir dize ve en fazla uzunluğu alır. Sağlanan metin belirtilen uzunluktan kısaysa, yardımcı bunu olduğu gibi verir. Daha uzunsa, metni keser ve "..." oluşturur geri kalanı için.

Şimdi, albüm başlığı ve sanatçı adı özelliklerinin 25 karakterden az olduğundan emin olmak için Truncate Helper 'ı kullanabiliriz. Yeni kesme yardımımızın kullanıldığı tüm görünüm kodu aşağıda gösterilir.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

Şimdi/StoreManager/URL 'ye gözatarken, albümler ve başlıklar en büyük uzunlularımızın altında tutulur.

![](mvc-music-store-part-5/_static/image18.png)

Note: Bu, bir yardım 'ın tek bir görünümde oluşturulması ve kullanılması için basit bir durumdur. Siteniz genelinde kullanabileceğiniz yardımcılar oluşturma hakkında daha fazla bilgi edinmek için bkz. blog gönderisi: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)

> [!div class="step-by-step"]
> [Önceki](mvc-music-store-part-4.md)
> [İleri](mvc-music-store-part-6.md)
