---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: Bir ASP.NET MVC uygulamasındaki Entity Framework eşzamanlılık işleme (7/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: b83f47c4-8521-4d0a-8644-e8f77e39733e
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9800a313879477f36a730e6a70c79bc06d403ae3
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074962"
---
# <a name="handling-concurrency-with-the-entity-framework-in-an-aspnet-mvc-application-7-of-10"></a>Bir ASP.NET MVC uygulamasındaki Entity Framework eşzamanlılık işleme (7/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki iki öğreticilerde ilgili verilerle çalıştık. Bu öğreticide eşzamanlılık işleme gösterilmektedir. `Department` varlıkla çalışan Web sayfaları oluşturacaksınız ve `Department` varlıkları düzenleme ve silme sayfaları eşzamanlılık hatalarını işleyecek. Aşağıdaki çizimler, bir eşzamanlılık çakışması oluşursa görüntülenen bazı iletiler dahil olmak üzere, dizin ve silme sayfalarını gösterir.

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>Eşzamanlılık Çakışmaları

Bir Kullanıcı bir varlığın verilerini düzenlemek için bir varlık verileri görüntülediğinde bir eşzamanlılık çakışması oluşur ve sonra, ilk kullanıcının değişikliği veritabanına yazılmadan önce diğer Kullanıcı aynı varlığın verilerini günceller. Bu tür çakışmaların algılanmasını etkinleştirmezseniz, veritabanını güncelleştirme son olarak diğer kullanıcının değişikliklerinin üzerine yazar. Birçok uygulamada, bu risk kabul edilebilir: birkaç Kullanıcı veya birkaç güncelleştirme varsa veya bazı değişikliklerin üzerine yazılırsa gerçekten önemli değilse, eşzamanlılık için programlama maliyeti avantajdan yararlanabilir. Bu durumda, uygulamayı eşzamanlılık çakışmalarını işleyecek şekilde yapılandırmanız gerekmez.

### <a name="pessimistic-concurrency-locking"></a>Kötümser eşzamanlılık (kilitleme)

Uygulamanızın eşzamanlılık senaryolarında yanlışlıkla veri kaybını önlemesi gerekiyorsa, bunu yapmanın bir yolu veritabanı kilitlerini kullanmaktır. Bu, *Kötümser eşzamanlılık*olarak adlandırılır. Örneğin, bir veritabanından bir satırı okuyabilmeniz için, salt okunurdur veya güncelleştirme erişimi için bir kilit isteyin. Bir satırı güncelleştirme erişimi için kilitlerseniz, başka hiçbir kullanıcının satırı değiştirme sürecinde olan verilerin bir kopyasını alması için salt okunurdur veya güncelleştirme erişimi için bu satırı kilitlemesine izin verilmez. Bir satırı salt okuma erişimi için kilitlerseniz, diğerleri dosyayı salt okuma erişimi için de kilitleyip güncelleştirme için de kilitleyebilirler.

Kilitleri yönetmek dezavantajlara sahiptir. Program, karmaşık olabilir. Bu, önemli ölçüde veritabanı yönetim kaynakları gerektirir ve bir uygulamanın kullanıcı sayısı arttıkça performans sorunlarına neden olabilir (yani, düzgün ölçeklenmez). Bu nedenlerden dolayı, tüm veritabanı yönetim sistemleri Kötümser eşzamanlılık 'yi desteklemez. Entity Framework, BT için yerleşik destek sağlamaz ve bu öğretici bunu nasıl uygulayacağınızı göstermez.

### <a name="optimistic-concurrency"></a>İyimser Eşzamanlılık

Kötümser eşzamanlılık yerine *iyimser*eşzamanlılık yapılır. İyimser eşzamanlılık, eşzamanlılık çakışmalarının gerçekleşmesine ve sonra uygun şekilde yeniden davranmasını sağlar. Örneğin John, departmanlar düzenleme sayfasını çalıştırıyorsa, Ingilizce departmanı $350.000,00 olan **Bütçe** tutarını $0,00 olarak değiştirir.

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

John, **Kaydet**' i tıklamadan önce, kemal aynı sayfayı çalıştırır ve **başlangıç tarihi** alanını 9/1/2007 ' den 8/8/2013 ' e değiştirir.

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

John önce **Kaydet** ' e tıklar ve tarayıcı dizin sayfasına döndüğünde değişikliği görür, sonra gamze **Kaydet**' i tıklatır. Sonraki işlemin ne eşzamanlılık çakışmalarını nasıl ele tarafından belirlenir. Bazı seçenekler şunlardır:

- Bir kullanıcının hangi özelliği değiştirdiği ve yalnızca ilgili sütunları veritabanında güncelleştirdiğinden haberdar olabilirsiniz. Örnek senaryoda, iki kullanıcı tarafından farklı özellikler güncelleştirildiğinden hiçbir veri kaybolmaz. Ingilizce bölüme bir dahaki sefer ilk kez gözattığında, 8/8/2013 başlangıç tarihi ve sıfır dolar bütçesine sahip olan John 'ın ve kemal 'in yaptığı değişiklikleri görürler.

    Bu güncelleştirme yöntemi, veri kaybına neden olabilecek çakışmaların sayısını azaltabilir, ancak bir varlığın aynı özelliğinde rekabet değişiklikleri yapılırsa veri kaybını önleyebilir. Entity Framework bu şekilde çalışıp çalışmadığını, güncelleştirme kodunuzu nasıl uygulayadığınıza bağlıdır. Genellikle bir Web uygulamasında pratik değildir, çünkü bir varlığın tüm özgün özellik değerlerini ve yeni değerleri izlemek için büyük miktarlarda durum tutmanızı gerektirebilir. Büyük miktarlarda durum bulundurma, uygulama performansını etkileyebilir çünkü sunucu kaynakları gerektirir veya Web sayfasının kendisine dahil olması gerekir (örneğin, gizli alanlarda).
- Gamze 'nin değişikliğini John 'ın değişikliğini geçersiz kılabilirsiniz. Ingilizce bölüme bir dahaki sefer gözattığında, 8/8/2013 ve geri yüklenen $350.000,00 değerini görür. Bu, *Istemci WINS* veya *son WINS* senaryosu olarak adlandırılır. (İstemci değerleri, veri deposundaki değerlere göre önceliklidir.) Bu bölümün giriş bölümünde belirtildiği gibi, eşzamanlılık işleme için herhangi bir kodlama yapmazsanız, bu otomatik olarak gerçekleşir.
- Gamze 'nin değişikliğini veritabanında güncelleştirilmesini engelleyebilirsiniz. Genellikle bir hata iletisi görüntüler, verilerin geçerli durumunu gösterir ve yine de yapmak istiyorsa, kendi değişikliklerini yeniden uygular. Buna *Mağaza WINS* senaryosu denir. (Veri deposu değerleri, istemci tarafından gönderilen değerlere göre önceliklidir.) Bu öğreticide mağaza WINS senaryosunu uygulayacaksınız. Bu yöntem, bir kullanıcının neler olduğunu bildirmeden önce hiçbir değişikliğin üzerine yazılmamasını sağlar.

### <a name="detecting-concurrency-conflicts"></a>Eşzamanlılık çakışmalarını algılama

Entity Framework oluşturduğu [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) özel durumlarını işleyerek çakışmaları çözebilirsiniz. Bu özel durumların ne zaman throw hakkında bilgi edinmek için Entity Framework çakışmaları algılayabilmelidir. Bu nedenle, veritabanını ve veri modelini uygun şekilde yapılandırmanız gerekir. Çakışma algılamayı etkinleştirmeye yönelik bazı seçenekler şunlardır:

- Veritabanı tablosunda, bir satırın ne zaman değiştirildiğini belirlemede kullanılabilecek bir izleme sütunu ekleyin. Daha sonra Entity Framework SQL `Update` veya `Delete` komutlarının `Where` yan tümcesinde bu sütunu içerecek şekilde yapılandırabilirsiniz.

    İzleme sütununun veri türü genellikle [ROWVERSION](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx)' dir. [Rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) değeri, satır her güncelleştirildiği zaman artılan sıralı bir sayıdır. Bir `Update` veya `Delete` komutunda, `Where` yan tümcesi, izleme sütununun (orijinal satır sürümü) orijinal değerini içerir. Güncelleştirilmekte olan satır başka bir kullanıcı tarafından değiştirilmişse, `rowversion` sütunundaki değer özgün değerden farklıdır, bu nedenle `Update` veya `Delete` deyimi `Where` yan tümcesi nedeniyle güncelleştirilecek satırı bulamaz. Entity Framework hiçbir satırın `Update` veya `Delete` komutuyla güncelleştirilmediğini bulduğunda (yani, etkilenen satırların sayısı sıfır olduğunda), bunu bir eşzamanlılık çakışması olarak yorumlar.
- Entity Framework, `Update` ve `Delete` komutlarının `Where` yan tümcesindeki tablodaki her sütunun özgün değerlerini içerecek şekilde yapılandırın.

    İlk seçenekte olduğu gibi, satırdaki herhangi bir şey satırın ilk okuduğundan beri değiştiyse, `Where` yan tümcesi güncelleştirilecek bir satır döndürmez, bu da Entity Framework eşzamanlılık çakışması olarak yorumlar. Birçok sütunu olan veritabanı tablolarında, bu yaklaşım çok büyük `Where` yan tümceleri oluşmasına neden olabilir ve büyük miktarlarda durum tutmanızı gerektirebilir. Daha önce belirtildiği gibi, büyük miktarlarda durumu korumak, sunucu kaynakları gerektirdiğinden veya Web sayfasının kendisine dahil olması gerektiğinden uygulama performansını etkileyebilir. Bu nedenle bu yaklaşım genellikle önerilmez ve bu öğreticide kullanılan yöntem değildir.

    Bu yaklaşımı eşzamanlılık 'e uygulamak istiyorsanız, [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) özniteliğini bunlara ekleyerek eşzamanlılık izlemek istediğiniz varlıktaki tüm birincil anahtar olmayan Özellikleri işaretlemeniz gerekir. Bu değişiklik, Entity Framework `UPDATE` deyimlerinin SQL `WHERE` yan tümcesindeki tüm sütunları içermesini sağlar.

Bu öğreticinin geri kalanında `Department` varlığına bir [ROWVERSION](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) izleme özelliği ekleyecek, bir denetleyici ve görünümler oluşturacak ve her şeyin doğru şekilde çalıştığını doğrulamak için test edeceksiniz.

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>Departman varlığına bir Iyimser eşzamanlılık özelliği ekleyin

*Models\Department.cs*içinde `RowVersion`adlı bir izleme özelliği ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=18-19)]

[Timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) özniteliği, bu sütunun veritabanına gönderilen `Update` ve `Delete` komutlarının `Where` yan tümcesine dahil edileceğini belirtir. Önceki SQL Server sürümleri, SQL [ROWVERSION](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) tarafından DEĞIŞTIRILMEDEN önce SQL [zaman damgası](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) veri türü kullandığından özniteliğe [zaman damgası](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) adı verilir. `rowversion` için .NET türü bir bayt dizisidir. Fluent API kullanmayı tercih ediyorsanız, aşağıdaki örnekte gösterildiği gibi izleme özelliğini belirtmek için [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) yöntemini kullanabilirsiniz:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

GitHub sorununa IsConcurrencyToken 'ın [Isrowversıon Ile değiştirme](https://github.com/aspnet/AspNetDocs/issues/302)bölümüne bakın.

Bir özellik ekleyerek, veritabanı modelini değiştirdiğiniz için başka bir geçiş yapmanız gerekir. Paket Yöneticisi konsolunda (PMC) aşağıdaki komutları girin:

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="create-a-department-controller"></a>Departman denetleyicisi oluşturma

Aşağıdaki ayarları kullanarak bir `Department` denetleyicisi ve diğer denetleyicilerle aynı şekilde görünümler oluşturun:

![Add_Controller_dialog_box_for_Department_controller](https://asp.net/media/2578041/Windows-Live-Writer_Handling-C.NET-MVC-Application-7-of-10h1_AFDC_Add_Controller_dialog_box_for_Department_controller_d1d9c788-f970-4d6a-9f5a-1eddc84330b7.png)

*Controllers\DepartmentController.cs*içinde `using` bir ifade ekleyin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

"LastName" öğesini bu dosyada her yerde (dört oluşum) "FullName" olarak değiştirin, böylece Departman Yöneticisi açılan listeleri yalnızca soyadı değil, eğitmenin tam adını içerecektir.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

`HttpPost` `Edit` yöntemi için mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Görünüm özgün `RowVersion` değerini gizli bir alanda depolar. Model Bağlayıcısı `department` örneğini oluşturduğunda, bu nesne, düzenleme sayfasındaki Kullanıcı tarafından girildiği gibi özgün `RowVersion` özellik değerine ve diğer özellikler için yeni değerlere sahip olur. Ardından Entity Framework bir SQL `UPDATE` komutu oluşturduğunda, bu komut orijinal `RowVersion` değerine sahip bir satırı gösteren bir `WHERE` yan tümcesi içerecektir.

`UPDATE` komutundan hiçbir satır etkilenmiyorsa (özgün `RowVersion` değerine sahip hiçbir satır yoksa), Entity Framework `DbUpdateConcurrencyException` özel durumu oluşturur ve `catch` bloğundaki kod, özel durum nesnesinden etkilenen `Department` varlığını alır. Bu varlığın her ikisi de veritabanından okunan değerlere ve Kullanıcı tarafından girilen yeni değerlere sahiptir:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Daha sonra, kod, Kullanıcı tarafından düzenleme sayfasına girilen verilerden farklı olan her bir sütun için özel bir hata iletisi ekler:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Daha uzun bir hata iletisi ne olduğunu ve bunun ne yapılacağını açıklar:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Son olarak kod, `Department` nesnesinin `RowVersion` değerini veritabanından alınan yeni değer olarak ayarlar. Bu yeni `RowVersion` değeri, düzenleme sayfası yeniden görüntülenirken gizli alanda saklanır ve Kullanıcı **Kaydet**' i tıkladığında, düzenleme sayfasının yeniden görüntülenmesinden bu yana yalnızca gerçekleşen eşzamanlılık hataları yakalanacaktır.

*Views\Department\Edit.cshtml*' de, `DepartmentID` özelliğinin Gizli alanını hemen takip eden `RowVersion` özellik değerini kaydetmek için bir gizli alan ekleyin:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml?highlight=17)]

*Views\Department\Index.cshtml*' de, satır bağlantılarını sola taşımak için mevcut kodu aşağıdaki kodla değiştirin ve sayfa başlığını ve sütun başlıklarını **yönetici** sütununda `LastName` yerine `FullName` görüntüleyecek şekilde değiştirin:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

## <a name="testing-optimistic-concurrency-handling"></a>Iyimser eşzamanlılık Işlemeyi test etme

Siteyi çalıştırın ve **Departmanlar**' a tıklayın:

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Kim Abercrombie için **düzenleme** köprüsünü sağ tıklayın ve **Yeni sekmede aç** ' ı seçin ve ardından Kim Abercrombie için köprü **Düzenle** ' ye tıklayın. İki pencere aynı bilgileri görüntüler.

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

İlk tarayıcı penceresinde bir alanı değiştirin ve **Kaydet**' e tıklayın.

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

Tarayıcı, değiştirilen değeri olan dizin sayfasını gösterir.

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

İkinci tarayıcı penceresinde herhangi bir alanı değiştirin ve **Kaydet**' e tıklayın.

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

İkinci tarayıcı penceresinde **Kaydet** ' e tıklayın. Bir hata iletisi görürsünüz:

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

Yeniden **Kaydet** ' e tıklayın. İkinci tarayıcıya girdiğiniz değer, ilk tarayıcıda değiştirdiğiniz verilerin özgün değeri ile birlikte kaydedilir. Dizin sayfası göründüğünde kaydedilen değerleri görürsünüz.

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>Silme sayfası güncelleştiriliyor

Silme sayfası için Entity Framework, başka birinin departmanı benzer bir şekilde düzenlemesinden kaynaklanan eşzamanlılık çakışmalarını algılar. `HttpGet` `Delete` yöntemi onay görünümünü görüntülediğinde, görünüm, gizli bir alanda orijinal `RowVersion` değerini içerir. Bu değer daha sonra Kullanıcı silme işlemini onayladığında çağrılan `HttpPost` `Delete` yöntemi için kullanılabilir. Entity Framework, SQL `DELETE` komutu oluşturduğunda, özgün `RowVersion` değerine sahip bir `WHERE` yan tümcesi içerir. Komut, sıfır satır etkilemesiyle sonuçlanırsa (satır silme onayı sayfası görüntülendikten sonra değiştirildiğinde), bir eşzamanlılık özel durumu oluşturulur ve onay sayfasını bir hata iletisiyle yeniden görüntülemek için `HttpGet Delete` yöntemi bir hata bayrağıyla `true` olarak çağırılır. Satır başka bir kullanıcı tarafından silindiği için sıfır satır etkilendi ve bu durumda farklı bir hata iletisi görüntülenir.

*DepartmentController.cs*' de `HttpGet` `Delete` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

Yöntemi, sayfanın bir eşzamanlılık hatasından sonra yeniden görüntülenip görüntülenmeyeceğini belirten isteğe bağlı bir parametresini kabul eder. Bu bayrak `true`, bir `ViewBag` özelliği kullanılarak görünüme bir hata mesajı gönderilir.

`HttpPost` `Delete` yönteminde (`DeleteConfirmed`adlı) kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Az önce değiştirdiğiniz scafkatlanmış kodda, bu yöntem yalnızca bir kayıt KIMLIĞI kabul etti:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

Bu parametreyi model Ciltçi tarafından oluşturulan bir `Department` varlık örneğine değiştirdiniz. Bu, kayıt anahtarına ek olarak `RowVersion` özellik değerine erişmenizi sağlar.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Ayrıca `DeleteConfirmed` eylem yöntemi adını `Delete`olarak değiştirdiniz. `HttpPost` `Delete` yöntemi adlı scafkatmış kod, `HttpPost` yöntemine benzersiz bir imza vermek `DeleteConfirmed`. (CLR aşırı yüklenmiş yöntemlerin farklı yöntem parametrelerine sahip olmasını gerektirir.) İmzalar benzersiz olduğuna göre, MVC kuralını seçebilir ve `HttpPost` ve `HttpGet` silme yöntemleri için aynı adı kullanabilirsiniz.

Bir eşzamanlılık hatası yakalanmışsa, kod silme onayı sayfasını yeniden görüntüler ve bir eşzamanlılık hata mesajı görüntülemesi gerektiğini belirten bir bayrak sağlar.

*Views\Department\Delete.cshtml*' de, scafkatli kodu, bazı biçimlendirme değişikliklerini yapan ve bir hata mesajı alanı ekleyen aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml?highlight=9,37,40,45-46)]

Bu kod `h2` ve `h3` başlıkları arasına bir hata iletisi ekler:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

`Administrator` alanındaki `FullName` `LastName` değiştirir:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

Son olarak, `Html.BeginForm` deyimden sonra `DepartmentID` ve `RowVersion` özellikleri için gizli alanlar ekler:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Departmanlar Dizin sayfasını çalıştırın. Ingilizce departman için **Sil** Köprüsü ' ne sağ tıklayın ve **Yeni pencerede aç** ' ı seçin ve ardından Ilk pencerede İngilizce bölümünün **düzenleme** Köprüsü ' ne tıklayın.

İlk pencerede, değerlerden birini değiştirin ve **Kaydet** ' e tıklayın:

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

Dizin sayfası değişikliği onaylar.

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

İkinci pencerede **Sil**' e tıklayın.

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

Eşzamanlılık hata iletisini görürsünüz ve departman değerleri şu anda veritabanında olan ile yenilenir.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

Yeniden **Sil** ' e tıklarsanız, departmanın silindiğini gösteren dizin sayfasına yönlendirilirsiniz.

## <a name="summary"></a>Özet

Bu, eşzamanlılık çakışmalarını işlemeye giriş işlemini tamamlar. Çeşitli eşzamanlılık senaryolarına yönelik diğer yollar hakkında daha fazla bilgi için bkz. [Iyimser eşzamanlılık desenleri](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx) ve Entity Framework ekip bloguna [özellik değerleriyle çalışma](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx) . Sonraki öğreticide, `Instructor` ve `Student` varlıkları için bir hiyerarşi başına tablo devralmanın nasıl uygulanacağı gösterilmektedir.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Önceki](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [İleri](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
