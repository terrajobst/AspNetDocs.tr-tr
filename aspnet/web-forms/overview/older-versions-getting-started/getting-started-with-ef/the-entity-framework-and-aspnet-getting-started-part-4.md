---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 4 ' ü kullanmaya başlama Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638168"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 4 ' ü kullanmaya başlama

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](the-entity-framework-and-aspnet-getting-started-part-1.md) bakın

## <a name="working-with-related-data"></a>Ilgili verilerle çalışma

Önceki öğreticide, verileri filtrelemek, sıralamak ve gruplandırmak için `EntityDataSource` denetimini kullandınız. Bu öğreticide ilgili verileri görüntüleyip güncelleştireceksiniz.

Eğitmenler listesini gösteren eğitmenler sayfasını oluşturacaksınız. Bir eğitmen seçtiğinizde, bu eğitmenin bir kurs listesini görürsünüz. Bir kurs seçtiğinizde, kursa ve kursa kayıtlı öğrencilerin bir listesine ilişkin ayrıntıları görürsünüz. Eğitmen adını, işe alma tarihini ve Office atamasını düzenleyebilirsiniz. Office ataması, bir gezinti özelliği aracılığıyla erişebileceğiniz ayrı bir varlık kümesidir.

Ana verileri, biçimlendirme veya koddaki ayrıntı verilerine bağlayabilirsiniz. Öğreticinin bu bölümünde her iki yöntemi de kullanacaksınız.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>GridView denetimindeki Ilgili varlıkları görüntüleme ve güncelleştirme

*Site. Master* ana sayfasını kullanan *eğitmenler. aspx* adlı yeni bir web sayfası oluşturun ve `Content2`adlı `Content` denetimine aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

Bu biçimlendirme, Eğitmenler 'i seçen ve güncelleştirmeleri sağlayan bir `EntityDataSource` denetimi oluşturur. `div` öğesi, daha sonra bir sütunu daha sonra ekleyebilmek için sola doğru işlenecek biçimlendirmeyi yapılandırır.

`EntityDataSource` biçimlendirme ve kapanış `</div>` etiketi arasında, hata iletileri için kullanacağınız bir `GridView` denetimi ve bir `Label` denetimi oluşturan aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

Bu `GridView` denetimi satır seçimini, seçili satırı açık gri arka plan rengiyle vurgular ve `SelectedIndexChanged` ve `Updating` olayları için işleyicileri (daha sonra oluşturacağınız) belirtir. Ayrıca, seçilen satırın anahtar değerinin daha sonra ekleyeceğiniz başka bir denetime geçirilebilmesi için `DataKeyNames` özelliği için `PersonID` belirtir.

Son sütun, ilişkili bir varlıktan geldiği için `Person` varlığın bir gezinti özelliğinde depolanan eğitmenin Office atamasını içerir. `GridView` denetimi onları güncelleştirmek için doğrudan gezinti özelliklerine bağlanamadığı için, `EditItemTemplate` öğesinin `Bind`yerine `Eval` belirttiğinden emin olun. Kodda Office atamasını güncelleştireceksiniz. Bunu yapmak için `TextBox` denetimine bir başvuru gerekir ve bunu `TextBox` denetiminin `Init` olayında alır ve kaydedersiniz.

`GridView` denetimini takip etmek, hata iletileri için kullanılan bir `Label` denetimidir. Denetimin `Visible` özelliği `false`ve Görünüm durumu kapalı olur, böylece etiket yalnızca kod bir hataya yanıt olarak görünür hale geldiğinde görünür.

*Instructors.aspx.cs* dosyasını açın ve aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

Office atama metin kutusuna bir başvuru tutmak için kısmi sınıf adı bildiriminden hemen sonra bir özel sınıf alanı ekleyin.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

Daha sonra kod ekleyeceğiniz `SelectedIndexChanged` olay işleyicisi için bir saplama ekleyin. Ayrıca, `TextBox` denetimine bir başvuru depolayabilmeniz için Office atama `TextBox` denetiminin `Init` olayı için bir işleyici ekleyin. Bu başvuruyu, kullanıcının gezinti özelliği ile ilişkili varlığı güncelleştirmek için girdiği değeri almak için kullanacaksınız.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

`GridView` denetimin `Updating` olayını, ilişkili `OfficeAssignment` varlığının `Location` özelliğini güncelleştirmek için kullanacaksınız. `Updating` olayı için aşağıdaki işleyiciyi ekleyin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

Bu kod, Kullanıcı `GridView` satırında **Güncelleştir** ' i tıklattığında çalıştırılır. Kod, geçerli `Person` varlıkla ilişkili `OfficeAssignment` varlığını almak için LINQ to Entities kullanır. Bu, olay bağımsız değişkeninden seçilen satırın `PersonID` kullanılarak yapılır.

Daha sonra kod, `InstructorOfficeTextBox` denetimindeki değere bağlı olarak aşağıdaki eylemlerden birini alır:

- Metin kutusunda bir değer varsa ve güncelleştirilecek `OfficeAssignment` varlık yoksa, bir tane oluşturur.
- Metin kutusunda bir değer varsa ve bir `OfficeAssignment` varlığı varsa, `Location` özellik değerini güncelleştirir.
- Metin kutusu boşsa ve bir `OfficeAssignment` varlığı varsa, varlığını siler.

Bundan sonra değişiklikleri veritabanına kaydeder. Bir özel durum oluşursa, bir hata iletisi görüntüler.

Sayfayı çalıştırın.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

**Düzenle** ' ye tıklayın ve tüm alanlar metin kutularına değişir.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

**Office ataması**dahil olmak üzere bu değerlerden herhangi birini değiştirin. **Güncelleştir** ' e tıkladığınızda, listede yansıtılan değişiklikleri görürsünüz.

## <a name="displaying-related-entities-in-a-separate-control"></a>Ilgili varlıkları ayrı bir denetimde görüntüleme

Her bir eğitmen bir veya daha fazla kurs öğretebilir. bu nedenle, Eğitmenler `GridView` denetiminde hangi eğitmenin seçildiğinden ilişkili kursları listelemek için bir `EntityDataSource` denetimi ve `GridView` denetimi ekleyeceksiniz. Kurslar varlıkları için bir başlık ve `EntityDataSource` denetimi oluşturmak için aşağıdaki biçimlendirmeyi hata iletisi `Label` denetimi ve kapanış `</div>` etiketi arasına ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

`Where` parametresi, `InstructorsGridView` denetiminde satırı seçili olan eğitmenin `PersonID` değerini içerir. `Where` özelliği, bir `Course` varlığının `People` gezinti özelliğinden tüm ilişkili `Person` varlıklarını alan ve yalnızca ilişkili `Course` varlıklarından biri seçili `Person` değerini içeriyorsa `PersonID` varlığını seçen bir seçmeden komutu içerir.

`GridView` denetimini oluşturmak için, `CoursesEntityDataSource` denetiminin hemen ardından aşağıdaki biçimlendirmeyi ekleyin (kapatma `</div>` etiketinden önce):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

Hiçbir eğitmen seçilmezse hiçbir kurs gösterilmediğinden, bir `EmptyDataTemplate` öğesi dahil edilir.

Sayfayı çalıştırın.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

Bir veya daha fazla kurs atanmış bir eğitmeni seçin ve kurs veya kurslar listede görüntülenir. (Note: veritabanı şeması birden çok kursa izin verse de, veritabanı ile sağlanan test verilerinde, hiçbir eğitmenin artık birden fazla kursu vardır. Daha sonraki bir öğreticide ekleyeceğiniz **Sunucu Gezgini** penceresini veya *CoursesAdd. aspx* sayfasını kullanarak veritabanına kurslar ekleyebilirsiniz.)

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

`CoursesGridView` denetimi yalnızca birkaç kurs alanını gösterir. Bir kursun tüm ayrıntılarını göstermek için kullanıcının seçtiği kurs için `DetailsView` bir denetim kullanırsınız. *Eğitmenler. aspx*' te, kapatma `</div>` etiketinden sonra aşağıdaki biçimlendirmeyi ekleyin (Bu biçimlendirmeyi kapatmadan önce değil, kapanış div etiketinden **sonra** yerleştirdiğinizden emin olun):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

Bu biçimlendirme `Courses` varlık kümesine bağlanan bir `EntityDataSource` denetimi oluşturur. `Where` özelliği, kurslar `GridView` denetimindeki seçili satırın `CourseID` değerini kullanarak bir kurs seçer. Biçimlendirme, daha sonra hiyerarşide daha düşük bir düzey olan öğrenci çalışmalarını görüntülemek için kullanacağınız `Selected` olayı için bir işleyici belirtir.

*Instructors.aspx.cs*' de `CourseDetailsEntityDataSource_Selected` yöntemi için aşağıdaki saplaması oluşturun. (Bu saplamaya daha sonra öğreticide dolduracağız; şimdilik, sayfanın derlenmesi ve çalışması için ihtiyacınız olur.)

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

Sayfayı çalıştırın.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

Başlangıçta hiçbir kurs seçilmediğinden hiçbir kurs ayrıntısı yok. Bir kurs atanmış olan bir eğitmeni seçin ve ardından ayrıntıları görmek için bir kurs seçin.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>Ilişkili verileri göstermek için EntityDataSource "Selected" olayını kullanma

Son olarak, tüm kayıtlı öğrencileri ve bunların seçili kursa ait notlarını göstermek istersiniz. Bunu yapmak için kurs `DetailsView`'e göre `EntityDataSource` denetimin `Selected` olayını kullanacaksınız.

*Eğitmenler. aspx*' te, `DetailsView` denetiminden sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

Bu biçimlendirme, seçilen kurs için öğrencilerin listesini ve bunların notlarını görüntüleyen bir `ListView` denetimi oluşturur. Kodda denetimin kaynağını belirlediğiniz için veri kaynağı belirtilmedi. `EmptyDataTemplate` öğesi hiçbir kurs seçildiğinde görüntülenecek bir ileti sağlar; Bu durumda görüntülenecek öğrenci yok. `LayoutTemplate` öğesi listeyi göstermek için bir HTML tablosu oluşturur ve `ItemTemplate` görüntülenecek sütunları belirtir. Öğrenci KIMLIĞI ve öğrenci derecesi `StudentGrade` varlıklardır ve öğrenci adı, Entity Framework `StudentGrade` varlığının `Person` gezinti özelliğinde kullanılabilir hale gelen `Person` varlıklarından oluşur.

*Instructors.aspx.cs*' de, saplaması-Out `CourseDetailsEntityDataSource_Selected` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

Bu olay için olay bağımsız değişkeni seçili verileri bir koleksiyon biçiminde sağlar, bu da hiçbir şey seçili değilse sıfır öğe veya `Course` varlık seçildiyse bir öğe olur. `Course` bir varlık seçilirse, kod koleksiyonu tek bir nesneye dönüştürmek için `First` yöntemini kullanır. Daha sonra gezinti özelliğinden `StudentGrade` varlıkları alır, bunları bir koleksiyona dönüştürür ve `GradesListView` denetimini koleksiyona bağlar.

Bu, notlarınızı göstermek için yeterlidir, ancak sayfanın ilk görüntülenişinde ve bir kurs seçilmediğinde boş veri şablonundaki iletinin görüntülendiğinden emin olmak istiyorsunuz. Bunu yapmak için, iki konumdan çağrıcağımız aşağıdaki yöntemi oluşturun:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

Sayfa ilk kez görüntülendiğinde boş veri şablonunu göstermek için `Page_Load` yönteminden bu yeni yöntemi çağırın. Ve `InstructorsGridView_SelectedIndexChanged` yönteminden çağırın çünkü bu olay bir eğitmen seçildiğinde tetiklenir, bu da yeni kurslar kurs `GridView` denetimine yüklenir ve henüz hiçbiri seçili değildir. İki çağrı aşağıda verilmiştir:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

Sayfayı çalıştırın.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

Bir kurs atanmış olan bir eğitmen seçin ve ardından kursu seçin.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

Artık ilgili verilerle çalışmanın birkaç yolunu gördünüz. Aşağıdaki öğreticide, mevcut varlıklar arasında ilişkiler eklemeyi, ilişkilerin nasıl kaldırılacağını ve var olan bir varlığa yönelik bir ilişkiye sahip olan yeni bir varlığın nasıl ekleneceğini öğreneceksiniz.

> [!div class="step-by-step"]
> [Önceki](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [İleri](the-entity-framework-and-aspnet-getting-started-part-5.md)
