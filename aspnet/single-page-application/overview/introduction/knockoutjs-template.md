---
uid: single-page-application/overview/introduction/knockoutjs-template
title: 'Tek sayfalı uygulama: altını gizleme Koutjs şablonu | Microsoft Docs'
author: MikeWasson
description: Altını gizleme şablonu
ms.author: riande
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 3a551db1caa9636eb7f2e04c287d3ef371263584
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578696"
---
# <a name="single-page-application-knockoutjs-template"></a>Tek Sayfalı Uygulama: KnockoutJS şablonu

, [Mike te son](https://github.com/MikeWasson)

> Altını gizleme MVC şablonu, ASP.NET and Web Tools 2012,2 parçasıdır
> 
> [2012,2 ASP.NET and Web Tools indirin](https://go.microsoft.com/fwlink/?LinkId=282650)

ASP.NET and Web Tools 2012,2 güncelleştirmesi, ASP.NET MVC 4 için tek sayfalı uygulama (SPA) şablonu içerir. Bu şablon, etkileşimli istemci tarafı Web uygulamalarını hızlıca oluşturmaya başlamanızı sağlamak için tasarlanmıştır.

"Tek sayfalı uygulama" (SPA), tek bir HTML sayfası yükleyen bir Web uygulaması için genel bir terimdir ve sonra yeni sayfalar yüklemek yerine sayfayı dinamik olarak güncelleştirir. İlk sayfa yüklendikten sonra, SPA, AJAX istekleri aracılığıyla sunucuyla iletişim kuran bir iletişim yükler.

![](knockoutjs-template/_static/image1.png)

AJAX yeni bir şey değildir, ancak bugün büyük bir Gelişmiş SPA uygulaması oluşturmayı ve bakımını kolaylaştıran JavaScript çerçeveleri vardır. Ayrıca, HTML 5 ve CSS3 zengin Usıs oluşturmayı kolaylaştırır.

Bu işlemi kullanmaya başlamak için, SPA şablonu örnek bir "yapılacaklar listesi" uygulaması oluşturur. Bu öğreticide, şablona yönelik kılavuzlu bir tura çıkacağız. İlk olarak yapılacaklar listesi uygulamasının kendisine bakacağız ve sonra çalışmasını sağlayan teknoloji parçalarını incelemektir.

## <a name="create-a-new-spa-template-project"></a>Yeni bir SPA şablonu projesi oluştur

Gereksinimler:

- Web için Visual Studio 2012 veya Visual Studio Express 2012
- ASP.NET Web araçları 2012,2 güncelleştirmesi. Güncelleştirmeyi [buraya](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2)yükleyebilirsiniz.

Visual Studio 'Yu başlatın ve başlangıç sayfasından **Yeni proje** ' yi seçin. Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi adlandırın ve **Tamam**' a tıklayın.

![](knockoutjs-template/_static/image2.png)

**Yeni proje** sihirbazında **tek sayfalı uygulama**' yı seçin.

![](knockoutjs-template/_static/image3.png)

Uygulamayı derleyip çalıştırmak için F5'e basın. Uygulama ilk kez çalıştırıldığında, oturum açma ekranını görüntüler.

![](knockoutjs-template/_static/image4.png)

&quot;&quot; bağlantısı ' na tıklayın ve yeni bir kullanıcı oluşturun.

![](knockoutjs-template/_static/image5.png)

Oturum açtıktan sonra, uygulama iki öğe ile varsayılan bir yapılacaklar listesi oluşturur. Yeni bir liste eklemek için "yapılacaklar listesi ekle" seçeneğine tıklayabilirsiniz.

![](knockoutjs-template/_static/image6.png)

Listeyi yeniden adlandırın, listeye öğe ekleyin ve bunları kapatın. Ayrıca, öğeleri silebilir veya bir listenin tamamını silebilirsiniz. Değişiklikler, uygulamayı yerel olarak çalıştırdığınız için sunucudaki bir veritabanında otomatik olarak kalıcı hale getirilir (Bu noktada aslında Yereldb).

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>SPA şablonunun mimarisi

Bu diyagramda uygulamanın ana yapı taşları gösterilmektedir.

![](knockoutjs-template/_static/image8.png)

Sunucu tarafında, ASP.NET MVC HTML 'yi sunar ve ayrıca form tabanlı kimlik doğrulamasını da işler.

ASP.NET Web API 'SI, ToDoLists ve Todoıtems ile ilgili tüm istekleri (alma, oluşturma, güncelleştirme ve silme dahil) işler. İstemci verileri JSON biçiminde Web API 'SI ile değiş tokuş eder.

Entity Framework (EF), O/RM katmanıdır. ASP.NET 'ın nesne odaklı dünyası ve temel alınan veritabanı arasında ortalaştırır. Veritabanı LocalDB kullanır, ancak bunu Web. config dosyasında değiştirebilirsiniz. Genellikle Yereldb 'yi yerel geliştirme için kullanacaksınız ve sonra EF Code-First geçişini kullanarak sunucuda bir SQL veritabanına dağıtmanız gerekir.

İstemci tarafında, altını gizleme. js kitaplığı, AJAX isteklerindeki sayfa güncelleştirmelerini işler. Altını gizleme sayfayı en son verilerle eşleştirmek için veri bağlamayı kullanır. Bu şekilde, JSON verilerinde izlenecek ve DOM güncelleştiren koddan herhangi birini yazmanız gerekmez. Bunun yerine, bildirime dayalı öznitelikleri, verileri nasıl sunacaklarını belirten HTML 'ye yerleştirebilirsiniz.

Bu mimarinin büyük bir avantajı, sunu katmanını uygulama mantığından ayırmadır. Web sayfanızın nasıl görüneceğine ilişkin hiçbir şey bilmeden Web API bölümünü oluşturabilirsiniz. İstemci tarafında, bu verileri temsil etmek için bir "model görüntüle" oluşturursunuz ve görünüm modeli HTML 'e bağlamak için altını gizleme kullanır. Bu, görünüm modelini değiştirmeden HTML 'yi kolayca değiştirmenize olanak sağlar. (Daha sonra bir bit altını gizleme bölümüne bakacağız.)

## <a name="models"></a>Modeller

Visual Studio projesinde modeller klasörü, sunucu tarafında kullanılan modelleri içerir. (Ayrıca, istemci tarafında modeller de vardır; bunlar için de bir alan olacaktır.)

![](knockoutjs-template/_static/image9.png)

**TodoItem, TodoList**

Bunlar, Entity Framework Code First için veritabanı modelleridir. Bu modellerin birbirini işaret eden özellikleri olduğunu unutmayın. `ToDoList` bir Todoıtems koleksiyonu içerir ve her `ToDoItem` üst ToDoList geri başvurusu vardır. Bu özelliklere, gezinti özellikleri adı verilir ve tek-çok ilişkisini ve yapılacaklar listesini ve yapılacaklar öğelerini temsil eder.

`ToDoItem` sınıfı, `ToDoListId` `ToDoList` tabloya yabancı anahtar olduğunu belirtmek için **[Yabancıkey]** özniteliğini de kullanır. Bu, veritabanına yabancı anahtar kısıtlaması ekleneceğini söyler.

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto, TodoListDto**

Bu sınıflar istemciye gönderilecek verileri tanımlar. "DTO", "veri aktarımı nesnesi" anlamına gelir. CTO, varlıkların JSON olarak nasıl serileştirilme şeklini tanımlar. Genel olarak, DTOs kullanmanın birkaç nedeni vardır:

- Hangi özelliklerin serileştirildiği denetlemek için. DTO, etki alanı modelinden özelliklerin bir alt kümesini içerebilir. Bunu güvenlik nedenleriyle (hassas verileri gizlemek için) veya yalnızca göndereceğiniz veri miktarını azaltmak için yapabilirsiniz.
- Verilerin şeklini değiştirmek için: Örneğin, daha karmaşık bir veri yapısını düzleştirmek için.
- Herhangi bir iş mantığını DTO dışında tutmak için (kaygıları ayrımı).
- Etki alanı modelleriniz bazı nedenlerle serileştirilemiyor. Örneğin, bir nesneyi seri hale getirmek istediğinizde döngüsel başvurular soruna neden olabilir (bkz. [Döngüsel nesne başvurularını işleme](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)); Ancak, bir DFOR kullanarak sorunu tamamen önler.

SPA şablonunda DTOs, etki alanı modelleriyle aynı verileri içerir. Ancak, gezinti özelliklerinden döngüsel başvuruları önlemediği ve genel DTO düzenlerini gösterdikleri için bunlar hala yararlıdır.

**AccountModels.cs**

Bu dosya, site üyeliği için modeller içerir. `UserProfile` sınıfı, üyelik VERITABANıNDAKI Kullanıcı profillerinin şemasını tanımlar. (Bu durumda, tek bilgi Kullanıcı KIMLIĞI ve kullanıcı adıdır.) Bu dosyadaki diğer model sınıfları, Kullanıcı kaydı ve oturum açma formları oluşturmak için kullanılır.

## <a name="entity-framework"></a>Varlık Çerçevesi

SPA şablonu EF Code First kullanır. Code First geliştirmek için, önce kod içinde modelleri tanımlar, sonra EF veritabanını oluşturmak için modeli kullanır. Aynı zamanda var olan bir veritabanı ([Database First](https://msdn.microsoft.com/data/jj206878.aspx)) ile EF de kullanabilirsiniz.

Modeller klasöründeki `TodoItemContext` sınıfı **DbContext**'ten türetiliyor. Bu sınıf modeller ve EF arasında "tutkalla" sağlar. `TodoItemContext`, bir `ToDoItem` koleksiyonu ve bir `TodoList` koleksiyonu barındırır. Veritabanını sorgulamak için, bu koleksiyonlara yönelik bir LINQ sorgusu yazmanız yeterlidir. Örneğin, "Gamze" kullanıcısı için tüm yapılacaklar listelerini nasıl seçebileceğiniz aşağıda verilmiştir:

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

Ayrıca, koleksiyona yeni öğeler ekleyebilir, öğeleri güncelleştirebilir veya öğeleri koleksiyondan silebilir ve değişiklikleri veritabanında kalıcı hale getirebilirsiniz.

## <a name="aspnet-web-api-controllers"></a>ASP.NET Web API 'SI denetleyicileri

ASP.NET Web API 'sinde, denetleyiciler HTTP isteklerini işleyen nesnelerdir. Belirtildiği gibi, SPA şablonu, `ToDoList` ve `ToDoItem` örneklerine CRUD işlemlerini etkinleştirmek için Web API kullanır. Denetleyiciler, çözümün denetleyiciler klasöründe bulunur.

![](knockoutjs-template/_static/image10.png)

- `TodoController`: Yapılacaklar öğeleri için HTTP isteklerini Işler
- `TodoListController`: Yapılacaklar listeleri için HTTP isteklerini Işler.

Web API 'SI, denetleyici adı URI yoluyla eşleştiğinden, bu adlar önemlidir. (Web API 'sinin denetleyicilere HTTP isteklerini nasıl yönlendirdiğini öğrenmek için bkz. [ASP.NET Web API 'de yönlendirme](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).)

`ToDoListController` sınıfına bakalım. Tek bir veri üyesi içerir:

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

`TodoItemContext`, daha önce açıklandığı gibi EF ile iletişim kurmak için kullanılır. Denetleyicideki Yöntemler CRUD işlemlerini uygular. Web API 'SI, istemciden denetleyici yöntemlerine HTTP isteklerini aşağıdaki gibi eşleştirir:

| HTTP Isteği | Controller yöntemi | Açıklama |
| --- | --- | --- |
| /Api/TODO Al | `GetTodoLists` | Yapılacaklar listelerinin koleksiyonunu alır. |
| /Api/Todo/*KIMLIĞI* al | `GetTodoList` | KIMLIĞE göre yapılacaklar listesini alır |
| /Api/Todo/*ID* koy | `PutTodoList` | Yapılacaklar listesini güncelleştirir. |
| Todo/api/gönderin | `PostTodoList` | Yeni bir yapılacaklar listesi oluşturur. |
| /Api/Todo/*KIMLIĞINI* Sil | `DeleteTodoList` | YAPıLACAKLAR listesini siler. |

Bazı işlemler için URI 'Lerin ID değeri için yer tutucular içerdiğini unutmayın. Örneğin, KIMLIĞI 42 olan bir yapılacaklar listesini silmek için URI `/api/todo/42`.

CRUD işlemleri için Web API kullanma hakkında daha fazla bilgi edinmek için bkz. [CRUD Işlemlerini destekleyen bir Web API 'Si oluşturma](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md). Bu denetleyicinin kodu oldukça basittir. İşte bazı ilginç noktaları:

- `GetTodoLists` yöntemi, oturum açmış kullanıcının KIMLIĞINE göre sonuçları filtrelemek için bir LINQ sorgusu kullanır. Bu şekilde, bir Kullanıcı yalnızca kendisine ait olan verileri görür. Ayrıca, `ToDoList` örneklerini `TodoListDto` örneklerine dönüştürmek için SELECT ifadesinin kullanıldığına dikkat edin.
- PUT ve POST yöntemleri, veritabanını değiştirmeden önce model durumunu denetler. **ModelState. IsValid** yanlış ise, bu yöntemler HTTP 400, hatalı istek döndürür. [Model doğrulamasında](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md)Web API 'sinde model doğrulama hakkında daha fazla bilgi edinin.
- Denetleyici sınıfı, **[Yetkilendir]** özniteliğiyle de donatılmış. Bu öznitelik, HTTP isteğinin kimlik doğrulamasının yapılıp yapılmayacağını denetler. İsteğin kimliği doğrulanmıyorsa, istemci HTTP 401, yetkisiz olarak alır. [ASP.NET Web API 'Sinde kimlik doğrulaması ve yetkilendirme](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md)hakkında daha fazla bilgi edinin.

`TodoController` sınıfı `TodoListController`çok benzer. En büyük fark, her bir GET yöntemini tanımlamaz çünkü istemci her yapılacaklar listesi ile birlikte yapılacaklar öğelerini alır.

## <a name="mvc-controllers-and-views"></a>MVC denetleyicileri ve görünümleri

MVC denetleyicileri çözümün denetleyiciler klasöründe de bulunur. `HomeController` uygulama için ana HTML 'i işler. Ana denetleyicinin görünümü Görünümler/Home/Index. cshtml içinde tanımlanır. Giriş görünümü, kullanıcının oturum açmış olmasına bağlı olarak farklı içerikleri işler:

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

Kullanıcılar oturum açtığında, ana Kullanıcı arabirimini görürler. Aksi takdirde, oturum açma paneli görüntülenir. Bu Koşullu işleme sunucu tarafında gerçekleştiğine unutmayın. İstemci tarafında&#8212;gizli içeriği gizlemeyi hiçbir şey, ham http iletilerini izleyen bir kişiye görünür.

## <a name="client-side-javascript-and-knockoutjs"></a>İstemci tarafı JavaScript ve altını gizleme. js

Şimdi uygulamanın sunucu tarafını istemciye etkinleştirelim. SPA şablonu, sorunsuz ve etkileşimli bir kullanıcı arabirimi oluşturmak için jQuery ve altını gizleme. js birleşimini kullanır. Altını gizleme. js, HTML 'yi verilere bağlamayı kolaylaştıran bir JavaScript kitaplığıdır. Altını gizleme. js, "Model-View-ViewModel" adlı bir model kullanır.

- Model, etki alanı verileri (ToDo listeleri ve Yapılacaklar öğeleri).
- Görünüm HTML belgesidir.
- View-model, model verilerini tutan bir JavaScript nesnesidir. View-model, Kullanıcı arabiriminin kod soyutlamasıdır. HTML temsili bilgisine sahip değildir. Bunun yerine, görünümün soyut özelliklerini temsil eder, örneğin "ToDo öğeleri listesi".

Görünüm, görünüm modeline veri ile bağlanır. Görünüm modeli güncelleştirmeleri otomatik olarak görünüme yansıtılır. Bağlamalar diğer yönle de çalışır. DOM 'daki Olaylar (tıklama gibi), AJAX çağrılarını tetikleyen görünüm modelindeki işlevlere veri bağımlıdır.

SPA şablonu, istemci tarafı JavaScript 'ı üç katmana düzenler:

- Todo. DataContext. js: AJAX istekleri gönderir.
- Todo. model. js: modelleri tanımlar.
- Todo. ViewModel. js: görünüm modelini tanımlar.

![](knockoutjs-template/_static/image11.png)

Bu betik dosyaları, çözümün betikler/App klasöründe bulunur.

![](knockoutjs-template/_static/image12.png)

**Todo. DataContext** , Web API denetleyicilerine YÖNELIK tüm Ajax çağrılarını işler. (Oturum açma için AJAX çağrıları, başka bir yerde, ajaxLogin. js ' de tanımlanır.)

**Todo. model. js** Yapılacaklar listeleri için istemci tarafı (tarayıcı) modellerini tanımlar. İki model sınıfı vardır: TodoItem ve todoList.

Model sınıflarında birçok özellik "Ko. Observable" türündedir. Gözlemlenenler, altını gizleme 'nin Magic 'i nasıl yapar. [Gizleme belgelerinden](http://knockoutjs.com/documentation/introduction.html): bir observable, abonelere değişiklikler hakkında bildirimde bulunan bir "JavaScript nesnesidir". Bir observable değeri değiştiğinde, altını gizleme bu gözlemlenenler ilişkili HTML öğelerini güncelleştirir. Örneğin, TodoItem başlık ve Isdone özellikleri için gözlemlenenler sahiptir:

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

Ayrıca, koddaki bir observable 'a abone olabilirsiniz. Örneğin, TodoItem sınıfı "Isdone" ve "title" özelliklerindeki değişikliklere abone olur:

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**Modeli görüntüle**

Görünüm modeli Todo. ViewModel. js ' de tanımlanmıştır. Görünüm modeli, uygulamanın HTML sayfası öğelerini etki alanı verilerine bağlandığı merkezi bir noktasıdır. SPA şablonunda, görünüm modeli bir todoLists observable dizisi içerir. Görünüm modelinde aşağıdaki kod, bağlamaları uygulamak için altını gizlemeyi söyler:

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML ve veri bağlama

Sayfa için ana HTML, görünümler/Home/Index. cshtml içinde tanımlanmıştır. Veri bağlamayı kullandığımızda, HTML yalnızca gerçekten işlenmiş olan şablona yönelik bir şablondur. Altını gizleme *bildirim temelli* bağlamaları kullanır. Öğeye bir "Data-bind" özniteliği ekleyerek sayfa öğelerini verilere bağlarsınız. Altını gizleme belgelerinden alınan çok basit bir örnek aşağıda verilmiştir:

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

Bu örnekte, altını gizleme **&lt;span&gt;** öğesinin içeriğini `myItems.count()`değeriyle güncelleştirir. Bu değer değiştiğinde, altını gizleme belgeyi güncelleştirir.

Altını gizleme birçok farklı bağlama türü sağlar. SPA şablonunda kullanılan bağlamalardan bazıları şunlardır:

- **foreach**: bir döngüde yineleme yapmanızı sağlar ve listedeki her öğeye aynı biçimlendirmeyi uygulayabilirsiniz. Bu, yapılacaklar listelerini ve yapılacaklar öğelerini işlemek için kullanılır. **Foreach**içinde bağlamalar, listenin öğelerine uygulanır.
- **görünür**: Görünürlüğü değiştirmek için kullanılır. Bir koleksiyon boş olduğunda işaretlemeyi gizleyin veya hata iletisini görünür hale getirin.
- **değer**: form değerlerini doldurmak için kullanılır.
- **tıklama**: bir tıklama olayını görünüm modelinde bir işleve bağlar.

## <a name="anti-csrf-protection"></a>Anti-CSRF koruması

Siteler arası Istek forgery (CSRF), kötü niyetli bir sitenin kullanıcının şu anda oturum açtığı bir güvenlik açığı olan siteye istek gönderdiği bir saldırıya neden olur. ASP.NET MVC, CSRF saldırılarını önlemeye yardımcı olmak için, istek doğrulama belirteçleri olarak da adlandırılan, güvenlik *yumuşatma belirteçlerini*kullanır. Fikir, sunucunun rastgele oluşturulmuş bir belirteci bir Web sayfasına yerleştirmesinden yarar. İstemci sunucuya veri gönderdiğinde, istek iletisinde bu değeri içermesi gerekir.

Kötü amaçlı sayfa, aynı kaynak ilkeleri nedeniyle kullanıcının belirteçlerini okuyamadığı için, karşı koruma belirteçleri çalışır. (Aynı kaynak ilkeleri, iki farklı sitede barındırılan belgelerin birbirlerinin içeriğine erişmesini önler.)

ASP.NET MVC, [antiforgery](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx) sınıfı ve [[Validateantiforgeryıtoken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx) özniteliği aracılığıyla, korsanlığa karşı koruma belirteçleri için yerleşik destek sağlar. Şu anda bu işlev Web API 'sinde yerleşik değildir. Ancak, SPA şablonu, Web API 'SI için özel bir uygulama içerir. Bu kod, çözümün Filters klasöründe bulunan `ValidateHttpAntiForgeryTokenAttribute` sınıfında tanımlanır. Web API 'sindeki Anti-CSRF hakkında daha fazla bilgi edinmek için bkz. [siteler arası Istek forgery (CSRF) saldırılarını önleme](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md).

## <a name="conclusion"></a>Sonuç

SPA şablonu, modern ve etkileşimli Web uygulamalarını hızlı bir şekilde yazmaya başlamanızı sağlayacak şekilde tasarlanmıştır. Veri ve uygulama mantığındaki sunumu (HTML biçimlendirmesi) ayırmak için altını gizleme. js kitaplığını kullanır. Ancak altını gizleme, SPA oluşturmak için kullanabileceğiniz tek JavaScript kitaplığı değildir. Diğer bazı seçenekleri araştırmak istiyorsanız [topluluk tarafından oluşturulan Spa şablonlarına](../templates/index.md)göz atın.
