---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: ASP.NET MVC uygulaması için daha karmaşık veri modeli oluşturma (4/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f81f3d80-3674-4d8e-a9b1-87feed1a93c9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9c19ec47ad98a319ddee17db014c4b15e3734778
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595357"
---
# <a name="creating-a-more-complex-data-model-for-an-aspnet-mvc-application-4-of-10"></a>ASP.NET MVC uygulaması için daha karmaşık veri modeli oluşturma (4/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticilerde, üç varlıktan oluşan basit bir veri modeliyle çalıştık. Bu öğreticide, daha fazla varlık ve ilişki ekleyeceksiniz ve biçimlendirme, doğrulama ve veritabanı eşleme kurallarını belirterek veri modelini özelleştireceksiniz. Veri modelini özelleştirmek için iki yol görürsünüz: varlık sınıflarına öznitelikler ekleyerek ve veritabanı bağlamı sınıfına kod ekleyerek.

İşiniz bittiğinde, varlık sınıfları aşağıdaki çizimde gösterilen tamamlanmış veri modelini oluşturacak:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

## <a name="customize-the-data-model-by-using-attributes"></a>Öznitelikleri kullanarak veri modelini özelleştirme

Bu bölümde, biçimlendirme, doğrulama ve veritabanı eşleme kurallarını belirten öznitelikleri kullanarak veri modelini nasıl özelleştireceğinizi göreceksiniz. Aşağıdaki bölümlerde, daha önce oluşturduğunuz sınıflara öznitelikler ekleyerek ve modeldeki kalan varlık türleri için yeni sınıflar oluşturarak tüm `School` veri modelini oluşturacaksınız.

### <a name="the-datatype-attribute"></a>DataType özniteliği

Öğrenci kayıt tarihleri için tüm Web sayfaları Şu anda tarihle birlikte görüntülenir, ancak bu alan için tüm önemli bir tarih olması gerekir. Veri ek açıklaması özniteliklerini kullanarak, verileri gösteren her görünümde görüntü biçimini giderecek bir kod değişikliği yapabilirsiniz. Bunun nasıl yapılacağını gösteren bir örnek görmek için, `Student` sınıfındaki `EnrollmentDate` özelliğine bir öznitelik ekleyeceksiniz.

*Models\student.cs*içinde, `System.ComponentModel.DataAnnotations` ad alanı için `using` bir ifade ekleyin ve aşağıdaki örnekte gösterildiği gibi `EnrollmentDate` özelliğine `DataType` ve `DisplayFormat` özniteliklerini ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,13-14)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, veritabanı iç türünden daha özel bir veri türü belirtmek için kullanılır. Bu durumda, tarihi ve saati değil yalnızca tarihi izlemek istiyoruz. Veri [türü numaralandırması](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , *Tarih, saat, PhoneNumber, para birimi, emaadresi* ve daha fazlası gibi birçok veri türü sağlar. `DataType` özniteliği Ayrıca uygulamanın türe özgü özellikleri otomatik olarak sağlamasını da sağlayabilir. Örneğin, [DataType. Emaadresi](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)için bir `mailto:` bağlantısı oluşturulabilir ve [HTML5](http://html5.org/)'ı destekleyen tarayıcılardaki [DataType. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) için bir tarih seçici sağlanmış olabilir. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri HTML 5 tarayıcısının ANLAYABILMESI için HTML 5 [veri](http://ejohn.org/blog/html-5-data-attributes/) (bir *veri Dash*) öznitelikleri yayar. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri herhangi bir doğrulama sağlamaz.

`DataType.Date`, görüntülenen tarihin biçimini belirtmez. Varsayılan olarak, veri alanı sunucunun [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)öğesine göre varsayılan biçimlere göre görüntülenir.

`DisplayFormat` özniteliği, açıkça tarih biçimini belirtmek için kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

`ApplyFormatInEditMode` ayarı, bir metin kutusunda değer görüntülenmek üzere görüntülendiğinde belirtilen biçimlendirmenin de uygulanacağını belirtir. (Örneğin, para birimi değerleri için, metin kutusundaki para birimi sembolünü, düzenlenebilir bir şekilde istemeyebilirsiniz.)

[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğini kendisi kullanabilirsiniz, ancak aynı zamanda [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliğini de kullanmak iyi bir fikir olabilir. `DataType` özniteliği, verilerin *semantiğini* bir ekranda nasıl işleneceğini değil, `DisplayFormat`ile elde olmadığınız avantajları sağlar:

- Tarayıcı HTML5 özelliklerini etkinleştirebilir (örneğin, bir Takvim denetimini, yerel ayara uygun para birimi sembolünü, e-posta bağlantılarını vb. göstermek için).
- Varsayılan olarak tarayıcı, verileri [yerel ayarınızı](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)temel alarak doğru biçimi kullanarak işleyebilir.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, verileri işlemek için doğru alan şablonunu seçmek üzere MVC 'yi etkinleştirebilir (kendisi tarafından kullanılıyorsa [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) , dize şablonunu kullanır). Daha fazla bilgi için bkz. atacan Solson 'ın [ASP.NET MVC 2 şablonları](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). (MVC 2 için yazılmış olsa da, bu makale hala ASP.NET MVC 'nin geçerli sürümü için geçerlidir.)

`DataType` özniteliğini bir Tarih alanıyla birlikte kullanıyorsanız, alanın Chrome tarayıcılarında doğru şekilde işlediğinden emin olmak için `DisplayFormat` özniteliğini de belirtmeniz gerekir. Daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)bakın.

Öğrenci dizini sayfasını yeniden çalıştırın ve zamanların kayıt tarihleri için artık gösterilmediğine dikkat edin. Aynı değer, `Student` modelini kullanan herhangi bir görünüm için de geçerli olacaktır.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

Ayrıca, öznitelikleri kullanarak veri doğrulama kurallarını ve iletilerini de belirtebilirsiniz. Kullanıcıların bir ad için 50 ' den fazla karakter girmemesini istediğinizi varsayalım. Bu kısıtlamayı eklemek için, aşağıdaki örnekte gösterildiği gibi `LastName` ve `FirstMidName` özelliklerine [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) öznitelikleri ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliği, bir kullanıcının ad için boşluk girmesini engellemez. Girişe kısıtlama uygulamak için [cevap içerisinde RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) özniteliğini kullanabilirsiniz. Örneğin aşağıdaki kod, ilk karakterin büyük küçük harf olmasını ve geri kalan karakterlerin alfabetik olmasını gerektirir:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) özniteliği, [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliğinde benzer işlevler sağlar, ancak istemci tarafı doğrulaması sağlamaz.

Uygulamayı çalıştırın ve **öğrenciler** sekmesine tıklayın. Şu hatayı alırsınız:

*' SchoolContext ' bağlamını destekleyen model veritabanı oluşturulduktan sonra değiştirildi. Veritabanını güncelleştirmek için Code First Migrations kullanmayı düşünün ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

Veritabanı modeli, veritabanı şemasında değişiklik yapılmasını gerektiren bir şekilde değiştirilmiştir ve Entity Framework olduğunu tespit etti. Kullanıcı arabirimini kullanarak veritabanına eklediğiniz herhangi bir veriyi kaybetmeden Şemayı güncelleştirmek için geçişleri kullanacaksınız. `Seed` yöntemi tarafından oluşturulan verileri değiştirdiyseniz, bu, `Seed` yönteminde kullandığınız [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) yöntemi nedeniyle özgün durumuna geri dönüştürülür. ([AddOrUpdate, veritabanı terminolojisindeki](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) bir "upsert" işlem ile eşdeğerdir.)

Paket Yöneticisi konsolunda (PMC) aşağıdaki komutları girin:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

`add-migration MaxLengthOnNames` komutu, *&lt;zaman damgası&gt;\_MaxLengthOnNames.cs*adlı bir dosya oluşturur. Bu dosya, veritabanını geçerli veri modeliyle eşleşecek şekilde güncelleştirecek kodu içerir. Geçişleri sıralamak için Entity Framework zaman damgası, geçişleri dosya adı tarafından kullanılır. Birden çok geçiş oluşturduktan sonra, veritabanını bırakırsanız veya bir projeyi geçişler kullanarak dağıtırsanız, tüm geçişler oluşturuldukları sırada uygulanır.

**Oluştur** sayfasını çalıştırın ve 50 karakterden daha uzun bir ad girin. 50 karakteri aştığınız anda, istemci tarafı doğrulaması anında bir hata iletisi gösterir.

![istemci tarafı değer hatası](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image3.png)

### <a name="the-column-attribute"></a>Column özniteliği

Ayrıca, sınıflarınızın ve özelliklerinin veritabanına nasıl eşlenildiğini denetlemek için özniteliklerini de kullanabilirsiniz. Alan aynı zamanda bir orta ad içerebileceğinden, ilk ad alanı için `FirstMidName` adı kullandığınızı varsayalım. Ancak veritabanına karşı geçici sorgular yazmayacak olan kullanıcılar bu ada alışkın olduğundan, veritabanı sütununun `FirstName`adlandırılmış olmasını isteyebilirsiniz. Bu eşlemeyi yapmak için, `Column` özniteliğini kullanabilirsiniz.

`Column` özniteliği, veritabanı oluşturulduğunda, `FirstMidName` özelliğine eşlenen `Student` tablosunun sütununun `FirstName`adlandırılacağını belirtir. Diğer bir deyişle, kodunuz `Student.FirstMidName`başvurduğunda, veriler `Student` tablosunun `FirstName` sütununda gönderilir veya güncelleştirilir. Sütun adları belirtmezseniz, bunlar Özellik adı ile aynı ada atanır.

Aşağıdaki Vurgulanan kodda gösterildiği gibi, [System. ComponentModel. Dataaçıklamalarda. Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) ve Column Name özniteliği için bir using ifadesini `FirstMidName` özelliğine ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

[Sütun özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) ekleme modeli, SchoolContext 'yi yedekleyen şekilde değiştirir, bu nedenle veritabanıyla eşleşmez. Başka bir geçiş oluşturmak için PMC 'de aşağıdaki komutları girin:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

**Sunucu Gezgini** (Web için Express kullanıyorsanız**veritabanı Gezgini** ) ' de *öğrenci* tablosuna çift tıklayın.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image4.png)

Aşağıdaki görüntüde, ilk iki geçişi uygulamadan önce olduğu gibi özgün sütun adı gösterilmektedir. `FirstMidName` değiştiren sütun adının yanı sıra `FirstName`, iki ad sütunu `MAX` uzunluktan 50 karakter olarak değiştirilmiştir.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Ayrıca, bu öğreticide daha sonra göreceğiniz gibi, [AKıCı API](https://msdn.microsoft.com/data/jj591617)kullanarak veritabanı eşleme değişiklikleri yapabilirsiniz.

> [!NOTE]
> Bu varlık sınıflarının tümünü oluşturmayı bitirmeden önce derlemeye çalışırsanız derleyici hataları alabilirsiniz.

## <a name="create-the-instructor-entity"></a>Eğitmen varlığı oluşturma

![Instructor_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image6.png)

Şablon kodunu aşağıdaki kodla değiştirerek *Models\komutctor.cs*oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Çeşitli özelliklerin `Student` ve `Instructor` varlıklarda aynı olduğuna dikkat edin. Devralma öğreticisini bu serinin ilerleyen kısımlarında [uyguladığınızda](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) , bu artıklığı ortadan kaldırmak için devralma kullanarak yeniden düzenleme yapmanız gerekir.

### <a name="the-required-and-display-attributes"></a>Gerekli ve görüntüleme öznitelikleri

`LastName` özelliğindeki öznitelikler gerekli bir alan olduğunu belirtir; metin kutusu için başlığın "soyadı" olması ve bu değerin 50 karakterden uzun olmaması için "soyadı" olması gerekir (özellik adı yerine).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

[StringLength özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , veritabanında en fazla uzunluğu ayarlar ve ASP.NET MVC için istemci tarafı ve sunucu tarafı doğrulaması sağlar. Bu öznitelikte en küçük dize uzunluğunu da belirtebilirsiniz, ancak en küçük değerin veritabanı şemasında hiçbir etkisi yoktur. DateTime, int, Double ve float gibi değer türleri için [gerekli öznitelik](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) gerekli değildir. Değer türlerine null değer atanamaz, bu nedenle bunlar doğal olarak gereklidir. [Gerekli özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) kaldırabilir ve `StringLength` özniteliği için minimum length parametresiyle değiştirebilirsiniz:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs?highlight=2)]

Birden çok özniteliği tek bir satıra koyabilirsiniz. bu nedenle, aşağıdaki gibi eğitmen sınıfını da yazabilirsiniz:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-fullname-calculated-property"></a>FullName hesaplanmış özelliği

`FullName`, diğer iki özelliği birleştirerek oluşturulmuş bir değer döndüren hesaplanmış bir özelliktir. Bu nedenle, yalnızca bir `get` erişimcisi vardır ve veritabanında hiçbir `FullName` sütunu oluşturulmaz.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Kurslar ve OfficeAssignment gezinti özellikleri

`Courses` ve `OfficeAssignment` özellikleri gezinti özellikleridir. Daha önce açıklandığı gibi, [yavaş yükleme](https://msdn.microsoft.com/magazine/hh205756.aspx)adlı bir Entity Framework özelliğinden yararlanabilmeleri için genellikle [sanal](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) olarak tanımlanır. Ayrıca, bir gezinti özelliği birden çok varlık tulıyorsa, türünün [ıcollection&lt;t&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) arabirimini uygulaması gerekir. (Örneğin [ılist&lt;t&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) , `IEnumerable<T>` [Add](https://msdn.microsoft.com/library/63ywd54z.aspx)uygulamadığı için [IEnumerable&lt;t&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) olarak nitelendirir.

Bir eğitmen herhangi bir sayıda kurs öğretebilir, bu nedenle `Courses` `Course` varlıkların bir koleksiyonu olarak tanımlanmıştır. İş kurallarımızda, bir eğitmenin yalnızca en fazla bir ofisi olabilir, bu nedenle `OfficeAssignment` tek bir `OfficeAssignment` varlık olarak tanımlanmıştır (Office atanmamışsa `null` olabilir).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-the-officeassignment-entity"></a>OfficeAssignment varlığını oluşturma

![OfficeAssignment_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image7.png)

Aşağıdaki kodla *Models\officeassignment.cs* oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Değişikliklerinizi kaydeden ve derleyicinin yakalayabileceği herhangi bir kopyalama ve yapıştırma hatası yapmadığınızı doğrulayan projeyi derleyin.

### <a name="the-key-attribute"></a>Anahtar özniteliği

`Instructor` ve `OfficeAssignment` varlıkları arasında bire sıfır veya arasında bir ilişki vardır. Bir Office ataması, atandığı eğitmenle ilişkili olarak yalnızca, birincil anahtarı da `Instructor` varlığa ait yabancı anahtarıdır. Ancak Entity Framework, adı `ID` ya da *classname* `ID` adlandırma kuralına uymadığından, bu varlığın birincil anahtarı olarak `InstructorID` otomatik olarak tanıyamaz. Bu nedenle, `Key` özniteliği onu anahtar olarak tanımlamak için kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Varlık kendi birincil anahtarına sahip olsa da, özelliği `classnameID` veya `ID`farklı bir şekilde adlandırmak istiyorsanız `Key` özniteliğini de kullanabilirsiniz. Varsayılan olarak, sütun bir tanımlayıcı ilişki için olduğu için, bu anahtarı, anahtarı veritabanı olmayan üretilmiş olarak değerlendirir.

### <a name="the-foreignkey-attribute"></a>ForeignKey özniteliği

Bire sıfır veya-tek bir ilişki ya da iki varlık arasında bire bir ilişki varsa (`OfficeAssignment` ve `Instructor`arasında), EF ilişkinin ne kadar sona düğüne ve hangisinin bağımlı olduğunu bir şekilde çalışmaz. Bire bir ilişkilerde, diğer sınıfa her bir sınıfta başvuru gezintisi özelliği vardır. İlişki kurmak için, [ForeignKey özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) bağımlı sınıfa uygulanabilir. [Yabancıanahtar özniteliğini](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)atlarsanız, geçişi oluşturmaya çalıştığınızda şu hatayı alırsınız:

' ContosoUniversity. modeller. OfficeAssignment ' ve ' ContosoUniversity. modeller. eğitmen ' türleri arasındaki bir ilişkinin asıl ucu belirlenemiyor. Bu ilişkinin asıl sonu, ilişki Fluent API veya veri ek açıklamaları kullanılarak açıkça yapılandırılmalıdır.

Öğreticide daha sonra bu ilişkiyi Fluent API ile nasıl yapılandıracağınızı göstereceğiz.

### <a name="the-instructor-navigation-property"></a>Eğitmen gezintisi özelliği

`Instructor` varlık null yapılabilir bir `OfficeAssignment` gezinti özelliğine sahiptir (bir eğitmenin bir Office ataması olmayabilir) ve `OfficeAssignment` varlık null atanamaz bir `Instructor` gezinti özelliğine sahiptir (bir Office ataması bir eğitmen olmadan mevcut olamaz--`InstructorID` null değer atanamaz). `Instructor` bir varlık ilişkili bir `OfficeAssignment` varlığına sahip olduğunda, her varlığın gezinti özelliğinde diğer birine bir başvurusu olur.

İlgili bir eğitmen olması gerektiğini belirtmek için, eğitmen gezinti özelliğine bir `[Required]` özniteliği koyabilirsiniz, ancak bunu yapmanız gerekmez çünkü bu, Komutctorıd yabancı anahtarı (aynı zamanda bu tabloya yönelik anahtar) null değer atanamaz.

## <a name="modify-the-course-entity"></a>Kurs varlığını değiştirme

![Course_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Models\course.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

Kurs varlığı, ilgili `Department` varlığına işaret eden ve bir `Department` gezinti özelliğine sahip `DepartmentID` yabancı anahtar özelliğine sahiptir. Entity Framework, ilgili varlık için bir gezinti özelliği olduğunda, veri modelinize yabancı anahtar özelliği eklemenizi gerektirmez. EF, gerektiğinde veritabanında yabancı anahtarlar otomatik olarak oluşturur. Ancak veri modelinde yabancı anahtar olması, güncelleştirmeleri daha basit ve daha verimli hale getirir. Örneğin, düzenlemek üzere bir kurs varlığı aldığınızda, bunu yüklemezseniz `Department` varlık null olur, böylece kurs varlığını güncelleştirdiğinizde öncelikle `Department` varlığını almanız gerekir. Yabancı anahtar özelliği `DepartmentID` veri modeline dahil edildiğinde, güncelleştirmeden önce `Department` varlığını almanız gerekmez.

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated özniteliği

`CourseID` özelliğinde [none](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parametresi olan [databasegenerated özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) , birincil anahtar değerlerinin veritabanı tarafından oluşturulması yerine Kullanıcı tarafından sağlandığını belirtir.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

Varsayılan olarak, Entity Framework birincil anahtar değerlerinin veritabanı tarafından oluşturulduğunu varsayar. Bu, Çoğu senaryoda istediğiniz şeydir. Ancak, `Course` varlıkları için bir departman için 1000 serisi, başka bir departman için 2000 serisi vb. gibi kullanıcı tarafından belirtilen kurs numarasını kullanırsınız.

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

`Course` varlığındaki yabancı anahtar özellikleri ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Bir kurs bir departmana atanır, bu nedenle yukarıda bahsedilen nedenlerle `DepartmentID` yabancı anahtar ve `Department` gezinti özelliği vardır. 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- Bir kurs, kayıtlı sayıda öğrenciye sahip olabilir, bu nedenle `Enrollments` gezinti özelliği bir koleksiyondur: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- Bir kurs birden fazla eğitmen tarafından tada olabilir, bu nedenle `Instructors` gezinti özelliği bir koleksiyondur: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="creating-the-department-entity"></a>Departman varlığı oluşturma

![Department_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image9.png)

Aşağıdaki kodla *Models\Department.cs* oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Column özniteliği

Daha önce sütun adı eşlemesini değiştirmek için [Column özniteliğini](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) kullandınız. `Department` varlığının kodunda, sütunun veritabanındaki SQL Server [para](https://msdn.microsoft.com/library/ms179882.aspx) türü kullanılarak TANıMLANMASı için SQL veri türü eşlemesini değiştirmek üzere `Column` özniteliği kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Entity Framework genellikle özellik için tanımladığınız CLR türüne göre uygun SQL Server veri türünü seçtiği için sütun eşlemesi genellikle gerekli değildir. CLR `decimal` türü bir SQL Server `decimal` türüne eşlenir. Ancak bu durumda, sütunun para birimi tutarlarını tutuını ve [para](https://msdn.microsoft.com/library/ms179882.aspx) veri türü bunun için daha uygun olduğunu bilirsiniz.

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

Yabancı anahtar ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Bir departman yönetici olabilir veya olmayabilir ve yönetici her zaman bir eğitmendir. Bu nedenle `InstructorID` özelliği, `Instructor` varlığına yabancı anahtar olarak dahil edilir ve özelliği null yapılabilir olarak işaretlemek için `int` tür atamadan sonra bir soru işareti eklenir. Gezinti özelliği `Administrator` olarak adlandırılır ancak bir `Instructor` varlığı tutar: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- Bir departmanın birçok kursu olabilir, bu nedenle `Courses` bir gezinti özelliği vardır: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > Kurala göre Entity Framework, null olamayan yabancı anahtarlar ve çoktan çoğa ilişkiler için art arda silme imkanı sağlar. Bu, başlatıcı kodunuz çalışırken bir özel duruma neden olacak dairesel basamaklı silme kurallarına neden olabilir. Örneğin, `Department.InstructorID` özelliğini null yapılabilir olarak tanımlamadıysanız, başlatıcı çalışırken aşağıdaki özel durum iletisini alırsınız: "başvurusal ilişki izin verilmeyen bir döngüsel başvuruya neden olur." İş kurallarınızın özelliği null yapılamayan olarak `InstructorID` gerekiyorsa, ilişkide basamaklı silmeyi devre dışı bırakmak için aşağıdaki Fluent API kullanmanız gerekir: 

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modifying-the-student-entity"></a>Öğrenci varlığını değiştirme

![Student_entity](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image10.png)

*Models\student.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=12,15,24-27)]

## <a name="the-enrollment-entity"></a>Kayıt varlığı

 *Models\kayıtlarına Ment.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs?highlight=16)]

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

Yabancı anahtar özellikleri ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Kayıt kaydı tek bir kurs için olduğundan `CourseID` yabancı anahtar özelliği ve `Course` gezinti özelliği vardır: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]
- Kayıt kaydı tek bir öğrenci içindir, bu nedenle `StudentID` yabancı anahtar özelliği ve `Student` gezinti özelliği vardır: 

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

### <a name="many-to-many-relationships"></a>Çoktan çoğa Ilişkiler

`Student` ve `Course` varlıkları arasında çok-çok ilişkisi vardır ve `Enrollment` varlığı, veritabanında *Yük içeren* çoktan çoğa bir JOIN tablosu gibi çalışır. Bu, `Enrollment` tablonun birleştirilmiş tablolar için yabancı anahtarlar (Bu örnekte, birincil anahtar ve bir `Grade` özelliği) yanında ek veriler içerdiği anlamına gelir.

Aşağıdaki çizimde bu ilişkilerin bir varlık diyagramında nasıl göründüğünü gösterilmektedir. (Bu diyagram [Entity Framework güç araçları](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)kullanılarak oluşturulmuştur; diyagramı oluşturma öğreticinin bir parçası değildir, burada yalnızca bir çizim olarak kullanılmaktadır.)

![Öğrenci-Course_many many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image11.png)

Her ilişki hattının 1 ' de bir sonda ve bir yıldız işareti (\*) vardır ve tek-çok ilişkisini gösterir.

`Enrollment` tablo, sınıf bilgilerini içermiyorsa, yalnızca iki yabancı anahtar `CourseID` ve `StudentID`içermesi gerekir. Bu durumda, veritabanında yük (veya *saf bir JOIN tablosu*) *olmadan* çoktan çoğa bir JOIN tablosuna karşılık gelir ve bir model sınıfı oluşturmanız gerekmez. `Instructor` ve `Course` varlıkların bu tür çok-çok ilişkisi vardır ve görebileceğiniz gibi, aralarında bir varlık sınıfı yoktur:

![Eğitmen-many_relationship Course_many](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

Veritabanında bir JOIN tablosu gereklidir, ancak aşağıdaki veritabanı diyagramında gösterildiği gibi:

![Eğitmen-many_relationship_tables Course_many](https://asp.net/media/2577802/Windows-Live-Writer_Creating-a.NET-MVC-Application-4-of-10h1_B662_Instructor-Course_many-to-many_relationship_tables_03e042cf-db89-4b4c-985a-e458351ada76.png)

Entity Framework, `CourseInstructor` tabloyu otomatik olarak oluşturur ve `Instructor.Courses` ve `Course.Instructors` gezinti özelliklerini okuyup güncelleştirerek onu dolaylı olarak okuyup güncelleyebilirsiniz.

## <a name="entity-diagram-showing-relationships"></a>Ilişkileri gösteren varlık diyagramı

Aşağıdaki çizimde, Entity Framework Power Tools 'un tamamlanmış okul modeli için kullandığı diyagram gösterilmektedir.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Çoktan çoğa ilişki satırlarından (\*\*) ve bire çok ilişki çizgilerinin yanı sıra (1 ' den \*) burada, `Instructor` ve `OfficeAssignment` varlıkları arasında bire sıfır veya-bir ilişki satırını (1 ila 0.. 1), eğitmen ve departman varlıkları arasında sıfır veya-bire çok ilişki satırını (0.. 1 ' den \*) görüntüleyebilirsiniz.

## <a name="customize-the-data-model-by-adding-code-to-the-database-context"></a>Veritabanı bağlamına kod ekleyerek veri modelini özelleştirme

Ardından, yeni varlıkları `SchoolContext` sınıfına ekleyecek ve [Fluent API](https://msdn.microsoft.com/data/jj591617) çağrılarını kullanarak eşlemenin bazılarını özelleştireceksiniz. (API, genellikle tek bir bildirimde bir dizi yöntem çağrısı tarafından kullanıldığı için kullanıldığından "akıcı hale gelir".)

Bu öğreticide, yalnızca özniteliklerle yapacağımız veritabanı eşlemesi için Fluent API kullanacaksınız. Ancak, özniteliklerini kullanarak yapabileceğiniz biçimlendirme, doğrulama ve eşleme kurallarının çoğunu belirtmek için Fluent API de kullanabilirsiniz. `MinimumLength` gibi bazı öznitelikler Fluent API uygulanamaz. Daha önce belirtildiği gibi, `MinimumLength` şemayı değiştirmez, yalnızca bir istemci ve sunucu tarafı doğrulama kuralı uygular

Bazı geliştiriciler, varlık sınıflarının "temiz" olmasını sağlamak için Fluent API özel olarak kullanmayı tercih eder. İsterseniz öznitelikleri ve Fluent API karıştırabilir ve yalnızca Fluent API kullanılarak gerçekleştirilebilecek bazı özelleştirmeler de vardır ancak genel olarak önerilen uygulama, bu iki yaklaşımdan birini seçmek ve bunları mümkün olduğunca tutarlı bir şekilde kullanmaktır.

Yeni varlıkları veri modeline eklemek ve öznitelikleri kullanarak gerçekleştirmediğiniz veritabanı eşlemesini gerçekleştirmek için *DAL\SchoolContext.cs* içindeki kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

[Onmodeloluþturma](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) yöntemindeki yeni ifade, çoktan çoğa JOIN tablosunu yapılandırır:

- `Instructor` ve `Course` varlıkları arasındaki çoktan çoğa ilişki için, kod, JOIN tablosunun tablo ve sütun adlarını belirtir. Code First, bu kod olmadan çoktan çoğa ilişkiyi yapılandırabilir, ancak bunu çağırmazsanız, `InstructorID` sütunu için `InstructorInstructorID` gibi varsayılan adlar alacaksınız.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

Aşağıdaki kod, `Instructor` ve `OfficeAssignment` varlıkları arasındaki ilişkiyi belirtmek için öznitelikleri yerine Fluent API nasıl kullanabileceğinizi gösteren bir örnek sağlar:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

Arka planda hangi "Fluent API" deyimlerinin bulunduğu hakkında bilgi için bkz. [Floent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog gönderisi.

## <a name="seed-the-database-with-test-data"></a>Veritabanını test verileriyle çekirdek olarak

Yeni oluşturduğunuz varlıklar için çekirdek verileri sağlamak üzere *Migrations\configuration.cs* dosyasındaki kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

İlk öğreticide gördüğünüz gibi, bu kodun çoğu yalnızca yeni varlık nesneleri güncelleştirir veya oluşturur ve test için gereken şekilde, örnek verileri özelliklere yükler. Ancak, `Instructor` varlığıyla çok-çok ilişkisi olan `Course` varlığın nasıl işlendiğini fark edebilirsiniz:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

`Course` nesnesi oluşturduğunuzda, `Instructors` gezinti özelliğini kod `Instructors = new List<Instructor>()`kullanarak boş bir koleksiyon olarak başlatırsınız. Bu, `Instructors.Add` yöntemi kullanılarak bu `Course` ilgili varlık `Instructor` eklemek mümkün hale getirir. Boş bir liste oluşturmadıysanız, `Instructors` özelliği null olduğu ve bir `Add` yöntemine sahip olmadığı için bu ilişkileri ekleyemezsiniz. Ayrıca, oluşturucuya liste başlatmayı da ekleyebilirsiniz.

## <a name="add-a-migration-and-update-the-database"></a>Geçiş ekleme ve veritabanını güncelleştirme

PMC 'den `add-migration` komutunu girin:

`PM> add-Migration Chap4`

Bu noktada veritabanını güncelleştirmeye çalışırsanız aşağıdaki hatayı alırsınız:

*ALTER TABLE ifadesi, "FK\_dbo yabancı anahtar kısıtlaması ile çakışıyor.\_dbo. Departman\_DepartmentID ". "ContosoUniversity" veritabanında, "dbo" tablosunda çakışma oluştu. Bölüm ", sütun ' DepartmentID '.*

&lt;*zaman damgası&gt;\_Chap4.cs* dosyasını düzenleyin ve aşağıdaki kod değişikliklerini yapın (bir SQL ifadesini ekler ve bir `AddColumn` ifadesini değiştirirsiniz):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

(Yenisini eklediğinizde var olan `AddColumn` satırı kullanıma almanızı veya sildikten emin olun veya `update-database` komutunu girerken bir hata alırsınız.)

Bazı durumlarda, mevcut verilerle geçişleri yürüttüğünüzde, yabancı anahtar kısıtlamalarını karşılamak için saplama verilerini veritabanına eklemeniz ve şimdi yaptığınız şeydir. Oluşturulan kod, `Course` tablosuna null yapılamayan `DepartmentID` yabancı anahtar ekler. Kod çalışırken `Course` tablosunda zaten satırlar varsa, SQL Server null olmayan sütuna hangi değerin yerleştirileceğini bilmediği için `AddColumn` işlemi başarısız olur. Bu nedenle, yeni sütuna varsayılan bir değer vermek için kodu değiştirdiniz ve varsayılan departman olarak davranacak "Temp" adlı bir saplama departmanı oluşturdunuz. Sonuç olarak, bu kod çalıştırıldığında mevcut `Course` satırları varsa, hepsi "geçici" departmanla ilgili olacaktır.

`Seed` yöntemi çalıştırıldığında, `Department` tabloya satır ekler ve mevcut `Course` satırları bu yeni `Department` satırlarıyla ilişkilendirilecektir. Kullanıcı arabirimine hiçbir kurs eklemediyseniz, bundan sonra artık `Course.DepartmentID` sütununda "geçici" Departmanı veya varsayılan değer gerekmez. Başka birinin uygulamayı kullanarak kurs eklemesine izin vermek için, sütundan varsayılan değeri kaldırmadan ve "geçici" departmanı silmeden önce tüm `Course` satırları (yalnızca `Seed` yönteminin önceki çalıştırmaları tarafından Eklenenler değil) geçerli `DepartmentID` değerlere sahip olduğundan emin olmak için `Seed` yöntemi kodunu da güncellemek isteyebilirsiniz.

&lt;*zaman damgasını&gt;\_Chap4.cs* dosyası düzenlemesini tamamladıktan sonra, geçişi yürütmek için PMC 'de `update-database` komutunu girin.

> [!NOTE]
> Verileri geçirirken ve şema değişiklikleri yaparken başka hatalar almak mümkündür. Çözümleyemez geçiş hataları alırsanız, *Web. config* dosyasındaki bağlantı dizesini değiştirebilir veya veritabanını silebilirsiniz. En basit yaklaşım, *Web. config* dosyasındaki veritabanını yeniden adlandırmalıdır. Örneğin, aşağıdaki şekilde gösterildiği gibi, veritabanı adını\_test olarak değiştirin:
> 
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.xml?highlight=1-2)]
> 
> Yeni bir veritabanı ile geçirilecek veri yoktur ve `update-database` komutunun hatasız tamamlanabilmesi çok daha yüksektir. Veritabanının nasıl silineceği hakkında yönergeler için bkz. [Visual Studio 'dan bir veritabanını bırakma 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).

Veritabanını daha önce yaptığınız gibi **Sunucu Gezgini** açın ve tabloların tümünün oluşturulduğunu görmek için **Tables** düğümünü genişletin. (Önceki zamandan hala **Sunucu Gezgini** açıksa **Yenile** düğmesine tıklayın.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

`CourseInstructor` tablosu için bir model sınıfı oluşturmadınız. Daha önce açıklandığı gibi, bu, `Instructor` ve `Course` varlıkları arasındaki çoktan çoğa ilişki için bir JOIN tablosudur.

`CourseInstructor` tabloya sağ tıklayıp **tablo verilerini göster** ' i seçerek, `Course.Instructors` gezinti özelliğine eklediğiniz `Instructor` varlıklarının bir sonucu olarak bu verinin içinde veri olduğunu doğrulayın.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image15.png)

## <a name="summary"></a>Özet

Artık daha karmaşık bir veri modeli ve ilgili veritabanınız var. Aşağıdaki öğreticide ilgili verilere erişmenin farklı yolları hakkında daha fazla bilgi edineceksiniz.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Önceki](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [İleri](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
