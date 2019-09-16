---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 'Öğretici: MVC 5 Web uygulaması için gelişmiş EF senaryoları hakkında bilgi edinin'
description: Bu öğreticide, Entity Framework Code First kullanan ASP.NET Web uygulamaları geliştirmeye yönelik temel bilgileri aşdığınızda bilmeniz gereken birkaç konu sunulmaktadır.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/16/2019
ms.locfileid: "58425281"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a>Öğretici: MVC 5 Web uygulaması için gelişmiş EF senaryoları hakkında bilgi edinin

Önceki öğreticide, hiyerarşi başına tablo devralma uyguladık. Bu öğreticide, Entity Framework Code First kullanan ASP.NET Web uygulamaları geliştirmeye yönelik temel bilgileri aşdığınızda bilmeniz gereken birkaç konu sunulmaktadır. İlk birkaç bölümde, kod boyunca size kılavuzluk eden ve Visual Studio 'Yu kullanarak görevleri tamamlamaya yönelik adım adım yönergeler vardır ve bu konuda daha fazla bilgi için kaynakların bağlantıları yer alan kısa tanıtımlar içeren çeşitli konular tanıtılmaktadır.

Bu konuların çoğu için, zaten oluşturduğunuz sayfalarla çalışacaksınız. Ham SQL 'i toplu güncelleştirmeler yapmak üzere kullanmak için, veritabanındaki tüm kursların kredi sayısını güncelleştiren yeni bir sayfa oluşturacaksınız:

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Ham SQL sorguları gerçekleştirme
> * Hiçbir izleme sorgusu gerçekleştirme
> * Veritabanına gönderilen SQL sorgularını inceleyin

Şunları da öğreneceksiniz:

> [!div class="checklist"]
> * Soyutlama katmanı oluşturma
> * Proxy sınıfları
> * Otomatik değişiklik algılama
> * Otomatik doğrulama
> * Entity Framework güç araçları
> * Entity Framework kaynak kodu

## <a name="prerequisite"></a>Önkoşul

* [Devralma Uygulama](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a>Ham SQL sorguları gerçekleştirme

Entity Framework Code First API 'SI, SQL komutlarını doğrudan veritabanına geçirmenize olanak sağlayan yöntemleri içerir. Şu seçenekleriniz vardır:

- Varlık türleri döndüren sorgular için [Dbset. SQLQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) yöntemini kullanın. Döndürülen nesneler `DbSet` nesne tarafından beklenen türde olmalıdır ve izlemeyi kapatmadığınız takdirde veritabanı bağlamı tarafından otomatik olarak izlenir. ( [Asnotracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) yöntemi hakkında aşağıdaki bölüme bakın.)
- Varlık olmayan türler döndüren sorgular için [Database. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) yöntemini kullanın. Döndürülen veriler, varlık türlerini almak için bu yöntemi kullanıyor olsanız bile veritabanı bağlamı tarafından izlenmez.
- Sorgu olmayan komutlar için [Database. ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) komutunu kullanın.

Entity Framework kullanmanın avantajlarından biri, kodunuzun veri depolarken belirli bir yönteme çok benzemesidir. Bunu sizin için SQL sorguları ve komutları oluşturarak yapar, bu da sizi kendiniz yazmak zorunda kalmaktan kurtarır. Ancak, el ile oluşturduğunuz belirli SQL sorgularını çalıştırmanız gerektiğinde olağanüstü senaryolar vardır ve bu yöntemler bu tür özel durumları idare etmek için bu yöntemleri mümkün kılar.

Her zaman doğru olduğu gibi, bir Web uygulamasında SQL komutları yürüttüğünüzde, sitenizi SQL ekleme saldırılarına karşı korumak için önlemler almalısınız. Bunu yapmanın bir yolu, bir Web sayfası tarafından gönderilen dizelerin SQL komutları olarak yorumlanamadığından emin olmak için parametreli sorgular kullanmaktır. Bu öğreticide Kullanıcı girişini bir sorguyla tümleştirdiğinizde parametreli sorgular kullanacaksınız.

### <a name="calling-a-query-that-returns-entities"></a>Varlıkları döndüren bir sorgu çağırma

[&lt;DbsetTEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx) sınıfı, türünde `TEntity`bir varlık döndüren bir sorguyu yürütmek için kullanabileceğiniz bir yöntem sağlar. Bunun nasıl çalıştığını görmek için, `Details` `Department` denetleyicinin yöntemindeki kodu değiştirirsiniz.

`db.Departments.FindAsync` *DepartmentController.cs* `Details` ' de, yönteminde aşağıdaki vurgulanmış kodda gösterildiği gibi yöntem çağrısını bir `db.Departments.SqlQuery` yöntem çağrısıyla değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

Yeni kodun doğru şekilde çalıştığını doğrulamak için **Departmanlar** sekmesini seçin ve sonra departmanlardan birine ilişkin **ayrıntıları** izleyin. Tüm verilerin beklenen şekilde görüntülendiğinden emin olun.

### <a name="calling-a-query-that-returns-other-types-of-objects"></a>Diğer nesne türlerini döndüren bir sorgu çağırma

Daha önce, yaklaşık bir kayıt tarihi için öğrenci sayısını gösteren hakkında sayfasında bir öğrenci istatistikleri Kılavuzu oluşturdunuz. *HomeController.cs* içinde bunu yapan kod LINQ kullanır:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

LINQ kullanmak yerine, bu verileri doğrudan SQL 'de alan kodu yazmak istediğinizi varsayalım. Bunu yapmak için, varlık nesneleri dışında bir şey döndüren bir sorgu çalıştırmanız gerekir, bu da [Database. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) yöntemini kullanmanız gereken anlamına gelir.

*HomeController.cs*içinde, aşağıdaki vurgulanmış kodda gösterildiği gibi, `About` yöntemindeki LINQ ifadesini bir SQL ifadesiyle değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

Hakkında sayfasını çalıştırın. Daha önce yaptığı verilerin aynısını görüntülediğini doğrulayın.

### <a name="calling-an-update-query"></a>Güncelleştirme sorgusu çağırma

Contoso Üniversitesi yöneticilerinin veritabanında toplu değişiklikler gerçekleştirebilmesini istediğini varsayalım (her kurs için kredilerin sayısını değiştirme gibi). Üniversitenin çok sayıda kursu varsa, bunların tümünü varlıklar olarak almak ve tek tek değiştirmek verimsiz olur. Bu bölümde, kullanıcının tüm kurslar için kredi sayısını değiştirecek bir faktör belirtmesini sağlayan bir Web sayfası uygulayacaksınız ve bir SQL `UPDATE` ifadesini yürüterek değişikliği yaparsınız. 

*CourseController.cs*' de, `UpdateCourseCredits` ve `HttpPost`için `HttpGet` yöntemleri ekleyin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

Denetleyici bir `HttpGet` isteği işlediğinde, `ViewBag.RowsAffected` değişkende hiçbir şey döndürülmez ve Görünüm boş bir metin kutusu ve bir Gönder düğmesi görüntüler.

**Güncelleştirme** düğmesine tıklandığında `HttpPost` , yöntemi çağrılır ve `multiplier` metin kutusuna girilen değere sahiptir. Kod daha sonra, kursları güncelleştiren SQL 'i yürütür ve etkilenen satır sayısını `ViewBag.RowsAffected` değişkende görünüme döndürür. Görünüm söz konusu değişkende bir değer aldığında, metin kutusu ve Gönder düğmesi yerine, güncellenen satır sayısını görüntüler.

*CourseController.cs*' de, `UpdateCourseCredits` yöntemlerden birine sağ tıklayın ve ardından **Görünüm Ekle**' ye tıklayın. **Görünüm Ekle** iletişim kutusu görünür. Varsayılanları bırakın ve **Ekle**' yi seçin.

*Views\course\updatecoursecredıts.exe*' de, şablon kodunu şu kodla değiştirin:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

**Kurs sekmesini** seçerek `http://localhost:50205/Course/UpdateCourseCredits`yöntemi çalıştırın, sonra tarayıcının adres çubuğundaki URL 'nin sonuna "/UpdateCourseCredits" ekleyin (örneğin:). `UpdateCourseCredits` Metin kutusuna bir sayı girin:

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

Tıklayın **güncelleştirme**. Etkilenen satır sayısını görürsünüz.

Düzeltilen kredi sayısına sahip kurslar listesini görmek için **listeye geri** ' ye tıklayın.

Ham SQL sorguları hakkında daha fazla bilgi için bkz. MSDN 'de [Ham SQL sorguları](https://msdn.microsoft.com/data/jj592907) .

## <a name="no-tracking-queries"></a>İzleme sorguları yok

Bir veritabanı bağlamı tablo satırları aldığında ve bunları temsil eden varlık nesneleri oluşturduğunda, varsayılan olarak, bellekteki varlıkların veritabanında bulunan verilerle eşitlenmiş olup olmadığını izler. Bellekteki veriler önbellek olarak davranır ve bir varlığı güncelleştirdiğinizde kullanılır. Bağlam örnekleri genellikle kısa süreli olduğundan (her istek için yeni bir tane oluşturulup bırakıldığı) ve bir varlığı okuyan bağlam genellikle bu varlık yeniden kullanılmadan önce atıldığından, bu önbelleğe alma işlemi bir Web uygulamasında genellikle gereksizdir.

[Asnotracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) metodunu kullanarak bellekte varlık nesnelerinin izlenmesini devre dışı bırakabilirsiniz. Bunu yapmak isteyebileceğiniz tipik senaryolar şunlardır:

- Bir sorgu, izlemeyi kapatan büyük miktarda veriyi alır, performansı önemli ölçüde artırabilir.
- Bir varlığı güncelleştirmek için eklemek istiyorsunuz, ancak daha önce aynı varlığı farklı bir amaç için elde edersiniz. Varlık veritabanı bağlamı tarafından zaten izlenmekte olduğundan, değiştirmek istediğiniz varlığı iliştiremiyoruz. Bu durumu işlemenin bir yolu, önceki sorguyla birlikte `AsNoTracking` seçeneğini kullanmaktır.

[Asnotracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) yönteminin nasıl kullanılacağını gösteren bir örnek için, [Bu öğreticinin önceki sürümüne](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)bakın. Öğreticinin bu sürümü, düzenleme yönteminde model cilt tarafından oluşturulan bir varlıkta değiştirilen bayrağı ayarlanmamış, bu nedenle gerekli `AsNoTracking`değildir.

## <a name="examine-sql-sent-to-database"></a>Veritabanına gönderilen SQL 'i İncele

Bazen veritabanına gönderilen gerçek SQL sorgularını görmeniz yararlı olabilir. Önceki bir öğreticide, bunu yakalayıcısı kodunda nasıl yapılacağını gördünüz; Şimdi de bunu, yakalayıcısı kodu yazmadan yapmak için bazı yollar göreceksiniz. Bunu denemek için, basit bir sorguya bakacaksınız ve sonra yükleme, filtreleme ve sıralama gibi seçenekleri eklerken ne olacağı hakkında bilgi edineceksiniz.

*Denetleyici/kurs secontroller*' da, `Index` yöntemi geçici olarak durdurmak için yöntemi aşağıdaki kodla değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

Şimdi `return` ifadede bir kesme noktası ayarlayın (bu satırdaki imleç ile F9). Projeyi hata ayıklama modunda çalıştırmak için **F5** tuşuna basın ve kurs dizini sayfasını seçin. Kod kesme noktasına ulaştığında, `sql` değişkeni inceleyin. SQL Server gönderilen sorguyu görürsünüz. Bu basit `Select` bir ifadedir.

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

**Metin Görselleştirici**içinde sorguyu görmek için Büyüteç Camı ' na tıklayın.

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

Şimdi, kullanıcıların belirli bir departmanı filtreleyebilmesi için kurslar dizin sayfasına açılan bir liste ekleyeceksiniz. Kursları başlığa göre sıralarsınız ve `Department` gezinti özelliği için bir Eager yüklemesi belirlersiniz.

*CourseController.cs*içinde, `Index` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

`return` Deyimdeki kesme noktasını geri yükleyin.

Yöntemi, `SelectedDepartment` parametresindeki açılan listenin seçili değerini alır. Hiçbir şey seçilmezse, bu parametre null olur.

Tüm `SelectList` departmanları içeren bir koleksiyon, açılan listenin görünümüne geçirilir. `SelectList` Oluşturucuya geçirilen parametreler değer alanı adını, metin alanı adını ve seçilen öğeyi belirtin.

Deponun yöntemi için kod, `Department` gezinti özelliği için bir filtre ifadesi, bir sıralama düzeni ve bir Eager yüklemesi belirtir. `Get` `Course` Filtre ifadesi her zaman, `true` açılan listede hiçbir şey seçilmezse (yani, null) ' i `SelectedDepartment` döndürür.

*Views\course\ındex.cshtml*içinde, açılış `table` etiketinden hemen önce, açılan listeyi ve bir Gönder düğmesini oluşturmak için aşağıdaki kodu ekleyin:

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

Kesme noktası hala ayarlanmış durumdayken kurs dizini sayfasını çalıştırın. Sayfanın tarayıcıda görüntülenebilmesi için kodun bir kesme noktasıyla ilk kez devam etmesini sağlayın. Açılan listeden bir departman seçin ve **Filtrele**' ye tıklayın.

Bu kez, ilk kesme noktası, açılan liste için departmanlar sorgusu olacaktır. Bu `Course` sorguyu atlayın ve bir `query` sonraki kod, şimdi sorgunun nasıl göründüğünü görmek için kesme noktasına bir sonraki sefer ulaştığında değişkeni görüntüleyin. Aşağıdakine benzer bir şey göreceksiniz:

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

Sorgunun artık verileri `JOIN` verilerle birlikte `Course` yükleyen `Department` bir sorgu olduğunu ve bir `WHERE` yan tümce içerdiğine bakabilirsiniz.

`var sql = courses.ToString()` Satırı kaldırın.

## <a name="create-an-abstraction-layer"></a>Soyutlama katmanı oluşturma

Birçok geliştirici, Entity Framework ile çalışan kodun etrafında bir sarmalayıcı olarak depo ve iş birimi düzenlerini uygulamak için kod yazar. Bu desenler, veri erişim katmanı ve bir uygulamanın iş mantığı katmanı arasında bir soyutlama katmanı oluşturmak için tasarlanmıştır. Bu desenleri uygulamak, uygulamanızın veri deposundaki değişikliklerden yalıtılmış hale getirmenize yardımcı olabilir ve otomatik birim testi veya test odaklı geliştirmeyi (TDD) kolaylaştırabilir. Ancak, bu desenleri uygulamak için ek kod yazmak, birkaç nedenden dolayı EF kullanan uygulamalar için her zaman en iyi seçenektir:

- EF bağlam sınıfının kendisi, veri deposuna özgü koddan kodunuzun kendisini uygular.
- EF bağlam sınıfı, EF kullanarak yaptığınız veritabanı güncelleştirmeleri için bir iş birimi sınıfı işlevi görebilir.
- Entity Framework 6 ' da tanıtılan özellikler, depo kodu yazmadan TDD 'yi uygulamayı kolaylaştırır.

Deponun ve iş düzeni birimlerinin nasıl uygulanacağı hakkında daha fazla bilgi için, [Bu öğretici serisinin Entity Framework 5 sürümüne](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)bakın. Entity Framework 6 ' da TDD uygulama yolları hakkında bilgi için aşağıdaki kaynaklara bakın:

- [EF6, Mocking DbSets 'i daha kolay nasıl sunar](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [Bir sahte işlem çerçevesiyle test etme](https://msdn.microsoft.com/data/dn314429)
- [Kendi testinizde test Double](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a>Proxy sınıfları

Entity Framework varlık örnekleri oluşturduğunda (örneğin, bir sorgu yürüttüğünüzde), bu, genellikle varlık için proxy görevi gören dinamik olarak oluşturulan türetilmiş türün örnekleri olarak oluşturulur. Örneğin, aşağıdaki iki hata ayıklayıcı görüntüsünü inceleyin. İlk görüntüde, varlığın örneği oluşturulduktan hemen sonra `student` değişkenin beklenen `Student` tür olduğunu görürsünüz. İkinci görüntüde, veritabanından bir öğrenci varlığını okumak için EF kullanıldıktan sonra proxy sınıfını görürsünüz.

![Proxy sınıfından önce](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![Proxy sınıfından sonra](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

Bu proxy sınıfı, özelliği erişildiği zaman otomatik olarak eylem gerçekleştirmeye yönelik kancalar eklemek için varlığın bazı sanal özelliklerini geçersiz kılar. Bu mekanizmanın, yavaş yükleme için kullanıldığı bir işlev.

Çoğu zaman, bu proxy kullanımını bilmeniz gerekmez, ancak özel durumlar vardır:

- Bazı senaryolarda Entity Framework proxy örnekleri oluşturmasını engellemek isteyebilirsiniz. Örneğin, varlıkları Serileştirmeye başladığınızda, proxy sınıfları değil, genellikle POCO sınıflarının olmasını istersiniz. Serileştirme sorunlarından kaçınmak için bir yol, varlık nesneleri yerine veri aktarımı nesneleri (DTOs) seri hale getirmenin yanı [Entity Framework, Web API 'Sini kullanma](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) öğreticisinde gösterildiği gibi. Başka bir yöntem de [proxy oluşturmayı devre dışı bırakmanız](https://msdn.microsoft.com/data/jj592886.aspx).
- `new` İşlecini kullanarak bir varlık sınıfını örneklediğinizde, proxy örneği edinmezsiniz. Bu, yavaş yükleme ve otomatik değişiklik izleme gibi işlevleri edinmeyeceğiniz anlamına gelir. Bu genellikle normaldir; Genellikle, veritabanında olmayan yeni bir varlık oluşturmakta olduğunuz ve genellikle varlığı `Added`açıkça işaretlemezseniz değişiklik izlemeye ihtiyaç duymadığınızı, genellikle geç yüklemeye gerek kalmaz. Ancak, geç yüklemeye ihtiyacınız varsa ve değişiklik izlemeye ihtiyacınız varsa, `DbSet` sınıfının [Create](https://msdn.microsoft.com/library/gg679504.aspx) yöntemini kullanarak proxy ile yeni varlık örnekleri oluşturabilirsiniz.
- Bir proxy türünden gerçek bir varlık türü almak isteyebilirsiniz. Bir proxy türü örneğinin gerçek varlık türünü almak için `ObjectContext` sınıfının [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) yöntemini kullanabilirsiniz.

Daha fazla bilgi için bkz. MSDN 'de [proxy Ile çalışma](https://msdn.microsoft.com/data/JJ592886.aspx) .

## <a name="automatic-change-detection"></a>Otomatik değişiklik algılama

Entity Framework bir varlığın geçerli değerlerini özgün değerlerle karşılaştırarak bir varlığın nasıl değiştiğini (ve bu nedenle veritabanına gönderilmesi gereken güncelleştirmeleri) belirler. Özgün değerler, varlık sorgulandığında veya eklendiğinde saklanır. Otomatik değişiklik algılamaya neden olan yöntemlerin bazıları şunlardır:

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

Çok sayıda varlığı izliyorsanız ve bu yöntemlerden birini bir döngüde birçok kez çağırırsanız, otomatik değişiklik algılamayı geçici olarak devre dışı [bırakarak otomatik değişiklik](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) algılamayı el ile kapatarak önemli performans iyileştirmeleri alabilirsiniz. Daha fazla bilgi için bkz. MSDN 'de [değişiklikleri otomatik olarak algılama](https://msdn.microsoft.com/data/jj556205) .

## <a name="automatic-validation"></a>Otomatik doğrulama

`SaveChanges` Yöntemini çağırdığınızda, varsayılan olarak Entity Framework, veritabanını güncelleştirmeden önce tüm değiştirilen varlıkların tüm özelliklerindeki verileri doğrular. Çok sayıda varlığı güncelleştirdiyseniz ve verileri zaten doğruladıysanız, bu çalışma gereksizdir ve değişiklikleri kaydetme sürecini geçici olarak doğrulamayı devre dışı bırakarak daha az zaman alabilir. Bunu, [Validateonsaveenabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) özelliğini kullanarak yapabilirsiniz. Daha fazla bilgi için bkz. MSDN 'de [doğrulama](https://msdn.microsoft.com/data/gg193959) .

## <a name="entity-framework-power-tools"></a>Entity Framework güç araçları

[Entity Framework güç araçları](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) , bu öğreticilerde gösterilen veri modeli diyagramlarını oluşturmak için kullanılan bir Visual Studio eklentisi. Bu araçlar, veritabanını Code First ile kullanabilmeniz için mevcut bir veritabanındaki tabloları temel alan varlık sınıfları oluşturma gibi başka bir işlev da gerçekleştirebilir. Araçları yükledikten sonra, bağlam menülerinde bazı ek seçenekler görünür. Örneğin, **Çözüm Gezgini**bağlam sınıfınızı sağ tıkladığınızda, ve **Entity Framework** seçeneğini görürsünüz. Bu, size diyagram oluşturma olanağı sağlar. Code First kullanırken, diyagramdaki veri modelini değiştiremezsiniz, ancak anlaşılması daha kolay hale getirmek için nesnelerin etrafında gezinebilirsiniz.

![EF diyagramı](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a>Entity Framework kaynak kodu

Entity Framework 6 ' nın kaynak kodu [GitHub](https://github.com/aspnet/EntityFramework6)' da kullanılabilir. Hataları dosyalayabilirsiniz ve kendi geliştirmelerinizi, EF kaynak koduna katkıda bulabilirsiniz.

Kaynak kodu açık olsa da Entity Framework, Microsoft ürünü olarak tam olarak desteklenmektedir. Microsoft Entity Framework ekibi, her bir yayının kalitesini sağlamak için, hangi katkıların kabul edildiğini denetler ve tüm kod değişikliklerini sınar.

## <a name="acknowledgments"></a>Bilgilendirme

- Tom Dykstra, Bu öğreticinin orijinal sürümünü yazdı, EF 5 güncelleştirmesini birlikte yazdı ve EF 6 güncelleştirmesini yazdı. Tom, Microsoft Web platformu ve araçlar Içerik ekibi üzerinde bir üst düzey programlama yazdır.
- [Rick Anderson](https://blogs.msdn.com/b/rickandy/) (Twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)), EF 5 ve MVC 4 için öğreticiyi güncelleştirti ve EF 6 güncelleştirmesini birlikte yazdı. Rick, Microsoft 'un Azure ve MVC 'ye odaklanarak bir üst düzey programlama yazdır.
- [Rowa Miller](http://www.romiller.com) ve kod incelemeleriyle Entity Framework ekip yardımlı diğer üyeleri, ve EF 5 ve EF 6 için öğreticiyi güncelleştirtiğimiz sırada çok sayıda sorunu ayıklamada yardımcı oldu.

## <a name="troubleshoot-common-errors"></a>Sık karşılaşılan hataları giderme

### <a name="cannot-createshadow-copy"></a>Gölge kopya oluşturulamıyor

Hata Iletisi:

> Bu dosya zaten mevcutsa, '&lt;filename&gt;' kopyası oluşturulamıyor/gölge kopyası oluşturulamıyor.

Çözüm

Birkaç saniye bekleyin ve sayfayı yenileyin.

### <a name="update-database-not-recognized"></a>Güncelleştirme-veritabanı tanınmıyor

Hata iletisi ( `Update-Database` PMC 'deki komuttan):

> ' Update-Database ' terimi bir cmdlet, işlev, betik dosyası veya çalıştırılabilir programının adı olarak tanınmıyor. Adın yazımını denetleyin veya bir yol içerilip yolun doğru olduğundan emin olun ve yeniden deneyin.

Çözüm

Visual Studio 'dan çıkın. Projeyi yeniden açın ve yeniden deneyin.

### <a name="validation-failed"></a>Doğrulama başarısız oldu

Hata iletisi ( `Update-Database` PMC 'deki komuttan):

> Bir veya daha fazla varlık için doğrulama başarısız oldu. Daha fazla ayrıntı için bkz. ' EntityValidationErrors ' özelliği.

Çözüm

`Seed` Yöntem çalışırken bu sorunun bir nedeni doğrulama hatalardır. `Seed` Yöntemi hata ayıklamayla ilgili ipuçları için bkz. [dağıtım ve hata ayıklama Entity Framework (EF) DBS](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) .

### <a name="http-50019-error"></a>HTTP 500,19 hatası

Hata Iletisi:

> HTTP hatası 500,19-Iç sunucu hatası istenen sayfaya erişilemiyor çünkü sayfa için ilgili yapılandırma verileri geçersiz.

Çözüm

Bu hatanın tek bir yolu, her biri aynı bağlantı noktası numarasını kullanarak çözümün birden çok kopyasının olmasını sağlayabilir. Bu sorunu genellikle Visual Studio 'nun tüm örneklerinden çıkıp üzerinde çalışmakta olduğunuz projeyi yeniden başlatarak çözebilirsiniz. Bu işe yaramazsa, bağlantı noktası numarasını değiştirmeyi deneyin. Proje dosyasına sağ tıklayın ve ardından Özellikler ' e tıklayın. **Web** sekmesini seçin ve ardından **proje URL 'si** metin kutusunda bağlantı noktası numarasını değiştirin.

### <a name="error-locating-sql-server-instance"></a>SQL Server örneği bulunurken hata oluştu

Hata Iletisi:

> SQL Server bağlantı kurulurken ağla ilgili veya örneğe özgü bir hata oluştu. Sunucu bulunamadı veya erişilebilir durumda değil. Örnek adının doğru olduğundan ve SQL Server uzak bağlantılara izin verecek şekilde yapılandırıldığından emin olun. sağlayıcısını SQL ağ arabirimleri, hata: 26-belirtilen sunucu/örnek bulunurken hata oluştu)

Çözüm

Bağlantı dizesini denetleyin. Veritabanını el ile sildiyseniz, oluşturulmakta olan dizedeki veritabanının adını değiştirin.

## <a name="get-the-code"></a>Kodu alın

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

 Entity Framework kullanarak verilerle çalışma hakkında daha fazla bilgi için MSDN ve [ASP.NET Data Access-önerilen kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md)' a yönelik [EF belgeleri sayfasına](https://msdn.microsoft.com/data/ee712907) bakın.

Web uygulamanızı oluşturduktan sonra dağıtma hakkında daha fazla bilgi için, MSDN Kitaplığı 'nda [ASP.NET Web dağıtımı-önerilen kaynaklar](../../../../whitepapers/aspnet-web-deployment-content-map.md) bölümüne bakın.

Kimlik doğrulama ve yetkilendirme gibi MVC ile ilgili diğer konular hakkında daha fazla bilgi için, bkz. [ASP.NET MVC-önerilen kaynaklar](../recommended-resources-for-mvc.md).

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Ham SQL sorguları gerçekleştiriliyor
> * Hiçbir izleme sorgusu gerçekleştirilmedi
> * Veritabanına gönderilen incelenen SQL sorguları

Ayrıca şunları öğrendiniz:

> [!div class="checklist"]
> * Soyutlama katmanı oluşturma
> * Proxy sınıfları
> * Otomatik değişiklik algılama
> * Otomatik doğrulama
> * Entity Framework güç araçları
> * Entity Framework kaynak kodu

Bu, bir ASP.NET MVC uygulamasında Entity Framework kullanma hakkında bu öğretici serisini tamamlar. EF Database First hakkında daha fazla bilgi edinmek istiyorsanız, DB Ilk öğretici serisi ' ne bakın.
> [!div class="nextstepaction"]
> [Entity Framework Database First](../database-first-development/setting-up-database.md)