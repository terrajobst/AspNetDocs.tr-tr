---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: bir ASP.NET MVC uygulamasında EF ile ilgili verileri güncelleştirme'
description: Bu öğreticide ilgili verileri güncelleştireceksiniz. Çoğu ilişki için, bu, yabancı anahtar alanları veya gezinti özellikleri güncelleştirilerek yapılabilir.
author: tdykstra
ms.author: riande
ms.date: 01/19/2019
ms.topic: tutorial
ms.assetid: 7ba88418-5d0a-437d-b6dc-7c3816d4ec07
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 4d5f6447fdccefdcdf9497a9e94f23243302a0e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616006"
---
# <a name="tutorial-update-related-data-with-ef-in-an-aspnet-mvc-app"></a>Öğretici: bir ASP.NET MVC uygulamasında EF ile ilgili verileri güncelleştirme

Önceki öğreticide ilgili verileri görüntülediyseniz. Bu öğreticide ilgili verileri güncelleştireceksiniz. Çoğu ilişki için, bu, yabancı anahtar alanları veya gezinti özellikleri güncelleştirilerek yapılabilir. Çoka çok ilişkiler için Entity Framework, JOIN tablosunu doğrudan kullanıma sunmaz, bu yüzden, uygun gezinti özelliklerine ve içindeki varlıkları ekleyip kaldırmanız gerekir.

Aşağıdaki çizimlerde, üzerinde çalıştığınız sayfaların bazıları gösterilmektedir.

![Course_create_page](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Instructor_edit_page_with_courses](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

![Kurslar ile eğitmen düzenleme](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Kurslar sayfalarını özelleştirme
> * Office 'i eğitmenler sayfasına Ekle
> * Eğitmenler sayfasına kurslar ekleyin
> * Deleteonaylandı Güncelleştir
> * Oluşturma sayfasına Office konum ve kurslar ekleme

## <a name="prerequisites"></a>Önkoşullar

* [İlgili Verileri Okuma](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-courses-pages"></a>Kurslar sayfalarını özelleştirme

Yeni bir kurs varlığı oluşturulduğunda, mevcut bir departmanla bir ilişkisi olmalıdır. Bunu kolaylaştırmak için, yapı iskelesi kodu denetleyici yöntemlerini içerir ve departmanı seçmeye yönelik bir açılan liste içeren görünümler oluşturup düzenleyebilir. Açılan liste `Course.DepartmentID` yabancı anahtar özelliğini ayarlar ve bu, `Department` gezinti özelliğini uygun `Department` varlığıyla yüklemek için tüm Entity Framework gereksinimlidir. Scafkatmış kodu kullanacaksınız, ancak hata işleme eklemek ve açılan listeyi sıralamak için biraz değişiklik yapacaksınız.

*CourseController.cs*' de, dört `Create` ve `Edit` yöntemleri silin ve bunları şu kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,11-12,19-25,40,44,46,48-78)]

Aşağıdaki `using` ifadesini dosyanın başına ekleyin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

`PopulateDepartmentsDropDownList` yöntemi, ada göre sıralanmış tüm bölümlerin bir listesini alır, açılan liste için bir `SelectList` koleksiyonu oluşturur ve koleksiyonu bir `ViewBag` özelliğindeki görünüme geçirir. Yöntemi, çağıran kodun, açılan liste işlendiğinde seçilecek öğeyi belirtmesini sağlayan isteğe bağlı `selectedDepartment` parametresini kabul eder. Görünüm, adı `DepartmentID` [DropDownList](../../older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc.md) Yardımcısı 'na geçecek ve yardımcı sonra `DepartmentID`adlı bir `SelectList` için `ViewBag` nesnesine bakmış olur.

`HttpGet` `Create` yöntemi, seçilen öğeyi ayarlamadan `PopulateDepartmentsDropDownList` yöntemini çağırır, çünkü yeni bir kurs için departman henüz kurulmadı:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

`HttpGet` `Edit` yöntemi, düzenlenen kursa zaten atanmış departmanın KIMLIğINE bağlı olarak seçili öğeyi ayarlar:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=12)]

Hem `Create` hem de `Edit` için `HttpPost` yöntemleri, bir hatadan sonra sayfayı yeniden görüntülerken seçili öğeyi ayarlayan kodu içerir:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=6)]

Bu kod, sayfa hata iletisini göstermek için yeniden görüntülendiğinde, seçilen bölümün seçili kalırsa emin olmanızı sağlar.

Kurs görünümleri, bölüm alanı için aşağı açılan listelerle zaten Uzlanabilir, ancak bu alanın DepartmentID açıklamalı başlığını istemezsiniz, bu nedenle başlık değiştirmek için *Views\course\create.exe* dosyasında aşağıdaki vurgulanmış değişikliği yapın.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml?highlight=43)]

*Views\course\edit.exe*' de aynı değişikliği yapın.

Normal olarak, anahtar değeri veritabanı tarafından oluşturulduğundan ve değiştirilemediğinden ve kullanıcılara gösterilemeyecek anlamlı bir değer olmadığından desteği birincil anahtar üzerinde değişiklik yapmaz. Kurs varlıkları için, `DatabaseGeneratedOption.None` özniteliğinin kullanıcının birincil anahtar değerini girebilmelidir anlamına geldiğini anladığından, desteği `CourseID` alanı için bir metin kutusu içerir. Ancak bu, sayının diğer görünümlerde görmek istediğiniz anlamlı olduğundan, bunu el ile eklemeniz gerektiğini anlamaz.

*Views\course\edit.exe*' de **başlık** alanından önce bir kurs numarası alanı ekleyin. Birincil anahtar olduğundan, görüntülenir, ancak değiştirilemez.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cshtml)]

Düzenleme görünümündeki kurs numarası için gizli bir alan (`Html.HiddenFor` Yardımcısı) zaten var. Bir *HTML. LabelFor* Helper eklemek, Kullanıcı düzenleme sayfasında **Kaydet** ' i tıklattığında, kurs numarasının gönderilen verilere dahil edilmesini neden olmadığı için gizli alanın gereksinimini ortadan kaldırmaz.

*Views\course\delete.exe* ve *Views\course\details.cshtml*' de, Bölüm adı başlığını "ad" iken "Departman" olarak değiştirin ve **başlık** alanından önce bir kurs numarası alanı ekleyin.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cshtml?highlight=2,9-15)]

**Oluştur** sayfasını çalıştırın (kurs dizinini görüntüle sayfasını ve **Yeni oluştur**' a tıklayın) ve yeni bir kurs için veri girin:

| Değer | Ayar |
| ----- | ------- |
| Sayı | *1000*girin. |
| Başlık | *Algeköşeli*girin. |
| Krediler | *4*girin. |
|Bölüm | **Matematik**seçeneğini belirleyin. |

**Oluştur**'u tıklatın. Kurs dizini sayfası, listeye eklenen yeni kursla birlikte görüntülenir. Dizin sayfası listesindeki departman adı, ilişkinin doğru şekilde oluşturulduğunu gösteren gezinti özelliğinden gelir.

**Düzenleme** sayfasını çalıştırın (kurs dizinini görüntüleyin ve bir kurs üzerinde **Düzenle** ' ye tıklayın).

Sayfadaki verileri değiştirin ve **Kaydet**' e tıklayın. Kurs dizini sayfası, güncelleştirilmiş kurs verileriyle birlikte görüntülenir.

## <a name="add-office-to-instructors-page"></a>Office 'i eğitmenler sayfasına Ekle

Bir eğitmen kaydını düzenlediğinizde, eğitmenin Office atamasını güncelleştirebilmek istersiniz. `Instructor` varlığı, `OfficeAssignment` varlığı ile bire sıfır veya-arasında bir ilişkiye sahiptir; yani aşağıdaki durumları işlemeniz gerekir:

- Kullanıcı Office atamasını temizlediğinde ve başlangıçta bir değer içeriyorsa, `OfficeAssignment` varlığını kaldırmanız ve silmeniz gerekir.
- Kullanıcı bir Office atama değeri girerse ve başlangıçta boşsa, yeni bir `OfficeAssignment` varlığı oluşturmanız gerekir.
- Kullanıcı bir Office atamasının değerini değiştirirse, mevcut bir `OfficeAssignment` varlığındaki değeri değiştirmeniz gerekir.

*InstructorController.cs* ' i açın ve `HttpGet` `Edit` yöntemine bakın:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Burada scafkatlama kodu istediğiniz gibi değildir. Bu, bir açılan liste için veri ayarlıyor, ancak ihtiyacınız olan bir metin kutusu. Bu yöntemi aşağıdaki kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=7-10)]

Bu kod `ViewBag` ifadesini bırakır ve ilişkili `OfficeAssignment` varlığı için ekip yükleme ekler. `Find` yöntemiyle Eager yüklemesi gerçekleştiremezsiniz, bu nedenle `Where` ve `Single` yöntemleri eğitmeni seçmek için kullanılır.

`HttpPost` `Edit` yöntemini aşağıdaki kodla değiştirin. Office atama güncelleştirmelerini işleyen:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`RetryLimitExceededException` başvurusu `using` bir ifade gerektirir; eklemek için farenizi `RetryLimitExceededException`üzerine getirin. Aşağıdaki ileti görünür: ![ yeniden deneme özel durum iletisi](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

**Olası düzeltmeleri göster**' i seçin ve ardından **System. Data. Entity. Infrastructure kullanarak**

![Yeniden deneme özel durumunu çözümle](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

Kod şunları yapar:

- İmza artık `HttpGet` yöntemiyle aynı olduğundan (`ActionName` özniteliği,/Edit/URL 'nin hala kullanıldığını belirten), yöntem adını `EditPost` olarak değiştirir.
- `OfficeAssignment` gezinti özelliği için Eager yükleme kullanarak geçerli `Instructor` varlığını veritabanından alır. Bu, `HttpGet` `Edit` yönteminde yaptığınız şeydir.
- Alınan `Instructor` varlığını model Ciltçideki değerlerle güncelleştirir. Kullanılan [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.108).aspx) aşırı yüklemesi, dahil etmek istediğiniz özellikleri *beyaz listelemenize* olanak sağlar. Bu, [ikinci öğreticide](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)açıklandığı gibi, daha fazla nakletmeyi önler.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]
- Office konumu boşsa, `OfficeAssignment` tablosundaki ilgili satırın silinebilmesi için `Instructor.OfficeAssignment` özelliğini null olarak ayarlar.

    [!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]
- Değişiklikleri veritabanına kaydeder.

*Views\komutctor\edit.exe*' de, **işe alma tarihi** alanı için `div` öğelerinden sonra, Office konumunu düzenlemekte yeni bir alan ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml)]

Sayfayı çalıştırın ( **eğitmenler** sekmesini seçin ve ardından bir eğitmende **Düzenle** ' ye tıklayın). **Office konumunu** değiştirin ve **Kaydet**' e tıklayın.

## <a name="add-courses-to-instructors-page"></a>Eğitmenler sayfasına kurslar ekleyin

Eğitmenler, istediğiniz sayıda kurs öğretebilir. Artık bir grup onay kutusu kullanarak kurs atamalarını değiştirme özelliğini ekleyerek eğitmen düzenleme sayfasını geliştirirsiniz.

`Course` ve `Instructor` varlıkları arasındaki ilişki çoktan çoğa, bu, JOIN tablosunda bulunan yabancı anahtar özelliklerine doğrudan erişiminizin olmadığı anlamına gelir. Bunun yerine, `Instructor.Courses` gezinti özelliğine ve öğesinden varlıkları ekler ve kaldırılır.

Bir eğitmenin hangi kurslara atandığını değiştirmenize olanak sağlayan kullanıcı arabirimi bir grup onay kutusu olur. Veritabanındaki her kurs için bir onay kutusu görüntülenir ve eğitmenin Şu anda atanmış olduğu yer seçilidir. Kullanıcı kurs atamalarını değiştirmek için onay kutularını seçebilir veya temizleyebilir. Kurs sayısı çok fazlaysa, büyük olasılıkla görünümde verileri göstermek için farklı bir yöntem kullanmak isteyeceksiniz, ancak ilişkiler oluşturmak veya silmek için gezinti özelliklerini düzenleme yöntemini kullanırsınız.

Onay kutuları listesinin görünümüne veri sağlamak için bir görünüm modeli sınıfı kullanacaksınız. *Viewmodeller* klasöründe *AssignedCourseData.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

*InstructorController.cs*' de `HttpGet` `Edit` yöntemini aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs?highlight=9,12,20-35)]

Kod, `Courses` gezinti özelliği için Eager yüklemesi ekler ve `AssignedCourseData` View model sınıfını kullanarak onay kutusu dizisi bilgilerini sağlamak için yeni `PopulateAssignedCourseData` yöntemini çağırır.

`PopulateAssignedCourseData` yöntemindeki kod, görünüm modeli sınıfını kullanarak bir kurs listesi yüklemek için tüm `Course` varlıklarından okur. Kod, her kurs için, kursun `Courses` gezinti özelliğinde mevcut olup olmadığını denetler. Eğitmenin bir kurs atanıp atanmadığını denetlerken etkili arama oluşturmak için, eğitmene atanan kurslar bir [diyez kümesi](https://msdn.microsoft.com/library/bb359438.aspx) koleksiyonuna konur. `Assigned` özelliği, eğitmenin atandığı kurslar için `true` olarak ayarlanır. Görünüm, hangi onay kutularının seçili olarak gösterileceğini belirlemede bu özelliği kullanır. Son olarak, liste bir `ViewBag` özelliğindeki görünüme geçirilir.

Sonra, Kullanıcı **Kaydet**' i tıklattığında yürütülen kodu ekleyin. `EditPost` yöntemini, `Instructor` varlığının `Courses` gezinti özelliğini güncelleştiren yeni bir yöntemi çağıran aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cs?highlight=3,11,25,37,40-68)]

Yöntem imzası artık `HttpGet` `Edit` yönteminden farklıdır. bu nedenle, yöntem adı `EditPost` geri `Edit`olarak değişir.

Görünümün bir `Course` varlıkları koleksiyonu olmadığından, model Bağlayıcısı `Courses` gezinti özelliğini otomatik olarak güncelleştiremez. `Courses` gezinti özelliğini güncelleştirmek için model cildi kullanmak yerine, bunu yeni `UpdateInstructorCourses` yönteminde yapacaksınız. Bu nedenle `Courses` özelliğini model bağlamadan çıkarmanız gerekir. Bu, *beyaz liste* aşırı yüklemesini kullandığınız ve `Courses` içerme listesinde olmadığı Için [TryUpdateModel](https://msdn.microsoft.com/library/dd470908(v=vs.98).aspx) 'i çağıran kodda herhangi bir değişiklik yapılmasını gerektirmez.

Hiçbir onay kutusu seçilmediyse `UpdateInstructorCourses` kod, `Courses` gezinti özelliğini boş bir koleksiyon ile başlatır:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

Kod daha sonra, veritabanındaki tüm kurslardan geçer ve bu her kursu, görünümde seçili olanlar ile ilgili olarak eğitmenin atandığı her bir kursa karşı denetler. Etkili aramaları kolaylaştırmak için, ikinci iki koleksiyon `HashSet` nesnelerinde depolanır.

Kurs onay kutusu seçilmişse ancak kurs `Instructor.Courses` gezinti özelliğinde değilse, kurs, Gezinti özelliğindeki koleksiyona eklenir.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

Kurs onay kutusu seçilmemişse, ancak kurs `Instructor.Courses` gezinti özelliği ise, kurs, gezinti özelliğinden kaldırılır.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs)]

*Views\komutctor\edit.exe*' de, `OfficeAssignment` alanı için `div` öğeden hemen sonra ve **kaydet** düğmesine ait `div` öğesinden önce aşağıdaki kodu ekleyerek bir dizi onay kutusu içeren bir **Kurslar** alanı ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cshtml)]

Kodu yapıştırdıktan sonra, satır sonları ve girintileme buradaki gibi görünmüyorsa, burada gördüğünüz gibi görünmesi için her şeyi el ile onarın. Girintide kusursuz olması gerekmez, ancak `@</tr><tr>`, `@:<td>`, `@:</td>`ve `@</tr>` satırların her biri gösterildiği gibi tek bir satırda olması gerekir, aksi halde bir çalışma zamanı hatası alırsınız.

Bu kod, üç sütun içeren bir HTML tablosu oluşturur. Her sütunda, bir onay kutusu ve ardından kurs numarası ve başlığından oluşan bir açıklamalı alt yazı bulunur. Onay kutularının hepsi aynı ada ("Selectedkurslar") sahiptir, bu da model cilde bir grup olarak değerlendirilme bildirir. Her onay kutusunun `value` özniteliği, sayfa gönderildiğinde `CourseID.` değerine ayarlanır, model Ciltçi yalnızca seçili onay kutularının `CourseID` değerlerinden oluşan bir diziyi denetleyiciye geçirir.

Onay kutuları başlangıçta işlendiğinde, eğitmenin atandığı kurslara yönelik olanlar, onları seçen `checked` özniteliklerine sahiptir (bunları işaretli olarak görüntüler).

Kurs atamalarını değiştirdikten sonra, site `Index` sayfasına döndüğünde değişiklikleri doğrulayabilmek isteyeceksiniz. Bu nedenle, bu sayfadaki tabloya bir sütun eklemeniz gerekir. Bu durumda, göstermek istediğiniz bilgiler, sayfaya model olarak geçirdiğiniz `Instructor` varlığının `Courses` gezinti özelliğinde zaten yer aldığı için `ViewBag` nesnesini kullanmanız gerekmez.

*Views\komutctor\ındex.cshtml*içinde, aşağıdaki örnekte gösterildiği gibi, **Office** başlığından hemen sonra bir **Kurslar** başlığı ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cshtml?highlight=6)]

Ardından, Office konumu ayrıntı hücresini hemen takip eden yeni bir ayrıntı hücresi ekleyin:

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml?highlight=7-14)]

Her bir eğitmene atanan kursları görmek için **eğitmen dizini** sayfasını çalıştırın.

Düzenleme sayfasını görmek için bir eğitmende **Düzenle** ' ye tıklayın.

Bazı kurs atamalarını değiştirin ve **Kaydet**' e tıklayın. Yaptığınız değişiklikler Dizin sayfasında yansıtılır.

 Note: Eğitmen Kursu verilerini düzenlemek için buradaki yaklaşım, sınırlı sayıda kurs olduğunda iyi bir şekilde gerçekleştirilir. Çok daha büyük olan koleksiyonlar için, farklı bir kullanıcı arabirimi ve farklı bir güncelleştirme yöntemi gerekir.

## <a name="update-deleteconfirmed"></a>Deleteonaylandı Güncelleştir

*InstructorController.cs*' de `DeleteConfirmed` yöntemini silin ve yerine aşağıdaki kodu ekleyin.

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample24.cs?highlight=5-8,12-18)]

Bu kod aşağıdaki değişikliği yapar:

- Eğitmen herhangi bir departmanın yöneticisi olarak atanırsa, bu departmandaki eğitmen atamasını kaldırır. Bu kod olmadan, bir departman için yönetici olarak atanmış bir eğitmeni silmeye çalıştıysanız, başvurusal bütünlük hatası alırsınız.

Bu kod, birden çok departman için yönetici olarak atanan bir eğitmenin senaryosunu işlemez. Son öğreticide, bu senaryonun oluşmasını önleyen bir kod ekleyeceksiniz.

## <a name="add-office-location-and-courses-to-the-create-page"></a>Oluşturma sayfasına Office konum ve kurslar ekleme

*InstructorController.cs*' de, `HttpGet` ve `HttpPost` `Create` yöntemleri silin ve ardından aşağıdaki kodu kendi yerine ekleyin:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample25.cs)]

Bu kod, başlangıçta hiçbir kurs seçilmemiş olması dışında, düzenleme yöntemleri için gördüklerinize benzer. `HttpGet` `Create` yöntemi `PopulateAssignedCourseData` yöntemini çağırır çünkü seçili kurslar olabilir ancak görünümdeki `foreach` döngüsü için boş bir koleksiyon sağlamak üzere (Aksi halde görünüm kodu bir null başvuru özel durumu oluşturur).

HttpPost oluşturma yöntemi, seçili her kursu, doğrulama hatalarını denetleyen şablon kodundan önce kurslar gezintisi özelliğine ekler ve yeni eğitmeni veritabanına ekler. Model hataları olduğunda (örneğin, Kullanıcı geçersiz bir tarih olarak anahtarlıdır), bu sayede, sayfa bir hata iletisiyle yeniden görüntülendiğinde, yapılan tüm kurs seçimleri otomatik olarak geri yüklendiğinde kurslar eklenir.

`Courses` gezinti özelliğine kurs ekleyebilmesinin, özelliği boş bir koleksiyon olarak başlatmak için sahip olmanız gerektiğini unutmayın:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample26.cs)]

Bunu denetleyici kodunda yapmanın bir alternatifi olarak, aşağıdaki örnekte gösterildiği gibi, özellik alıcısının, koleksiyonu otomatik olarak oluşturmak üzere değiştirerek, bunu eğitmen modelinde yapabilirsiniz:

[!code-csharp[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Courses` özelliğini bu şekilde değiştirirseniz, denetleyicideki açık özellik başlatma kodunu kaldırabilirsiniz.

*Views\komutctor\create.exe*' de, işe alma tarihi alanından sonra ve **Gönder** düğmesinden önce bir Office konum metin kutusu ve kurs onay kutuları ekleyin.

[!code-cshtml[Main](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample28.cshtml)]

Kodu yapıştırdıktan sonra, düzenleme sayfasında daha önce yaptığınız gibi satır sonlarını ve girintiyi düzeltir.

Oluştur sayfasını çalıştırın ve bir eğitmen ekleyin.

<a id="transactions"></a>

## <a name="handling-transactions"></a>İşlemleri işleme

[Temel CRUD işlevselliği öğreticisinde](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)açıklandığı gibi, varsayılan olarak Entity Framework işlemleri örtülü olarak uygular. Daha fazla denetime ihtiyacınız olan senaryolar için--örneğin, bir işlem içinde Entity Framework dışında yapılan işlemleri eklemek istiyorsanız, bkz. MSDN 'de [Işlemlerle çalışma](https://msdn.microsoft.com/data/dn456843) .

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indirin](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar, [ASP.NET Data Access-önerilen kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md)bölümünde bulunabilir.

## <a name="next-step"></a>Sonraki adım

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Özelleştirilmiş Kurslar sayfaları
> * Office, Eğitmenler sayfasına eklendi
> * Eğitmenler sayfasına kurslar eklendi
> * Deleteonaylandı güncelleştirildi
> * Office konumu ve kurslar oluşturma sayfasına eklendi

Bir zaman uyumsuz programlama modelinin nasıl uygulanacağını öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Zaman uyumsuz programlama modeli](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)
