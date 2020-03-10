---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 3 ' ü kullanmaya başlama | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ccdc3f8c-2568-40a7-8f8b-3c23d2e05388
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-3
msc.type: authoredcontent
ms.openlocfilehash: 88debb11a9157dce9ff000b1cb459b876dbceaf3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78643250"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-3"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 3 ' ü kullanmaya başlama

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](the-entity-framework-and-aspnet-getting-started-part-1.md) bakın

## <a name="filtering-ordering-and-grouping-data"></a>Verileri filtreleme, sıralama ve gruplama

Önceki öğreticide, verileri göstermek ve düzenlemek için `EntityDataSource` denetimini kullandınız. Bu öğreticide, verileri filtreleyecek, sıralarız ve gruplarız. `EntityDataSource` denetiminin özelliklerini ayarlayarak bunu yaptığınızda söz dizimi diğer veri kaynağı denetimlerinden farklıdır. Ancak gördüğünüz gibi, bu farklılıkları en aza indirmek için `QueryExtender` denetimini kullanabilirsiniz.

Öğrenciler için filtre uygulamak, ada göre sıralamak ve ad aramak için *öğrenciler. aspx* sayfasını değiştireceksiniz. Ayrıca, *Kurslar. aspx* sayfasını, seçilen departmanın kurslarını görüntüleyecek ve kurs adına göre arayacak şekilde değiştireceksiniz. Son olarak, *About. aspx* sayfasına öğrenci istatistiklerini ekleyeceksiniz.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image1.png)

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image3.png)

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image5.png)

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image7.png)

## <a name="using-the-entitydatasource-where-property-to-filter-data"></a>Verileri filtrelemek için EntityDataSource "Where" özelliğini kullanma

Önceki öğreticide oluşturduğunuz *öğrenciler. aspx* sayfasını açın. Şu anda yapılandırıldığı gibi, sayfadaki `GridView` denetim `People` varlık kümesindeki tüm adları görüntüler. Ancak, yalnızca, null olmayan kayıt tarihleri olan `Person` varlıkları seçerek bulabileceğiniz öğrencileri göstermek istersiniz.

**Tasarım** görünümüne geçin ve `EntityDataSource` denetimi seçin. **Özellikler** penceresinde `Where` özelliğini `it.EnrollmentDate is not null`olarak ayarlayın.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-3/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image9.png)

`EntityDataSource` denetiminin `Where` özelliğinde kullandığınız sözdizimi Entity SQL. Entity SQL Transact-SQL ' e benzer, ancak veritabanı nesneleri yerine varlıklarla birlikte kullanılmak üzere özelleştirilir. İfade `it.EnrollmentDate is not null`, `it` sözcük, sorgu tarafından döndürülen varlığa bir başvuruyu temsil eder. Bu nedenle `it.EnrollmentDate`, `EntityDataSource` denetiminin döndürdüğü `Person` varlığının `EnrollmentDate` özelliğine başvurur.

Sayfayı çalıştırın. Öğrenciler listesi artık yalnızca öğrenciler içeriyor. (Kayıt tarihi olmayan bir satır görüntülenir.)

[![Image02](the-entity-framework-and-aspnet-getting-started-part-3/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image11.png)

## <a name="using-the-entitydatasource-orderby-property-to-order-data"></a>Verileri sıralamak için EntityDataSource "OrderBy" özelliğini kullanma

Bu listenin, ilk görüntülenmesiyle aynı sırada olmasını istersiniz. *Öğrenciler. aspx* sayfası **Tasarım** görünümünde hala açıkken ve `EntityDataSource` denetimi hala seçili durumdayken, **Özellikler** penceresinde **OrderBy** özelliğini `it.LastName`olarak ayarlayın.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-3/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image13.png)

Sayfayı çalıştırın. Öğrenciler listesi artık son ada göre sırada.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-3/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image15.png)

## <a name="using-a-control-parameter-to-set-the-where-property"></a>"Where" özelliğini ayarlamak için bir denetim parametresi kullanma

Diğer veri kaynağı denetimlerinde olduğu gibi, `Where` özelliğine parametre değerleri geçirebilirsiniz. Öğreticinin 2. bölümünde oluşturduğunuz *Kurslar. aspx* sayfasında, bir kullanıcının açılan listeden seçtiği departmanla ilişkili kursları göstermek için bu yöntemi kullanabilirsiniz.

*Kurslar. aspx* ' i açın ve **Tasarım** görünümüne geçin. Sayfaya ikinci bir `EntityDataSource` denetimi ekleyin ve `CoursesEntityDataSource`olarak adlandırın. `SchoolEntities` modeline bağlayın ve **entitySetName** değeri olarak `Courses` ' ı seçin.

**Özellikler** penceresinde, **WHERE** özellik kutusunda üç nokta simgesine tıklayın. ( **Özellikler** penceresini kullanmadan önce `CoursesEntityDataSource` denetiminin hala seçili olduğundan emin olun.)

[![Image06](the-entity-framework-and-aspnet-getting-started-part-3/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image17.png)

**Ifade Düzenleyicisi** iletişim kutusu görüntülenir. Bu iletişim kutusunda, **belirtilen parametrelere göre WHERE Ifadesini otomatik olarak oluştur**' u seçin ve ardından **parametre Ekle**' ye tıklayın. `DepartmentID`parametreyi adlandırın, **parametre kaynak** değeri olarak **Denetim** ' i seçin ve **ControlID** değeri olarak **DepartmentsDropDownList** ' ı seçin.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-3/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image19.png)

**Gelişmiş özellikleri göster**' e tıklayın ve **ifade Düzenleyicisi** iletişim kutusunun **Özellikler** penceresinde `Type` özelliğini `Int32`olarak değiştirin.

[![Image15](the-entity-framework-and-aspnet-getting-started-part-3/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image21.png)

İşiniz bittiğinde, **Tamam**’a tıklayın.

Aşağı açılan listenin altında, sayfaya bir `GridView` denetimi ekleyin ve `CoursesGridView`adlandırın. `CoursesEntityDataSource` veri kaynağı denetimine bağlayın, **şemayı Yenile**' ye tıklayın, **Sütunları Düzenle**' ye tıklayın ve `DepartmentID` sütununu kaldırın. `GridView` denetim biçimlendirmesi aşağıdaki örneğe benzer.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample1.aspx)]

Kullanıcı aşağı açılan listede seçilen departmanı değiştirdiğinde, ilişkili kurslar listesinin otomatik olarak değiştirilmesini istiyorsunuz. Bunun gerçekleşmesini sağlamak için açılır listeyi seçin ve **Özellikler** penceresinde `AutoPostBack` özelliğini `True`olarak ayarlayın.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-3/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image23.png)

Tasarımcı 'yı kullanmayı tamamladığınıza göre, **kaynak** görünümüne geçin ve `CoursesEntityDataSource` denetiminin `ConnectionString` ve `DefaultContainer` adı özelliklerini `ContextTypeName="ContosoUniversity.DAL.SchoolEntities"` özniteliğiyle değiştirin. İşiniz bittiğinde, denetim biçimlendirmesi aşağıdaki örneğe benzer şekilde görünür.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample2.aspx)]

Sayfayı çalıştırın ve farklı departmanlar seçmek için açılan listeyi kullanın. Yalnızca seçilen departman tarafından sunulan kurslar `GridView` denetiminde görüntülenir.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-3/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image25.png)

## <a name="using-the-entitydatasource-groupby-property-to-group-data"></a>Verileri gruplamak için EntityDataSource "GroupBy" özelliğini kullanma

Contoso University 'in, hakkında daha fazla öğrenci-gövde istatistiklerini almak istediğini varsayalım. Özellikle, kaydolduğu tarihe göre öğrencilerin numaralarının dökümünü göstermek istemektedir.

*. Aspx*' i açın ve **kaynak** görünümü ' nde, `BodyContent` denetiminin varolan içeriğini `h2` Etiketler arasında "öğrenci gövdesi istatistikleri" ile değiştirin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample3.aspx)]

Başlıktan sonra, `EntityDataSource` bir denetim ekleyin ve `StudentStatisticsEntityDataSource`adlandırın. `SchoolEntities`bağlayın, `People` varlık kümesini seçin ve sihirbazdaki **Seç** kutusunu değiştirmeden bırakın. **Özellikler** penceresinde aşağıdaki özellikleri ayarlayın:

- Yalnızca öğrencilerle filtrelemek için `Where` özelliğini `it.EnrollmentDate is not null`olarak ayarlayın.
- Sonuçları kayıt tarihine göre gruplandırmak için `GroupBy` özelliğini `it.EnrollmentDate`olarak ayarlayın.
- Kayıt tarihini ve öğrenci sayısını seçmek için `Select` özelliğini `it.EnrollmentDate, Count(it.EnrollmentDate) AS NumberOfStudents`olarak ayarlayın.
- Sonuçları kayıt tarihine göre sıralamak için `OrderBy` özelliğini `it.EnrollmentDate`olarak ayarlayın.

**Kaynak** görünümü ' nde, `ConnectionString` ve `DefaultContainer` adı özelliklerini bir `ContextTypeName` özelliği ile değiştirin. `EntityDataSource` denetim biçimlendirmesi artık aşağıdaki örneğe benzer.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample4.aspx)]

`Select`, `GroupBy`ve `Where` özelliklerinin sözdizimi, geçerli varlığı belirten `it` anahtar sözcüğü dışında Transact-SQL ' i benzerdir.

Verileri göstermek için bir `GridView` denetimi oluşturmak üzere aşağıdaki biçimlendirmeyi ekleyin.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample5.aspx)]

Kayıt tarihine göre öğrenci sayısını gösteren bir liste görmek için sayfayı çalıştırın.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-3/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image27.png)

## <a name="using-the-queryextender-control-for-filtering-and-ordering"></a>Filtreleme ve sıralama için Querygenişletici denetimini kullanma

`QueryExtender` denetim, İşaretlemede filtreleme ve sıralamayı belirtmenin bir yolunu sağlar. Sözdizimi, kullanmakta olduğunuz veritabanı yönetim sistemi 'nden (DBMS) bağımsızdır. Ayrıca, gezinti özellikleri için kullandığınız söz dizimi Entity Framework benzersiz olan özel durum ile, genellikle Entity Framework bağımsızdır.

Öğreticinin bu bölümünde, verileri filtrelemek ve sıralamak için bir `QueryExtender` denetimi kullanacaksınız ve order by alanlarından biri bir gezinti özelliği olacaktır.

(`EntityDataSource` denetimi tarafından otomatik olarak oluşturulan sorguları genişletmek için biçimlendirme yerine kodu kullanmayı tercih ediyorsanız, bunu `QueryCreated` olayını işleyerek yapabilirsiniz. `QueryExtender` denetimi, `EntityDataSource` denetim sorgularını de genişletmektedir.)

*Kurslar. aspx* sayfasını açın ve daha önce eklediğiniz biçimlendirmenin altında, bir başlık oluşturmak için aşağıdaki biçimlendirmeyi, arama dizeleri girmeye yönelik bir metin kutusunu, bir arama düğmesini ve `Courses` varlık kümesine bağlanan `EntityDataSource` denetimini ekleyin.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample6.aspx)]

`EntityDataSource` denetiminin `Include` özelliğinin `Department`olarak ayarlandığını unutmayın. Veritabanında, `Course` tablosu departman adını içermez; `DepartmentID` yabancı anahtar sütunu içerir. Veritabanını doğrudan sorguladığınız takdirde, Bölüm adını kurs verileriyle birlikte almak için `Course` ve `Department` tablolarına katılmanız gerekir. `Include` özelliğini `Department`olarak ayarlayarak, Entity Framework bir `Course` varlığı aldığında ilgili `Department` varlığı alma işini yapması gerektiğini belirtirsiniz. `Department` varlık daha sonra `Course` varlığının `Department` gezinti özelliğinde depolanır. (Varsayılan olarak, veri modeli Tasarımcısı tarafından oluşturulan `SchoolEntities` sınıfı, gerektiğinde ilgili verileri alır ve veri kaynağı denetimini bu sınıfa bağlamışsanız, `Include` özelliğinin ayarlanması gerekli değildir. Ancak, Entity Framework, bu sayfanın performansını artırır, aksi takdirde `Course` varlıklar ve ilgili `Department` varlıkları için verileri almak üzere veritabanına ayrı çağrılar yapacağından.)

Yeni oluşturduğunuz `EntityDataSource` denetiminden sonra, bu `EntityDataSource` denetimine bağlanan `QueryExtender` bir denetim oluşturmak için aşağıdaki biçimlendirmeyi ekleyin.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample7.aspx)]

`SearchExpression` öğesi, başlıkları metin kutusuna girilen değerle eşleşen kurslar seçmek istediğinizi belirtir. `SearchType` özelliği `StartsWith`belirttiğinden, yalnızca metin kutusuna girilen sayıda karakter karşılaştırılacaktır.

`OrderByExpression` öğesi, sonuç kümesinin, Bölüm adı içindeki kurs başlığına göre sipariş olacağını belirtir. Bölüm adının nasıl belirtildiğine dikkat edin: `Department.Name`. `Course` varlık ve `Department` varlık arasındaki ilişki bire bir, `Department` gezinti özelliği bir `Department` varlığı içerir. (Bu bir-çok ilişkisi ise, özelliği bir koleksiyon içerir.) Bölüm adını almak için `Department` varlığının `Name` özelliğini belirtmeniz gerekir.

Son olarak, kurslar listesini göstermek için bir `GridView` denetimi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample8.aspx)]

İlk sütun, Bölüm adını görüntüleyen bir şablon alanıdır. Veri bağlama ifadesi, tıpkı `QueryExtender` denetiminde gördüğünüz gibi `Department.Name`belirtir.

Sayfayı çalıştırın. İlk ekran, bölüm ve ardından kurs başlığına göre sırasıyla tüm kursların bir listesini gösterir.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-3/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image29.png)

Başlıkları "d" ile başlayan tüm kursları görmek için "d" girin ve **Ara** ' ya tıklayın (arama büyük/küçük harfe duyarlı değildir).

[![Image12](the-entity-framework-and-aspnet-getting-started-part-3/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image31.png)

## <a name="using-the-like-operator-to-filter-data"></a>Verileri filtrelemek için "Like" Işlecini kullanma

`Like` denetiminin `EntityDataSource` özelliğinde bir `Where` işleci kullanarak `QueryExtender` denetiminin `StartsWith`, `Contains`ve `EndsWith` arama türlerine benzer bir efekt elde edebilirsiniz. Öğreticinin bu bölümünde, ada göre bir öğrenci aramak için `Like` işlecini nasıl kullanacağınızı göreceksiniz.

**Kaynak** görünümünde *öğrenciler. aspx* ' i açın. `GridView` denetiminden sonra aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-3/samples/sample9.aspx)]

Bu biçimlendirme, `Where` Özellik değeri dışında daha önce gördüğünüze benzerdir. `Where` ifadesinin ikinci bölümü, metin kutusuna her şey için hem ilk hem de soyadlarını arayan bir alt dize aramasını (`LIKE %FirstMidName% or LIKE %LastName%`) tanımlar.

Sayfayı çalıştırın. Başlangıçta tüm öğrencileri görürsünüz çünkü `StudentName` parametresi için varsayılan değer "%".

[![Image13](the-entity-framework-and-aspnet-getting-started-part-3/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image33.png)

Metin kutusuna "g" harfini girin ve **Ara**' ya tıklayın. Adında "g" olan öğrencilerin bir listesini görürsünüz.

[![Image14](the-entity-framework-and-aspnet-getting-started-part-3/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-3/_static/image35.png)

Artık tek tek tablolardan, güncelleştirilmiş, filtrelenmiş, sıralanmış ve gruplandırılmış verileri görüntüdiniz. Sonraki öğreticide ilgili verilerle (ana ayrıntı senaryolarında) çalışmaya başlayabilirsiniz.

> [!div class="step-by-step"]
> [Önceki](the-entity-framework-and-aspnet-getting-started-part-2.md)
> [İleri](the-entity-framework-and-aspnet-getting-started-part-4.md)
