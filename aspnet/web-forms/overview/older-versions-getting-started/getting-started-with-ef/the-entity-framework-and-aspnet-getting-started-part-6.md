---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 6 | ile çalışmaya başlama Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 994a5496-c648-4830-b03c-55bb43f325d2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-6
msc.type: authoredcontent
ms.openlocfilehash: 8bfbe74f90eb03ea9aab7610842ef2578e80d113
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564227"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-6"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms ile çalışmaya başlama-Bölüm 6

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](the-entity-framework-and-aspnet-getting-started-part-1.md) bakın

## <a name="implementing-table-per-hierarchy-inheritance"></a>Tablo başına devralmayı uygulama

Önceki öğreticide, ilişki ekleyerek ve silerek ve var olan bir varlıkla ilişkisi olan yeni bir varlık ekleyerek ilgili verilerle çalıştık. Bu öğretici, veri modelinde devralmayı nasıl uygulayacağınızı gösterir.

Nesne odaklı programlamada, ilgili sınıflarla çalışmayı kolaylaştırmak için devralmayı kullanabilirsiniz. Örneğin, `Person` temel sınıfından türetilen `Instructor` ve `Student` sınıfları oluşturabilirsiniz. Entity Framework varlıklar arasında aynı tür devralma yapılarını oluşturabilirsiniz.

Öğreticinin bu bölümünde yeni Web sayfaları oluşturmayacağız. Bunun yerine, veri modeline türetilmiş varlıklar ekler ve mevcut sayfaları yeni varlıkları kullanacak şekilde değiştirirsiniz.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>Tablo başına hiyerarşi ve tablo başına tür devralma

Bir veritabanı, bir tablodaki veya birden çok tabloda ilgili nesneler hakkında bilgi saklayabilir. Örneğin, `School` veritabanında `Person` tablo, tek bir tabloda hem öğrenciler hem de eğitmenler hakkında bilgiler içerir. Sütunlardan bazıları yalnızca Eğitmenler (`HireDate`), bazıları yalnızca öğrencilerle (`EnrollmentDate`) ve bazıları (`LastName`, `FirstName`) için geçerlidir.

[![image11](the-entity-framework-and-aspnet-getting-started-part-6/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image1.png)

Entity Framework, `Person` varlığından devraldığı `Instructor` ve `Student` varlıkları oluşturacak şekilde yapılandırabilirsiniz. Tek bir veritabanı tablosundan bir varlık devralma yapısı oluşturmanın bu düzeni, *hiyerarşi başına tablo* (TPH) devralma olarak adlandırılır.

Kurslar için `School` veritabanı farklı bir model kullanır. Çevrimiçi kurslar ve yerinde kurslar, her birinin `Course` tablosuna işaret eden bir yabancı anahtarı olan ayrı tablolarda depolanır. Her iki kurs türüyle ortak bilgiler yalnızca `Course` tablosunda depolanır.

[![image12](the-entity-framework-and-aspnet-getting-started-part-6/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image3.png)

Entity Framework veri modelini, `OnlineCourse` ve `OnsiteCourse` varlıkların `Course` varlıktan devralması için yapılandırabilirsiniz. Her tür için ayrı tablolardan bir varlık devralma yapısı oluşturma düzeni, tüm türlere ortak olan verileri depolayan bir tabloya geri başvuran her ayrı tabloyla birlikte *tür başına tablo* (TPT) devralma olarak adlandırılır.

TPH devralma desenleri genellikle TPT devralma desenlerinden daha iyi Entity Framework performans sağlar, çünkü TPT desenleri karmaşık JOIN sorgularına yol açabilir. Bu izlenecek yol, TPH devralmanın nasıl uygulanacağını gösterir. Bunu aşağıdaki adımları gerçekleştirerek gerçekleştirirsiniz:

- `Person`türetilen `Instructor` ve `Student` varlık türleri oluşturun.
- Türetilmiş varlıklara ait özellikleri, `Person` varlığındaki türetilmiş varlıklara taşıyın.
- Türetilmiş türlerdeki özelliklerde kısıtlamalar ayarlayın.
- `Person` varlığını soyut bir varlık yapın.
- Her türetilmiş varlığı `Person` tablosuna eşleyin, bir `Person` satırının bu türetilmiş türü temsil edip etmediğini belirleyen bir koşul.

## <a name="adding-instructor-and-student-entities"></a>Eğitmen ve öğrenci varlıkları ekleme

<em>SchoolModel. edmx</em> dosyasını açın, tasarımcıda dolu olmayan bir alana sağ tıklayın, <strong>Ekle</strong>' yi ve ardından varlık ' ı seçin<em>.</em>

[![image01](the-entity-framework-and-aspnet-getting-started-part-6/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image5.png)

**Varlık Ekle** iletişim kutusunda varlığı `Instructor` adlandırın ve **temel tür** seçeneğini `Person`olarak ayarlayın.

[![image02](the-entity-framework-and-aspnet-getting-started-part-6/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image7.png)

**Tamam**’a tıklayın. Tasarımcı, `Person` varlıktan türetilen bir `Instructor` varlığı oluşturur. Yeni varlık henüz bir özelliğe sahip değil.

[![image03](the-entity-framework-and-aspnet-getting-started-part-6/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image9.png)

`Person`türeten `Student` bir varlık oluşturmak için yordamı tekrarlayın.

Yalnızca Eğitmenler için işe alma tarihleri vardır, bu yüzden bu özelliği `Person` varlığındaki `Instructor` varlığına taşımanız gerekir. `Person` varlıkta, `HireDate` özelliğine sağ tıklayın ve **Kes**' e tıklayın. Sonra `Instructor` varlığındaki **Özellikler** ' e sağ tıklayıp **Yapıştır**' a tıklayın.

[![image04](the-entity-framework-and-aspnet-getting-started-part-6/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image11.png)

`Instructor` varlığının işe alınma tarihi null olamaz. `HireDate` özelliğine sağ tıklayın, **Özellikler**' e tıklayın ve ardından **özellikler** penceresinde `Nullable` `False`olarak değiştirin.

[![image05](the-entity-framework-and-aspnet-getting-started-part-6/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image13.png)

`EnrollmentDate` özelliğini `Person` varlığındaki `Student` varlığına taşımak için yordamı tekrarlayın. `EnrollmentDate` özelliği için `False` `Nullable` de ayarladığınızdan emin olun.

Artık `Person` bir varlık yalnızca `Instructor` ve `Student` varlıkları için ortak olan özelliklere sahip olduğuna göre (taşımakta olduğunuz gezinti özelliklerinden farklı olarak), varlık yalnızca devralma yapısında temel varlık olarak kullanılabilir. Bu nedenle, bunun bağımsız bir varlık olarak değerlendirilmeyeceğinden emin olmanız gerekir. `Person` varlığına sağ tıklayın, **Özellikler**' i seçin ve ardından **Özellikler** penceresinde **abstract** özelliğinin değerini **true**olarak değiştirin.

[![image06](the-entity-framework-and-aspnet-getting-started-part-6/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image15.png)

## <a name="mapping-instructor-and-student-entities-to-the-person-table"></a>Eğitmen ve öğrenci varlıklarını kişi tablosu ile eşleme

Şimdi veritabanındaki `Instructor` ve `Student` varlıkların ayırt edilmesine Entity Framework söylemeniz gerekir.

`Instructor` varlığına sağ tıklayıp **Tablo eşleme**' yi seçin. **Eşleme ayrıntıları** penceresinde **Tablo Ekle veya görüntüle** ' ye tıklayın ve **kişi**' yi seçin.

[![image07](the-entity-framework-and-aspnet-getting-started-part-6/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image17.png)

**Koşul Ekle**' ye tıklayın ve ardından **HireDate**' i seçin.

[![image09](the-entity-framework-and-aspnet-getting-started-part-6/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image19.png)

**İşleci** to ve **Value/Property değerlerini** **null** **olarak değiştirin** .

[![image10](the-entity-framework-and-aspnet-getting-started-part-6/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image21.png)

`EnrollmentDate` sütunu null olmadığında bu varlığın `Person` tabloya eşlendiğini belirterek `Students` varlık için yordamı tekrarlayın. Ardından veri modelini kaydedip kapatın.

Yeni varlıkları sınıf olarak oluşturmak ve tasarımcıda kullanılabilir hale getirmek için projeyi derleyin.

## <a name="using-the-instructor-and-student-entities"></a>Eğitmen ve öğrenci varlıklarını kullanma

Öğrenci ve eğitmen verileriyle çalışan Web sayfalarını oluşturduğunuzda, bunları `Person` varlık kümesine göre filtreleyerek ve döndürülen verileri öğrenciler veya eğitmenler 'e kısıtlamak için `HireDate` veya `EnrollmentDate` özelliğini filtrelürsünüz. Ancak, artık her bir veri kaynağı denetimini `Person` varlık kümesine bağladığınızda, yalnızca `Student` veya `Instructor` varlık türlerinin seçili olması gerektiğini belirtebilirsiniz. Entity Framework, `Person` varlık kümesindeki öğrencileri ve eğitmenleri ayırt etmek için, el ile girdiğiniz `Where` özellik ayarlarını bu şekilde kaldırabilirsiniz.

Visual Studio tasarımcısında, aşağıdaki örnekte gösterildiği gibi, bir `EntityDataSource` denetiminin, `Configure Data Source` sihirbazının **EntityTypeFilter** açılan kutusunda seçmesini gerektiren varlık türünü belirtebilirsiniz.

[![image13](the-entity-framework-and-aspnet-getting-started-part-6/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image23.png)

**Özellikler** penceresinde, aşağıdaki örnekte gösterildiği gibi artık gerekli olmayan `Where` yan tümce değerlerini kaldırabilirsiniz.

[![image14](the-entity-framework-and-aspnet-getting-started-part-6/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image25.png)

Ancak, `EntityDataSource` denetimleri için biçimlendirmeyi `ContextTypeName` özniteliğini kullanacak şekilde değiştirdiğiniz için, zaten oluşturmuş olduğunuz `EntityDataSource` denetimlerinde **veri kaynağı yapılandırma** Sihirbazı 'nı çalıştıramazsınız. Bu nedenle, bunun yerine biçimlendirmeyi değiştirerek gerekli değişiklikleri yaparsınız.

*Öğrenciler. aspx* sayfasını açın. `StudentsEntityDataSource` denetiminde, `Where` özniteliğini kaldırın ve bir `EntityTypeFilter="Student"` özniteliği ekleyin. Biçimlendirme artık aşağıdaki örneğe benzeyecektir:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample1.aspx)]

`EntityTypeFilter` özniteliği ayarlandığında, `EntityDataSource` denetiminin yalnızca belirtilen varlık türünü seçmesini sağlar. Hem `Student` hem de `Instructor` varlık türlerini almak isterseniz, bu özniteliği ayarlayamazsınız. (Yalnızca salt okunurdur veri erişimi için denetim kullanıyorsanız, tek bir `EntityDataSource` denetimiyle birden fazla varlık türü alma seçeneğiniz vardır. Varlıkları eklemek, güncelleştirmek veya silmek için bir `EntityDataSource` denetimi kullanıyorsanız ve bu, bağlandığı varlık kümesi birden çok tür içeriyorsa, yalnızca bir varlık türüyle çalışabilir ve bu özniteliği ayarlamanız gerekir.)

Özelliği tamamen kaldırmak yerine `Student` varlıkları seçen `Where` özniteliğinin yalnızca kısmını kaldır hariç `SearchEntityDataSource` denetimi için yordamı tekrarlayın. Denetimin açılış etiketi artık aşağıdaki örneğe benzeyecektir:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample2.aspx)]

Daha önce olduğu gibi çalıştığını doğrulamak için sayfayı çalıştırın.

[![image15](the-entity-framework-and-aspnet-getting-started-part-6/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image27.png)

Önceki öğreticilerde oluşturduğunuz aşağıdaki sayfaları `Person` varlıklar yerine yeni `Student` ve `Instructor` varlıkları kullanacak şekilde güncelleştirin ve ardından bunları daha önce olduğu gibi çalıştığını doğrulamak için çalıştırın:

- *StudentsAdd. aspx*içinde, `StudentsEntityDataSource` denetimine `EntityTypeFilter="Student"` ekleyin. Biçimlendirme artık aşağıdaki örneğe benzeyecektir: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample3.aspx)]

    [![image16](the-entity-framework-and-aspnet-getting-started-part-6/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image29.png)
- *About. aspx*dosyasında `StudentStatisticsEntityDataSource` denetimine `EntityTypeFilter="Student"` ekleyin ve `Where="it.EnrollmentDate is not null"`kaldırın. Biçimlendirme artık aşağıdaki örneğe benzeyecektir: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample4.aspx)]

    [![image17](the-entity-framework-and-aspnet-getting-started-part-6/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image31.png)
- *Eğitmenler. aspx* ve *Komutctorskurslar. aspx*' de `InstructorsEntityDataSource` denetimine `EntityTypeFilter="Instructor"` ekleyin ve `Where="it.HireDate is not null"`kaldırın. *Eğitmenler. aspx* dosyasındaki biçimlendirme artık aşağıdaki örneğe benzer: 

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample5.aspx)]

    [![image18](the-entity-framework-and-aspnet-getting-started-part-6/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image33.png)

    *Komutctorskurslar. aspx* dosyasındaki biçimlendirme artık aşağıdaki örneğe benzeyecektir:

    [!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-6/samples/sample6.aspx)]

    [![image19](the-entity-framework-and-aspnet-getting-started-part-6/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-6/_static/image35.png)

Bu değişikliklerin sonucu olarak, Contoso Üniversitesi uygulamasının bakımınızın bir kısmını çeşitli yollarla geliştirdiniz. Seçim ve doğrulama mantığını UI katmanından ( *. aspx* Markup) taşımış ve veri erişim katmanının ayrılmaz bir parçası yaptı. Bu, gelecekte veritabanı şeması veya veri modeli için yaptığınız değişikliklerden uygulama kodunuzu yalıtmaya yardımcı olur. Örneğin, öğrenciler öğretmen ' i yardımtı olarak işe alınır ve bu nedenle bir işe alım tarihi alabilir. Ardından öğrencileri Eğitmenler ' den ayırt etmek ve veri modelini güncelleştirmek için yeni bir özellik ekleyebilirsiniz. Öğrenciler için bir işe alma tarihi göstermek istediğiniz durumlar dışında, Web uygulamasında hiçbir kodun değiştirilmesi gerekmez. `Instructor` ve `Student` varlıkların eklenmesinin başka bir avantajı da, kodunuzun gerçekten öğrenci veya eğitmenler olan `Person` nesneler tarafından daha kolay anlaşılamasıdır.

Artık Entity Framework devralma deseninin uygulanması için bir yol gördünüz. Aşağıdaki öğreticide, Entity Framework veritabanına nasıl eriştiği hakkında daha fazla denetime sahip olmak için saklı yordamları nasıl kullanacağınızı öğreneceksiniz.

> [!div class="step-by-step"]
> [Önceki](the-entity-framework-and-aspnet-getting-started-part-5.md)
> [İleri](the-entity-framework-and-aspnet-getting-started-part-7.md)
