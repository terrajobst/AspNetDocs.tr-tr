---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: ASP.NET MVC uygulamasındaki Entity Framework temel CRUD Işlevlerini uygulama (2/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: eba146d2975e0dcf243facf7c205c4acfe40b6f6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595337"
---
# <a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>ASP.NET MVC uygulamasındaki Entity Framework temel CRUD Işlevlerini uygulama (2/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticide, Entity Framework ve LocalDB SQL Server kullanarak verileri depolayan ve görüntüleyen bir MVC uygulaması oluşturdunuz. Bu öğreticide, bu CRUD (oluşturma, okuma, güncelleştirme, silme) kodunu inceleyerek, MVC yapı iskelesi denetleyiciler ve görünümlerde sizin için otomatik olarak oluşturulur.

> [!NOTE]
> Denetleyiciniz ve veri erişim katmanı arasında bir soyutlama katmanı oluşturmak için depo deseninin uygulanması yaygın bir uygulamadır. Bu öğreticileri basit tutmak için, bu serideki bir sonraki öğreticiye kadar bir depoyu uygulamayacağız.

Bu öğreticide, aşağıdaki Web sayfalarını oluşturacaksınız:

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>Ayrıntı sayfası oluşturma

Bu özellik bir koleksiyon tuttuğundan, öğrenciler için yapı `Index` sayfa `Enrollments` özelliğini bıraktı. `Details` sayfasında, bir HTML tablosunda koleksiyonun içeriğini görüntüleriz.

 *Controllers\studentcontroller.cs*içinde, `Details` görünümü için eylem yöntemi, tek bir `Student` varlığını almak için `Find` yöntemini kullanır. 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 Anahtar değeri yönteme `id` parametresi olarak geçirilir ve Dizin sayfasındaki **Ayrıntılar** köprüde yol verilerinden gelir. 

1. *Views\student\details.cshtml*dosyasını açın. Her alan, aşağıdaki örnekte gösterildiği gibi `DisplayFor` Yardımcısı kullanılarak görüntülenir: 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. `EnrollmentDate` alanından sonra ve kapanış `fieldset` etiketinden hemen önce, aşağıdaki örnekte gösterildiği gibi, kayıtlar listesini göstermek için kod ekleyin:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    Bu kod, `Enrollments` Gezinti özelliğindeki varlıklar aracılığıyla döngü yapılır. Özelliğindeki her `Enrollment` varlık için kurs başlığını ve sınıfı görüntüler. Kurs başlığı, `Enrollments` varlığının `Course` gezinti özelliğinde depolanan `Course` varlığından alınır. Bu verilerin tümü, gerektiğinde veritabanından otomatik olarak alınır. (Başka bir deyişle, burada yavaş yükleme kullanıyorsunuz. `Courses` gezinti özelliği için *Eager yüklemesi* belirtmediniz, bu nedenle bu özelliğe ilk kez erişmeye çalıştığınızda, verileri almak için veritabanına bir sorgu gönderilir. Bu serinin ilerleyen kısımlarında [Ilgili verileri okuma](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) öğreticisinde geç yükleme ve Eager yükleme hakkında daha fazla bilgi edinebilirsiniz.)
3. **Öğrenciler** sekmesini seçerek ve Alexander Carson Için bir **Ayrıntılar** bağlantısına tıklayarak sayfayı çalıştırın. Seçili öğrenci için Kurslar ve notlar listesini görürsünüz:

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>Oluşturma sayfası güncelleştiriliyor

1. *Controllers\studentcontroller.cs*içinde, `HttpPost``Create` Action metodunu aşağıdaki kodla değiştirin ve bu yönteme bir `try-catch` bloğu ve [bind özniteliği](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) ekleyin: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    Bu kod, ASP.NET MVC model Ciltçi tarafından oluşturulan `Student` varlığını `Students` varlık kümesine ekler ve sonra değişiklikleri veritabanına kaydeder. (*Model Ciltçi* , bir form tarafından gönderilen verilerle çalışmanıza daha kolay hale GETIREN ASP.NET MVC işlevselliğine başvurur; bir model Bağlayıcısı, postalanan form değerlerini clr türlerine dönüştürür ve parametreleri parametreler ' de eylem yöntemine geçirir. Bu durumda, model Ciltçi, `Form` koleksiyonundan özellik değerlerini kullanarak sizin için bir `Student` varlığı başlatır.)

    `ValidateAntiForgeryToken` özniteliği, [siteler arası istek sahteciliği](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) saldırıları önlemeye yardımcı olur.

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.cshtml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. **Öğrenciler** sekmesini seçip **Yeni oluştur**' a tıklayarak sayfayı çalıştırın.

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    Bazı veri doğrulamaları varsayılan olarak işe yarar. Ad ve geçersiz bir tarih girin ve hata iletisini görmek için **Oluştur** ' a tıklayın.

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    Aşağıdaki Vurgulanan kodda model doğrulama denetimi gösterilmektedir.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    Tarihi, 9/1/2005 gibi geçerli bir değer olarak değiştirin ve yeni öğrencinin **Dizin** sayfasında göründüğünü görmek için **Oluştur** ' a tıklayın.

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>GÖNDERI düzenleme sayfasını güncelleştirme

*Controllers\studentcontroller.cs*içinde, `HttpGet` `Edit` yöntemi (`HttpPost` özniteliği olmadan) `Student` yönteminde gördüğünüz gibi seçili `Details` varlığını almak için `Find` yöntemini kullanır. Bu yöntemi değiştirmeniz gerekmez.

Ancak, bir `try-catch` bloğu ve [bind özniteliği](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx)eklemek için `HttpPost` `Edit` eylem yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

Bu kod, `HttpPost` `Create` yönteminde gördüğünüz gibi benzerdir. Ancak, model Ciltçi tarafından oluşturulan varlığı varlık kümesine eklemek yerine, bu kod varlığın değiştirildiğini belirten bir bayrak ayarlar. [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) yöntemi çağrıldığında, [değiştirilen](https://msdn.microsoft.com/library/system.data.entitystate.aspx) bayrak, veritabanı SATıRıNı güncelleştirmek için Entity Framework SQL deyimleri oluşturmasına neden olur. Veritabanı satırının tüm sütunları, kullanıcının değiştirenler de dahil olmak üzere güncelleştirilir ve eşzamanlılık çakışmaları yok sayılır. (Bu serinin sonraki bir öğreticide eşzamanlılık işleme hakkında bilgi edineceksiniz.)

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>Varlık durumları ve Attach ve SaveChanges yöntemleri

Veritabanı bağlamı, bellekteki varlıkların veritabanında karşılık gelen satırlarıyla eşitlenmiş olup olmadığını izler ve bu bilgiler `SaveChanges` yöntemini çağırdığınızda ne olacağını belirler. Örneğin, [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) yöntemine yeni bir varlık geçirdiğinizde, bu varlığın durumu `Added`olarak ayarlanır. Ardından, [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) yöntemini çağırdığınızda Veritabanı BAĞLAMı bir SQL `INSERT` komutu yayınlar.

Bir varlık[aşağıdaki durumlardan](https://msdn.microsoft.com/library/system.data.entitystate.aspx)birinde olabilir:

- `Added`. Varlık veritabanında henüz yok. `SaveChanges` yöntemi bir `INSERT` ifadesini vermelidir.
- `Unchanged`. `SaveChanges` yöntemi tarafından bu varlıkla ilgili hiçbir şey yapılması gerekmez. Veritabanından bir varlık okuduğunuzda, varlık bu durumla başlar.
- `Modified`. Varlığın özellik değerlerinin bazıları veya tümü değiştirildi. `SaveChanges` yöntemi bir `UPDATE` ifadesini vermelidir.
- `Deleted`. Varlık silinmek üzere işaretlendi. `SaveChanges` yöntemi bir `DELETE` ifadesini vermelidir.
- `Detached`. Varlık, veritabanı bağlamı tarafından izlenmiyor.

Bir masaüstü uygulamasında durum değişiklikleri genellikle otomatik olarak ayarlanır. Bir uygulamanın masaüstü türünde bir varlığı okur ve bazı özellik değerlerinde değişiklik yaparsınız. Bu, varlık durumunun otomatik olarak `Modified`olarak değiştirilmesine neden olur. `SaveChanges`çağırdığınızda Entity Framework, yalnızca değiştirdiğiniz gerçek özellikleri güncelleştiren bir SQL `UPDATE` ifadesini oluşturur.

Web uygulamalarının bağlantısı kesilen doğası bu sürekli sıraya izin vermez. Bir varlığı okuyan [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) , bir sayfa işlendikten sonra atılmış olur. `HttpPost` `Edit` eylem yöntemi çağrıldığında, yeni bir istek yapılır ve [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)'in yeni bir örneğine sahip olursunuz. bu nedenle, `SaveChanges`çağırdığınızda Entity Framework, veritabanının hangi özellikleri değiştireceğinin hiçbir yolu olmadığı `Modified.` için, veritabanı satırının tüm sütunlarını günceller.

SQL `Update` deyimin yalnızca kullanıcının gerçekten değiştirdiği alanları güncelleştirmesini istiyorsanız, `HttpPost` `Edit` yöntemi çağrıldığında kullanılabilir olmaları için özgün değerleri bir şekilde (gizli alanlar gibi) kaydedebilirsiniz. Ardından, özgün değerleri kullanarak bir `Student` varlık oluşturabilir, `Attach` yöntemini varlığın orijinal sürümüyle çağırabilir, varlığın değerlerini yeni değerlerle güncelleştirebilir ve daha fazla bilgi Için `SaveChanges.` çağırabilirsiniz. MSDN Data Developer Center 'daki [varlık durumları ve SaveChanges](https://msdn.microsoft.com/data/jj592676) ve [yerel veriler](https://msdn.microsoft.com/data/jj592872) konusuna bakın.

*Views\student\edit.exe* içindeki kod, *Create. cshtml*içinde gördüklerinize benzerdir ve hiçbir değişiklik yapılması gerekmez.

**Öğrenciler** sekmesini seçip bir **düzenleme** köprüsüne tıklayarak sayfayı çalıştırın.

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

Bazı verileri değiştirin ve **Kaydet**' e tıklayın. Değiştirilen verileri Dizin sayfasında görürsünüz.

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>Silme sayfası güncelleştiriliyor

*Controllers\studentcontroller.cs*içinde, `HttpGet` `Delete` yöntemi için şablon kodu, `Details` ve `Edit` yöntemlerinde gördüğünüz gibi seçili `Student` varlığı almak için `Find` yöntemini kullanır. Ancak, `SaveChanges` çağrısı başarısız olduğunda özel bir hata iletisi uygulamak için, bu yönteme ve buna karşılık gelen görünüme bazı işlevler eklersiniz.

Güncelleştirme ve oluşturma işlemleri için gördüğünüz gibi silme işlemleri için iki eylem yöntemi gerekir. GET isteğine yanıt olarak çağrılan yöntem, kullanıcıya silme işlemini onaylama veya iptal etme şansı veren bir görünüm görüntüler. Kullanıcı onu onayladığında, bir POST isteği oluşturulur. Bu durumda, `HttpPost` `Delete` yöntemi çağrılır ve bu yöntem aslında silme işlemini gerçekleştirir.

Veritabanı güncelleştirilirken oluşabilecek hataları işlemek için `HttpPost` `Delete` yöntemine bir `try-catch` bloğu ekleyeceksiniz. Bir hata oluşursa, `HttpPost` `Delete` yöntemi `HttpGet` `Delete` yöntemini çağırır, bu da bir hatanın oluştuğunu gösteren bir parametre geçiyor. `HttpGet Delete` yöntemi daha sonra hata iletisiyle birlikte onay sayfasını yeniden görüntüler ve kullanıcıya iptal veya yeniden deneme fırsatı verir.

1. `HttpGet` `Delete` eylem yöntemini aşağıdaki kodla değiştirin, bu hata raporlamayı yönetir: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    Bu kod, değişiklikleri kaydetme hatasından sonra döndürülüp çağrılmadığını belirten [isteğe bağlı](https://msdn.microsoft.com/library/dd264739.aspx) bir Boolean parametresini kabul eder. Bu parametre, `HttpGet` `Delete` yöntemi önceki bir hata olmadan çağrıldığında `false`. Veritabanı güncelleştirme hatasına yanıt olarak `HttpPost` `Delete` yöntemi tarafından çağrıldığında, parametre `true` ve görünüme bir hata mesajı geçirilir.
2. `HttpPost` `Delete` eylemi yöntemini (`DeleteConfirmed`), gerçek silme işlemini gerçekleştiren ve tüm veritabanı güncelleştirme hatalarını yakalayan aşağıdaki kodla değiştirin.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     Bu kod seçili varlığı alır, ardından varlığın durumunu `Deleted`olarak ayarlamak için [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) yöntemini çağırır. `SaveChanges` çağrıldığında bir SQL `DELETE` komutu oluşturulur. Ayrıca `DeleteConfirmed` eylem yöntemi adını `Delete`olarak değiştirdiniz. `HttpPost` `Delete` yöntemi adlı scafkatmış kod, `HttpPost` yöntemine benzersiz bir imza vermek `DeleteConfirmed`. (CLR aşırı yüklenmiş yöntemlerin farklı yöntem parametrelerine sahip olmasını gerektirir.) İmzalar benzersiz olduğuna göre, MVC kuralını seçebilir ve `HttpPost` ve `HttpGet` silme yöntemleri için aynı adı kullanabilirsiniz.

     Yüksek hacimli bir uygulamadaki performansı artırmak öncese, `Find` ve `Remove` yöntemlerini çağıran kod satırlarını, sarı vurgulamada gösterildiği gibi aşağıdaki kodla değiştirerek satırı almak için gereksiz bir SQL sorgusundan kaçınabilirsiniz:

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     Bu kod yalnızca birincil anahtar değerini kullanarak bir `Student` varlığı başlatır ve ardından varlık durumunu `Deleted`olarak ayarlar. Bu, Entity Framework varlığı silmek için ihtiyaç duymaktadır.

     Belirtildiği gibi, `HttpGet` `Delete` yöntemi verileri silmez. Bir GET isteğine yanıt olarak silme işlemi gerçekleştirme (veya bu konuyla ilgili olarak herhangi bir düzenleme işlemi, oluşturma işlemi yapma veya verileri değiştiren başka bir işlem) güvenlik riski oluşturur. Daha fazla bilgi için bkz. ASP.NET MVC Ipucu #46 —, Stephen Walther 'un blogundaki [güvenlik delikleri oluşturdıklarından, DELETE bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) .
3. *Views\student\delete.exe*' de, aşağıdaki örnekte gösterildiği gibi `h2` başlığı ve `h3` başlığı arasına bir hata iletisi ekleyin:

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     **Öğrenciler** sekmesini seçip bir **Delete** köprüsüne tıklayarak sayfayı çalıştırın:

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. **Sil**' e tıklayın. Dizin sayfası, silinen öğrenci olmadan görüntülenir. (Bu serinin ilerleyen kısımlarında bulunan [eşzamanlılık](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) öğreticisinde işlem sırasında kodu işleme hatası hakkında bir örnek görürsünüz.)

## <a name="ensuring-that-database-connections-are-not-left-open"></a>Veritabanı bağlantılarının açık bırakılması doğrulanıyor

Veritabanı bağlantılarının düzgün şekilde kapatıldığından ve serbest bırakıldığı kaynakların serbest bırakıldığından emin olmak için, içerik örneğinin atıldığı konusunda görmeniz gerekir. Bu nedenle, aşağıdaki örnekte gösterildiği gibi, yapı iskelesi kodu, *StudentController.cs*içinde `StudentController` sınıfının sonunda bir [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) yöntemi sağlar:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

Temel `Controller` sınıfı `IDisposable` arabirimini zaten uyguluyor, bu nedenle bu kod yalnızca bağlam örneğini açıkça atmak için `Dispose(bool)` yöntemine bir geçersiz kılma ekler.

## <a name="summary"></a>Özet

Artık `Student` varlıkları için basit CRUD işlemleri gerçekleştiren tamamen bir sayfa kümesine sahipsiniz. Veri alanları için UI öğeleri oluşturmak üzere MVC yardımcıları kullandınız. MVC yardımcıları hakkında daha fazla bilgi için bkz. [HTML Yardımcıları kullanarak form işleme](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (sayfa MVC 3 için, ancak MVC 4 için hala geçerlidir).

Sonraki öğreticide, sıralama ve sayfalama ekleyerek dizin sayfasının işlevlerini genişletebilirsiniz.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Önceki](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [İleri](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
