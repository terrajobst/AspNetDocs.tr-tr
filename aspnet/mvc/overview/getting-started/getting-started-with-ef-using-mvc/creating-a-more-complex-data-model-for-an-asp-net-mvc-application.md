---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
title: 'Öğretici: ASP.NET MVC uygulaması için daha karmaşık veri modeli oluşturma'
author: tdykstra
description: Bu öğreticide, daha fazla varlık ve ilişki ekleyeceksiniz ve biçimlendirme, doğrulama ve veritabanı eşleme kurallarını belirterek veri modelini özelleştireceksiniz.
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 46f7f3c9-274f-4649-811d-92222a9b27e2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-a-more-complex-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 933354b09eb4674e6f523f8a65816410521f026f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583330"
---
# <a name="tutorial-create-a-more-complex-data-model-for-an-aspnet-mvc-app"></a>Öğretici: ASP.NET MVC uygulaması için daha karmaşık veri modeli oluşturma

Önceki öğreticilerde, üç varlıktan oluşan basit bir veri modeliyle çalıştık. Bu öğreticide, daha fazla varlık ve ilişki ekler ve biçimlendirme, doğrulama ve veritabanı eşleme kurallarını belirterek veri modelini özelleştirirsiniz. Bu makalede, veri modelini özelleştirmenin iki yolu gösterilmektedir: varlık sınıflarına öznitelikler ekleyerek ve veritabanı bağlamı sınıfına kod ekleyerek.

İşiniz bittiğinde, varlık sınıfları aşağıdaki çizimde gösterilen tamamlanmış veri modelini oluşturacak:

![School_class_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Veri modelini özelleştirme
> * Öğrenci varlığını Güncelleştir
> * Eğitmen varlığı oluşturma
> * OfficeAssignment varlığı oluştur
> * Kurs varlığını değiştirme
> * Departman varlığı oluşturma
> * Kayıt varlığını değiştirme
> * Veritabanı bağlamına kod ekleme
> * Test verileriyle çekirdek veritabanı
> * Geçiş Ekle
> * Veritabanını güncelleştirme

## <a name="prerequisites"></a>Önkoşullar

* [Geçişleri ve dağıtımı Code First](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="customize-the-data-model"></a>Veri modelini özelleştirme

Bu bölümde, biçimlendirme, doğrulama ve veritabanı eşleme kurallarını belirten öznitelikleri kullanarak veri modelini nasıl özelleştireceğinizi göreceksiniz. Aşağıdaki bölümlerde, daha önce oluşturduğunuz sınıflara öznitelikler ekleyerek ve modeldeki kalan varlık türleri için yeni sınıflar oluşturarak tüm `School` veri modelini oluşturacaksınız.

### <a name="the-datatype-attribute"></a>DataType özniteliği

Öğrenci kayıt tarihleri için tüm Web sayfaları Şu anda tarihle birlikte görüntülenir, ancak bu alan için tüm önemli bir tarih olması gerekir. Veri ek açıklaması özniteliklerini kullanarak, verileri gösteren her görünümde görüntü biçimini giderecek bir kod değişikliği yapabilirsiniz. Bunun nasıl yapılacağını gösteren bir örnek görmek için, `Student` sınıfındaki `EnrollmentDate` özelliğine bir öznitelik ekleyeceksiniz.

*Models\student.cs*içinde, `System.ComponentModel.DataAnnotations` ad alanı için `using` bir ifade ekleyin ve aşağıdaki örnekte gösterildiği gibi `EnrollmentDate` özelliğine `DataType` ve `DisplayFormat` özniteliklerini ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,12-13)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, veritabanı iç türünden daha özel bir veri türü belirtmek için kullanılır. Bu durumda, tarihi ve saati değil yalnızca tarihi izlemek istiyoruz. Veri [türü numaralandırması](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , *Tarih, saat, PhoneNumber, para birimi, emaadresi* ve daha fazlası gibi birçok veri türü sağlar. `DataType` özniteliği Ayrıca uygulamanın türe özgü özellikleri otomatik olarak sağlamasını da sağlayabilir. Örneğin, [DataType. Emaadresi](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)için bir `mailto:` bağlantısı oluşturulabilir ve [HTML5](http://html5.org/)'ı destekleyen tarayıcılardaki [DataType. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) için bir tarih seçici sağlanmış olabilir. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri HTML 5 tarayıcısının ANLAYABILMESI için HTML 5 [veri](http://ejohn.org/blog/html-5-data-attributes/) (bir *veri Dash*) öznitelikleri yayar. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri herhangi bir doğrulama sağlamaz.

`DataType.Date`, görüntülenen tarihin biçimini belirtmez. Varsayılan olarak, veri alanı sunucunun [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)öğesine göre varsayılan biçimlere göre görüntülenir.

`DisplayFormat` özniteliği, açıkça tarih biçimini belirtmek için kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

`ApplyFormatInEditMode` ayarı, bir metin kutusunda değer görüntülenmek üzere görüntülendiğinde belirtilen biçimlendirmenin de uygulanacağını belirtir. (Örneğin, para birimi değerleri için, metin kutusundaki para birimi sembolünü, düzenlenebilir bir şekilde istemeyebilirsiniz.)

[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğini kendisi kullanabilirsiniz, ancak aynı zamanda [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliğini de kullanmak iyi bir fikir olabilir. `DataType` özniteliği, verilerin *semantiğini* bir ekranda nasıl işleneceğini değil, `DisplayFormat`ile elde olmadığınız avantajları sağlar:

- Tarayıcı HTML5 özelliklerini etkinleştirebilir (örneğin, bir Takvim denetimini, yerel ayara uygun para birimi sembolünü, e-posta bağlantılarını, bazı istemci tarafı giriş doğrulamasını vb. göstermek için).
- Varsayılan olarak tarayıcı, verileri [yerel ayarınızı](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)temel alarak doğru biçimi kullanarak işleyebilir.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, verileri işlemek için doğru alan şablonunu seçmek üzere MVC 'yi etkinleştirebilir ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) dize şablonunu kullanır). Daha fazla bilgi için bkz. atacan Solson 'ın [ASP.NET MVC 2 şablonları](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). (MVC 2 için yazılmış olsa da, bu makale hala ASP.NET MVC 'nin geçerli sürümü için geçerlidir.)

`DataType` özniteliğini bir Tarih alanıyla birlikte kullanıyorsanız, alanın Chrome tarayıcılarında doğru şekilde işlediğinden emin olmak için `DisplayFormat` özniteliğini de belirtmeniz gerekir. Daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)bakın.

MVC 'de diğer tarih biçimlerinin nasıl işleneceği hakkında daha fazla bilgi için, [MVC 5 tanıtım sayfasına gidin: düzenleme yöntemlerini İnceleme ve düzenleme görünümü](../introduction/examining-the-edit-methods-and-edit-view.md) ve sayfada &quot;uluslararası duruma getirme&quot;için arama.

Öğrenci dizini sayfasını yeniden çalıştırın ve zamanların kayıt tarihleri için artık gösterilmediğine dikkat edin. Aynı değer, `Student` modelini kullanan herhangi bir görünüm için de geçerli olacaktır.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

Ayrıca, öznitelikleri kullanarak veri doğrulama kuralları ve doğrulama hata iletileri de belirtebilirsiniz. [StringLength özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , veritabanında en fazla uzunluğu ayarlar ve ASP.NET MVC için istemci tarafı ve sunucu tarafı doğrulaması sağlar. Bu öznitelikte en küçük dize uzunluğunu da belirtebilirsiniz, ancak en küçük değerin veritabanı şemasında hiçbir etkisi yoktur.

Kullanıcıların bir ad için 50 ' den fazla karakter girmemesini istediğinizi varsayalım. Bu kısıtlamayı eklemek için, aşağıdaki örnekte gösterildiği gibi `LastName` ve `FirstMidName` özelliklerine [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) öznitelikleri ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliği, bir kullanıcının ad için boşluk girmesini engellemez. Girişe kısıtlama uygulamak için [cevap içerisinde RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) özniteliğini kullanabilirsiniz. Örneğin aşağıdaki kod, ilk karakterin büyük küçük harf olmasını ve geri kalan karakterlerin alfabetik olmasını gerektirir:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) özniteliği, [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliğinde benzer işlevler sağlar, ancak istemci tarafı doğrulaması sağlamaz.

Uygulamayı çalıştırın ve **öğrenciler** sekmesine tıklayın. Şu hatayı alırsınız:

*' SchoolContext ' bağlamını destekleyen model veritabanı oluşturulduktan sonra değiştirildi. Veritabanını güncelleştirmek için Code First Migrations kullanmayı düşünün ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

Veritabanı modeli, veritabanı şemasında değişiklik yapılmasını gerektiren bir şekilde değiştirilmiştir ve Entity Framework olduğunu tespit etti. Kullanıcı arabirimini kullanarak veritabanına eklediğiniz herhangi bir veriyi kaybetmeden Şemayı güncelleştirmek için geçişleri kullanacaksınız. `Seed` yöntemi tarafından oluşturulan verileri değiştirdiyseniz, bu, `Seed` yönteminde kullandığınız [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) yöntemi nedeniyle özgün durumuna geri dönüştürülür. ([AddOrUpdate, veritabanı terminolojisindeki](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) bir "upsert" işlem ile eşdeğerdir.)

Paket Yöneticisi konsolunda (PMC) aşağıdaki komutları girin:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

`add-migration` komutu, *&lt;zaman damgası&gt;\_MaxLengthOnNames.cs*adlı bir dosya oluşturur. Bu dosya, veritabanını geçerli veri modeliyle eşleşecek şekilde güncelleştirecek `Up` yönteminde kod içerir. `update-database` komutu bu kodu çalıştırdı.

Geçişleri sıralamak için Entity Framework zaman damgası, geçişleri dosya adı tarafından kullanılır. `update-database` komutunu çalıştırmadan önce birden çok geçiş oluşturabilirsiniz ve sonra tüm geçişler oluşturuldukları sırada uygulanır.

**Oluştur** sayfasını çalıştırın ve 50 karakterden daha uzun bir ad girin. **Oluştur**' a tıkladığınızda, istemci tarafı doğrulaması bir hata iletisi gösterir: *LastName alanı en fazla 50 uzunluğunda bir dize olmalıdır.*

### <a name="the-column-attribute"></a>Column özniteliği

Ayrıca, sınıflarınızın ve özelliklerinin veritabanına nasıl eşlenildiğini denetlemek için özniteliklerini de kullanabilirsiniz. Alan aynı zamanda bir orta ad içerebileceğinden, ilk ad alanı için `FirstMidName` adı kullandığınızı varsayalım. Ancak veritabanına karşı geçici sorgular yazmayacak olan kullanıcılar bu ada alışkın olduğundan, veritabanı sütununun `FirstName`adlandırılmış olmasını isteyebilirsiniz. Bu eşlemeyi yapmak için, `Column` özniteliğini kullanabilirsiniz.

`Column` özniteliği, veritabanı oluşturulduğunda, `FirstMidName` özelliğine eşlenen `Student` tablosunun sütununun `FirstName`adlandırılacağını belirtir. Diğer bir deyişle, kodunuz `Student.FirstMidName`başvurduğunda, veriler `Student` tablosunun `FirstName` sütununda gönderilir veya güncelleştirilir. Sütun adları belirtmezseniz, bunlar Özellik adı ile aynı ada atanır.

*Student.cs* dosyasında, [System. ComponentModel. Dataaçıklamalarda. Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) için bir `using` ekstresi ekleyin ve aşağıdaki vurgulanmış kodda gösterildiği gibi, `FirstMidName` özelliğine Column Name özniteliğini ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

[Sütun özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) ekleme modeli, SchoolContext 'yi yedekleyen şekilde değiştirir, bu nedenle veritabanıyla eşleşmez. Başka bir geçiş oluşturmak için PMC 'de aşağıdaki komutları girin:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

**Sunucu Gezgini** *, öğrenci tablosuna* çift tıklayarak *öğrenci* tablosu tasarımcısını açın.

Aşağıdaki görüntüde, ilk iki geçişi uygulamadan önce olduğu gibi özgün sütun adı gösterilmektedir. `FirstMidName` değiştiren sütun adının yanı sıra `FirstName`, iki ad sütunu `MAX` uzunluktan 50 karakter olarak değiştirilmiştir.

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Ayrıca, bu öğreticide daha sonra göreceğiniz gibi, [AKıCı API](https://msdn.microsoft.com/data/jj591617)kullanarak veritabanı eşleme değişiklikleri yapabilirsiniz.

> [!NOTE]
> Aşağıdaki bölümlerde tüm varlık sınıflarını oluşturmayı bitirmeden önce derlemeyi denerseniz Derleyici hataları alabilirsiniz.

## <a name="update-student-entity"></a>Öğrenci varlığını Güncelleştir

*Models\student.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=11,13,15,18,22,25-32)]

### <a name="the-required-attribute"></a>Gerekli öznitelik

[Gerekli öznitelik](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) , ad özellikleri gereken alanları sağlar. `Required attribute` DateTime, int, Double ve float gibi değer türleri için gerekli değildir. Değer türlerine null değer atanamaz, bu nedenle bunlar doğal olarak gerekli alanlar olarak kabul edilir. 

`MinimumLength` zorlanmak için `Required` özniteliği `MinimumLength` ile birlikte kullanılmalıdır.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs?highlight=2)]

`MinimumLength` ve `Required`, doğrulamanın doğrulanmasını yerine getirmek için boşluk kullanılmasına izin verir. Dize üzerinde tam denetimi için `RegularExpression` özniteliğini kullanın.

### <a name="the-display-attribute"></a>Display özniteliği

`Display` özniteliği, metin kutularının açıklamalı alt yazısının her örnekteki Özellik adı yerine "Ilk ad", "soyadı", "tam ad" ve "kayıt tarihi" olması gerektiğini belirtir (kelimeleri bir boşluk yoktur).

### <a name="the-fullname-calculated-property"></a>FullName hesaplanmış özelliği

`FullName`, diğer iki özelliği birleştirerek oluşturulmuş bir değer döndüren hesaplanmış bir özelliktir. Bu nedenle, yalnızca bir `get` erişimcisi vardır ve veritabanında hiçbir `FullName` sütunu oluşturulmaz.

## <a name="create-instructor-entity"></a>Eğitmen varlığı oluşturma

Şablon kodunu aşağıdaki kodla değiştirerek *Models\komutctor.cs*oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs)]

Çeşitli özelliklerin `Student` ve `Instructor` varlıklarda aynı olduğuna dikkat edin. Devralma öğreticisini bu serinin ilerleyen kısımlarında [uyguladığınızda](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) , artıklığı ortadan kaldırmak için bu kodu yeniden düzenlemelisiniz.

Birden çok özniteliği tek bir satıra koyabilirsiniz. bu nedenle, aşağıdaki gibi eğitmen sınıfını da yazabilirsiniz:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Kurslar ve OfficeAssignment gezinti özellikleri

`Courses` ve `OfficeAssignment` özellikleri gezinti özellikleridir. Daha önce açıklandığı gibi, [yavaş yükleme](https://msdn.microsoft.com/magazine/hh205756.aspx)adlı bir Entity Framework özelliğinden yararlanabilmeleri için genellikle [sanal](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) olarak tanımlanır. Ayrıca, bir gezinti özelliği birden çok varlık tulıyorsa, türünün [ıcollection&lt;t&gt;](https://msdn.microsoft.com/library/92t2ye13.aspx) arabirimini uygulaması gerekir. Örneğin [ılist&lt;t&gt;](https://msdn.microsoft.com/library/5y536ey6.aspx) , `IEnumerable<T>` [Add](https://msdn.microsoft.com/library/63ywd54z.aspx)uygulamadığı için [IEnumerable&lt;t&gt;](https://msdn.microsoft.com/library/9eekhta0.aspx) nitelendirir ancak değil.

Bir eğitmen herhangi bir sayıda kurs öğretebilir, bu nedenle `Courses` `Course` varlıkların bir koleksiyonu olarak tanımlanmıştır.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

İş kurallarımızda, bir eğitmenin yalnızca en fazla bir ofisi olabilir, bu nedenle `OfficeAssignment` tek bir `OfficeAssignment` varlık olarak tanımlanmıştır (Office atanmamışsa `null` olabilir).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-officeassignment-entity"></a>OfficeAssignment varlığı oluştur

Aşağıdaki kodla *Models\officeassignment.cs* oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Değişikliklerinizi kaydeden ve derleyicinin yakalayabileceği herhangi bir kopyalama ve yapıştırma hatası yapmadığınızı doğrulayan projeyi derleyin.

### <a name="the-key-attribute"></a>Anahtar özniteliği

`Instructor` ve `OfficeAssignment` varlıkları arasında bire sıfır veya arasında bir ilişki vardır. Bir Office ataması, atandığı eğitmenle ilişkili olarak yalnızca, birincil anahtarı da `Instructor` varlığa ait yabancı anahtarıdır. Ancak Entity Framework, adı `ID` ya da *classname* `ID` adlandırma kuralına uymadığından, bu varlığın birincil anahtarı olarak `InstructorID` otomatik olarak tanıyamaz. Bu nedenle, `Key` özniteliği onu anahtar olarak tanımlamak için kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Varlık kendi birincil anahtarına sahip olsa da, özelliği `classnameID` veya `ID`farklı bir şekilde adlandırmak istiyorsanız `Key` özniteliğini de kullanabilirsiniz. Varsayılan olarak, sütun bir tanımlayıcı ilişki için olduğu için, bu anahtarı, anahtarı veritabanı olmayan üretilmiş olarak değerlendirir.

### <a name="the-foreignkey-attribute"></a>ForeignKey özniteliği

Bire sıfır veya-tek bir ilişki ya da iki varlık arasında bire bir ilişki varsa (`OfficeAssignment` ve `Instructor`arasında), EF ilişkinin ne kadar sona düğüne ve hangisinin bağımlı olduğunu bir şekilde çalışmaz. Bire bir ilişkilerde, diğer sınıfa her bir sınıfta başvuru gezintisi özelliği vardır. İlişki kurmak için, [ForeignKey özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) bağımlı sınıfa uygulanabilir. [Yabancıanahtar özniteliğini](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)atlarsanız, geçişi oluşturmaya çalıştığınızda şu hatayı alırsınız:

*' ContosoUniversity. modeller. OfficeAssignment ' ve ' ContosoUniversity. modeller. eğitmen ' türleri arasındaki bir ilişkinin asıl ucu belirlenemiyor. Bu ilişkinin asıl sonu, ilişki Fluent API veya veri ek açıklamaları kullanılarak açıkça yapılandırılmalıdır.*

Öğreticide daha sonra bu ilişkiyi Fluent API ile nasıl yapılandıracağınızı öğreneceksiniz.

### <a name="the-instructor-navigation-property"></a>Eğitmen gezintisi özelliği

`Instructor` varlık null yapılabilir bir `OfficeAssignment` gezinti özelliğine sahiptir (bir eğitmenin bir Office ataması olmayabilir) ve `OfficeAssignment` varlık null atanamaz bir `Instructor` gezinti özelliğine sahiptir (bir Office ataması bir eğitmen olmadan mevcut olamaz--`InstructorID` null değer atanamaz). `Instructor` bir varlık ilişkili bir `OfficeAssignment` varlığına sahip olduğunda, her varlığın gezinti özelliğinde diğer birine bir başvurusu olur.

İlgili bir eğitmen olması gerektiğini belirtmek için, eğitmen gezinti özelliğine bir `[Required]` özniteliği koyabilirsiniz, ancak bunu yapmanız gerekmez çünkü bu, Komutctorıd yabancı anahtarı (aynı zamanda bu tabloya yönelik anahtar) null değer atanamaz.

## <a name="modify-the-course-entity"></a>Kurs varlığını değiştirme

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

## <a name="create-the-department-entity"></a>Departman varlığı oluşturma

Aşağıdaki kodla *Models\Department.cs* oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Column özniteliği

Daha önce sütun adı eşlemesini değiştirmek için [Column özniteliğini](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) kullandınız. `Department` varlığının kodunda, sütunun veritabanındaki SQL Server [para](https://msdn.microsoft.com/library/ms179882.aspx) türü kullanılarak TANıMLANMASı için SQL veri türü eşlemesini değiştirmek üzere `Column` özniteliği kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Entity Framework genellikle özellik için tanımladığınız CLR türüne göre uygun SQL Server veri türünü seçtiği için sütun eşlemesi genellikle gerekli değildir. CLR `decimal` türü bir SQL Server `decimal` türüne eşlenir. Ancak bu durumda, sütunun para birimi tutarlarını tutuını ve [para](https://msdn.microsoft.com/library/ms179882.aspx) veri türü bunun için daha uygun olduğunu bilirsiniz. CLR veri türleri ve bunların SQL Server veri türleriyle nasıl eşleştiği hakkında daha fazla bilgi için bkz. [Entity FrameworkTypes Için SqlClient](https://msdn.microsoft.com/library/bb896344.aspx).

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

Yabancı anahtar ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Bir departman yönetici olabilir veya olmayabilir ve yönetici her zaman bir eğitmendir. Bu nedenle `InstructorID` özelliği, `Instructor` varlığına yabancı anahtar olarak dahil edilir ve özelliği null yapılabilir olarak işaretlemek için `int` tür atamadan sonra bir soru işareti eklenir. Gezinti özelliği `Administrator` olarak adlandırılır ancak bir `Instructor` varlığı tutar:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- Bir departmanın birçok kursu olabilir, bu nedenle `Courses` bir gezinti özelliği vardır:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > Kurala göre Entity Framework, null olamayan yabancı anahtarlar ve çoktan çoğa ilişkiler için art arda silme imkanı sağlar. Bu, bir geçiş eklemeye çalıştığınızda bir özel duruma neden olacak dairesel basamaklı silme kurallarına neden olabilir. Örneğin, `Department.InstructorID` özelliğini null yapılabilir olarak tanımlamadıysanız şu özel durum iletisini alırsınız: "başvurusal ilişki izin verilmeyen bir döngüsel başvuruya neden olur." İş kurallarınızın `InstructorID` özelliğinin null değer atanamaz olması gerekiyorsa, ilişkide basamaklı silmeyi devre dışı bırakmak için aşağıdaki Fluent API ifadesini kullanmanız gerekir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modify-the-enrollment-entity"></a>Kayıt varlığını değiştirme

 *Models\kayıtlarına Ment.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=1,15)]

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

Yabancı anahtar özellikleri ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Kayıt kaydı tek bir kurs için olduğundan `CourseID` yabancı anahtar özelliği ve `Course` gezinti özelliği vardır:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs)]
- Kayıt kaydı tek bir öğrenci içindir, bu nedenle `StudentID` yabancı anahtar özelliği ve `Student` gezinti özelliği vardır:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]

### <a name="many-to-many-relationships"></a>Çoktan çoğa Ilişkiler

`Student` ve `Course` varlıkları arasında çok-çok ilişkisi vardır ve `Enrollment` varlığı, veritabanında *Yük içeren* çoktan çoğa bir JOIN tablosu gibi çalışır. Bu, `Enrollment` tablonun birleştirilmiş tablolar için yabancı anahtarlar (Bu örnekte, birincil anahtar ve bir `Grade` özelliği) yanında ek veriler içerdiği anlamına gelir.

Aşağıdaki çizimde bu ilişkilerin bir varlık diyagramında nasıl göründüğünü gösterilmektedir. (Bu diyagram [Entity Framework güç araçları](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)kullanılarak oluşturulmuştur; diyagramı oluşturma öğreticinin bir parçası değildir, burada yalnızca bir çizim olarak kullanılmaktadır.)

![Öğrenci-Course_many many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

Her ilişki hattının 1 ' de bir sonda ve bir yıldız işareti (\*) vardır ve tek-çok ilişkisini gösterir.

`Enrollment` tablo, sınıf bilgilerini içermiyorsa, yalnızca iki yabancı anahtar `CourseID` ve `StudentID`içermesi gerekir. Bu durumda, veritabanında yük (veya *saf bir JOIN tablosu*) *olmadan* çoktan çoğa bir JOIN tablosuna karşılık gelir ve bir model sınıfı oluşturmanız gerekmez. `Instructor` ve `Course` varlıkların bu tür çok-çok ilişkisi vardır ve görebileceğiniz gibi, aralarında bir varlık sınıfı yoktur:

![Eğitmen-many_relationship Course_many](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Veritabanında bir JOIN tablosu gereklidir, ancak aşağıdaki veritabanı diyagramında gösterildiği gibi:

![Eğitmen-many_relationship_tables Course_many](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

Entity Framework, `CourseInstructor` tabloyu otomatik olarak oluşturur ve `Instructor.Courses` ve `Course.Instructors` gezinti özelliklerini okuyup güncelleştirerek onu dolaylı olarak okuyup güncelleyebilirsiniz.

## <a name="entity-relationship-diagram"></a>Varlık ilişkisi diyagramı

Aşağıdaki çizimde, Entity Framework Power Tools 'un tamamlanmış okul modeli için kullandığı diyagram gösterilmektedir.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

Çoktan çoğa ilişki satırlarından (\*\*) ve bire çok ilişki çizgilerinin yanı sıra (1 ' den \*) burada, `Instructor` ve `OfficeAssignment` varlıkları arasında bire sıfır veya-bir ilişki satırını (1 ila 0.. 1), eğitmen ve departman varlıkları arasında sıfır veya-bire çok ilişki satırını (0.. 1 ' den \*) görüntüleyebilirsiniz.

## <a name="add-code-to-database-context"></a>Veritabanı bağlamına kod ekleme

Ardından, yeni varlıkları `SchoolContext` sınıfına ekleyecek ve [Fluent API](https://msdn.microsoft.com/data/jj591617) çağrılarını kullanarak eşlemenin bazılarını özelleştireceksiniz. Aşağıdaki örnekte olduğu gibi, bir dizi yöntemi çağıran tek bir deyime dizerek kullanıldığından, API "akıcı" olur.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

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

## <a name="seed-database-with-test-data"></a>Test verileriyle çekirdek veritabanı

Yeni oluşturduğunuz varlıklar için çekirdek verileri sağlamak üzere *Migrations\configuration.cs* dosyasındaki kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

İlk öğreticide gördüğünüz gibi, bu kodun çoğu yalnızca yeni varlık nesneleri güncelleştirir veya oluşturur ve test için gereken şekilde, örnek verileri özelliklere yükler. Ancak, `Instructor` varlığıyla çok-çok ilişkisi olan `Course` varlığın nasıl işlendiğini fark edebilirsiniz:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

`Course` nesnesi oluşturduğunuzda, `Instructors` gezinti özelliğini kod `Instructors = new List<Instructor>()`kullanarak boş bir koleksiyon olarak başlatırsınız. Bu, `Instructors.Add` yöntemi kullanılarak bu `Course` ilgili varlık `Instructor` eklemek mümkün hale getirir. Boş bir liste oluşturmadıysanız, `Instructors` özelliği null olduğu ve bir `Add` yöntemine sahip olmadığı için bu ilişkileri ekleyemezsiniz. Ayrıca, oluşturucuya liste başlatmayı da ekleyebilirsiniz.

## <a name="add-a-migration"></a>Geçiş Ekle

PMC 'den `add-migration` komutunu girin (`update-database` komutunu henüz yapmayın):

`add-Migration ComplexDataModel`

`update-database` komutunu bu noktada çalıştırmayı denediyseniz (henüz yapmayın), şu hatayı alırsınız:

*ALTER TABLE ifadesi, "FK\_dbo yabancı anahtar kısıtlaması ile çakışıyor.\_dbo. Departman\_DepartmentID ". "ContosoUniversity" veritabanında, "dbo" tablosunda çakışma oluştu. Bölüm ", sütun ' DepartmentID '.*

Bazı durumlarda, mevcut verilerle geçişleri yürüttüğünüzde, yabancı anahtar kısıtlamalarını karşılamak için saplama verilerini veritabanına eklemeniz ve şimdi yapmanız gerekenler vardır. ComplexDataModel `Up` yöntemi içindeki oluşturulan kod `Course` tabloya null atanamaz `DepartmentID` yabancı anahtar ekler. Kod çalışırken `Course` tablosunda zaten satırlar bulunduğundan, SQL Server null olmayan sütuna hangi değerin yerleştirileceğini bilmediği için `AddColumn` işlemi başarısız olur. Bu nedenle, yeni sütuna varsayılan bir değer vermek için kodu değiştirmesi ve varsayılan departman görevi gören "Temp" adlı bir saplama departmanı oluşturulması gerekir. Sonuç olarak, `Up` yöntemi çalıştıktan sonra var olan `Course` satırları "geçici" departmanıyla ilişkilendirilir. `Seed` yönteminde doğru departmanlarla ilişkilendirebilirsiniz.

&lt;*zaman damgasını&gt;\_ComplexDataModel.cs* dosyasını düzenleyin, DepartmentID sütununu kurs tablosuna ekleyen kod satırını açıklama satırı yapın ve aşağıdaki vurgulanmış kodu ekleyin (açıklamalı çizgi de vurgulanır):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

`Seed` yöntemi çalıştırıldığında, `Department` tabloya satır ekler ve mevcut `Course` satırları bu yeni `Department` satırlarıyla ilişkilendirilecektir. Kullanıcı arabirimine hiçbir kurs eklemediyseniz, bundan sonra artık `Course.DepartmentID` sütununda "geçici" Departmanı veya varsayılan değer gerekmez. Başka birinin uygulamayı kullanarak kurs eklemesine izin vermek için, sütundan varsayılan değeri kaldırmadan ve "geçici" departmanı silmeden önce tüm `Course` satırları (yalnızca `Seed` yönteminin önceki çalıştırmaları tarafından Eklenenler değil) geçerli `DepartmentID` değerlere sahip olduğundan emin olmak için `Seed` yöntemi kodunu da güncellemek isteyebilirsiniz.

## <a name="update-the-database"></a>Veritabanını güncelleştirme

&lt;*zaman damgasını&gt;\_ComplexDataModel.cs* dosyası düzenlemesini tamamladıktan sonra, geçişi yürütmek için PMC 'de `update-database` komutunu girin.

[!code-powershell[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.ps1)]

> [!NOTE]
> Verileri geçirirken ve şema değişiklikleri yaparken başka hatalar almak mümkündür. Çözümleyemez geçiş hataları alırsanız, bağlantı dizesindeki veritabanı adını değiştirebilir veya veritabanını silebilirsiniz. En basit yaklaşım, *Web. config* dosyasındaki veritabanını yeniden adlandırmalıdır. Aşağıdaki örnek,\_test olarak değiştirilen adı gösterir:
>
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample36.xml?highlight=1)]
>
> Yeni bir veritabanı ile geçirilecek veri yoktur ve `update-database` komutunun hatasız tamamlanabilmesi çok daha yüksektir. Veritabanının nasıl silineceği hakkında yönergeler için bkz. [Visual Studio 'dan bir veritabanını bırakma 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).
>
> Bu başarısız olursa, aşağıdaki komutu PMC 'e girerek deneyebileceğiniz başka bir şey veritabanını yeniden başlatmalıdır:
>
> `update-database -TargetMigration:0`

Veritabanını daha önce yaptığınız gibi **Sunucu Gezgini** açın ve tabloların tümünün oluşturulduğunu görmek için **Tables** düğümünü genişletin. (Önceki zamandan hala **Sunucu Gezgini** açıksa **Yenile** düğmesine tıklayın.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image16.png)

`CourseInstructor` tablosu için bir model sınıfı oluşturmadınız. Daha önce açıklandığı gibi, bu, `Instructor` ve `Course` varlıkları arasındaki çoktan çoğa ilişki için bir JOIN tablosudur.

`CourseInstructor` tabloya sağ tıklayıp **tablo verilerini göster** ' i seçerek, `Course.Instructors` gezinti özelliğine eklediğiniz `Instructor` varlıklarının bir sonucu olarak bu verinin içinde veri olduğunu doğrulayın.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image17.png)

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET Data Access-önerilen kaynaklarda](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Veri modeli özelleştirildi
> * Güncelleştirilmiş öğrenci varlığı
> * Eğitmen varlığı oluşturuldu
> * OfficeAssignment varlığı oluşturuldu
> * Kurs varlığını değiştirme
> * Departman varlığı oluşturuldu
> * Kayıt varlığı değiştirildi
> * Kod veritabanı bağlamına eklendi
> * Test verileriyle birlikte sağlanan veritabanı
> * Geçiş eklendi
> * Veritabanı güncelleştirildi

Entity Framework gezinti özelliklerine yüklediği ilgili verileri okumayı ve görüntülemeyi öğrenmek için sonraki makaleye ilerleyin.

> [!div class="nextstepaction"]
> [İlgili verileri okuma](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
