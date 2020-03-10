---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: "Öğretici: ASP.NET MVC 'de Entity Framework CRUD Işlevselliği uygulama | Microsoft Docs"
description: MVC yapı iskelesi denetleyiciler ve görünümlerde otomatik olarak oluşturulan oluşturma, okuma, güncelleştirme, silme (CRUD) kodunu gözden geçirin ve özelleştirin.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9ed388543dd54d209ff2a0b92df4f7659962582c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583162"
---
# <a name="tutorial-implement-crud-functionality-with-the-entity-framework-in-aspnet-mvc"></a>Öğretici: ASP.NET MVC 'de Entity Framework CRUD Işlevselliği uygulama

[Önceki öğreticide](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), ENTITY Framework (EF) 6 ve SQL Server LocalDB kullanarak veri depolayan ve GÖRÜNTÜLEYEN bir MVC uygulaması oluşturdunuz. Bu öğreticide, MVC yapı iskelesi, denetleyiciler ve görünümlerde sizin için otomatik olarak oluşturulan oluşturma, okuma, güncelleştirme, silme (CRUD) kodunu gözden geçirdikten ve özelleştirirsiniz.

> [!NOTE]
> Denetleyiciniz ve veri erişim katmanı arasında bir soyutlama katmanı oluşturmak için depo deseninin uygulanması yaygın bir uygulamadır. Bu öğreticileri basit tutmak ve EF 6 ' ı nasıl kullanacağınızı öğretmeniz için depoları kullanmaz. Depoların nasıl uygulanacağı hakkında bilgi için bkz. [ASP.NET Data Access Content Map](../../../../whitepapers/aspnet-data-access-content-map.md).

Oluşturduğunuz Web sayfalarına örnekler aşağıda verilmiştir:

![Öğrenci Ayrıntıları sayfasının ekran görüntüsü.](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Öğrenci oluşturma sayfasının ekran görüntüsü.](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Öğrenci silme sayfasına bir ekran görüntüsü.](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Ayrıntı sayfası oluşturma
> * Oluştur sayfasını Güncelleştir
> * HttpPost düzenleme yöntemini güncelleştirme
> * Silme sayfası
> * Veritabanı bağlantılarını kapat
> * İşlemleri işle

## <a name="prerequisites"></a>Önkoşullar

* [Entity Framework veri modelini oluşturma](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

## <a name="create-a-details-page"></a>Ayrıntı sayfası oluşturma

Bu özellik bir koleksiyon tuttuğundan, öğrenciler için yapı `Index` sayfa `Enrollments` özelliğini bıraktı. `Details` sayfasında, koleksiyonun içeriğini bir HTML tablosunda görüntüleyeceksiniz.

*Controllers\studentcontroller.cs*içinde, `Details` görünümü için eylem yöntemi, tek bir `Student` varlığını almak için [Find](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx) yöntemini kullanır.

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

Anahtar değeri yönteme `id` parametresi olarak geçirilir ve Dizin sayfasındaki **Ayrıntılar** köprüde *yol verilerinden* gelir.

### <a name="tip-route-data"></a>İpucu: **verileri yönlendirme**

Rota verileri, model cildin yönlendirme tablosunda belirtilen bir URL kesiminde bulduğu veri. Örneğin, varsayılan yol `controller`, `action`ve `id` segmentlerini belirtir:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

Aşağıdaki URL 'de, varsayılan yol `controller`olarak `Instructor` eşler, `action` olarak `Index` ve `id`olarak 1; Bunlar rota veri değerleridir.

`http://localhost:1230/Instructor/Index/1?courseID=2021`

`?courseID=2021` bir sorgu dizesi değeridir. Model bağlayıcı, `id` bir sorgu dizesi değeri olarak geçirirseniz de çalışacaktır:

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

URL 'Ler Razor görünümündeki `ActionLink` deyimleri tarafından oluşturulur. Aşağıdaki kodda, `id` parametresi varsayılan yol ile eşleşir, bu nedenle `id` yol verilerine eklenir.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

Aşağıdaki kodda `courseID`, bir sorgu dizesi olarak eklendiğinden, varsayılan rotadaki bir parametreyle eşleşmez.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]

### <a name="to-create-the-details-page"></a>Ayrıntılar sayfasını oluşturmak için

1. *Views\student\details.cshtml*dosyasını açın.

   Her alan, aşağıdaki örnekte gösterildiği gibi `DisplayFor` Yardımcısı kullanılarak görüntülenir:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]

2. `EnrollmentDate` alanından sonra ve kapanış `</dl>` etiketinden hemen önce, aşağıdaki örnekte gösterildiği gibi, kayıtlar listesini göstermek için vurgulanmış kodu ekleyin:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    Kodu yapıştırdıktan sonra kod girintileme yanlış ise, biçimlendirmek için **ctrl**+**K**, **CTRL**+**D** tuşlarına basın.

    Bu kod, `Enrollments` Gezinti özelliğindeki varlıklar aracılığıyla döngü yapılır. Özelliğindeki her `Enrollment` varlık için kurs başlığını ve sınıfı görüntüler. Kurs başlığı, `Enrollments` varlığının `Course` gezinti özelliğinde depolanan `Course` varlığından alınır. Bu verilerin tümü, gerektiğinde veritabanından otomatik olarak alınır. Diğer bir deyişle, burada yavaş yükleme kullanıyorsunuz. `Courses` gezinti özelliği için *Eager yüklemesi* belirtmediniz, bu nedenle kayıtlar öğrencilerle aynı sorgu içinde alınmadı. Bunun yerine, `Enrollments` gezinti özelliğine ilk kez erişmeye çalıştığınızda, verileri almak için veritabanına yeni bir sorgu gönderilir. Bu serinin ilerleyen kısımlarında [Ilgili verileri okuma](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) öğreticisinde geç yükleme ve Eager yükleme hakkında daha fazla bilgi edinebilirsiniz.

3. Programı başlatarak (**Ctrl**+**F5**), **öğrenciler** sekmesini seçerek ve sonra Alexander Carson için **Ayrıntılar** bağlantısına tıklayarak Ayrıntılar sayfasını açın. ( *Details. cshtml* dosyası açıkken **CTRL**+**F5** tuşuna basarsanız, bir HTTP 400 hatası alırsınız. Bunun nedeni, Visual Studio 'Nun Ayrıntılar sayfasını çalıştırmaya çalıştığı, ancak görüntülenecek öğrenci 'yi belirten bir bağlantıdan erişilmediği bir bağlantıdır. Bu durumda, URL 'den "öğrenci/Ayrıntılar" ı kaldırın ve yeniden deneyin veya tarayıcıyı kapatın, projeye sağ tıklayın ve > **görünümü tarayıcıda** **görüntüle** ' ye tıklayın.)

    Seçili öğrenci için Kurslar ve notlar listesini görürsünüz.

4. Tarayıcıyı kapatın.

## <a name="update-the-create-page"></a>Oluştur sayfasını Güncelleştir

1. *Controllers\studentcontroller.cs*içinde, <xref:System.Web.Mvc.HttpPostAttribute> `Create` Action metodunu aşağıdaki kodla değiştirin. Bu kod, `try-catch` bir blok ekler ve `ID`, scafkatlama yöntemi için <xref:System.Web.Mvc.BindAttribute> özniteliğinden kaldırır:

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    Bu kod, ASP.NET MVC model Ciltçi tarafından oluşturulan `Student` varlığını `Students` varlık kümesine ekler ve sonra değişiklikleri veritabanına kaydeder. *Model Ciltçi* , bir form tarafından gönderilen verilerle çalışmanıza daha kolay hale GETIREN ASP.NET MVC işlevselliğine başvurur; Model Ciltçi, postalanan form değerlerini CLR türlerine dönüştürür ve parametreleri içindeki eylem yöntemine geçirir. Bu durumda, model Ciltçi, `Form` koleksiyonundan özellik değerlerini kullanarak sizin için bir `Student` varlığı oluşturur.

    `ID`, satır eklendiğinde SQL Server otomatik olarak ayarlayacağından birincil anahtar değeri olduğundan, `ID` bind özniteliğinden kaldırmış olursunuz. Kullanıcı girişi `ID` değerini belirtmiyor.

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgery-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>Güvenlik Uyarısı-`ValidateAntiForgeryToken` özniteliği, [siteler arası istek sahteciliği](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) saldırıları önlemeye yardımcı olur. Görünümünde, daha sonra göreceğiniz şekilde karşılık gelen bir `Html.AntiForgeryToken()` ifadesini gerektirir.

    `Bind` özniteliği, oluşturma senaryolarında daha *fazla* gönderim yapmanın bir yoludur. Örneğin, `Student` varlığın bu Web sayfasının ayarlamak istemediğiniz bir `Secret` özelliği içerdiğini varsayalım.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    Web sayfasında bir `Secret` alanınız olmasa da, bir bilgisayar bir `Secret` form değeri göndermek için [Fiddler](http://fiddler2.com/home)gibi bir araç kullanabilir veya bazı JavaScript yazabilir. Model cildin, bir `Student` örneği oluşturduğunda kullandığı alanları sınırlayan <xref:System.Web.Mvc.BindAttribute> özniteliği olmadan<em>,</em> bu `Secret` form değerini seçip `Student` varlık örneğini oluşturmak için onu kullanacaktır. Daha sonra, `Secret` form alanı için belirtilen korsanın hangi değeri veritabanınızda güncelleştirilenecektir. Aşağıdaki görüntüde, `Secret` alanı ("OverPost" değeri ile), postalanan form değerlerine eklenen Fiddler aracı gösterilmektedir.

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

    Daha sonra "OverPost" değeri, eklenen satırın `Secret` özelliğine başarıyla eklenir, ancak Web sayfasının bu özelliği ayarlayabilmesini amaçlayamazsınız.

    Alanları *beyaz liste olarak listelemek* için `Bind` özniteliğiyle `Include` parametresini kullanmak en iyisidir. Dışlamak istediğiniz *liste* listesi alanlarını `Exclude` parametresini kullanmak da mümkündür. `Include` neden daha güvenlidir, varlığa yeni bir özellik eklediğinizde yeni alan bir `Exclude` listesi tarafından otomatik olarak korunmaz.

    Düzenleme senaryolarında fazla nakletmeyi engelleyebilirsiniz, önce varlığı veritabanından okuyup ardından `TryUpdateModel`çağırarak açık izin verilen bir özellikler listesini geçirerek. Bu, bu öğreticilerde kullanılan yöntemidir.

    Birçok geliştirici tarafından tercih edilen aşırı nakletmeyi önlemenin alternatif bir yolu, model bağlamasıyla varlık sınıfları yerine görüntüleme modellerini kullanmaktır. Yalnızca görünüm modelinde güncelleştirmek istediğiniz özellikleri ekleyin. MVC model Bağlayıcısı tamamlandıktan sonra, görünüm modeli özelliklerini, isteğe bağlı olarak, [Automaber](http://automapper.org/)gibi bir araç kullanarak varlık örneğine kopyalayın. DB kullanın. Varlık örneği üzerinde, durumunu değiştirilmemiş olarak ayarlamak için giriş yapın ve sonra özelliği ("PropertyName") ayarlayın. , Görünüm modelinde bulunan her bir varlık özelliğinde true olarak değiştirilmiştir. Bu yöntem hem düzenleme hem de oluşturma senaryolarında çalışmaktadır.

    `Bind` özniteliği dışında, `try-catch` bloğu, yapı iskelesi kodunda yaptığınız tek değişikdir. Değişiklikler kaydedilirken <xref:System.Data.DataException> türetilen bir özel durum yakalanmışsa, genel bir hata iletisi görüntülenir. <xref:System.Data.DataException> özel durumlar bazen bir programlama hatası yerine uygulamanın harici bir şeydir. bu nedenle, kullanıcının yeniden denemek tavsiye edilir. Bu örnekte uygulanmamış olsa da, bir üretim kalitesi uygulaması özel durumu günlüğe kaydeder. Daha fazla bilgi için bkz. Izleme ve telemetri bölümünde **Öngörüler Için günlük** [(Azure Ile gerçek bulut uygulamaları oluşturma)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log).

    *Views\student\create.exe* içindeki kod, *Ayrıntılar. cshtml*' de gördüğünüz gibi, `EditorFor` ve `ValidationMessageFor` yardımcılarının `DisplayFor`yerine her alan için kullanılması dışında benzerdir. İlgili kod aşağıda verilmiştir:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    *Create. cshtml* Ayrıca, [siteler arası istek sahteciliği](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) saldırıları önlemeye yardımcı olmak için denetleyicideki `ValidateAntiForgeryToken` özniteliğiyle birlikte çalışan `@Html.AntiForgeryToken()`de içerir.

    *Create. cshtml*içinde herhangi bir değişiklik yapılması gerekmez.

2. Programı başlatarak, **öğrenciler** sekmesini seçerek ve ardından **Yeni oluştur**' a tıklayarak sayfayı çalıştırın.

3. Ad ve geçersiz bir tarih girin ve hata iletisini görmek için **Oluştur** ' a tıklayın.

    Bu, varsayılan olarak aldığınız sunucu tarafı doğrulamadır. Sonraki bir öğreticide, istemci tarafı doğrulama için kod üreten öznitelikler ekleme hakkında bilgi edineceksiniz. Aşağıdaki Vurgulanan kodda, **Create** yönteminde model doğrulama denetimi gösterilmektedir.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]

4. Tarihi geçerli bir değer olarak değiştirin ve yeni öğrencinin **Dizin** sayfasında göründüğünü görmek için **Oluştur** ' a tıklayın.

5. Tarayıcıyı kapatın.

## <a name="update-httppost-edit-method"></a>HttpPost düzenleme yöntemini güncelleştir

1. <xref:System.Web.Mvc.HttpPostAttribute> `Edit` Action metodunu aşağıdaki kodla değiştirin:

   [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

   > [!NOTE]
   > *Controllers\studentcontroller.cs*içinde `HttpGet Edit` yöntemi (`HttpPost` özniteliği olmayan), `Details` yönteminde gördüğünüz gibi seçili `Student` varlığı almak için `Find` yöntemini kullanır. Bu yöntemi değiştirmeniz gerekmez.

   Bu değişiklikler, [aşırı muhasebeleştirme](#overpost)'yi engellemek için en iyi güvenlik uygulaması uygular, desteği bir `Bind` özniteliği oluşturdu ve model Ciltçi tarafından oluşturulan varlığı değiştirilmiş bayrağıyla birlikte varlık kümesine ekledi. Bu kod artık önerilmez çünkü `Bind` özniteliği `Include` parametresinde listelenmeyen alanlarda önceden var olan verileri temizler. Gelecekte, MVC denetleyicisi desteği, düzenleme yöntemleri için `Bind` öznitelikleri üretmeyecek şekilde güncelleştirilecektir.

   Yeni kod, mevcut varlığı okur ve verileri, postalanan form verilerinde Kullanıcı girişinden alanları güncelleştirmek için <xref:System.Web.Mvc.Controller.TryUpdateModel%2A> çağırır. Entity Framework otomatik değişiklik izleme varlıkta [EntityState. Modified](<xref:System.Data.EntityState.Modified>) bayrağını ayarlar. [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) yöntemi çağrıldığında <xref:System.Data.EntityState.Modified> bayrağı, Entity Framework veritabanı satırını GÜNCELLEŞTIRMEK için SQL deyimleri oluşturmasına neden olur. [Eşzamanlılık çakışmaları](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) yok sayılır ve kullanıcının değiştirmamaları da dahil olmak üzere veritabanı satırının tüm sütunları güncellenir. (Sonraki bir öğreticide eşzamanlılık çakışmalarının nasıl işleneceği gösterilmektedir ve yalnızca tek tek alanların veritabanında güncelleştirilmesini isterseniz, varlığı [EntityState. Unchanged](<xref:System.Data.EntityState.Unchanged>) olarak ayarlayabilir ve ayrı alanları [EntityState. Modified](<xref:System.Data.EntityState.Modified>)olarak ayarlayabilirsiniz.)

   Fazla nakletmeyi engellemek için düzenleme sayfası tarafından güncelleştirilemek istediğiniz alanlar `TryUpdateModel` parametrelerinde beyaz listeye alınır. Şu anda koruduğunuz ek alan yok, ancak model cildin bağlamasını istediğiniz alanları listelemek, gelecekte veri modeline alanlar eklerseniz, bunları buraya açıkça eklemeene kadar otomatik olarak korunur.

   Bu değişikliklerin sonucu olarak, HttpPost düzenleme yönteminin yöntem imzası, HttpGet düzenleme yöntemiyle aynıdır; Bu nedenle, EditPost yöntemini yeniden adlandırdınız.

   > [!TIP]
   >
   > **Varlık durumları ve Attach ve SaveChanges yöntemleri**
   >
   > Veritabanı bağlamı, bellekteki varlıkların veritabanında karşılık gelen satırlarıyla eşitlenmiş olup olmadığını izler ve bu bilgiler `SaveChanges` yöntemini çağırdığınızda ne olacağını belirler. Örneğin, [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) yöntemine yeni bir varlık geçirdiğinizde, bu varlığın durumu `Added`olarak ayarlanır. Ardından, [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) yöntemini çağırdığınızda Veritabanı BAĞLAMı bir SQL `INSERT` komutu yayınlar.
   >
   > Bir varlık aşağıdaki [durumlardan](xref:System.Data.EntityState)birinde olabilir:
   >
   > - `Added`. Varlık veritabanında henüz yok. `SaveChanges` yöntemi bir `INSERT` ifadesini vermelidir.
   > - `Unchanged`. `SaveChanges` yöntemi tarafından bu varlıkla ilgili hiçbir şey yapılması gerekmez. Veritabanından bir varlık okuduğunuzda, varlık bu durumla başlar.
   > - `Modified`. Varlığın özellik değerlerinin bazıları veya tümü değiştirildi. `SaveChanges` yöntemi bir `UPDATE` ifadesini vermelidir.
   > - `Deleted`. Varlık silinmek üzere işaretlendi. `SaveChanges` yöntemi bir `DELETE` ifadesini vermelidir.
   > - `Detached`. Varlık, veritabanı bağlamı tarafından izlenmiyor.
   >
   > Bir masaüstü uygulamasında durum değişiklikleri genellikle otomatik olarak ayarlanır. Bir uygulamanın masaüstü türünde bir varlığı okur ve bazı özellik değerlerinde değişiklik yaparsınız. Bu, varlık durumunun otomatik olarak `Modified`olarak değiştirilmesine neden olur. `SaveChanges`çağırdığınızda Entity Framework, yalnızca değiştirdiğiniz gerçek özellikleri güncelleştiren bir SQL `UPDATE` ifadesini oluşturur.
   >
   > Web uygulamalarının bağlantısı kesilen doğası bu sürekli sıraya izin vermez. Bir varlığı okuyan [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) , bir sayfa işlendikten sonra atılmış olur. `HttpPost` `Edit` eylem yöntemi çağrıldığında, yeni bir istek yapılır ve [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)'in yeni bir örneğine sahip olursunuz. bu nedenle, `SaveChanges`çağırdığınızda Entity Framework, veritabanının hangi özellikleri değiştireceğinin hiçbir yolu olmadığı `Modified.` için, veritabanı satırının tüm sütunlarını günceller.
   >
   > SQL `Update` deyimin yalnızca kullanıcının gerçekten değiştirdiği alanları güncelleştirmesini istiyorsanız, `HttpPost` `Edit` yöntemi çağrıldığında kullanılabilir olmaları için özgün değerleri bir şekilde (gizli alanlar gibi) kaydedebilirsiniz. Ardından, özgün değerleri kullanarak bir `Student` varlığı oluşturabilir, `Attach` yöntemini varlığın orijinal sürümüyle çağırabilir, varlığın değerlerini yeni değerlerle güncelleştirebilir `SaveChanges.` ve daha fazla bilgi Için bkz. [varlık durumları ve SaveChanges](/ef/ef6/saving/change-tracking/entity-state) ve [yerel veriler](/ef/ef6/querying/local-data).

   *Views\student\edit.exe* içindeki HTML ve Razor kodu *Create. cshtml*' de gördüğünüz şekilde benzerdir ve hiçbir değişiklik yapılması gerekmez.

2. Programı başlatarak, **öğrenciler** sekmesini seçerek ve ardından bir **Düzenle** Köprüsü ' ne tıklayarak sayfayı çalıştırın.

3. Bazı verileri değiştirin ve **Kaydet**' e tıklayın. Değiştirilen verileri Dizin sayfasında görürsünüz.

4. Tarayıcıyı kapatın.

## <a name="update-the-delete-page"></a>Silme sayfası

*Controllers\studentcontroller.cs*içinde, <xref:System.Web.Mvc.HttpGetAttribute> `Delete` yöntemi için şablon kodu, `Details` ve `Edit` yöntemlerinde gördüğünüz gibi seçili `Student` varlığı almak için `Find` yöntemini kullanır. Ancak, `SaveChanges` çağrısı başarısız olduğunda özel bir hata iletisi uygulamak için, bu yönteme ve buna karşılık gelen görünüme bazı işlevler eklersiniz.

Güncelleştirme ve oluşturma işlemleri için gördüğünüz gibi silme işlemleri için iki eylem yöntemi gerekir. GET isteğine yanıt olarak çağrılan yöntem, kullanıcıya silme işlemini onaylama veya iptal etme şansı veren bir görünüm görüntüler. Kullanıcı onu onayladığında, bir POST isteği oluşturulur. Bu durumda, `HttpPost` `Delete` yöntemi çağrılır ve bu yöntem aslında silme işlemini gerçekleştirir.

Veritabanı güncelleştirilirken oluşabilecek hataları işlemek için <xref:System.Web.Mvc.HttpPostAttribute> `Delete` yöntemine bir `try-catch` bloğu ekleyeceksiniz. Bir hata oluşursa, <xref:System.Web.Mvc.HttpPostAttribute> `Delete` yöntemi <xref:System.Web.Mvc.HttpGetAttribute> `Delete` yöntemini çağırır, bu da bir hatanın oluştuğunu gösteren bir parametre geçiyor. <xref:System.Web.Mvc.HttpGetAttribute> `Delete` yöntemi daha sonra hata iletisiyle birlikte onay sayfasını yeniden görüntüler ve kullanıcıya iptal veya yeniden deneme fırsatı verir.

1. <xref:System.Web.Mvc.HttpGetAttribute> `Delete` eylem yöntemini aşağıdaki kodla değiştirin, bu hata raporlamayı yönetir:

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    Bu kod, bir yöntemin değişiklikleri kaydetme hatasından sonra döndürülüp çağrılmadığını belirten [isteğe bağlı bir parametresini](https://msdn.microsoft.com/library/dd264739.aspx) kabul eder. Bu parametre, `HttpGet` `Delete` yöntemi önceki bir hata olmadan çağrıldığında `false`. Veritabanı güncelleştirme hatasına yanıt olarak `HttpPost` `Delete` yöntemi tarafından çağrıldığında, parametre `true` ve görünüme bir hata mesajı geçirilir.

2. <xref:System.Web.Mvc.HttpPostAttribute> `Delete` eylemi yöntemini (`DeleteConfirmed`), gerçek silme işlemini gerçekleştiren ve tüm veritabanı güncelleştirme hatalarını yakalayan aşağıdaki kodla değiştirin.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

    Bu kod seçili varlığı alır, ardından varlığın durumunu `Deleted`olarak ayarlamak için [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) yöntemini çağırır. `SaveChanges` çağrıldığında bir SQL `DELETE` komutu oluşturulur. Ayrıca `DeleteConfirmed` eylem yöntemi adını `Delete`olarak değiştirdiniz. `HttpPost` `Delete` yöntemi adlı scafkatmış kod, `HttpPost` yöntemine benzersiz bir imza vermek `DeleteConfirmed`. (CLR aşırı yüklenmiş yöntemlerin farklı yöntem parametrelerine sahip olmasını gerektirir.) İmzalar benzersiz olduğuna göre, MVC kuralını seçebilir ve `HttpPost` ve `HttpGet` silme yöntemleri için aynı adı kullanabilirsiniz.

    Yüksek hacimli bir uygulamadaki performansı artırmak öncese, `Find` ve `Remove` yöntemlerini çağıran kod satırlarını aşağıdaki kodla değiştirerek satırı almak için gereksiz bir SQL sorgusundan kaçınabilirsiniz:

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

    Bu kod yalnızca birincil anahtar değerini kullanarak bir `Student` varlığı başlatır ve ardından varlık durumunu `Deleted`olarak ayarlar. Bu, Entity Framework varlığı silmek için ihtiyaç duymaktadır.

    Belirtildiği gibi, `HttpGet` `Delete` yöntemi verileri silmez. Bir GET isteğine yanıt olarak silme işlemi gerçekleştirme (veya bu konuyla ilgili olarak herhangi bir düzenleme işlemi, oluşturma işlemi yapma veya verileri değiştiren başka bir işlem) güvenlik riski oluşturur. Daha fazla bilgi için bkz. ASP.NET MVC Ipucu #46 —, Stephen Walther 'un blogundaki [güvenlik delikleri oluşturdıklarından, DELETE bağlantılarını kullanmayın](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) .

3. *Views\student\delete.exe*' de, aşağıdaki örnekte gösterildiği gibi `h2` başlığı ve `h3` başlığı arasına bir hata iletisi ekleyin:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

4. Programı başlatarak, **öğrenciler** sekmesini seçerek ve ardından bir **Delete** Köprüsü ' ne tıklayarak sayfayı çalıştırın.

5. Sayfada **Sil ' i** seçerek **bunu silmek istediğinize emin olun**.

    Dizin sayfası, silinen öğrenci olmadan görüntülenir. ( [Eşzamanlılık öğreticisinde](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)işlem içinde kodu işleme hatası hakkında bir örnek görürsünüz.)

## <a name="close-database-connections"></a>Veritabanı bağlantılarını kapat

Veritabanı bağlantılarını kapatmak ve en kısa sürede tutdukları kaynakları boşaltmak için, bununla işiniz bittiğinde bağlam örneğini atın. Bu nedenle, aşağıdaki örnekte gösterildiği gibi, yapı iskelesi kodu, *StudentController.cs*içinde `StudentController` sınıfının sonunda bir [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) yöntemi sağlar:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

Temel `Controller` sınıfı `IDisposable` arabirimini zaten uyguluyor, bu nedenle bu kod yalnızca bağlam örneğini açıkça atmak için `Dispose(bool)` yöntemine bir geçersiz kılma ekler.

## <a name="handle-transactions"></a>İşlemleri işle

Entity Framework, varsayılan olarak işlemleri örtülü olarak uygular. Birden çok satır veya tabloda değişiklik yaptığınız ve sonra `SaveChanges`çağıran senaryolarda, Entity Framework otomatik olarak tüm değişikliklerinizin başarılı veya başarısız olduğundan emin olur. Önce bazı değişiklikler yapıldıktan sonra bir hata oluşursa, bu değişiklikler otomatik olarak geri alınır. Daha fazla denetime ihtiyaç duyduğunuz senaryolar için&mdash;Örneğin,&mdash;işlem Entity Framework dışında yapılan işlemleri eklemek istiyorsanız, bkz. [işlemler Ile çalışma](/ef/ef6/saving/transactions).

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Artık `Student` varlıkları için basit CRUD işlemleri gerçekleştiren tamamen bir sayfa kümesine sahipsiniz. Veri alanları için UI öğeleri oluşturmak üzere MVC yardımcıları kullandınız. MVC yardımcıları hakkında daha fazla bilgi için bkz. [HTML Yardımcıları kullanarak form işleme](/previous-versions/aspnet/dd410596(v=vs.98)) (MVC 3 için bir makale, ancak MVC 5 için hala geçerlidir).

Diğer EF 6 kaynaklarına bağlantılar, [ASP.NET Data Access-önerilen kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md)bölümünde bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Ayrıntılar sayfası oluşturuldu
> * Oluşturma sayfası güncelleştirildi
> * HttpPost düzenleme yöntemi güncelleştirildi
> * Silme sayfası güncelleştirildi
> * Kapalı veritabanı bağlantıları
> * İşlenmiş işlemler

Projeye sıralama, filtreleme ve sayfalama ekleme hakkında bilgi edinmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Sıralama, Filtreleme ve Sayfalama](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
