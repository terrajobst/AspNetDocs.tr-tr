---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 5 ' i kullanmaya başlama Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528002"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms ile çalışmaya başlama-5. Bölüm

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](the-entity-framework-and-aspnet-getting-started-part-1.md) bakın

## <a name="working-with-related-data-continued"></a>Ilgili verilerle çalışma, devam eden

Önceki öğreticide, ilgili verilerle çalışmak için `EntityDataSource` denetimini kullanmaya başladığınızdan. Gezinti özelliklerinde birden fazla hiyerarşi düzeyi ve düzenlenmiş veri görüntülendi. Bu öğreticide, ilişki ekleyerek ve silerek ve var olan bir varlığa ilişki olan yeni bir varlık ekleyerek ilgili verilerle çalışmaya devam edersiniz.

Departmanlara atanan kurslar ekleyen bir sayfa oluşturacaksınız. Departmanlar zaten mevcut ve yeni bir kurs oluşturduğunuzda, bu ve mevcut bir departman arasında bir ilişki kurarsınız.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

Ayrıca, bir kursa bir eğitmen atayarak (seçtiğiniz iki varlık arasında bir ilişki ekleyerek) veya bir Kurstaki bir eğitmeni kaldırarak çoktan çoğa ilişki ile çalışacak bir sayfa oluşturacaksınız (iki varlık arasındaki ilişkiyi kaldırma seçin). Veritabanında, bir eğitmen ve kurs arasında bir ilişki eklemek `CourseInstructor` ilişkilendirme tablosuna yeni bir satır eklenmesine neden olur. bir ilişkinin kaldırılması `CourseInstructor` ilişkilendirme tablosundan bir satırı silmeyi içerir. Ancak bunu, `CourseInstructor` tablosuna açıkça başvurulmadan, gezinti özelliklerini ayarlayarak Entity Framework.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>Mevcut bir varlığa Ilişki içeren bir varlık ekleme

*Site. Master* ana sayfasını kullanan *CoursesAdd. aspx* adlı yeni bir web sayfası oluşturun ve `Content2`adlı `Content` denetimine aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

Bu biçimlendirme, ekleme sağlayan ve `Inserting` olayı için bir işleyici belirten kurslar seçen bir `EntityDataSource` denetimi oluşturur. Yeni bir `Course` varlık oluşturulduğunda `Department` gezinti özelliğini güncellemek için işleyiciyi kullanacaksınız.

Biçimlendirme Ayrıca yeni `Course` varlıkları eklemek için kullanmak üzere bir `DetailsView` denetimi oluşturur. Biçimlendirme `Course` varlık özellikleri için bağlantılı alanları kullanır. Bu, sistem tarafından oluşturulan bir KIMLIK alanı olmadığından `CourseID` değerini girmeniz gerekir. Bunun yerine, kurs oluşturulduğunda el ile belirtilmesi gereken bir kurs numarasıdır.

Gezinti özellikleri `BoundField` denetimleriyle kullanılamadığından `Department` gezinti özelliği için bir şablon alanı kullanırsınız. Şablon alanı, departmanı seçmek için bir açılır liste sağlar. Aşağı açılan liste, `Bind`yerine `Eval` kullanılarak `Departments` varlık kümesine bağlanır, çünkü onları güncelleştirmek için doğrudan doğrudan bağlayamazsınız. `DepartmentID` yabancı anahtarı güncelleştiren kodun kullanımı için bir başvuruyu depolayabilmeniz için `DropDownList` denetiminin `Init` olayı için bir işleyici belirtirsiniz.

*CoursesAdd.aspx.cs* ' de, yalnızca kısmi sınıf bildiriminden sonra, `DepartmentsDropDownList` denetimine bir başvuru tutmak için bir sınıf alanı ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

Denetime bir başvuru depolayabilmeniz için `DepartmentsDropDownList` denetiminin `Init` olayı için bir işleyici ekleyin. Bu, kullanıcının girdiği değeri almanıza ve `Course` varlığının `DepartmentID` değerini güncelleştirmek için kullanmasına olanak sağlar.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

`DetailsView` denetiminin `Inserting` olayı için bir işleyici ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

Kullanıcı `Insert`tıkladığında, yeni kayıt eklenmeden önce `Inserting` olayı oluşturulur. İşleyicisindeki kod, `DropDownList` denetiminden `DepartmentID` alır ve `Course` varlığının `DepartmentID` özelliği için kullanılacak değeri ayarlamak için onu kullanır.

Entity Framework, bu kursu ilişkili `Department` varlığının `Courses` gezinti özelliğine ekleme işlemini gerçekleştirir. Ayrıca, departmanı `Course` varlığının `Department` gezinti özelliğine de ekler.

Sayfayı çalıştırın.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

Bir KIMLIK, başlık, bir kredi sayısı girip bir departman seçip **Ekle**' ye tıklayın.

*Kurslar. aspx* sayfasını çalıştırın ve yeni kursu görmek için aynı departmanı seçin.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>Çoktan çoğa Ilişkilerle çalışma

`Courses` varlık kümesi ve `People` varlık kümesi arasındaki ilişki çoka çok ilişkidir. `Course` varlık, sıfır, bir veya daha fazla ilgili `Person` varlığı içerebilen `People` adlı bir gezinti özelliğine sahiptir (Bu kursu öğretmede atanan eğitmenleri temsil eder). `Person` bir varlık, sıfır, bir veya daha fazla ilgili `Course` varlığı içerebilen `Courses` adlı bir gezinti özelliğine sahiptir (eğitmen 'in öğretmek için bu kursu temsil eder). Bir eğitmen birden çok kurs öğretebilir ve bir kurs birden fazla eğitmen tarafından tada gelebilir. İzlenecek yolun bu bölümünde, ilgili varlıkların gezinti özelliklerini güncelleştirerek `Person` ve `Course` varlıkları arasında ilişkiler ekleyip kaldıracaksınız.

*Site. Master* ana sayfasını kullanan *Komutctorskurslar. aspx* adlı yeni bir web sayfası oluşturun ve `Content2`adlı `Content` denetimine aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

Bu biçimlendirme, Eğitmenler için `Person` varlıkların adını ve `PersonID` alan bir `EntityDataSource` denetimi oluşturur. `DropDrownList` denetim `EntityDataSource` denetimine bağlanır. `DropDownList` denetimi `DataBound` olayı için bir işleyici belirtir. Bu işleyiciyi, kursları görüntüleyen iki açılan listeyi bağlamak için kullanacaksınız.

Biçimlendirme Ayrıca seçili eğitmene bir kurs atamak için kullanılacak aşağıdaki denetim gruplarını oluşturur:

- Atanacak kursu seçmek için `DropDownList` bir denetim. Bu denetim, seçili eğitmende Şu anda atanmamış kurslar ile doldurulur.
- Atamayı başlatmak için bir `Button` denetimi.
- Atama başarısız olursa bir hata iletisi göstermek için `Label` denetimi.

Son olarak, biçimlendirme Ayrıca seçili eğitmenden bir kursu kaldırmak için kullanılacak bir denetim grubu oluşturur.

*InstructorsCourses.aspx.cs*içinde, bir using ifadesini ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

Kursları görüntüleyen iki açılan listeyi doldurmak için bir yöntem ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

Bu kod `Courses` varlık kümesinden tüm kursları alır ve seçilen eğitmenin `Person` varlığının `Courses` gezinti özelliğinden kurslar alır. Daha sonra bu eğitmene hangi kursların atandığını belirler ve açılan listeleri buna göre doldurur.

`Assign` düğmenin `Click` olayı için bir işleyici ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

Bu kod, seçilen eğitmenin `Person` varlığını alır, seçili kurs için `Course` varlığını alır ve seçili kursu, eğitmenin `Person` varlığının `Courses` gezinti özelliğine ekler. Daha sonra değişiklikleri veritabanına kaydeder ve sonuçların hemen görünebilmesi için açılan listeleri yeniden doldurur.

`Remove` düğmenin `Click` olayı için bir işleyici ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

Bu kod, seçilen eğitmenin `Person` varlığını alır, seçili kurs için `Course` varlığını alır ve seçilen kursu `Person` varlığın `Courses` gezinti özelliğinden kaldırır. Daha sonra değişiklikleri veritabanına kaydeder ve sonuçların hemen görünebilmesi için açılan listeleri yeniden doldurur.

Raporlanacak hata olmadığında hata iletilerinin görünür olmadığından emin olan `Page_Load` yöntemine kod ekleyin ve kurslar açılan listelerini doldurmak için Eğitmenler açılan listesinin `DataBound` ve `SelectedIndexChanged` olaylarına yönelik işleyiciler ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

Sayfayı çalıştırın.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

Bir eğitmen seçin. <strong>Kurs atama</strong> açılan listesi, eğitmenin eğitim kurmadığı kursları görüntüler ve <strong>kursu kaldır</strong> açılır listesi, eğitmenin zaten atandığı kursları görüntüler. <strong>Kurs ata</strong> bölümünde bir kurs seçin ve ardından <strong>ata</strong>' ya tıklayın. Kurs, <strong>kursu kaldır</strong> açılır listesine gider. <strong>Kursu kaldır</strong> bölümünde bir kurs seçin ve Kaldır ' ı tıklatın<em>.</em> Kurs, <strong>Kurs ata</strong> açılır listesine gider.

Artık ilgili verilerle çalışmanın daha fazla yolunu gördünüz. Aşağıdaki öğreticide, uygulamanızın bakımlılığını artırmak için veri modelinde devralmayı nasıl kullanacağınızı öğreneceksiniz.

> [!div class="step-by-step"]
> [Önceki](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [İleri](the-entity-framework-and-aspnet-getting-started-part-6.md)
