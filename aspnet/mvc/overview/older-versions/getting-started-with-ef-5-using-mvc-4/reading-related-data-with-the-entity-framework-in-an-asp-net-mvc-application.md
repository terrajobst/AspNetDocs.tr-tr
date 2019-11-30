---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: Bir ASP.NET MVC uygulamasındaki Entity Framework ile Ilgili verileri okuma (5/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 0d6fb83b-71f7-425d-8dec-981197d7ec42
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: e1752022b66952783039fbea0c2880e2f9be6ef8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595218"
---
# <a name="reading-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-5-of-10"></a>ASP.NET MVC uygulamasındaki Entity Framework ile Ilgili verileri okuma (5/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticide okul veri modelini tamamladınız. Bu öğreticide ilgili verileri (yani Entity Framework, gezinti özelliklerine yüklediği verileri) okuyup görüntüleyeceksiniz.

Aşağıdaki çizimlerde, birlikte çalışacağımız sayfalar gösterilmektedir.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="lazy-eager-and-explicit-loading-of-related-data"></a>Geç, Eager ve Ilgili verilerin açık bir şekilde yüklenmesi

Entity Framework bir varlığın gezinti özelliklerine ilgili verileri yükleyebilmesinin birkaç yolu vardır:

- *Yavaş yükleme*. Varlık ilk kez okunmadıysa ilgili veriler alınmadı. Ancak, bir gezinti özelliğine ilk kez erişmeye çalıştığınızda, bu gezinti özelliği için gereken veriler otomatik olarak alınır. Bu, tek bir varlığın kendisi için ve varlık için ilgili verilerin alınması gereken her seferinde veritabanına gönderilen birden çok sorguya neden olur. 

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *Eager yükleniyor*. Varlık okurken ilgili veriler onunla birlikte alınır. Bu, genellikle gereken tüm verileri alan tek bir JOIN sorgusuna neden olur. `Include` yöntemini kullanarak Eager yükleme belirtirsiniz.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *Açık yükleme*. Bu, yavaş yüklemeye benzer, ancak kodda ilgili verileri açıkça almanızı sağlar; bir gezinti özelliğine eriştiğinizde otomatik olarak gerçekleşmez. Bir varlık için nesne durumu Yöneticisi girişini alarak ve tek bir varlık tutan özellikler için Koleksiyonlar için `Collection.Load` yöntemini veya `Reference.Load` yöntemini çağırarak ilgili verileri el ile yüklersiniz. (Aşağıdaki örnekte, yönetici gezinti özelliğini yüklemek istediğinizde `Collection(x => x.Courses)` `Reference(x => x.Administrator)`ile değiştirirsiniz.)

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

Özellik değerlerini hemen almadıklarından, geç yükleme ve açık yükleme aynı zamanda *ertelenmiş yükleme*olarak da bilinir.

Genel olarak, alınan her varlık için ilgili verilerin gerekli olduğunu biliyorsanız, tek bir sorgu veritabanına gönderilen tek bir sorgu genellikle alınan her varlık için ayrı sorgulardan daha verimli olduğundan, Eager yüklemesi en iyi performansı sunar. Örneğin, Yukarıdaki örneklerde, her departmanın on ile ilgili kurs olduğunu varsayalım. Eager yükleme örneği yalnızca tek bir (JOIN) sorgusuna ve veritabanına yönelik tek bir gidiş dönüş oluşmasına neden olur. Yavaş yükleme ve açık yükleme örnekleri, her ikisi de on bir sorgu ve veritabanı üzerinde on bir gidiş dönüş ile sonuçlanır. Gecikme süresi yüksek olduğunda veritabanına yönelik ek gidiş dönüşler özellikle performansa neden olur.

Öte yandan, bazı senaryolarda geç yükleme daha etkilidir. Eager yüklemesi, SQL Server verimli bir şekilde işleyemeyecek çok karmaşık bir birleştirmenin oluşturulmasına neden olabilir. Ya da bir varlığın gezinti özelliklerine yalnızca işlemekte olduğunuz varlıkların bir alt kümesi için erişmeniz gerekiyorsa, Eager yüklemesi gereksiniminizden daha fazla veri alacağından, yavaş yükleme daha iyi çalışabilir. Performans önemliyse, en iyi seçimi yapmak için her iki şekilde de performansı test etmek en iyisidir.

Genellikle, yalnızca yavaş yüklemeyi kapattığınız zaman açık yüklemeyi kullanırsınız. Bir senaryo serileştirme sırasında geç yükleme kapalı olmalıdır. Yavaş yükleme ve serileştirme iyi bir şekilde karıştırmayın ve bu konuda dikkatli değilseniz, yavaş yükleme etkinleştirildiğinde amaçlamadan önemli ölçüde daha fazla veri sorgulama yapabilirsiniz. Serileştirme genellikle bir türün örneğindeki her özelliğe erişerek işe yarar. Özellik erişimi, yavaş yüklemeyi tetikler ve bu yavaş yüklenen varlıklar serileştirilir. Seri hale getirme işlemi daha sonra, yavaş yüklenen varlıkların her özelliğine erişir, bu da daha fazla yavaş yükleme ve Serileştirmeye neden olabilir. Bu çalışma zinciri yeniden eylemini engellemek için, bir varlığı serileştirmadan önce yavaş yüklemeyi kapatın.

Veritabanı bağlamı sınıfı varsayılan olarak yavaş yükleme gerçekleştirir. Yavaş yüklemeyi devre dışı bırakmak için iki yol vardır:

- Belirli gezinme özellikleri için, özelliği bildirdiğinizde `virtual` anahtar sözcüğünü atlayın.
- Tüm gezinme özellikleri için `LazyLoadingEnabled` `false`olarak ayarlayın. Örneğin, aşağıdaki kodu bağlam sınıfınızın oluşturucusuna koyabilirsiniz: 

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Yavaş yükleme, performans sorunlarına neden olan kodu maskeleyebilir. Örneğin, Eager veya açık yükleme belirtmeyen, ancak yüksek hacimli varlıkları işleyen ve her yinelemede birçok gezinti özelliği kullanan kod çok verimsiz olabilir (veritabanına gidiş dönüş nedeniyle). Şirket içi SQL Server 'ı kullanarak geliştirmede iyi işlem yapan bir uygulama, artan gecikme süresi ve yavaş yükleme nedeniyle Azure SQL veritabanı 'na taşındığında performans sorunlarına neden olabilir. Veritabanı sorgularının gerçekçi bir test yüklemesiyle profili oluşturulması, geç yüklemenin uygun olup olmadığını belirlemenize yardımcı olur. Daha fazla bilgi için bkz. [Demystifying Entity Framework stratejileri: Ilgili verileri yükleme](https://msdn.microsoft.com/magazine/hh205756.aspx) ve [Entity Framework kullanarak SQL Azure ağ gecikmesini azaltma](https://msdn.microsoft.com/magazine/gg309181.aspx).

## <a name="create-a-courses-index-page-that-displays-department-name"></a>Bölüm adını görüntüleyen bir kurslar Dizin sayfası oluşturma

`Course` varlığı, kursun atandığı departmanın `Department` varlığını içeren bir gezinti özelliği içerir. Bir kurs listesinde atanan departmanın adını göstermek için, `Course.Department` Gezinti özelliğindeki `Department` varlığındaki `Name` özelliğini almanız gerekir.

Aşağıdaki çizimde gösterildiği gibi, `Student` denetleyicisi için daha önce yaptığınız aynı seçenekleri kullanarak `Course` varlık türü için `CourseController` adlı bir denetleyici oluşturun (görüntünün aksine bağlam sınıfınız, model ad alanında değil DAL ad alanında bulunur):

![Add_Controller_dialog_box_for_Course_controller](https://asp.net/media/2577868/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Course_controller_c167c11e-2d3e-4b64-a2b9-a0b368b8041d.png)

*Controllers\coursecontroller.cs* ' i açın ve `Index` yöntemine bakın:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Otomatik yapı iskelesi, `Department` gezinti özelliği için `Include` yöntemi kullanılarak bir Eager yüklemesi belirtti.

*Views\course\ındex.cshtml* dosyasını açın ve mevcut kodu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,15,18,28-30)]

Yapı iskelesi kodunda aşağıdaki değişiklikleri yaptınız:

- Başlık **dizinden** **Kurslar**olarak değiştirildi.
- Satır bağlantıları sola taşındı.
- Başlık **numarasının** altına `CourseID` özellik değerini gösteren bir sütun eklediniz. (Varsayılan olarak, son kullanıcılar için anlamlı olduklarından birincil anahtarlar yapı iskelesi değildir. Ancak, bu durumda birincil anahtar anlamlı olur ve göstermek istersiniz.)
- Son sütun başlığını **DepartmentID** (yabancı anahtarın adı `Department` varlığına) **bölüm**olarak değiştirdi.

Son sütun için, scafkatlanmış kodun `Department` gezinti özelliğine yüklenen `Department` varlığının `Name` özelliğini görüntülediğini fark edersiniz:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml)]

Bölüm adlarıyla listeyi görmek için sayfayı çalıştırın (contoso Üniversitesi giriş sayfasında **Kurslar** sekmesini seçin).

![Courses_index_page_with_department_names](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="create-an-instructors-index-page-that-shows-courses-and-enrollments"></a>Kurslar ve kayıtları gösteren bir eğitmenler Dizin sayfası oluşturun

Bu bölümde, Eğitmenler Dizin sayfasını görüntülemek için `Instructor` varlık için bir denetleyici ve görünüm oluşturacaksınız:

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Bu sayfa aşağıdaki yollarla ilgili verileri okur ve görüntüler:

- Eğitmenler listesi `OfficeAssignment` varlığındaki ilgili verileri görüntüler. `Instructor` ve `OfficeAssignment` varlıkları bire sıfır veya-bir ilişkidir. `OfficeAssignment` varlıkları için Eager yükleme kullanacaksınız. Daha önce açıklandığı gibi, birincil tablonun alınan tüm satırları için ilgili verilere ihtiyacınız olduğunda Eager yüklemesi genellikle daha etkilidir. Bu durumda, tüm görüntülenen Eğitmenler için Office atamalarını göstermek istersiniz.
- Kullanıcı bir eğitmen seçtiğinde ilgili `Course` varlıkları görüntülenir. `Instructor` ve `Course` varlıkları çoktan çoğa bir ilişkidir. `Course` varlıkları ve ilgili `Department` varlıkları için Eager yükleme kullanacaksınız. Bu durumda, yalnızca seçili eğitmen için kurslar gerektiğinden, geç yükleme daha verimli olabilir. Ancak, bu örnek, gezinti özellikleri ' nde olan varlıkların içindeki gezinti özellikleri için Eager yükleme 'nin nasıl kullanılacağını gösterir.
- Kullanıcı bir kurs seçtiğinde `Enrollments` varlık kümesinden ilgili veriler görüntülenir. `Course` ve `Enrollment` varlıkları bire çok ilişkidir. `Enrollment` varlıkları ve ilgili `Student` varlıklarını için açık yükleme ekleyeceksiniz. (Açık yükleme gerekli değildir çünkü Lazy yüklemesi etkindir, ancak bu, açık yüklemenin nasıl yapılacağını gösterir.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>Eğitmen dizini görünümü için bir görünüm modeli oluşturun

Eğitmen dizini sayfası, üç farklı tablo gösterir. Bu nedenle, her biri tablolardan birine ait verileri tutan üç özellik içeren bir görünüm modeli oluşturacaksınız.

*Viewmodeller* klasöründe *InstructorIndexData.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="adding-a-style-for-selected-rows"></a>Seçili satırlar için stil ekleme

Seçili satırları işaretlemek için farklı bir arka plan rengine ihtiyacınız vardır. Bu Kullanıcı arabirimine bir stil sağlamak için aşağıdaki vurgulanmış kodu aşağıda gösterildiği gibi *Content\site.exe*içindeki `/* info and errors */` bölümüne ekleyin:

[!code-css[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.css?highlight=2-5)]

### <a name="creating-the-instructor-controller-and-views"></a>Eğitmen denetleyicisi ve görünümleri oluşturma

Aşağıdaki çizimde gösterildiği gibi bir `InstructorController` denetleyicisi oluşturun:

![Add_Controller_dialog_box_for_Instructor_controller](https://asp.net/media/2577909/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Add_Controller_dialog_box_for_Instructor_controller_f99c10aa-1efd-49d6-af1d-b00461616107.png)

*Controllers\komutctorcontroller.cs* dosyasını açın ve `ViewModels` ad alanı için `using` bir ifade ekleyin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

`Index` yöntemi içindeki scafkatlı kod yalnızca `OfficeAssignment` gezinti özelliği için Eager yüklemeyi belirtir:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

`Index` yöntemini, ek ilgili verileri yüklemek ve görünüm modeline koymak için aşağıdaki kodla değiştirin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Yöntemi, isteğe bağlı yol verilerini (`id`) ve seçilen eğitmenin ve seçili kursun KIMLIK değerlerini sağlayan bir sorgu dizesi parametresini (`courseID`) kabul eder ve gerekli tüm verileri görünüme geçirir. Parametreler, sayfadaki Köprü **seçme** ile sağlanır.

> [!TIP]
> 
> **Verileri yönlendirme**
> 
> Rota verileri, model cildin yönlendirme tablosunda belirtilen bir URL kesiminde bulduğu veri. Örneğin, varsayılan yol `controller`, `action`ve `id` segmentlerini belirtir:
> 
> ```csharp
> routes.MapRoute(  
>  name: "Default",  
>  url: "{controller}/{action}/{id}",  
>  defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }  
> );
> ```
> 
> Aşağıdaki URL 'de, varsayılan yol `controller`olarak `Instructor` eşler, `action` olarak `Index` ve `id`olarak 1; Bunlar rota veri değerleridir.
> 
> `http://localhost:1230/Instructor/Index/1?courseID=2021`
> 
> "? courseID = 2021" bir sorgu dizesi değeridir. Model bağlayıcı, `id` bir sorgu dizesi değeri olarak geçirirseniz de çalışacaktır:
> 
> `http://localhost:1230/Instructor/Index?id=1&CourseID=2021`
> 
> URL 'Ler Razor görünümündeki `ActionLink` deyimleri tarafından oluşturulur. Aşağıdaki kodda, `id` parametresi varsayılan yol ile eşleşir, bu nedenle `id` yol verilerine eklenir.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml)]
> 
> Aşağıdaki kodda `courseID`, bir sorgu dizesi olarak eklendiğinden, varsayılan rotadaki bir parametreyle eşleşmez.
> 
> [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

Kod, görünüm modelinin bir örneğini oluşturarak ve bu örneğe eğitmen listesine yerleştirilerek başlar. Kod, `Instructor.OfficeAssignment` ve `Instructor.Courses` gezinti özelliği için Eager yüklemeyi belirtir.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs?highlight=3-4)]

İkinci `Include` yöntemi kursu yükler ve yüklenen her kurs için `Course.Department` gezinti özelliği için yükleme yapmaz.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Daha önce belirtildiği gibi, Eager yüklemesi gerekli değildir ancak performansı artırmak için yapılır. Görünüm her zaman `OfficeAssignment` varlığı gerektirdiğinden, bunu aynı sorguda getirmek daha etkilidir. Web sayfasında bir eğitmen seçildiğinde `Course` varlıkların olması gerekir. bu nedenle, yükleme işlemi yalnızca sayfa daha fazla sıklıkta seçili bir kurs ile daha fazla görüntüleniyorsa, yavaş yüklemeden daha iyidir.

Bir eğitmen KIMLIĞI seçilmişse, seçilen eğitmen, görünüm modelindeki eğitmenler listesinden alınır. Görünüm modelinin `Courses` özelliği daha sonra bu eğitmenin `Courses` gezinti özelliğinden `Course` varlıklar ile yüklenir.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

`Where` yöntemi bir koleksiyon döndürür, ancak bu yönteme geçirilen kriterler yalnızca tek bir `Instructor` varlığının döndürüldüğünden sonuçlanır. `Single` yöntemi, koleksiyonu, bu varlığın `Courses` özelliğine erişmenizi sağlayan tek bir `Instructor` varlığına dönüştürür.

Koleksiyonun yalnızca bir öğesi olacağını bildiğiniz durumlarda [tek](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) yöntemi bir koleksiyonda kullanırsınız. `Single` yöntemi, kendisine geçirilen koleksiyon boşsa veya birden fazla öğe varsa bir özel durum oluşturur. Bir alternatif, koleksiyon boşsa varsayılan bir değer (Bu durumda`null`) döndüren [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)değeridir. Bununla birlikte, bu durumda yine de bir özel durumla sonuçlanacaktır (bir `null` başvurusu üzerinde `Courses` özelliği bulmaya çalışırken) ve özel durum iletisi sorunun nedenini daha az gösterir. `Single` yöntemini çağırdığınızda, ayrıca `Where` yöntemini ayrı çağırmak yerine `Where` koşulu da geçirebilirsiniz:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Onun yerine:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

Ardından, bir kurs seçilmişse, seçilen kurs, görünüm modelindeki kurslar listesinden alınır. Ardından, görünüm modelinin `Enrollments` özelliği, bu kursun `Enrollments` gezinti özelliğinden `Enrollment` varlıklar ile yüklenir.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

### <a name="modifying-the-instructor-index-view"></a>Eğitmen dizini görünümünü değiştirme

*Views\komutctor\ındex.cshtml*içinde, mevcut kodu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml?highlight=1,4,18,22-27,29,43-48)]

Varolan koda aşağıdaki değişiklikleri yaptınız:

- Model sınıfı `InstructorIndexData`olarak değiştirildi.
- Sayfa başlığı **dizinden** **eğitmenler**olarak değiştirildi.
- Satır bağlantısı sütunları sola taşındı.
- **FullName** sütunu kaldırıldı.
- Yalnızca `item.OfficeAssignment` null değilse `item.OfficeAssignment.Location` görüntüleyen bir **Office** sütunu eklendi. (Bu bire sıfır veya-bir ilişki olduğundan ilgili `OfficeAssignment` varlığı bulunmayabilir.) 

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]
- Seçilen eğitmenin `tr` öğesine dinamik olarak `class="selectedrow"` ekleyen kod eklendi. Bu, daha önce oluşturduğunuz CSS sınıfını kullanarak seçili satır için bir arka plan rengi ayarlar. (`valign` özniteliği, tabloya çok satırlı bir sütun eklediğinizde aşağıdaki öğreticide yararlı olacaktır.) 

    [!code-html[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html)]
- Her satırdaki diğer bağlantılardan hemen önce **Seç** etiketli yeni bir `ActionLink` eklediniz, bu da SEÇILI eğitmen kimliğinin `Index` yöntemine gönderilmesine neden olur.

Uygulamayı çalıştırın ve **eğitmenler** sekmesini seçin. Bu sayfa ilgili `OfficeAssignment` varlıkların `Location` özelliğini ve ilişkili `OfficeAssignment` varlığı olmadığında boş bir tablo hücresini görüntüler.

![Instructors_index_page_with_nothing_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

*Views\komutctor\ındex.cshtml* dosyasında, kapanış `table` öğesinden sonra (dosyanın sonunda), aşağıdaki vurgulanmış kodu ekleyin. Bu, bir eğitmen seçildiğinde bir eğitmenin ilgili kursların bir listesini görüntüler.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=11-46)]

Bu kod, kurs listesini görüntülemek için görünüm modelinin `Courses` özelliğini okur. Ayrıca, seçilen kursun KIMLIĞINI `Index` eylem yöntemine gönderen bir `Select` köprü sağlar.

> [!NOTE]
> *. Css* dosyası tarayıcılar tarafından önbelleğe alınır. Uygulamayı çalıştırdığınızda değişiklikleri görmüyorsanız, bir sabit yenileme yapın ( **Yenile** düğmesine tıklarken Ctrl tuşunu basılı tutun veya CTRL + F5 tuşlarına basın).

Sayfayı çalıştırın ve bir eğitmen seçin. Artık Seçili eğitmenin atandığı kursları görüntüleyen bir kılavuz görürsünüz ve her kurs için atanan departmanın adını görürsünüz.

![Instructors_index_page_with_instructor_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Yeni eklediğiniz kod bloğundan sonra aşağıdaki kodu ekleyin. Bu, kurs seçildiğinde bir kursa kaydedilen öğrencilerin listesini görüntüler.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml)]

Bu kod, kursa kayıtlı öğrencilerin listesini görüntülemek için görünüm modelinin `Enrollments` özelliğini okur.

Sayfayı çalıştırın ve bir eğitmen seçin. Ardından, kayıtlı öğrenciler ve bunların onların listesini görmek için bir kurs seçin.

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="adding-explicit-loading"></a>Açık yükleme ekleniyor

*InstructorController.cs* ' i açın ve `Index` yönteminin seçili bir kurs için kayıtlar listesini nasıl aldığından öğrenin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

Eğitmenler listesini aldığınızda, `Courses` gezinti özelliği ve her kursun `Department` özelliği için Eager yüklemeyi belirttiniz. Daha sonra, `Courses` koleksiyonunu görünüm modeline yerleştirin ve artık bu koleksiyondaki bir varlıktan `Enrollments` gezinti özelliğine erişiyorsunuz. `Course.Enrollments` gezinti özelliği için bir Eager yüklemesi belirtmediğinizden, bu özelliğin verileri, yavaş yükleme sonucu olarak sayfada görünür.

Herhangi bir şekilde kodu değiştirmeden geç yüklemeyi devre dışı bırakırsanız, Kurstaki kayıt sayısına bakılmaksızın `Enrollments` özelliği null olur. Bu durumda, `Enrollments` özelliğini yüklemek için Eager yükleme veya açık yükleme seçeneklerinden birini belirtmeniz gerekir. Nasıl yükleme yapılacağını zaten gördünüz. Açık yüklemeye bir örnek görmek için `Index` yöntemini, `Enrollments` özelliğini açıkça yükleyen aşağıdaki kodla değiştirin. Değiştirilen kod vurgulanır.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=20-27)]

Seçili `Course` varlığı alındıktan sonra, yeni kod bu kursun `Enrollments` gezinti özelliğini açıkça yükler:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

Ardından, her bir `Enrollment` varlığının ilgili `Student` varlığını açıkça yükler:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

Bir koleksiyon özelliğini yüklemek için `Collection` yöntemini kullanacağınızı, ancak yalnızca bir varlık tutan bir özellik için `Reference` yöntemini kullanacağınızı unutmayın. Artık eğitmen dizini sayfasını çalıştırabilirsiniz ve sayfada görüntülendikleriyle ilgili hiçbir fark görmezsiniz; ancak verilerin nasıl alındığını değiştirmiş olursunuz.

## <a name="summary"></a>Özet

Artık ilgili verileri gezinti özelliklerine yüklemek için üç yolu (Lazy, Eager ve açık) kullandınız. Sonraki öğreticide ilgili verileri güncelleştirme hakkında bilgi edineceksiniz.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Önceki](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
> [İleri](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
