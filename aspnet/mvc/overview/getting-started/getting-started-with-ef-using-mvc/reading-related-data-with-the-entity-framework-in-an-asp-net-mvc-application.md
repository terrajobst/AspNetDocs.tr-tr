---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: ASP.NET MVC uygulamasında EF ile ilgili verileri okuma'
description: Bu öğreticide ilgili verileri (yani Entity Framework, gezinti özelliklerine yüklediği verileri) okuyup görüntüleyeceksiniz.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 18cdd896-8ed9-4547-b143-114711e3eafb
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d804c8dd45ad131949260c85d9d9c6683bfe9646
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445652"
---
# <a name="tutorial-read-related-data-with-ef-in-an-aspnet-mvc-app"></a>Öğretici: ASP.NET MVC uygulamasında EF ile ilgili verileri okuma

Önceki öğreticide okul veri modelini tamamladınız. Bu öğreticide ilgili verileri (yani Entity Framework, gezinti özelliklerine yüklediği verileri) okuyup görüntüleyeceksiniz.

Aşağıdaki çizimlerde, birlikte çalışacağımız sayfalar gösterilmektedir.

![](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructors_index_page_with_instructor_and_course_selected](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASPNET-MVC-Application-b01a9fe8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 6 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 5 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın.

Bu öğreticide şunları yapabilirsiniz:

> [!div class="checklist"]
> * İlgili verileri yüklemeyi öğrenin
> * Kurslar sayfası oluşturma
> * Eğitmenler sayfası oluşturma

## <a name="prerequisites"></a>Prerequisites

* [Daha karmaşık veri modeli oluşturma](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="learn-how-to-load-related-data"></a>İlgili verileri yüklemeyi öğrenin

Entity Framework bir varlığın gezinti özelliklerine ilgili verileri yükleyebilmesinin birkaç yolu vardır:

- *Yavaş yükleme*. Varlık ilk kez okunmadıysa ilgili veriler alınmadı. Ancak, bir gezinti özelliğine ilk kez erişmeye çalıştığınızda, bu gezinti özelliği için gereken veriler otomatik olarak alınır. Bu, tek bir varlığın kendisi için ve varlık için ilgili verilerin alınması gereken her seferinde veritabanına gönderilen birden çok sorguya neden olur. `DbContext` sınıfı varsayılan olarak yavaş yüklemeye izin vermez.

    ![Lazy_loading_example](https://asp.net/media/2577850/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Lazy_loading_example_2c44eabb-5fd3-485a-837d-8e3d053f2c0c.png)
- *Eager yükleniyor*. Varlık okurken ilgili veriler onunla birlikte alınır. Bu, genellikle gereken tüm verileri alan tek bir JOIN sorgusuna neden olur. `Include` yöntemini kullanarak Eager yükleme belirtirsiniz.

    ![Eager_loading_example](https://asp.net/media/2577856/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Eager_loading_example_33f907ff-f0b0-4057-8e75-05a8cacac807.png)
- *Açık yükleme*. Bu, yavaş yüklemeye benzer, ancak kodda ilgili verileri açıkça almanızı sağlar; bir gezinti özelliğine eriştiğinizde otomatik olarak gerçekleşmez. Bir varlık için nesne durumu Yöneticisi girişini alarak ve [koleksiyon Için Collection. Load](https://msdn.microsoft.com/library/gg696220(v=vs.103).aspx) yöntemini ya da tek bir varlığı tutan özellikler için [Reference. Load](https://msdn.microsoft.com/library/gg679166(v=vs.103).aspx) metodunu çağırarak ilgili verileri el ile yüklersiniz. (Aşağıdaki örnekte, yönetici gezinti özelliğini yüklemek istediğinizde `Collection(x => x.Courses)` `Reference(x => x.Administrator)`ile değiştirirsiniz.) Genellikle, yalnızca yavaş yüklemeyi kapattığınız zaman açık yüklemeyi kullanırsınız.

    ![Explicit_loading_example](https://asp.net/media/2577862/Windows-Live-Writer_Reading-Re.NET-MVC-Application-5-of-10h1_ADC3_Explicit_loading_example_79d8c368-6d82-426f-be9a-2b443644ab15.png)

Özellik değerlerini hemen almadıklarından, geç yükleme ve açık yükleme aynı zamanda *ertelenmiş yükleme*olarak da bilinir.

### <a name="performance-considerations"></a>Performans değerlendirmeleri

Alınan her varlık için ilgili verilerin gerekli olduğunu biliyorsanız, tek bir sorgu genellikle en iyi performansı sunar, çünkü veritabanına gönderilen tek bir sorgu genellikle alınan her varlık için ayrı sorgulardan daha etkilidir. Örneğin, Yukarıdaki örneklerde, her departmanın on ile ilgili kurs olduğunu varsayalım. Eager yükleme örneği yalnızca tek bir (JOIN) sorgusuna ve veritabanına yönelik tek bir gidiş dönüş oluşmasına neden olur. Yavaş yükleme ve açık yükleme örnekleri, her ikisi de on bir sorgu ve veritabanı üzerinde on bir gidiş dönüş ile sonuçlanır. Gecikme süresi yüksek olduğunda veritabanına yönelik ek gidiş dönüşler özellikle performansa neden olur.

Öte yandan, bazı senaryolarda geç yükleme daha etkilidir. Eager yüklemesi, SQL Server verimli bir şekilde işleyemeyecek çok karmaşık bir birleştirmenin oluşturulmasına neden olabilir. Ya da bir varlığın gezinti özelliklerine yalnızca işlemekte olduğunuz varlıkların kümesinin bir alt kümesi için erişmeniz gerekiyorsa, Eager yüklemesi gereksiniminizden daha fazla veri alacağından, yavaş yükleme daha iyi çalışabilir. Performans önemliyse, en iyi seçimi yapmak için her iki şekilde de performansı test etmek en iyisidir.

Yavaş yükleme, performans sorunlarına neden olan kodu maskeleyebilir. Örneğin, Eager veya açık yükleme belirtmeyen, ancak yüksek hacimli varlıkları işleyen ve her yinelemede birçok gezinti özelliği kullanan kod çok verimsiz olabilir (veritabanına gidiş dönüş nedeniyle). Şirket içi SQL Server 'ı kullanarak geliştirmede iyi işlem yapan bir uygulama, artan gecikme süresi ve yavaş yükleme nedeniyle Azure SQL veritabanı 'na taşındığında performans sorunlarına neden olabilir. Veritabanı sorgularının gerçekçi bir test yüklemesiyle profili oluşturulması, geç yüklemenin uygun olup olmadığını belirlemenize yardımcı olur. Daha fazla bilgi için bkz. [Demystifying Entity Framework stratejileri: Ilgili verileri yükleme](https://msdn.microsoft.com/magazine/hh205756.aspx) ve [Entity Framework kullanarak SQL Azure ağ gecikmesini azaltma](https://msdn.microsoft.com/magazine/gg309181.aspx).

### <a name="disable-lazy-loading-before-serialization"></a>Serileştirme öncesinde geç yüklemeyi devre dışı bırak

Serileştirme sırasında geç yüklemeyi etkin bırakırsanız, amaçlamadan çok daha fazla veri sorgulama işlemi gerçekleştirebilirsiniz. Serileştirme genellikle bir türün örneğindeki her özelliğe erişerek işe yarar. Özellik erişimi, yavaş yüklemeyi tetikler ve bu yavaş yüklenen varlıklar serileştirilir. Seri hale getirme işlemi daha sonra, yavaş yüklenen varlıkların her özelliğine erişir, bu da daha fazla yavaş yükleme ve Serileştirmeye neden olabilir. Bu çalışma zinciri yeniden eylemini engellemek için, bir varlığı serileştirmadan önce yavaş yüklemeyi kapatın.

Serileştirme, [Gelişmiş senaryolar öğreticisinde](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#proxies)açıklandığı gibi Entity Framework kullandığı proxy sınıfları tarafından da karmaşık olabilir.

Serileştirme sorunlarından kaçınmak için bir yol, varlık nesneleri yerine veri aktarımı nesneleri (DTOs) seri hale getirmenin yanı [Entity Framework, Web API 'Sini kullanma](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-5.md) öğreticisinde gösterildiği gibi.

DTOs kullanmıyorsanız, yavaş yüklemeyi devre dışı bırakabilir ve [proxy oluşturmayı devre dışı bırakarak](https://msdn.microsoft.com/data/jj592886.aspx)proxy sorunlarından kaçınabilirsiniz.

[Yavaş yüklemeyi devre dışı bırakmak için](https://msdn.microsoft.com/data/jj574232)bazı diğer yollar şunlardır:

- Belirli gezinme özellikleri için, özelliği bildirdiğinizde `virtual` anahtar sözcüğünü atlayın.
- Tüm gezinti özellikleri için `LazyLoadingEnabled` `false`olarak ayarlayın, aşağıdaki kodu bağlam sınıfınızın oluşturucusuna koyun:

    [!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="create-a-courses-page"></a>Kurslar sayfası oluşturma

`Course` varlığı, kursun atandığı departmanın `Department` varlığını içeren bir gezinti özelliği içerir. Bir kurs listesinde atanan departmanın adını göstermek için, `Course.Department` Gezinti özelliğindeki `Department` varlığındaki `Name` özelliğini almanız gerekir.

`Student` denetleyicisi için daha önce yaptığınız Entity Framework desteği **kullanarak, MVC 5 denetleyici ile** aynı seçenekleri kullanarak `Course` varlık türü için `CourseController` (coursescontroller) adlı bir denetleyici oluşturun:

| Ayar | Değer |
| ------- | ----- |
| Model sınıfı | **Kurs (ContosoUniversity. modeller)** seçeneğini belirleyin. |
| Veri bağlamı sınıfı | **SchoolContext (ContosoUniversity. dal)** öğesini seçin. |
| Denetleyici adı | *Coursecontroller*girin. Yeniden, bir *s*Ile *Kurs denetleyicisi* değil. **Kursu (ContosoUniversity. modeller)** seçtiğinizde, **Denetleyici adı** değeri otomatik olarak doldurulur. Değeri değiştirmeniz gerekir. |

Diğer varsayılan değerleri bırakın ve denetleyiciyi ekleyin.

*Controllers\coursecontroller.cs* ' i açın ve `Index` yöntemine bakın:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Otomatik yapı iskelesi, `Department` gezinti özelliği için `Include` yöntemi kullanılarak bir Eager yüklemesi belirtti.

*Views\course\ındex.cshtml* dosyasını açın ve şablon kodunu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=4,7,14-16,23-25,31-33,40-42)]

Yapı iskelesi kodunda aşağıdaki değişiklikleri yaptınız:

- Başlık **dizinden** **Kurslar**olarak değiştirildi.
- `CourseID` özellik değerini gösteren bir **sayı** sütunu eklendi. Birincil anahtarlar, genellikle son kullanıcılara anlamlı olduklarından, varsayılan olarak iskele değildir. Ancak, bu durumda birincil anahtar anlamlı olur ve göstermek istersiniz.
- **Departman** sütunu sağ tarafa taşındı ve başlığını değiştirdi. Desteği, `Department` varlığındaki `Name` özelliğini doğru şekilde görüntülemeyi tercih ediyor, ancak buradaki kurs sayfasında sütun başlığı **ad**yerine **Departman** olmalıdır.

Bölüm sütunu için, yapı iskelesi kodu, `Department` gezinti özelliğine yüklenen `Department` varlığının `Name` özelliğini gösterir:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=2)]

Bölüm adlarıyla listeyi görmek için sayfayı çalıştırın (contoso Üniversitesi giriş sayfasında **Kurslar** sekmesini seçin).

## <a name="create-an-instructors-page"></a>Eğitmenler sayfası oluşturma

Bu bölümde, Eğitmenler sayfasını görüntülemek için `Instructor` varlık için bir denetleyici ve görünüm oluşturacaksınız. Bu sayfa aşağıdaki yollarla ilgili verileri okur ve görüntüler:

- Eğitmenler listesi `OfficeAssignment` varlığındaki ilgili verileri görüntüler. `Instructor` ve `OfficeAssignment` varlıkları bire sıfır veya-bir ilişkidir. `OfficeAssignment` varlıkları için Eager yükleme kullanacaksınız. Daha önce açıklandığı gibi, birincil tablonun alınan tüm satırları için ilgili verilere ihtiyacınız olduğunda Eager yüklemesi genellikle daha etkilidir. Bu durumda, tüm görüntülenen Eğitmenler için Office atamalarını göstermek istersiniz.
- Kullanıcı bir eğitmen seçtiğinde, ilgili `Course` varlıkları görüntülenir. `Instructor` ve `Course` varlıkları çoktan çoğa bir ilişkidir. `Course` varlıkları ve ilgili `Department` varlıkları için Eager yükleme kullanacaksınız. Bu durumda, yalnızca seçili eğitmen için kurslar gerektiğinden, geç yükleme daha verimli olabilir. Ancak, bu örnek, gezinti özellikleri ' nde olan varlıkların içindeki gezinti özellikleri için Eager yükleme 'nin nasıl kullanılacağını gösterir.
- Kullanıcı bir kurs seçtiğinde `Enrollments` varlık kümesinden ilgili veriler görüntülenir. `Course` ve `Enrollment` varlıkları bire çok ilişkidir. `Enrollment` varlıkları ve ilgili `Student` varlıklarını için açık yükleme ekleyeceksiniz. (Açık yükleme gerekli değildir çünkü Lazy yüklemesi etkindir, ancak bu, açık yüklemenin nasıl yapılacağını gösterir.)

### <a name="create-a-view-model-for-the-instructor-index-view"></a>Eğitmen dizini görünümü için bir görünüm modeli oluşturun

Eğitmenler sayfasında üç farklı tablo gösterilir. Bu nedenle, her biri tablolardan birine ait verileri tutan üç özellik içeren bir görünüm modeli oluşturacaksınız.

*Viewmodeller* klasöründe *InstructorIndexData.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

### <a name="create-the-instructor-controller-and-views"></a>Eğitmen denetleyicisi ve görünümleri oluşturma

EF okuma/yazma eylemiyle `InstructorController` (Komutctorscontroller değil) denetleyicisi oluşturun:

| Ayar | Değer |
| ------- | ----- |
| Model sınıfı | **Eğitmen (ContosoUniversity. modeller)** öğesini seçin. |
| Veri bağlamı sınıfı | **SchoolContext (ContosoUniversity. dal)** öğesini seçin. |
| Denetleyici adı | *Komutctorcontroller*girin. Yine *, bir ile*birlikte *Komutctorscontroller* değil. **Kursu (ContosoUniversity. modeller)** seçtiğinizde, **Denetleyici adı** değeri otomatik olarak doldurulur. Değeri değiştirmeniz gerekir. |

Diğer varsayılan değerleri bırakın ve denetleyiciyi ekleyin.

*Controllers\komutctorcontroller.cs* dosyasını açın ve `ViewModels` ad alanı için `using` bir ifade ekleyin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

`Index` yöntemi içindeki scafkatlı kod yalnızca `OfficeAssignment` gezinti özelliği için Eager yüklemeyi belirtir:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

`Index` yöntemini, ek ilgili verileri yüklemek ve görünüm modeline koymak için aşağıdaki kodla değiştirin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Yöntemi, isteğe bağlı yol verilerini (`id`) ve seçilen eğitmenin ve seçili kursun KIMLIK değerlerini sağlayan bir sorgu dizesi parametresini (`courseID`) kabul eder ve gerekli tüm verileri görünüme geçirir. Parametreler, sayfadaki Köprü **seçme** ile sağlanır.

Kod, görünüm modelinin bir örneğini oluşturarak ve bu örneğe eğitmen listesine yerleştirilerek başlar. Kod, `Instructor.OfficeAssignment` ve `Instructor.Courses` gezinti özelliği için Eager yüklemeyi belirtir.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=3-4)]

İkinci `Include` yöntemi kursu yükler ve yüklenen her kurs için `Course.Department` gezinti özelliği için yükleme yapmaz.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

Daha önce belirtildiği gibi, Eager yüklemesi gerekli değildir ancak performansı artırmak için yapılır. Görünüm her zaman `OfficeAssignment` varlığı gerektirdiğinden, bunu aynı sorguda getirmek daha etkilidir. Web sayfasında bir eğitmen seçildiğinde `Course` varlıkların olması gerekir. bu nedenle, yükleme işlemi yalnızca sayfa daha fazla sıklıkta seçili bir kurs ile daha fazla görüntüleniyorsa, yavaş yüklemeden daha iyidir.

Bir eğitmen KIMLIĞI seçilmişse, seçilen eğitmen, görünüm modelindeki eğitmenler listesinden alınır. Görünüm modelinin `Courses` özelliği daha sonra bu eğitmenin `Courses` gezinti özelliğinden `Course` varlıklar ile yüklenir.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Where` yöntemi bir koleksiyon döndürür, ancak bu yönteme geçirilen kriterler yalnızca tek bir `Instructor` varlığının döndürüldüğünden sonuçlanır. `Single` yöntemi, koleksiyonu, bu varlığın `Courses` özelliğine erişmenizi sağlayan tek bir `Instructor` varlığına dönüştürür.

Koleksiyonun yalnızca bir öğesi olacağını bildiğiniz durumlarda [tek](https://msdn.microsoft.com/library/system.linq.enumerable.single.aspx) yöntemi bir koleksiyonda kullanırsınız. `Single` yöntemi, kendisine geçirilen koleksiyon boşsa veya birden fazla öğe varsa bir özel durum oluşturur. Bir alternatif, koleksiyon boşsa varsayılan bir değer (Bu durumda`null`) döndüren [SingleOrDefault](https://msdn.microsoft.com/library/bb342451.aspx)değeridir. Bununla birlikte, bu durumda yine de bir özel durumla sonuçlanacaktır (bir `null` başvurusu üzerinde `Courses` özelliği bulmaya çalışırken) ve özel durum iletisi sorunun nedenini daha az gösterir. `Single` yöntemini çağırdığınızda, ayrıca `Where` yöntemini ayrı çağırmak yerine `Where` koşulu da geçirebilirsiniz:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

Onun yerine:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Ardından, bir kurs seçilmişse, seçilen kurs, görünüm modelindeki kurslar listesinden alınır. Ardından, görünüm modelinin `Enrollments` özelliği, bu kursun `Enrollments` gezinti özelliğinden `Enrollment` varlıklar ile yüklenir.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

### <a name="modify-the-instructor-index-view"></a>Eğitmen dizini görünümünü değiştirme

*Views\komutctor\ındex.cshtml*içinde, şablon kodunu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır:

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1,4,14-18,21,23-28,38-43,45)]

Varolan koda aşağıdaki değişiklikleri yaptınız:

- Model sınıfı `InstructorIndexData` olarak değiştirildi.
- Sayfa başlığı **dizinden** **eğitmenler**olarak değiştirildi.
- Yalnızca `item.OfficeAssignment` null değilse `item.OfficeAssignment.Location` görüntüleyen bir **Office** sütunu eklendi. (Bu bire sıfır veya-bir ilişki olduğundan ilgili `OfficeAssignment` varlığı bulunmayabilir.)

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]
- Seçilen eğitmenin `tr` öğesine dinamik olarak `class="success"` ekleyen kod eklendi. Bu, bir [önyükleme](../../../../visual-studio/overview/2013/creating-web-projects-in-visual-studio.md#bootstrap) sınıfı kullanarak seçili satır için bir arka plan rengi ayarlar.

    [!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]
- Her satırdaki diğer bağlantılardan hemen önce **Seç** etiketli yeni bir `ActionLink` eklediniz, bu da SEÇILI eğitmen kimliğinin `Index` yöntemine gönderilmesine neden olur.

Uygulamayı çalıştırın ve **eğitmenler** sekmesini seçin. Bu sayfa ilgili `OfficeAssignment` varlıkların `Location` özelliğini ve ilişkili `OfficeAssignment` varlığı olmadığında boş bir tablo hücresini görüntüler.

*Views\komutctor\ındex.cshtml* dosyasında, kapanış `table` öğesinden sonra (dosyanın sonunda) aşağıdaki kodu ekleyin. Bu kod, bir eğitmen seçildiğinde bir eğitmenin ilgili kursların bir listesini görüntüler.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

Bu kod, kurs listesini görüntülemek için görünüm modelinin `Courses` özelliğini okur. Ayrıca, seçilen kursun KIMLIĞINI `Index` eylem yöntemine gönderen bir `Select` köprü sağlar.

Sayfayı çalıştırın ve bir eğitmen seçin. Artık Seçili eğitmenin atandığı kursları görüntüleyen bir kılavuz görürsünüz ve her kurs için atanan departmanın adını görürsünüz.

Yeni eklediğiniz kod bloğundan sonra aşağıdaki kodu ekleyin. Bu, kurs seçildiğinde bir kursa kaydedilen öğrencilerin listesini görüntüler.

[!code-cshtml[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Bu kod, kursa kayıtlı öğrencilerin listesini görüntülemek için görünüm modelinin `Enrollments` özelliğini okur.

Sayfayı çalıştırın ve bir eğitmen seçin. Ardından, kayıtlı öğrenciler ve bunların onların listesini görmek için bir kurs seçin.

### <a name="adding-explicit-loading"></a>Açık yükleme ekleniyor

*InstructorController.cs* ' i açın ve `Index` yönteminin seçili bir kurs için kayıtlar listesini nasıl aldığından öğrenin:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

Eğitmenler listesini aldığınızda, `Courses` gezinti özelliği ve her kursun `Department` özelliği için Eager yüklemeyi belirttiniz. Daha sonra, `Courses` koleksiyonunu görünüm modeline yerleştirin ve artık bu koleksiyondaki bir varlıktan `Enrollments` gezinti özelliğine erişiyorsunuz. `Course.Enrollments` gezinti özelliği için bir Eager yüklemesi belirtmediğinizden, bu özelliğin verileri, yavaş yükleme sonucu olarak sayfada görünür.

Herhangi bir şekilde kodu değiştirmeden geç yüklemeyi devre dışı bırakırsanız, Kurstaki kayıt sayısına bakılmaksızın `Enrollments` özelliği null olur. Bu durumda, `Enrollments` özelliğini yüklemek için Eager yükleme veya açık yükleme seçeneklerinden birini belirtmeniz gerekir. Nasıl yükleme yapılacağını zaten gördünüz. Açık yüklemeye bir örnek görmek için `Index` yöntemini, `Enrollments` özelliğini açıkça yükleyen aşağıdaki kodla değiştirin. Değiştirilen kod vurgulanır.

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs?highlight=20-31)]

Seçili `Course` varlığı alındıktan sonra, yeni kod bu kursun `Enrollments` gezinti özelliğini açıkça yükler:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

Ardından, her bir `Enrollment` varlığının ilgili `Student` varlığını açıkça yükler:

[!code-csharp[Main](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cs)]

Bir koleksiyon özelliğini yüklemek için `Collection` yöntemini kullanacağınızı, ancak yalnızca bir varlık tutan bir özellik için `Reference` yöntemini kullanacağınızı unutmayın.

Şimdi eğitmen dizini sayfasını çalıştırın ve sayfada görüntülendikleriyle ilgili hiçbir fark görmezsiniz; ancak verilerin nasıl alındığını değiştirmiş olursunuz.

## <a name="get-the-code"></a>Kodu alın

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET Data Access-önerilen kaynaklarda](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yapabilirsiniz:

> [!div class="checklist"]
> * İlgili verileri yükleme hakkında öğrenilen
> * Bir kurslar sayfası oluşturuldu
> * Bir eğitmenler sayfası oluşturuldu

İlgili verileri güncelleştirme hakkında bilgi edinmek için sonraki makaleye ilerleyin.

> [!div class="nextstepaction"]
> [İlgili verileri güncelleştirme](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
