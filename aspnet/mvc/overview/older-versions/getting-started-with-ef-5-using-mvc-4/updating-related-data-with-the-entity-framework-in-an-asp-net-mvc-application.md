---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC uygulamasındaki Entity Framework Ilişkili verileri güncelleştirme (6/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 7871dc05-2750-470f-8b4c-3a52511949bc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: d29cb172d642b67947b461d1a7e55d01872bb8c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74592435"
---
# <a name="updating-related-data-with-the-entity-framework-in-an-aspnet-mvc-application-6-of-10"></a>ASP.NET MVC uygulamasındaki Entity Framework Ilişkili verileri güncelleştirme (6/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticide ilgili verileri görüntülediyseniz; Bu öğreticide ilgili verileri güncelleştireceksiniz. Çoğu ilişki için, bu, uygun yabancı anahtar alanları güncelleştirilerek yapılabilir. Çoka çok ilişkiler için Entity Framework, JOIN tablosunu doğrudan kullanıma sunmaz, bu nedenle, uygun gezinti özelliklerine ve içindeki varlıkları açıkça eklemeniz ve kaldırmanız gerekir.

Aşağıdaki çizimlerde, birlikte çalışacağımız sayfalar gösterilmektedir.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="customize-the-create-and-edit-pages-for-courses"></a>Kurslar için oluşturma ve düzenleme sayfalarını özelleştirme

Yeni bir kurs varlığı oluşturulduğunda, mevcut bir departmanla bir ilişkisi olmalıdır. Bunu kolaylaştırmak için, yapı iskelesi kodu denetleyici yöntemlerini içerir ve departmanı seçmeye yönelik bir açılan liste içeren görünümler oluşturup düzenleyebilir. Açılan liste `Course.DepartmentID` yabancı anahtar özelliğini ayarlar ve bu, `Department` gezinti özelliğini uygun `Department` varlığıyla yüklemek için tüm Entity Framework gereksinimlidir. Scafkatmış kodu kullanacaksınız, ancak hata işleme eklemek ve açılan listeyi sıralamak için biraz değişiklik yapacaksınız.

*CourseController.cs*' de, dört `Edit` ve `Create` yöntemleri silin ve bunları şu kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,10,13-14,21-27,34,41,44-45,52-58,62-68)]

`PopulateDepartmentsDropDownList` yöntemi, ada göre sıralanmış tüm bölümlerin bir listesini alır, açılan liste için bir `SelectList` koleksiyonu oluşturur ve koleksiyonu bir `ViewBag` özelliğindeki görünüme geçirir. Yöntemi, çağıran kodun, açılan liste işlendiğinde seçilecek öğeyi belirtmesini sağlayan isteğe bağlı `selectedDepartment` parametresini kabul eder. Görünüm adı `DepartmentID` [`DropDownList` Yardımcısı](../working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md)' na geçecek ve yardımcı sonra `ViewBag` nesnesine `DepartmentID`adlı bir `SelectList` bakabilecektir.

`HttpGet` `Create` yöntemi, seçilen öğeyi ayarlamadan `PopulateDepartmentsDropDownList` yöntemini çağırır, çünkü yeni bir kurs için departman henüz kurulmadı:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`HttpGet` `Edit` yöntemi, düzenlenen kursa zaten atanmış departmanın KIMLIğINE bağlı olarak seçili öğeyi ayarlar:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

Hem `Create` hem de `Edit` için `HttpPost` yöntemleri, bir hatadan sonra sayfayı yeniden görüntülerken seçili öğeyi ayarlayan kodu içerir:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Bu kod, sayfa hata iletisini göstermek için yeniden görüntülendiğinde, seçilen bölümün seçili kalırsa emin olmanızı sağlar.

*Views\course\create.exe*' de, **başlık** alanından önce yeni bir kurs numarası alanı oluşturmak için vurgulanan kodu ekleyin. Önceki bir öğreticide açıklandığı gibi, birincil anahtar alanları varsayılan olarak iskele değildir, ancak bu birincil anahtar anlamlı olduğundan kullanıcının anahtar değerini girebilmesini istersiniz.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=17-23)]

*Views\course\edit.exe*, *Views\course\delete.exe*ve *Views\course\details.cshtml*içinde **başlık** alanından önce bir kurs numarası alanı ekleyin. Birincil anahtar olduğundan, görüntülenir, ancak değiştirilemez.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

**Oluştur** sayfasını çalıştırın (kurs dizinini görüntüle sayfasını ve **Yeni oluştur**' a tıklayın) ve yeni bir kurs için veri girin:

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

**Oluştur**'u tıklatın. Kurs dizini sayfası, listeye eklenen yeni kursla birlikte görüntülenir. Dizin sayfası listesindeki departman adı, ilişkinin doğru şekilde oluşturulduğunu gösteren gezinti özelliğinden gelir.

![Course_Index_page_showing_new_course](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

**Düzenleme** sayfasını çalıştırın (kurs dizinini görüntüleyin ve bir kurs üzerinde **Düzenle** ' ye tıklayın).

![Course_edit_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Sayfadaki verileri değiştirin ve **Kaydet**' e tıklayın. Kurs dizini sayfası, güncelleştirilmiş kurs verileriyle birlikte görüntülenir.

## <a name="adding-an-edit-page-for-instructors"></a>Eğitmenler için düzenleme sayfası ekleme

Bir eğitmen kaydını düzenlediğinizde, eğitmenin Office atamasını güncelleştirebilmek istersiniz. `Instructor` varlığı, `OfficeAssignment` varlığı ile bire sıfır veya-arasında bir ilişkiye sahiptir; yani aşağıdaki durumları işlemeniz gerekir:

- Kullanıcı Office atamasını temizlediğinde ve başlangıçta bir değer içeriyorsa, `OfficeAssignment` varlığını kaldırmanız ve silmeniz gerekir.
- Kullanıcı bir Office atama değeri girerse ve başlangıçta boşsa, yeni bir `OfficeAssignment` varlığı oluşturmanız gerekir.
- Kullanıcı bir Office atamasının değerini değiştirirse, mevcut bir `OfficeAssignment` varlığındaki değeri değiştirmeniz gerekir.

*InstructorController.cs* ' i açın ve `HttpGet` `Edit` yöntemine bakın:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Burada scafkatlama kodu istediğiniz gibi değildir. Bu, bir açılan liste için veri ayarlıyor, ancak ihtiyacınız olan bir metin kutusu. Bu yöntemi aşağıdaki kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Bu kod `ViewBag` ifadesini bırakır ve ilişkili `OfficeAssignment` varlığı için ekip yükleme ekler. `Find` yöntemiyle Eager yüklemesi gerçekleştiremezsiniz, bu nedenle `Where` ve `Single` yöntemleri eğitmeni seçmek için kullanılır.

`HttpPost` `Edit` yöntemini aşağıdaki kodla değiştirin. Office atama güncelleştirmelerini işleyen:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Kod şunları yapar:

- `OfficeAssignment` gezinti özelliği için Eager yükleme kullanarak geçerli `Instructor` varlığını veritabanından alır. Bu, `HttpGet` `Edit` yönteminde yaptığınız şeydir.
- Alınan `Instructor` varlığını model Ciltçideki değerlerle güncelleştirir. Kullanılan [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) aşırı yüklemesi, dahil etmek istediğiniz özellikleri *beyaz listelemenize* olanak sağlar. Bu, [ikinci öğreticide](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)açıklandığı gibi, daha fazla nakletmeyi önler.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]
- Office konumu boşsa, `OfficeAssignment` tablosundaki ilgili satırın silinebilmesi için `Instructor.OfficeAssignment` özelliğini null olarak ayarlar.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]
- Değişiklikleri veritabanına kaydeder.

*Views\komutctor\edit.exe*' de, **işe alma tarihi** alanı için `div` öğelerinden sonra, Office konumunu düzenlemekte yeni bir alan ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml)]

Sayfayı çalıştırın ( **eğitmenler** sekmesini seçin ve ardından bir eğitmende **Düzenle** ' ye tıklayın). **Office konumunu** değiştirin ve **Kaydet**' e tıklayın.

![Changing_the_office_location](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

## <a name="adding-course-assignments-to-the-instructor-edit-page"></a>Eğitmen düzenleme sayfasına kurs atamaları ekleme

Eğitmenler, istediğiniz sayıda kurs öğretebilir. Artık, aşağıdaki ekran görüntüsünde gösterildiği gibi, bir grup onay kutusu kullanarak kurs atamalarını değiştirme özelliğini ekleyerek eğitmen düzenleme sayfasını geliştirirsiniz:

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

`Course` ve `Instructor` varlıkları arasındaki ilişki çoktan çoğa, bu, JOIN tablosuna doğrudan erişiminizin olmadığı anlamına gelir. Bunun yerine, `Instructor.Courses` gezinti özelliğine ve öğesinden varlık ekleyip kaldıracaksınız.

Bir eğitmenin hangi kurslara atandığını değiştirmenize olanak sağlayan kullanıcı arabirimi bir grup onay kutusu olur. Veritabanındaki her kurs için bir onay kutusu görüntülenir ve eğitmenin Şu anda atanmış olduğu yer seçilidir. Kullanıcı kurs atamalarını değiştirmek için onay kutularını seçebilir veya temizleyebilir. Kurs sayısı çok fazlaysa, büyük olasılıkla görünümde verileri göstermek için farklı bir yöntem kullanmak isteyeceksiniz, ancak ilişkiler oluşturmak veya silmek için gezinti özelliklerini düzenleme yöntemini kullanırsınız.

Onay kutuları listesinin görünümüne veri sağlamak için bir görünüm modeli sınıfı kullanacaksınız. *Viewmodeller* klasöründe *AssignedCourseData.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

*InstructorController.cs*' de `HttpGet` `Edit` yöntemini aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=5,8,12-27)]

Kod, `Courses` gezinti özelliği için Eager yüklemesi ekler ve `AssignedCourseData` View model sınıfını kullanarak onay kutusu dizisi bilgilerini sağlamak için yeni `PopulateAssignedCourseData` yöntemini çağırır.

`PopulateAssignedCourseData` yöntemindeki kod, görünüm modeli sınıfını kullanarak bir kurs listesi yüklemek için tüm `Course` varlıklarından okur. Kod, her kurs için, kursun `Courses` gezinti özelliğinde mevcut olup olmadığını denetler. Eğitmenin bir kurs atanıp atanmadığını denetlerken etkili arama oluşturmak için, eğitmene atanan kurslar bir [diyez kümesi](https://msdn.microsoft.com/library/bb359438.aspx) koleksiyonuna konur. `Assigned` özelliği, eğitmenin atandığı kurslar için `true` olarak ayarlanır. Görünüm, hangi onay kutularının seçili olarak gösterileceğini belirlemede bu özelliği kullanır. Son olarak, liste bir `ViewBag` özelliğindeki görünüme geçirilir.

Sonra, Kullanıcı **Kaydet**' i tıklattığında yürütülen kodu ekleyin. `HttpPost` `Edit` yöntemini, `Instructor` varlığının `Courses` gezinti özelliğini güncelleştiren yeni bir yöntemi çağıran aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs?highlight=3,7,20,33,37-65)]

Görünümün bir `Course` varlıkları koleksiyonu olmadığından, model Bağlayıcısı `Courses` gezinti özelliğini otomatik olarak güncelleştiremez. Kurs gezintisi özelliğini güncelleştirmek için model cildi kullanmak yerine, bunu yeni `UpdateInstructorCourses` yönteminde yapmanız gerekir. Bu nedenle `Courses` özelliğini model bağlamadan çıkarmanız gerekir. Bu, *beyaz liste* aşırı yüklemesini kullandığınız ve `Courses` içerme listesinde olmadığı Için [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 'i çağıran kodda herhangi bir değişiklik yapılmasını gerektirmez.

Hiçbir onay kutusu seçilmediyse `UpdateInstructorCourses` kod, `Courses` gezinti özelliğini boş bir koleksiyon ile başlatır:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

Kod daha sonra, veritabanındaki tüm kurslardan geçer ve bu her kursu, görünümde seçili olanlar ile ilgili olarak eğitmenin atandığı her bir kursa karşı denetler. Etkili aramaları kolaylaştırmak için, ikinci iki koleksiyon `HashSet` nesnelerinde depolanır.

Kurs onay kutusu seçilmişse ancak kurs `Instructor.Courses` gezinti özelliğinde değilse, kurs, Gezinti özelliğindeki koleksiyona eklenir.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs)]

Kurs onay kutusu seçilmemişse, ancak kurs `Instructor.Courses` gezinti özelliği ise, kurs, gezinti özelliğinden kaldırılır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

*Views\komutctor\edit.exe*' de, `OfficeAssignment` alanı için `div` öğelerinden hemen sonra aşağıdaki vurgulanmış kodu ekleyerek bir dizi onay kutusu Içeren bir **Kurslar** alanı ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml?highlight=51-73)]

Bu kod, üç sütun içeren bir HTML tablosu oluşturur. Her sütunda, bir onay kutusu ve ardından kurs numarası ve başlığından oluşan bir açıklamalı alt yazı bulunur. Onay kutularının hepsi aynı ada ("Selectedkurslar") sahiptir, bu da model cilde bir grup olarak değerlendirilme bildirir. Her onay kutusunun `value` özniteliği, sayfa gönderildiğinde `CourseID.` değerine ayarlanır, model Ciltçi yalnızca seçili onay kutularının `CourseID` değerlerinden oluşan bir diziyi denetleyiciye geçirir.

Onay kutuları başlangıçta işlendiğinde, eğitmenin atandığı kurslara yönelik olanlar, onları seçen `checked` özniteliklerine sahiptir (bunları işaretli olarak görüntüler).

Kurs atamalarını değiştirdikten sonra, site `Index` sayfasına döndüğünde değişiklikleri doğrulayabilmek isteyeceksiniz. Bu nedenle, bu sayfadaki tabloya bir sütun eklemeniz gerekir. Bu durumda, göstermek istediğiniz bilgiler, sayfaya model olarak geçirdiğiniz `Instructor` varlığının `Courses` gezinti özelliğinde zaten yer aldığı için `ViewBag` nesnesini kullanmanız gerekmez.

*Views\komutctor\ındex.cshtml*içinde, aşağıdaki örnekte gösterildiği gibi, **Office** başlığından hemen sonra bir **Kurslar** başlığı ekleyin:

[!code-html[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.html?highlight=7)]

Ardından, Office konumu ayrıntı hücresini hemen takip eden yeni bir ayrıntı hücresi ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml?highlight=19,50-57)]

Her bir eğitmene atanan kursları görmek için **eğitmen dizini** sayfasını çalıştırın:

![Instructor_index_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Düzenleme sayfasını görmek için bir eğitmende **Düzenle** ' ye tıklayın.

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

Bazı kurs atamalarını değiştirin ve **Kaydet**' e tıklayın. Yaptığınız değişiklikler Dizin sayfasında yansıtılır.

 Note: Eğitmen Kursu verilerini düzenlemek için uygulanan yaklaşım, sınırlı sayıda kurs olduğunda iyi sonuç verir. Çok daha büyük olan koleksiyonlar için, farklı bir kullanıcı arabirimi ve farklı bir güncelleştirme yöntemi gerekir.  

## <a name="update-the-delete-method"></a>Delete metodunu Güncelleştir

Http atama kaydının (varsa) eğitmen silindiğinde silinmesi için HttpPost silme yöntemindeki kodu değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs?highlight=6,10)]

Bir departmana yönetici olarak atanmış bir eğitmeni silmeye çalışırsanız, bir başvuru bütünlüğü hatası alırsınız. Eğitmeni bir yönetici olarak atanan herhangi bir departmandan otomatik olarak kaldıracak olan ek kod için [Bu öğreticinin güncel sürümüne](../../getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) bakın.

## <a name="summary"></a>Özet

Artık ilgili verilerle çalışmaya yönelik bu girişi tamamladınız. Bu öğreticilerde, çok sayıda CRUD işlemi yaptık, ancak eşzamanlılık sorunlarıyla karşılaşmadınız. Sonraki öğreticide eşzamanlılık, işleme için açıklama seçenekleri ve bir varlık türü için zaten yazdığınız CRUD koduna eşzamanlılık işleme ekleme konusu ele alınacaktır.

Diğer Entity Framework kaynaklarına bağlantılar, [Bu serideki son öğreticinin](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)sonunda bulunabilir.

> [!div class="step-by-step"]
> [Önceki](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [İleri](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
