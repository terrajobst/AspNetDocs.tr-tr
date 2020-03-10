---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: bir ASP.NET MVC 5 uygulamasında EF ile eşzamanlılık Işleme'
description: Bu öğreticide, birden fazla kullanıcı aynı anda aynı varlığı güncelleştirilişinde, çakışmaları işlemek için iyimser eşzamanlılık kullanımı gösterilmektedir.
author: tdykstra
ms.author: riande
ms.topic: tutorial
ms.date: 01/15/2019
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 43c5fdff5601c9bff32300d3460de0079a498d28
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616111"
---
# <a name="tutorial-handle-concurrency-with-ef-in-an-aspnet-mvc-5-app"></a>Öğretici: bir ASP.NET MVC 5 uygulamasında EF ile eşzamanlılık Işleme

Önceki öğreticilerde, verileri güncelleştirme hakkında daha fazla öğrenirsiniz. Bu öğreticide, birden fazla kullanıcı aynı anda aynı varlığı güncelleştirilişinde, çakışmaları işlemek için iyimser eşzamanlılık kullanımı gösterilmektedir. `Department` varlıkla birlikte çalışan Web sayfalarını, eşzamanlılık hatalarını işleyecek şekilde değiştirirsiniz. Aşağıdaki çizimler, bir eşzamanlılık çakışması oluşursa görüntülenen bazı iletiler dahil olmak üzere, düzenleme ve silme sayfalarını gösterir.

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Eşzamanlılık çakışmaları hakkında bilgi edinin
> * İyimser eşzamanlılık ekleyin
> * Bölüm denetleyicisini değiştirme
> * Eşzamanlılık işlemeyi test etme
> * Silme sayfası

## <a name="prerequisites"></a>Önkoşullar

* [Zaman Uyumsuz ve Saklı Yordamlar](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="concurrency-conflicts"></a>Eşzamanlılık çakışmaları

Bir Kullanıcı bir varlığın verilerini düzenlemek için bir varlık verileri görüntülediğinde bir eşzamanlılık çakışması oluşur ve sonra, ilk kullanıcının değişikliği veritabanına yazılmadan önce diğer Kullanıcı aynı varlığın verilerini günceller. Bu tür çakışmaların algılanmasını etkinleştirmezseniz, veritabanını güncelleştirme son olarak diğer kullanıcının değişikliklerinin üzerine yazar. Birçok uygulamada, bu risk kabul edilebilir: birkaç Kullanıcı veya birkaç güncelleştirme varsa veya bazı değişikliklerin üzerine yazılırsa gerçekten önemli değilse, eşzamanlılık için programlama maliyeti avantajdan yararlanabilir. Bu durumda, uygulamayı eşzamanlılık çakışmalarını işleyecek şekilde yapılandırmanız gerekmez.

### <a name="pessimistic-concurrency-locking"></a>Kötümser eşzamanlılık (kilitleme)

Uygulamanızın eşzamanlılık senaryolarında yanlışlıkla veri kaybını önlemesi gerekiyorsa, bunu yapmanın bir yolu veritabanı kilitlerini kullanmaktır. Bu, *Kötümser eşzamanlılık*olarak adlandırılır. Örneğin, bir veritabanından bir satırı okuyabilmeniz için, salt okunurdur veya güncelleştirme erişimi için bir kilit isteyin. Bir satırı güncelleştirme erişimi için kilitlerseniz, başka hiçbir kullanıcının satırı değiştirme sürecinde olan verilerin bir kopyasını alması için salt okunurdur veya güncelleştirme erişimi için bu satırı kilitlemesine izin verilmez. Bir satırı salt okuma erişimi için kilitlerseniz, diğerleri dosyayı salt okuma erişimi için de kilitleyip güncelleştirme için de kilitleyebilirler.

Kilitleri yönetmek dezavantajlara sahiptir. Program, karmaşık olabilir. Önemli veritabanı yönetim kaynakları gerektirir ve bir uygulamanın kullanıcı sayısı arttıkça performans sorunlarına neden olabilir. Bu nedenlerden dolayı, tüm veritabanı yönetim sistemleri Kötümser eşzamanlılık 'yi desteklemez. Entity Framework, BT için yerleşik destek sağlamaz ve bu öğretici bunu nasıl uygulayacağınızı göstermez.

### <a name="optimistic-concurrency"></a>İyimser Eşzamanlılık

Kötümser eşzamanlılık yerine *iyimser*eşzamanlılık yapılır. İyimser eşzamanlılık, eşzamanlılık çakışmalarının gerçekleşmesine ve sonra uygun şekilde yeniden davranmasını sağlar. Örneğin John, departmanlar düzenleme sayfasını çalıştırıyorsa, Ingilizce departmanı $350.000,00 olan **Bütçe** tutarını $0,00 olarak değiştirir.

John, **Kaydet**' i tıklamadan önce, kemal aynı sayfayı çalıştırır ve **başlangıç tarihi** alanını 9/1/2007 ' den 8/8/2013 ' e değiştirir.

John önce **Kaydet** ' e tıklar ve tarayıcı dizin sayfasına döndüğünde değişikliği görür, sonra gamze **Kaydet**' i tıklatır. Sonraki işlemin ne eşzamanlılık çakışmalarını nasıl ele tarafından belirlenir. Bazı seçenekler şunlardır:

- Bir kullanıcının hangi özelliği değiştirdiği ve yalnızca ilgili sütunları veritabanında güncelleştirdiğinden haberdar olabilirsiniz. Örnek senaryoda, iki kullanıcı tarafından farklı özellikler güncelleştirildiğinden hiçbir veri kaybolmaz. Ingilizce bölüme bir dahaki sefer ilk kez gözattığında, 8/8/2013 başlangıç tarihi ve sıfır dolar bütçesine sahip olan John 'ın ve kemal 'in yaptığı değişiklikleri görürler.

    Bu güncelleştirme yöntemi, veri kaybına neden olabilecek çakışmaların sayısını azaltabilir, ancak bir varlığın aynı özelliğinde rekabet değişiklikleri yapılırsa veri kaybını önleyebilir. Entity Framework bu şekilde çalışıp çalışmadığını, güncelleştirme kodunuzu nasıl uygulayadığınıza bağlıdır. Genellikle bir Web uygulamasında pratik değildir, çünkü bir varlığın tüm özgün özellik değerlerini ve yeni değerleri izlemek için büyük miktarlarda durum tutmanızı gerektirebilir. Büyük miktarlarda durum bulundurma, uygulama performansını etkileyebilir çünkü sunucu kaynakları gerektirir ya da Web sayfasının kendisine (örneğin, gizli alanlarda) veya bir tanımlama bilgisinde yer almalıdır.
- Gamze 'nin değişikliğini John 'ın değişikliğini geçersiz kılabilirsiniz. Ingilizce bölüme bir dahaki sefer gözattığında, 8/8/2013 ve geri yüklenen $350.000,00 değerini görür. Bu, *Istemci WINS* veya *son WINS* senaryosu olarak adlandırılır. (İstemciden gelen tüm değerler veri deposunda yer alacak şekilde önceliklidir.) Bu bölümün giriş bölümünde belirtildiği gibi, eşzamanlılık işleme için herhangi bir kodlama yapmazsanız, bu otomatik olarak gerçekleşir.
- Gamze 'nin değişikliğini veritabanında güncelleştirilmesini engelleyebilirsiniz. Genellikle bir hata iletisi görüntüler, verilerin geçerli durumunu gösterir ve yine de yapmak istiyorsa, kendi değişikliklerini yeniden uygular. Buna *Mağaza WINS* senaryosu denir. (Veri deposu değerleri, istemci tarafından gönderilen değerlere göre önceliklidir.) Bu öğreticide mağaza WINS senaryosunu uygulayacaksınız. Bu yöntem, bir kullanıcının neler olduğunu bildirmeden önce hiçbir değişikliğin üzerine yazılmamasını sağlar.

### <a name="detecting-concurrency-conflicts"></a>Eşzamanlılık çakışmalarını algılama

Entity Framework oluşturduğu [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) özel durumlarını işleyerek çakışmaları çözebilirsiniz. Bu özel durumların ne zaman throw hakkında bilgi edinmek için Entity Framework çakışmaları algılayabilmelidir. Bu nedenle, veritabanını ve veri modelini uygun şekilde yapılandırmanız gerekir. Çakışma algılamayı etkinleştirmeye yönelik bazı seçenekler şunlardır:

- Veritabanı tablosunda, bir satırın ne zaman değiştirildiğini belirlemede kullanılabilecek bir izleme sütunu ekleyin. Daha sonra Entity Framework SQL `Update` veya `Delete` komutlarının `Where` yan tümcesinde bu sütunu içerecek şekilde yapılandırabilirsiniz.

    İzleme sütununun veri türü genellikle [ROWVERSION](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)' dir. [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) değeri, satır her güncelleştirildiği zaman artılan sıralı bir sayıdır. Bir `Update` veya `Delete` komutunda, `Where` yan tümcesi, izleme sütununun (orijinal satır sürümü) orijinal değerini içerir. Güncelleştirilmekte olan satır başka bir kullanıcı tarafından değiştirilmişse, `rowversion` sütunundaki değer özgün değerden farklıdır, bu nedenle `Update` veya `Delete` deyimi `Where` yan tümcesi nedeniyle güncelleştirilecek satırı bulamaz. Entity Framework hiçbir satırın `Update` veya `Delete` komutuyla güncelleştirilmediğini bulduğunda (yani, etkilenen satırların sayısı sıfır olduğunda), bunu bir eşzamanlılık çakışması olarak yorumlar.
- Entity Framework, `Update` ve `Delete` komutlarının `Where` yan tümcesindeki tablodaki her sütunun özgün değerlerini içerecek şekilde yapılandırın.

    İlk seçenekte olduğu gibi, satırdaki herhangi bir şey satırın ilk okuduğundan beri değiştiyse, `Where` yan tümcesi güncelleştirilecek bir satır döndürmez, bu da Entity Framework eşzamanlılık çakışması olarak yorumlar. Birçok sütunu olan veritabanı tablolarında, bu yaklaşım çok büyük `Where` yan tümceleri oluşmasına neden olabilir ve büyük miktarlarda durum tutmanızı gerektirebilir. Daha önce belirtildiği gibi, büyük miktarlarda durumu korumak uygulama performansını etkileyebilir. Bu nedenle bu yaklaşım genellikle önerilmez ve bu öğreticide kullanılan yöntem değildir.

    Bu yaklaşımı eşzamanlılık 'e uygulamak istiyorsanız, [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) özniteliğini bunlara ekleyerek eşzamanlılık izlemek istediğiniz varlıktaki tüm birincil anahtar olmayan Özellikleri işaretlemeniz gerekir. Bu değişiklik, Entity Framework `UPDATE` deyimlerinin SQL `WHERE` yan tümcesindeki tüm sütunları içermesini sağlar.

Bu öğreticinin geri kalanında `Department` varlığına bir [ROWVERSION](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) izleme özelliği ekleyecek, bir denetleyici ve görünümler oluşturacak ve her şeyin doğru şekilde çalıştığını doğrulamak için test edeceksiniz.

## <a name="add-optimistic-concurrency"></a>İyimser eşzamanlılık ekleyin

*Models\Department.cs*içinde `RowVersion`adlı bir izleme özelliği ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) özniteliği, bu sütunun veritabanına gönderilen `Update` ve `Delete` komutlarının `Where` yan tümcesine dahil edileceğini belirtir. Önceki SQL Server sürümleri, SQL [ROWVERSION](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) tarafından DEĞIŞTIRILMEDEN önce SQL [zaman damgası](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) veri türü kullandığından özniteliğe [zaman damgası](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) adı verilir. [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) için .NET türü bir bayt dizisidir.

Fluent API kullanmayı tercih ediyorsanız, aşağıdaki örnekte gösterildiği gibi izleme özelliğini belirtmek için [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) yöntemini kullanabilirsiniz:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Bir özellik ekleyerek, veritabanı modelini değiştirdiğiniz için başka bir geçiş yapmanız gerekir. Paket Yöneticisi konsolunda (PMC) aşağıdaki komutları girin:

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-department-controller"></a>Bölüm denetleyicisini değiştirme

*Controllers\DepartmentController.cs*içinde `using` bir ifade ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

*DepartmentController.cs* dosyasında, "LastName" sözcüğünün dört yinelemesini "FullName" olarak değiştirin, böylece Departman Yöneticisi açılan listeleri yalnızca soyadı değil, eğitmenin tam adını içerecektir.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

`HttpPost` `Edit` yöntemi için mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`FindAsync` yöntemi null döndürürse, departman başka bir kullanıcı tarafından silindi. Gösterilen kod, düzenleme sayfasının bir hata iletisiyle yeniden görüntülenebilmesi için bir departman varlığı oluşturmak üzere postalanan form değerlerini kullanır. Alternatif olarak, departman alanlarını yeniden görüntülemeden yalnızca bir hata iletisi görüntülediğinizde, departman varlığını yeniden oluşturmanız gerekmez.

Görünüm özgün `RowVersion` değerini gizli bir alana depolar ve yöntemi bunu `rowVersion` parametresinde alır. `SaveChanges`çağırmadan önce, bu özgün `RowVersion` özellik değerini varlık için `OriginalValues` koleksiyonuna koymanız gerekir. Ardından Entity Framework bir SQL `UPDATE` komutu oluşturduğunda, bu komut orijinal `RowVersion` değerine sahip bir satırı gösteren bir `WHERE` yan tümcesi içerecektir.

`UPDATE` komutundan hiçbir satır etkilenmiyorsa (özgün `RowVersion` değerine sahip hiçbir satır yoksa), Entity Framework `DbUpdateConcurrencyException` özel durumu oluşturur ve `catch` bloğundaki kod, özel durum nesnesinden etkilenen `Department` varlığını alır.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Bu nesne, Kullanıcı tarafından `Entity` özelliğinde girilen yeni değerleri içerir ve `GetDatabaseValues` yöntemini çağırarak veritabanından okunan değerleri alabilirsiniz.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

`GetDatabaseValues` yöntemi, bir kullanıcı veritabanından satırı siliyorsa null değerini döndürür; Aksi takdirde, `Department` özelliklerine erişebilmek için döndürülen nesneyi `Department` sınıfına atamalısınız. (Zaten silme işlemi yaptığınız için `databaseEntry`, yalnızca bölüm `FindAsync` yürütüldükten sonra ve `SaveChanges` yürütmeden önce silinmişse null olur.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Daha sonra, kod, Kullanıcı tarafından düzenleme sayfasına girilen verilerden farklı olan her bir sütun için özel bir hata iletisi ekler:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

Daha uzun bir hata iletisi ne olduğunu ve bunun ne yapılacağını açıklar:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Son olarak kod, `Department` nesnesinin `RowVersion` değerini veritabanından alınan yeni değer olarak ayarlar. Bu yeni `RowVersion` değeri, düzenleme sayfası yeniden görüntülenirken gizli alanda saklanır ve Kullanıcı **Kaydet**' i tıkladığında, düzenleme sayfasının yeniden görüntülenmesinden bu yana yalnızca gerçekleşen eşzamanlılık hataları yakalanacaktır.

*Views\Department\Edit.cshtml*' de, `DepartmentID` özelliğinin Gizli alanını hemen takip eden `RowVersion` özellik değerini kaydetmek için bir gizli alan ekleyin:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="test-concurrency-handling"></a>Eşzamanlılık işlemeyi test etme

Siteyi çalıştırın ve **Departmanlar**' a tıklayın.

Ingilizce departman için **düzenleme** köprüsüne sağ tıklayın ve **Yeni sekmesinde aç** ' ı seçin ve ardından İngilizce bölümünün **düzenleme** Köprüsü ' ne tıklayın. İki sekme aynı bilgileri görüntüler.

İlk tarayıcı sekmesinde bir alanı değiştirin ve **Kaydet**' e tıklayın.

Tarayıcı, değiştirilen değeri olan dizin sayfasını gösterir.

İkinci tarayıcı sekmesinde bir alanı değiştirin ve **Kaydet**' e tıklayın. Bir hata iletisi görürsünüz:

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

Yeniden **Kaydet** ' e tıklayın. İkinci tarayıcı sekmesine girdiğiniz değer, ilk tarayıcıda değiştirdiğiniz verilerin özgün değeri ile birlikte kaydedilir. Dizin sayfası göründüğünde kaydedilen değerleri görürsünüz.

## <a name="update-the-delete-page"></a>Silme sayfası

Silme sayfası için Entity Framework, başka birinin departmanı benzer bir şekilde düzenlemesinden kaynaklanan eşzamanlılık çakışmalarını algılar. `HttpGet` `Delete` yöntemi onay görünümünü görüntülediğinde, görünüm, gizli bir alanda orijinal `RowVersion` değerini içerir. Bu değer daha sonra Kullanıcı silme işlemini onayladığında çağrılan `HttpPost` `Delete` yöntemi için kullanılabilir. Entity Framework, SQL `DELETE` komutu oluşturduğunda, özgün `RowVersion` değerine sahip bir `WHERE` yan tümcesi içerir. Komut, sıfır satır etkilemesiyle sonuçlanırsa (satır silme onayı sayfası görüntülendikten sonra değiştirildiğinde), bir eşzamanlılık özel durumu oluşturulur ve onay sayfasını bir hata iletisiyle yeniden görüntülemek için `HttpGet Delete` yöntemi bir hata bayrağıyla `true` olarak çağırılır. Satır başka bir kullanıcı tarafından silindiği için sıfır satır etkilendi ve bu durumda farklı bir hata iletisi görüntülenir.

*DepartmentController.cs*' de `HttpGet` `Delete` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Yöntemi, sayfanın bir eşzamanlılık hatasından sonra yeniden görüntülenip görüntülenmeyeceğini belirten isteğe bağlı bir parametresini kabul eder. Bu bayrak `true`, bir `ViewBag` özelliği kullanılarak görünüme bir hata mesajı gönderilir.

`HttpPost` `Delete` yönteminde (`DeleteConfirmed`adlı) kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

Az önce değiştirdiğiniz scafkatlanmış kodda, bu yöntem yalnızca bir kayıt KIMLIĞI kabul etti:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Bu parametreyi model Ciltçi tarafından oluşturulan bir `Department` varlık örneğine değiştirdiniz. Bu, kayıt anahtarına ek olarak `RowVersion` özellik değerine erişmenizi sağlar.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

Ayrıca `DeleteConfirmed` eylem yöntemi adını `Delete`olarak değiştirdiniz. `HttpPost` `Delete` yöntemi adlı scafkatmış kod, `HttpPost` yöntemine benzersiz bir imza vermek `DeleteConfirmed`. (CLR aşırı yüklenmiş yöntemlerin farklı yöntem parametrelerine sahip olmasını gerektirir.) İmzalar benzersiz olduğuna göre, MVC kuralını seçebilir ve `HttpPost` ve `HttpGet` silme yöntemleri için aynı adı kullanabilirsiniz.

Bir eşzamanlılık hatası yakalanmışsa, kod silme onayı sayfasını yeniden görüntüler ve bir eşzamanlılık hata mesajı görüntülemesi gerektiğini belirten bir bayrak sağlar.

*Views\Department\Delete.cshtml*' de, scafkatlama kodunu, DepartmentID ve rowversion özellikleri için bir hata iletisi alanı ve gizli alanları ekleyen aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

Bu kod `h2` ve `h3` başlıkları arasına bir hata iletisi ekler:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

`Administrator` alanındaki `FullName` `LastName` değiştirir:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Son olarak, `Html.BeginForm` deyimden sonra `DepartmentID` ve `RowVersion` özellikleri için gizli alanlar ekler:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

Departmanlar Dizin sayfasını çalıştırın. Ingilizce departman için **Sil** köprüsünü sağ tıklayın ve **Yeni sekmede aç** ' ı seçin ve ardından ilk sekmede İngilizce departman için **düzenleme** Köprüsü ' ne tıklayın.

İlk pencerede, değerlerden birini değiştirin ve **Kaydet**' e tıklayın.

Dizin sayfası değişikliği onaylar.

İkinci sekmede **Sil**' e tıklayın.

Eşzamanlılık hata iletisini görürsünüz ve departman değerleri şu anda veritabanında olan ile yenilenir.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

Yeniden **Sil** ' e tıklarsanız, departmanın silindiğini gösteren dizin sayfasına yönlendirilirsiniz.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET Data Access-önerilen kaynaklarda](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

Çeşitli eşzamanlılık senaryolarını işlemenin diğer yolları hakkında bilgi için bkz. [Iyimser eşzamanlılık desenleri](https://msdn.microsoft.com/data/jj592904) ve MSDN 'de [özellik değerleriyle çalışma](https://msdn.microsoft.com/data/jj592677) . Sonraki öğreticide, `Instructor` ve `Student` varlıkları için bir hiyerarşi başına tablo devralmanın nasıl uygulanacağı gösterilmektedir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Eşzamanlılık çakışmaları hakkında öğrenildi
> * İyimser eşzamanlılık eklendi
> * Değiştirilen departman denetleyicisi
> * Test edilen eşzamanlılık işleme
> * Silme sayfası güncelleştirildi

Veri modelinde devralmayı nasıl uygulayacağınızı öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Veri modelinde devralma uygulama](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
