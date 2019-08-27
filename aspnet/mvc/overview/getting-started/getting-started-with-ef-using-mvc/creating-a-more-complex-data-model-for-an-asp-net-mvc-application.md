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
ms.sourcegitcommit: aa3c2efd56466fc6bdc387ee01ad6f50a261665b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2019
ms.locfileid: "70021003"
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

Bu bölümde, biçimlendirme, doğrulama ve veritabanı eşleme kurallarını belirten öznitelikleri kullanarak veri modelini nasıl özelleştireceğinizi göreceksiniz. Ardından, aşağıdaki bölümlerde, önceden oluşturduğunuz sınıflara öznitelikler ekleyerek ve modeldeki `School` kalan varlık türleri için yeni sınıflar oluşturarak tüm veri modelini oluşturacaksınız.

### <a name="the-datatype-attribute"></a>DataType özniteliği

Öğrenci kayıt tarihleri için tüm Web sayfaları Şu anda tarihle birlikte görüntülenir, ancak bu alan için tüm önemli bir tarih olması gerekir. Veri ek açıklaması özniteliklerini kullanarak, verileri gösteren her görünümde görüntü biçimini giderecek bir kod değişikliği yapabilirsiniz. Bunun nasıl yapılacağını gösteren bir örnek görmek için, `EnrollmentDate` `Student` sınıfındaki özelliğine bir özniteliği ekleyeceksiniz.

*Models\student.cs* `using` içinde, `DataType` `System.ComponentModel.DataAnnotations` adalanı`DisplayFormat` için bir ifade ekleyin ve aşağıdaki örnekte gösterildiği gibi özelliğeveöznitelikleriniekleyin:`EnrollmentDate`

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample1.cs?highlight=3,12-13)]

[DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, veritabanı iç türünden daha özel bir veri türü belirtmek için kullanılır. Bu durumda, tarihi ve saati değil yalnızca tarihi izlemek istiyoruz. Veri [türü numaralandırması](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) , *Tarih, saat, PhoneNumber, para birimi, emaadresi* ve daha fazlası gibi birçok veri türü sağlar. `DataType` Özniteliği Ayrıca uygulamanın türe özgü özellikleri otomatik olarak sağlamasını da sağlayabilir. Örneğin, `mailto:` [DataType. emaadresi](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx)için bir bağlantı oluşturulabilir ve [HTML5](http://html5.org/)'i destekleyen tarayıcılarda [DataType. Date](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) için bir tarih seçici sağlanmış olabilir. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri HTML 5 tarayıcısının ANLAYABILMESI için HTML 5 [veri](http://ejohn.org/blog/html-5-data-attributes/) (bir *veri Dash*) öznitelikleri yayar. [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) öznitelikleri herhangi bir doğrulama sağlamaz.

`DataType.Date`görüntülenen tarihin biçimini belirtmez. Varsayılan olarak, veri alanı sunucunun [CultureInfo](https://msdn.microsoft.com/library/vstudio/system.globalization.cultureinfo(v=vs.110).aspx)öğesine göre varsayılan biçimlere göre görüntülenir.

`DisplayFormat` Öznitelik, tarih biçimini açıkça belirtmek için kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample2.cs)]

`ApplyFormatInEditMode` Ayar, bir metin kutusunda değer görüntülenmek üzere görüntülendiğinde belirtilen biçimlendirmenin de uygulanacağını belirtir. (Örneğin, para birimi değerleri için, metin kutusundaki para birimi sembolünü, düzenlenebilir bir şekilde istemeyebilirsiniz.)

[DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) özniteliğini kendisi kullanabilirsiniz, ancak aynı zamanda [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliğini de kullanmak iyi bir fikir olabilir. Özniteliği, bir ekranda nasıl işlenirim `DisplayFormat`aksine, verilerin *semantiğini* sunar ve aşağıdaki avantajları sağlar: `DataType`

- Tarayıcı HTML5 özelliklerini etkinleştirebilir (örneğin, bir Takvim denetimini, yerel ayara uygun para birimi sembolünü, e-posta bağlantılarını, bazı istemci tarafı giriş doğrulamasını vb. göstermek için).
- Varsayılan olarak tarayıcı, verileri [yerel ayarınızı](https://msdn.microsoft.com/library/vstudio/wyzd2bce.aspx)temel alarak doğru biçimi kullanarak işleyebilir.
- [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) özniteliği, verileri işlemek için doğru alan şablonunu seçmek üzere MVC 'yi etkinleştirebilir ( [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) dize şablonunu kullanır). Daha fazla bilgi için bkz. atacan Solson 'ın [ASP.NET MVC 2 şablonları](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). (MVC 2 için yazılmış olsa da, bu makale hala ASP.NET MVC 'nin geçerli sürümü için geçerlidir.)

`DataType` Özniteliğini bir tarih alanı ile birlikte kullanıyorsanız, alanın Chrome tarayıcılarında doğru şekilde işlediğinden emin `DisplayFormat` olmak için özniteliği de belirtmeniz gerekir. Daha fazla bilgi için [Bu StackOverflow iş parçacığına](http://stackoverflow.com/questions/12633471/mvc4-datatype-date-editorfor-wont-display-date-value-in-chrome-fine-in-ie)bakın.

MVC 'de diğer tarih biçimlerinin nasıl işleneceği hakkında daha fazla bilgi için [MVC 5 giriş sayfasına gidin: Düzenleme yöntemleri ve düzenleme görünümü](../introduction/examining-the-edit-methods-and-edit-view.md) inceleniyor ve sayfada uluslararası duruma getirme&quot;için &quot;arama yapın.

Öğrenci dizini sayfasını yeniden çalıştırın ve zamanların kayıt tarihleri için artık gösterilmediğine dikkat edin. Aynı değer, `Student` modeli kullanan herhangi bir görünüm için de geçerli olacaktır.

![Students_index_page_with_formatted_date](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image2.png)

### <a name="the-stringlengthattribute"></a>StringLengthAttribute

Ayrıca, öznitelikleri kullanarak veri doğrulama kuralları ve doğrulama hata iletileri de belirtebilirsiniz. [StringLength özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) , veritabanında en fazla uzunluğu ayarlar ve ASP.NET MVC için istemci tarafı ve sunucu tarafı doğrulaması sağlar. Bu öznitelikte en küçük dize uzunluğunu da belirtebilirsiniz, ancak en küçük değerin veritabanı şemasında hiçbir etkisi yoktur.

Kullanıcıların bir ad için 50 ' den fazla karakter girmemesini istediğinizi varsayalım. Bu kısıtlamayı eklemek için aşağıdaki örnekte gösterildiği gibi [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliklerini `LastName` ve `FirstMidName` özelliklerine ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=10,12)]

[StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliği, bir kullanıcının ad için boşluk girmesini engellemez. Girişe kısıtlama uygulamak için [cevap içerisinde RegularExpression](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.regularexpressionattribute.aspx) özniteliğini kullanabilirsiniz. Örneğin aşağıdaki kod, ilk karakterin büyük küçük harf olmasını ve geri kalan karakterlerin alfabetik olmasını gerektirir:

`[RegularExpression(@"^[A-Z]+[a-zA-Z""'\s-]*$")]`

[MaxLength](https://msdn.microsoft.com/library/System.ComponentModel.DataAnnotations.MaxLengthAttribute.aspx) özniteliği, [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) özniteliğinde benzer işlevler sağlar, ancak istemci tarafı doğrulaması sağlamaz.

Uygulamayı çalıştırın ve **öğrenciler** sekmesine tıklayın. Şu hatayı alırsınız:

*' SchoolContext ' bağlamını destekleyen model veritabanı oluşturulduktan sonra değiştirildi. Veritabanını güncelleştirmek için Code First Migrations kullanmayı düşünün ([https://go.microsoft.com/fwlink/?LinkId=238269](https://go.microsoft.com/fwlink/?LinkId=238269)).*

Veritabanı modeli, veritabanı şemasında değişiklik yapılmasını gerektiren bir şekilde değiştirilmiştir ve Entity Framework olduğunu tespit etti. Kullanıcı arabirimini kullanarak veritabanına eklediğiniz herhangi bir veriyi kaybetmeden Şemayı güncelleştirmek için geçişleri kullanacaksınız. `Seed` Yöntemi tarafından oluşturulan verileri değiştirdiyseniz, `Seed` yönteminde kullandığınız [AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) yöntemi nedeniyle bu, özgün durumuna geri dönüştürülür. ([AddOrUpdate](https://msdn.microsoft.com/library/hh846520(v=vs.103).aspx) , veritabanı terminolojisindeki bir "upsert" işlem ile eşdeğerdir.)

Paket Yöneticisi konsolunda (PMC) aşağıdaki komutları girin:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample4.cmd)]

Komut zaman  *&lt;damgasıMaxLengthOnNames.cs\_adlıbir dosya oluşturur.&gt;* `add-migration` Bu dosya, geçerli veri modeliyle `Up` eşleşecek şekilde veritabanını güncelleştirecek yöntemdeki kodu içerir. `update-database` Komut bu kodu çalıştırdı.

Geçişleri sıralamak için Entity Framework zaman damgası, geçişleri dosya adı tarafından kullanılır. `update-database` Komutu çalıştırmadan önce birden çok geçiş oluşturabilirsiniz ve sonra tüm geçişler oluşturuldukları sırada uygulanır.

**Oluştur** sayfasını çalıştırın ve 50 karakterden daha uzun bir ad girin. **Oluştur**' a tıkladığınızda, istemci tarafı doğrulaması bir hata iletisi gösterir: *LastName alanı, en fazla 50 uzunluğunda bir dize olmalıdır.*

### <a name="the-column-attribute"></a>Column özniteliği

Ayrıca, sınıflarınızın ve özelliklerinin veritabanına nasıl eşlenildiğini denetlemek için özniteliklerini de kullanabilirsiniz. Alan aynı zamanda bir orta ad `FirstMidName` içerebileceğinden, birinci ad alanı için adı kullandığınızı varsayalım. Ancak veritabanına karşı geçici sorgular yazmayacak olan kullanıcılar `FirstName`bu ada alışkın olduğundan, veritabanı sütununun adlandırılmak istiyorsunuz. Bu eşlemeyi yapmak için `Column` özniteliğini kullanabilirsiniz.

Özniteliği veritabanı oluşturulduğunda `FirstMidName` , özelliği ile eşlenen `Student` tablonun sütununun adlandırılacağını `FirstName`belirtir. `Column` Diğer bir deyişle, kodunuz öğesine `Student.FirstMidName`başvurduğunda, veriler `Student` tablonun `FirstName` sütununda gelir veya güncelleştirilir. Sütun adları belirtmezseniz, bunlar Özellik adı ile aynı ada atanır.

*Student.cs* dosyasında, `using` [System. ComponentModel. dataaçıklamalarda. Schema](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.aspx) için bir ifade ekleyin ve aşağıdaki vurgulanmış kodda gösterildiği gibi, `FirstMidName` özelliğine sütun adı özniteliğini ekleyin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample5.cs?highlight=4,14)]

[Sütun özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) ekleme modeli, SchoolContext 'yi yedekleyen şekilde değiştirir, bu nedenle veritabanıyla eşleşmez. Başka bir geçiş oluşturmak için PMC 'de aşağıdaki komutları girin:

[!code-console[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample6.cmd)]

**Sunucu Gezgini**, öğrenci tablosuna çift tıklayarak *öğrenci* tablosu tasarımcısını açın.

Aşağıdaki görüntüde, ilk iki geçişi uygulamadan önce olduğu gibi özgün sütun adı gösterilmektedir. ' Den `FirstMidName` ' a değiştirme sütun adının yanı sıra, iki `MAX` Ad sütununun uzunluğu 50 karakter olarak değiştirilmiştir. `FirstName`

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image5.png)

Ayrıca, bu öğreticide daha sonra göreceğiniz gibi, [AKıCı API](https://msdn.microsoft.com/data/jj591617)kullanarak veritabanı eşleme değişiklikleri yapabilirsiniz.

> [!NOTE]
> Aşağıdaki bölümlerde tüm varlık sınıflarını oluşturmayı bitirmeden önce derlemeyi denerseniz Derleyici hataları alabilirsiniz.

## <a name="update-student-entity"></a>Öğrenci varlığını Güncelleştir

*Models\student.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=11,13,15,18,22,25-32)]

### <a name="the-required-attribute"></a>Gerekli öznitelik

[Gerekli öznitelik](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) , ad özellikleri gereken alanları sağlar. `Required attribute` DateTime, int, Double ve float gibi değer türleri için gerekli değildir. Değer türlerine null değer atanamaz, bu nedenle bunlar doğal olarak gerekli alanlar olarak kabul edilir. 

Özniteliğinin zorlanmak üzere ile birlikte `MinimumLength` `MinimumLength` kullanılması gerekir. `Required`

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample8.cs?highlight=2)]

`MinimumLength`ve `Required` doğrulamanın doğrulanmasını karşılamamak için boşluk. Dize üzerinde tam denetimi için özniteliğikullanın.`RegularExpression`

### <a name="the-display-attribute"></a>Display özniteliği

`Display` Öznitelik, metin kutularının açıklamalı alt yazısının her örnekteki Özellik adı yerine "ilk ad", "soyadı", "tam ad" ve "kayıt tarihi" olması gerektiğini belirtir (kelimeleri hiçbir alan içermez).

### <a name="the-fullname-calculated-property"></a>FullName hesaplanmış özelliği

`FullName`, iki diğer özelliğin bitiştirerek oluşturulmuş bir değer döndüren hesaplanmış bir özelliktir. Bu nedenle, yalnızca bir `get` erişimcisi vardır ve veritabanında `FullName` hiçbir sütun oluşturulmaz.

## <a name="create-instructor-entity"></a>Eğitmen varlığı oluşturma

Şablon kodunu aşağıdaki kodla değiştirerek *Models\komutctor.cs*oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample9.cs)]

Çeşitli özelliklerin `Student` ve `Instructor` varlıklarında aynı olduğuna dikkat edin. Devralma öğreticisini bu serinin ilerleyen kısımlarında [uyguladığınızda](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md) , artıklığı ortadan kaldırmak için bu kodu yeniden düzenlemelisiniz.

Birden çok özniteliği tek bir satıra koyabilirsiniz. bu nedenle, aşağıdaki gibi eğitmen sınıfını da yazabilirsiniz:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

### <a name="the-courses-and-officeassignment-navigation-properties"></a>Kurslar ve OfficeAssignment gezinti özellikleri

`Courses` Ve`OfficeAssignment` özellikleri gezinti özellikleridir. Daha önce açıklandığı gibi, [yavaş yükleme](https://msdn.microsoft.com/magazine/hh205756.aspx)adlı bir Entity Framework özelliğinden yararlanabilmeleri için genellikle [sanal](https://msdn.microsoft.com/library/9fkccyh4(v=vs.110).aspx) olarak tanımlanır. Ayrıca, bir gezinti özelliği birden çok varlık tulıyorsa, türünün [ICollection&lt;T&gt; ](https://msdn.microsoft.com/library/92t2ye13.aspx) arabirimini uygulaması gerekir. Örneğin, [&lt;IList&gt; ](https://msdn.microsoft.com/library/5y536ey6.aspx) , [Add](https://msdn.microsoft.com/library/63ywd54z.aspx)uygulamadığı [&lt;&gt; ](https://msdn.microsoft.com/library/9eekhta0.aspx) içinIEnumerabletolaraknitelendirirancakyok`IEnumerable<T>` .

Bir eğitmen herhangi bir sayıda kurs öğretebilir, bu `Courses` nedenle bir `Course` varlık koleksiyonu olarak tanımlanmıştır.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

İş kurallarımızda bir eğitmenin yalnızca en fazla bir ofisi olabilir, bu `OfficeAssignment` `null` nedenle tek `OfficeAssignment` bir varlık olarak tanımlanır (hiçbir Office atanmadığında olabilir).

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

## <a name="create-officeassignment-entity"></a>OfficeAssignment varlığı oluştur

Aşağıdaki kodla *Models\officeassignment.cs* oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

Değişikliklerinizi kaydeden ve derleyicinin yakalayabileceği herhangi bir kopyalama ve yapıştırma hatası yapmadığınızı doğrulayan projeyi derleyin.

### <a name="the-key-attribute"></a>Anahtar özniteliği

`Instructor` Ve varlıklarıarasındabiresıfırveyaarasındabirilişkivardır.`OfficeAssignment` Bir Office ataması, atandığı eğitmenle ilişkili olarak yalnızca birincil anahtarı `Instructor` varlığa ait yabancı anahtarıdır. Ancak Entity Framework `InstructorID` , adı `ID` ya da *ClassName* `ID` adlandırma kuralına uymadığından, bu varlığın birincil anahtarı olarak otomatik olarak tanıyamaz. Bu nedenle, `Key` özniteliği anahtar olarak tanımlamak için kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample14.cs)]

Varlık kendi birincil anahtarına sahip `Key` olsa da, özelliği veya `ID`' den `classnameID` farklı bir şekilde adlandırmak istiyorsanız özniteliğini de kullanabilirsiniz. Varsayılan olarak, sütun bir tanımlayıcı ilişki için olduğu için, bu anahtarı, anahtarı veritabanı olmayan üretilmiş olarak değerlendirir.

### <a name="the-foreignkey-attribute"></a>ForeignKey özniteliği

Bire sıfır veya-tek bir ilişki ya da iki varlık arasında bire bir ilişki olduğunda (örneğin, ve `OfficeAssignment` `Instructor`arasında), EF ilişkinin ne kadar sona düğüne ve hangisinin bağımlı olduğunu bir şekilde çalışmaz. Bire bir ilişkilerde, diğer sınıfa her bir sınıfta başvuru gezintisi özelliği vardır. İlişki kurmak için, [ForeignKey özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx) bağımlı sınıfa uygulanabilir. [Yabancıanahtar özniteliğini](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.foreignkeyattribute.aspx)atlarsanız, geçişi oluşturmaya çalıştığınızda şu hatayı alırsınız:

*' ContosoUniversity. modeller. OfficeAssignment ' ve ' ContosoUniversity. modeller. eğitmen ' türleri arasındaki bir ilişkinin asıl ucu belirlenemiyor. Bu ilişkinin asıl sonu, ilişki Fluent API veya veri ek açıklamaları kullanılarak açıkça yapılandırılmalıdır.*

Öğreticide daha sonra bu ilişkiyi Fluent API ile nasıl yapılandıracağınızı öğreneceksiniz.

### <a name="the-instructor-navigation-property"></a>Eğitmen gezintisi özelliği

Varlık null yapılabilir `OfficeAssignment` bir gezinti özelliğine sahiptir (bir eğitmenin bir Office `OfficeAssignment` ataması olmayabilir) ve varlık null yapılamayan `Instructor` bir gezinti özelliğine sahiptir (bir Office ataması `Instructor` bir eğitmen olmadan var-- `InstructorID` null değer atanamaz). Bir `Instructor` varlık ilişkili `OfficeAssignment` bir varlığa sahip olduğunda, her varlığın gezinti özelliğinde diğer birine bir başvurusu olacaktır.

İlgili bir eğitmen olması `[Required]` gerektiğini belirtmek için, eğitmen gezinti özelliğine bir öznitelik koyabilirsiniz, ancak bunu yapmak zorunda kalmazsınız çünkü bu, komutctorıd yabancı anahtarı (aynı zamanda bu tabloya yönelik anahtar) null değer atanamaz.

## <a name="modify-the-course-entity"></a>Kurs varlığını değiştirme

*Models\course.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

Kurs varlığının, ilgili `DepartmentID` `Department` varlığa işaret eden ve bir `Department` gezinti özelliği olan yabancı anahtar özelliği vardır. Entity Framework, ilgili varlık için bir gezinti özelliği olduğunda, veri modelinize yabancı anahtar özelliği eklemenizi gerektirmez. EF, gerektiğinde veritabanında yabancı anahtarlar otomatik olarak oluşturur. Ancak veri modelinde yabancı anahtar olması, güncelleştirmeleri daha basit ve daha verimli hale getirir. Örneğin, düzenlemek `Department` üzere bir kurs varlığı aktardığınızda varlık null olur, bu nedenle kurs varlığını güncelleştirdiğinizde, önce `Department` varlığı almanız gerekir. Yabancı anahtar özelliği `DepartmentID` veri modeline dahil edildiğinde, güncelleştirmeden önce `Department` varlığı getirme gerekmez.

### <a name="the-databasegenerated-attribute"></a>DatabaseGenerated özniteliği

Özelliğindeki`CourseID` [none](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.110).aspx) parametresi olan [databasegenerated özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute.aspx) , birincil anahtar değerlerinin veritabanı tarafından oluşturulması yerine Kullanıcı tarafından sağlandığını belirtir.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

Varsayılan olarak, Entity Framework birincil anahtar değerlerinin veritabanı tarafından oluşturulduğunu varsayar. Bu, Çoğu senaryoda istediğiniz şeydir. Ancak, varlıklar `Course` için bir departman için 1000 serisi, başka bir departman için 2000 serisi vb. gibi kullanıcı tarafından belirtilen kurs numarasını kullanacaksınız.

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

`Course` Varlıktaki yabancı anahtar özellikleri ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Bir kurs bir departmana atanır, bu nedenle yukarıda bahsedilen nedenlerden dolayı `DepartmentID` bir yabancı anahtar ve `Department` bir gezinti özelliği vardır.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]
- Bir kurs, kayıtlı sayıda öğrenciye sahip olabilir, bu nedenle `Enrollments` gezinti özelliği bir koleksiyondur:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample18.cs)]
- Kurs, birden fazla eğitmen tarafından tada olabilir, bu nedenle `Instructors` gezinti özelliği bir koleksiyon olur:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample19.cs)]

## <a name="create-the-department-entity"></a>Departman varlığı oluşturma

Aşağıdaki kodla *Models\Department.cs* oluşturun:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample20.cs)]

### <a name="the-column-attribute"></a>Column özniteliği

Daha önce sütun adı eşlemesini değiştirmek için [Column özniteliğini](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.columnattribute.aspx) kullandınız. `Department` Varlığın kodunda`Column` , sütunu, veritabanının SQL Server [para](https://msdn.microsoft.com/library/ms179882.aspx) türü kullanılarak tanımlanacak şekilde SQL veri türü eşlemesini değiştirmek için kullanılır:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample21.cs)]

Entity Framework genellikle özellik için tanımladığınız CLR türüne göre uygun SQL Server veri türünü seçtiği için sütun eşlemesi genellikle gerekli değildir. CLR `decimal` türü SQL Server `decimal` bir türe eşlenir. Ancak bu durumda, sütunun para birimi tutarlarını tutuını ve [para](https://msdn.microsoft.com/library/ms179882.aspx) veri türü bunun için daha uygun olduğunu bilirsiniz. CLR veri türleri ve bunların SQL Server veri türleriyle nasıl eşleştiği hakkında daha fazla bilgi için bkz. [Entity FrameworkTypes Için SqlClient](https://msdn.microsoft.com/library/bb896344.aspx).

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

Yabancı anahtar ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Bir departman yönetici olabilir veya olmayabilir ve yönetici her zaman bir eğitmendir. Bu nedenle, `Instructor` `int` özelliği varlığa yabancı anahtar olarak dahil edilir ve özelliği null yapılabilir olarak işaretlemek için tür atamadan sonra bir soru işareti eklenir. `InstructorID` Gezinti özelliği adlandırılır `Administrator` ancak bir `Instructor` varlık barındırır:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample22.cs)]
- Bir departmanın birçok kursu olabilir, bu nedenle bir `Courses` gezinti özelliği vardır:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample23.cs)]

  > [!NOTE]
  > Kurala göre Entity Framework, null olamayan yabancı anahtarlar ve çoktan çoğa ilişkiler için art arda silme imkanı sağlar. Bu, bir geçiş eklemeye çalıştığınızda bir özel duruma neden olacak dairesel basamaklı silme kurallarına neden olabilir. Örneğin, `Department.InstructorID` özelliği null yapılabilir olarak tanımlamadıysanız aşağıdaki özel durum iletisini alırsınız: "Başvurusal ilişki izin verilmeyen bir döngüsel başvuruya neden olacak." İşletmenizde gerekli `InstructorID` özelliği null atanamaz olarak ayarlanırsa, ilişkide basamaklı silmeyi devre dışı bırakmak için aşağıdaki Fluent API ifadesini kullanmanız gerekir:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample24.cs)]

## <a name="modify-the-enrollment-entity"></a>Kayıt varlığını değiştirme

 *Models\kayıtlarına Ment.cs*içinde, daha önce eklediğiniz kodu aşağıdaki kodla değiştirin

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample25.cs?highlight=1,15)]

### <a name="foreign-key-and-navigation-properties"></a>Yabancı anahtar ve gezinti özellikleri

Yabancı anahtar özellikleri ve gezinti özellikleri aşağıdaki ilişkileri yansıtır:

- Kayıt kaydı tek bir kurs için olduğundan, `CourseID` yabancı anahtar özelliği ve bir `Course` gezinti özelliği vardır:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample26.cs)]
- Kayıt kaydı tek bir öğrenci içindir, bu nedenle bir `StudentID` yabancı anahtar özelliği ve bir `Student` gezinti özelliği vardır:

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample27.cs)]

### <a name="many-to-many-relationships"></a>Çoktan çoğa Ilişkiler

`Student` `Enrollment` Ve varlıkları`Course` arasında çok-çok ilişkisi vardır ve varlık, veritabanında *Yük ile* çoktan çoğa bir JOIN tablosu gibi çalışır. Bu, `Enrollment` tablonun birleştirilmiş tablolar için yabancı anahtarlar (Bu örnekte, birincil anahtar ve bir `Grade` özellik) gibi ek veriler içerdiği anlamına gelir.

Aşağıdaki çizimde bu ilişkilerin bir varlık diyagramında nasıl göründüğünü gösterilmektedir. (Bu diyagram [Entity Framework güç araçları](https://visualstudiogallery.msdn.microsoft.com/72a60b14-1581-4b9b-89f2-846072eff19d)kullanılarak oluşturulmuştur; diyagramı oluşturma öğreticinin bir parçası değildir, burada yalnızca bir çizim olarak kullanılmaktadır.)

![Öğrenci-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image12.png)

Her ilişki satırında 1 bir sonda ve diğeri de bir yıldız işareti (\*) vardır ve bir-çok ilişkisini gösterir.

Tablo, sınıf bilgileri içermiyorsa, yalnızca iki yabancı anahtar `CourseID` ve `StudentID`içermelidir. `Enrollment` Bu durumda, veritabanında yük (veya *saf bir JOIN tablosu*) *olmadan* çoktan çoğa bir JOIN tablosuna karşılık gelir ve bir model sınıfı oluşturmanız gerekmez. `Instructor` Ve`Course` varlıklarının bu tür çok-çok ilişkisi vardır ve görebileceğiniz gibi, aralarında bir varlık sınıfı yoktur:

![Eğitmen-Course_many-to-many_relationship](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image13.png)

Veritabanında bir JOIN tablosu gereklidir, ancak aşağıdaki veritabanı diyagramında gösterildiği gibi:

![Eğitmen-Course_many-to-many_relationship_tables](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image14.png)

Entity Framework `CourseInstructor` tabloyu otomatik olarak oluşturur ve `Instructor.Courses` ve `Course.Instructors` gezinti özelliklerini okuyup güncelleştirerek onu dolaylı olarak okuyup güncelleştirebilirsiniz.

## <a name="entity-relationship-diagram"></a>Varlık ilişkisi diyagramı

Aşağıdaki çizimde, Entity Framework Power Tools 'un tamamlanmış okul modeli için kullandığı diyagram gösterilmektedir.

![School_data_model_diagram](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image1.png)

Çoktan çoğa ilişki çizgilerinin (\* to \*) ve bire çok ilişki çizgilerinin (1 ile \*) yanı sıra, burada, `Instructor` ve `OfficeAssignment` arasında bire bir veya-bir ilişki satırını (1 ile 0.. 1) görebilirsiniz eğitmen ve departman varlıkları arasındaki varlıklar ve sıfır veya bire çok ilişki satırı (0.. 1 \*' den fazla).

## <a name="add-code-to-database-context"></a>Veritabanı bağlamına kod ekleme

Ardından, yeni varlıkları `SchoolContext` sınıfa ekleyecek ve [Fluent API](https://msdn.microsoft.com/data/jj591617) çağrılarını kullanarak eşlemenin bazılarını özelleştireceksiniz. Aşağıdaki örnekte olduğu gibi, bir dizi yöntemi çağıran tek bir deyime dizerek kullanıldığından, API "akıcı" olur.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample28.cs)]

Bu öğreticide, yalnızca özniteliklerle yapacağımız veritabanı eşlemesi için Fluent API kullanacaksınız. Ancak, özniteliklerini kullanarak yapabileceğiniz biçimlendirme, doğrulama ve eşleme kurallarının çoğunu belirtmek için Fluent API de kullanabilirsiniz. Gibi bazı öznitelikler `MinimumLength` Fluent API uygulanamaz. Daha önce belirtildiği gibi `MinimumLength` , şemayı değiştirmez, yalnızca bir istemci ve sunucu tarafı doğrulama kuralı uygular

Bazı geliştiriciler, varlık sınıflarının "temiz" olmasını sağlamak için Fluent API özel olarak kullanmayı tercih eder. İsterseniz öznitelikleri ve Fluent API karıştırabilir ve yalnızca Fluent API kullanılarak gerçekleştirilebilecek bazı özelleştirmeler de vardır ancak genel olarak önerilen uygulama, bu iki yaklaşımdan birini seçmek ve bunları mümkün olduğunca tutarlı bir şekilde kullanmaktır.

Yeni varlıkları veri modeline eklemek ve öznitelikleri kullanarak gerçekleştirmediğiniz veritabanı eşlemesini gerçekleştirmek için *DAL\SchoolContext.cs* içindeki kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample29.cs)]

[Onmodeloluþturma](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) yöntemindeki yeni ifade, çoktan çoğa JOIN tablosunu yapılandırır:

- `Instructor` Ve`Course` varlıkları arasındaki çoktan çoğa ilişki için, kod, JOIN tablosunun tablo ve sütun adlarını belirtir. Code First, bu kod olmadan çoktan çoğa ilişkiyi yapılandırabilir, ancak bunu çağırmazsanız, `InstructorInstructorID` `InstructorID` sütun için gibi varsayılan adlar alacaksınız.

    [!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample30.cs)]

Aşağıdaki kod, `Instructor` ve `OfficeAssignment` varlıkları arasındaki ilişkiyi belirtmek için öznitelikleri yerine Fluent API nasıl kullanabileceğinizi gösteren bir örnek sağlar:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample31.cs)]

Arka planda hangi "Fluent API" deyimlerinin bulunduğu hakkında bilgi için bkz. [Floent API](https://blogs.msdn.com/b/aspnetue/archive/2011/05/04/entity-framework-code-first-tutorial-supplement-what-is-going-on-in-a-fluent-api-call.aspx) blog gönderisi.

## <a name="seed-database-with-test-data"></a>Test verileriyle çekirdek veritabanı

Yeni oluşturduğunuz varlıklar için çekirdek verileri sağlamak üzere *Migrations\configuration.cs* dosyasındaki kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample32.cs)]

İlk öğreticide gördüğünüz gibi, bu kodun çoğu yalnızca yeni varlık nesneleri güncelleştirir veya oluşturur ve test için gereken şekilde, örnek verileri özelliklere yükler. Bununla birlikte, `Instructor` varlıkla çok `Course` -çok ilişkisi olan varlığın nasıl işlendiğini fark edebilirsiniz:

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample33.cs)]

Bir `Course` nesne oluşturduğunuzda, kodu `Instructors = new List<Instructor>()`kullanarak `Instructors` gezinti özelliğini boş bir koleksiyon olarak başlatırsınız. Bu, `Instructor` `Course` yöntemi kullanılarakbukonuylailgilivarlıklarıneklenmesinimümkünkılar.`Instructors.Add` Boş bir liste oluşturmadıysanız, `Instructors` özellik null olduğu ve bir `Add` yöntemi olmadığı için bu ilişkileri ekleyemezsiniz. Ayrıca, oluşturucuya liste başlatmayı da ekleyebilirsiniz.

## <a name="add-a-migration"></a>Geçiş Ekle

PMC 'den `add-migration` komutunu girin ( `update-database` komutu henüz yapmayın):

`add-Migration ComplexDataModel`

`update-database` Komutu bu noktada çalıştırmayı denediyseniz (henüz yapmayın), şu hatayı alırsınız:

*ALTER table ifadesi, "FK\_dbo" yabancı anahtar kısıtlaması ile çakışıyor. Kurs\_dbo 'su. Bölüm\_DepartmentID ". "ContosoUniversity" veritabanında, "dbo" tablosunda çakışma oluştu. Bölüm ", sütun ' DepartmentID '.*

Bazı durumlarda, mevcut verilerle geçişleri yürüttüğünüzde, yabancı anahtar kısıtlamalarını karşılamak için saplama verilerini veritabanına eklemeniz ve şimdi yapmanız gerekenler vardır. Complexdatamodel `Up` yönteminde oluşturulan kod, `Course` tabloya null yapılamayan `DepartmentID` yabancı bir anahtar ekler. Kod çalıştırıldığı sırada `Course` tabloda daha fazla satır bulunduğundan, SQL Server null olmayan sütuna hangi `AddColumn` değerin yerleştirileceğini bilmediği için işlem başarısız olur. Bu nedenle, yeni sütuna varsayılan bir değer vermek için kodu değiştirmesi ve varsayılan departman görevi gören "Temp" adlı bir saplama departmanı oluşturulması gerekir. Sonuç olarak, mevcut `Course` satırların tümü "geçici" departmanla ilişkili olur ve `Up` Yöntem çalıştıktan sonra. Bunları `Seed` yöntemdeki doğru departmanlarla ilişkilendirebilirsiniz.

&lt; *Zamandamgası\_ComplexDataModel.cs dosyasını düzenleyin, DepartmentID sütununu kurs tablosuna ekleyen kod satırını açıklama satırı yapın ve aşağıdaki vurgulanmış kodu ekleyin (açıklamalı satır da&gt;* vurgulanmış):

[!code-csharp[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample34.cs?highlight=14-18)]

Yöntem çalıştığında, `Department` tabloya satır ekler ve mevcut `Course` satırları bu yeni `Department` satırlarla ilişkilendirir. `Seed` Kullanıcı arabirimine hiçbir kurs eklemediyseniz, bundan sonra "geçici" Departmanı veya `Course.DepartmentID` sütunda varsayılan değer gerekmez. Birisi uygulamayı kullanarak kurs ekleme olasılığa izin vermek için, tüm `Seed` `Course` satırların (yalnızca daha önce bir `Seed` önceki çalıştırılanlara yerleştirilenler) sahip olduğundan emin olmak üzere Yöntem kodunu da güncellemek isteyeceksiniz. sütundan `DepartmentID` varsayılan değeri kaldırmadan önce geçerli değerler ve "geçici" departmanı silmelisiniz.

## <a name="update-the-database"></a>Veritabanını güncelleştirme

&lt; `update-database` *Zamandamgası\_ComplexDataModel.cs dosyasını düzenlemesini tamamladıktan sonra, geçişi yürütmek için PMC 'de komutunu girin.&gt;*

[!code-powershell[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample35.ps1)]

> [!NOTE]
> Verileri geçirirken ve şema değişiklikleri yaparken başka hatalar almak mümkündür. Çözümleyemez geçiş hataları alırsanız, bağlantı dizesindeki veritabanı adını değiştirebilir veya veritabanını silebilirsiniz. En basit yaklaşım, *Web. config* dosyasındaki veritabanını yeniden adlandırmalıdır. Aşağıdaki örnek, cu\_testi olarak değiştirilen adı gösterir:
>
> [!code-xml[Main](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/samples/sample36.xml?highlight=1)]
>
> Yeni bir veritabanı ile geçirilecek veri yoktur ve `update-database` komutun hatasız tamamlanabilmesi çok daha yüksektir. Veritabanının nasıl silineceği hakkında yönergeler için bkz. [Visual Studio 'dan bir veritabanını bırakma 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/).
>
> Bu başarısız olursa, aşağıdaki komutu PMC 'e girerek deneyebileceğiniz başka bir şey veritabanını yeniden başlatmalıdır:
>
> `update-database -TargetMigration:0`

Veritabanını daha önce yaptığınız gibi **Sunucu Gezgini** açın ve tabloların tümünün oluşturulduğunu görmek için **Tables** düğümünü genişletin. (Önceki zamandan hala **Sunucu Gezgini** açıksa **Yenile** düğmesine tıklayın.)

![](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image16.png)

`CourseInstructor` Tablo için bir model sınıfı oluşturmadınız. Daha önce açıklandığı gibi, `Instructor` ve `Course` varlıkları arasındaki çoktan çoğa ilişki için bir JOIN tablosudur.

`CourseInstructor` Tabloya sağ tıklayıp **tablo verilerini göster** ' i seçerek `Instructor` `Course.Instructors` gezinti özelliğine eklediğiniz varlıkların bir sonucu olarak bu verilerin içinde veri olduğunu doğrulayın.

![Table_data_in_CourseInstructor_table](creating-a-more-complex-data-model-for-an-asp-net-mvc-application/_static/image17.png)

## <a name="get-the-code"></a>Kodu alın

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
