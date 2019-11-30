---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: ASP.NET MVC uygulamasında Entity Framework devralma uygulama (8/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: a5c3feff-5335-4cdd-a97d-f7a8785c2494
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9507cba71b976825257cc9948d54f2651355959d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595314"
---
# <a name="implementing-inheritance-with-the-entity-framework-in-an-aspnet-mvc-application-8-of-10"></a>Bir ASP.NET MVC uygulamasında Entity Framework devralma uygulama (8/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticide eşzamanlılık özel durumları ele alınır. Bu öğretici, veri modelinde devralmayı nasıl uygulayacağınızı gösterir.

Nesne odaklı programlamada, gereksiz kodu kaldırmak için devralmayı kullanabilirsiniz. Bu öğreticide, `Instructor` ve `Student` sınıflarını, hem Eğitmenler hem de öğrenciler için ortak olan `LastName` gibi özellikleri içeren bir `Person` taban sınıftan türetireceğiz olacak şekilde değiştireceksiniz. Herhangi bir Web sayfası eklemez veya değiştirmezsiniz, ancak koddan bazılarını değiştireceksiniz ve bu değişiklikler otomatik olarak veritabanına yansıtılacaktır.

## <a name="table-per-hierarchy-versus-table-per-type-inheritance"></a>Tablo başına hiyerarşi ve tablo başına tür devralma

Nesne odaklı programlamada, ilgili sınıflarla çalışmayı kolaylaştırmak için devralmayı kullanabilirsiniz. Örneğin, `School` veri modelindeki `Instructor` ve `Student` sınıfları, çok sayıda özelliği paylaşır ve bu da gereksiz kod ile sonuçlanır:

![Student_and_Instructor_classes](https://asp.net/media/2578113/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_e7a32f99-8bc4-48ce-aeaf-216a18071a8b.png)

`Instructor` ve `Student` varlıkları tarafından paylaşılan özellikler için gereksiz kodu ortadan kaldırmak istediğinizi varsayalım. Yalnızca bu paylaşılan özellikleri içeren `Person` bir temel sınıf oluşturabilirsiniz, sonra `Instructor` ve `Student` varlıkların aşağıdaki çizimde gösterildiği gibi bu temel sınıftan devralmasını sağlayabilirsiniz:

![Student_and_Instructor_classes_deriving_from_Person_class](https://asp.net/media/2578119/Windows-Live-Writer_58f5a93579b2_CC7B_Student_and_Instructor_classes_deriving_from_Person_class_671d708c-cbb8-454a-a8f8-c2d99439acd9.png)

Bu devralma yapısının veritabanında temsil edilebilmesi için birkaç yol vardır. Tek bir tabloda hem öğrenciler hem de eğitmenler hakkında bilgi içeren bir `Person` tablonuz olabilir. Bazı sütunlar yalnızca Eğitmenler (`HireDate`), bazıları yalnızca öğrencilerle (`EnrollmentDate`), bazıları ise (`LastName`, `FirstName`) uygulanabilir. Genellikle, her bir satırın temsil ettiği türü belirtmek için bir *ayrıştırıcı* sütunu vardır. Örneğin, ayrıştırıcı sütununda, Eğitmenler için "eğitmen" ve öğrenciler için "öğrenci" bulunabilir.

![Hierarchy_example başına tablo](https://asp.net/media/2578125/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-hierarchy_example_244067cd-b451-4e9b-9595-793b9afca505.png)

Tek bir veritabanı tablosundan bir varlık devralma yapısı oluşturmanın bu düzeni, *hiyerarşi başına tablo* (TPH) devralma olarak adlandırılır.

Alternatif olarak, veritabanının devralma yapısına benzer bir şekilde görünmesini sağlayabilirsiniz. Örneğin, `Person` tablosunda yalnızca ad alanları olabilir ve Tarih alanlarıyla ayrı `Instructor` ve `Student` tabloları vardır.

![Type_inheritance başına tablo](https://asp.net/media/2578131/Windows-Live-Writer_58f5a93579b2_CC7B_Table-per-type_inheritance.png)

Her varlık sınıfı için bir veritabanı tablosu yapmanın bu düzeni, *tür başına tablo* (TPT) devralma olarak adlandırılır.

TPH devralma desenleri genellikle TPT devralma desenlerinden daha iyi Entity Framework performans sağlar, çünkü TPT desenleri karmaşık JOIN sorgularına yol açabilir. Bu öğreticide, TPH devralmanın nasıl uygulanacağı gösterilmektedir. Bunu aşağıdaki adımları gerçekleştirerek gerçekleştirirsiniz:

- `Person` sınıf oluşturun ve `Person`türetmede `Instructor` ve `Student` sınıfları değiştirin.
- Veritabanı bağlamı sınıfına modelden veritabanına eşleme kodu ekleyin.
- Proje genelinde `InstructorID` ve `StudentID` başvurularını `PersonID`olarak değiştirin.

## <a name="creating-the-person-class"></a>Kişi sınıfı oluşturma

 Note: Bu sınıfları kullanan denetleyicileri güncelleştirene kadar, aşağıdaki sınıfları oluşturduktan sonra projeyi derleyemeyeceksiniz. 

*Modeller* klasöründe *Person.cs* oluşturun ve şablon kodunu şu kodla değiştirin:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

*Instructor.cs*' de, `Instructor` sınıfını `Person` sınıfından türetirsiniz ve anahtar ve ad alanlarını kaldırın. Kod aşağıdaki örneğe benzer şekilde görünür:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

*Student.cs*'de benzer değişiklikler yapın. `Student` sınıfı aşağıdaki örneğe benzer şekilde görünür:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="adding-the-person-entity-type-to-the-model"></a>Kişi varlık türü modele ekleniyor

*SchoolContext.cs*' de, `Person` varlık türü için bir `DbSet` özelliği ekleyin:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Bu, Entity Framework hiyerarşinin devralma devralınmasını yapılandırmak için gereklidir. Gördüğünüz gibi, veritabanı yeniden oluşturulduğunda, `Student` ve `Instructor` tablolarının yerine bir `Person` tablosu olacaktır.

## <a name="changing-instructorid-and-studentid-to-personid"></a>Komutctorıd ve StudentID ile PersonID arasında değişiklik

*SchoolContext.cs*' de, eğitmen-kurs eşleme bildiriminde `MapRightKey("InstructorID")` `MapRightKey("PersonID")`olarak değiştirin:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=4)]

Bu değişiklik gerekli değildir; yalnızca çok-çok birleşme tablosundaki Komutctorıd sütununun adını değiştirir. Adı Komutctorıd olarak bıraktıysanız, uygulama yine de doğru şekilde çalışır. Tamamlanan *SchoolContext.cs*şunlardır:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=15,24)]

Daha sonra, *geçişler* klasöründeki zaman damgalı geçişler dosyaları ***hariç*** `InstructorID` `PersonID` ve proje genelinde `PersonID` `StudentID` değiştirmeniz gerekir. Bunu yapmak için yalnızca değiştirilmesi gereken dosyaları bulup açarak açılan dosyalarda genel bir değişiklik yapmanız gerekir. *Geçiş* klasörünüzdeki tek dosya *Migrations\configuration.exe* ' dir.

1. > [!IMPORTANT]
   > Visual Studio 'daki tüm açık dosyaları kapatarak başlayın.
2. Bul ve Değiştir ' e tıklayın, **Düzenle** menüsünde **tüm dosyaları bul** ' u ve ardından projede `InstructorID`içeren tüm dosyaları ara ' yı tıklatın.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. Her dosya için bir satıra çift tıklayarak *geçişler* klasöründeki &lt;zaman damgası&gt; *\_. cs* geçiş dosyaları ***dışında*** her bir dosyayı açın.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)
4. **Dosyaları değiştir** iletişim kutusunu açın ve **açık belgelerin tümünde** **görünümü** değiştirin.
5. Tüm `InstructorID` `PersonID.` olarak değiştirmek için **dosyaları değiştir** iletişim kutusunu kullanın  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)
6. Projedeki `StudentID`içeren tüm dosyaları bulun.
7. Her bir dosya için bir satıra çift tıklayarak *geçişler* klasöründeki &lt;zaman damgası&gt; *\_\*. cs* geçiş dosyaları ***dışında*** her bir dosyayı açın.  
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
8. **Dosyaları değiştir** iletişim kutusunu açın ve **açık belgelerin tümünde** **görünümü** değiştirin.
9. Tüm `StudentID` `PersonID`olacak şekilde değiştirmek için **dosyaları değiştir** iletişim kutusunu kullanın.   
  
    ![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)
10. Projeyi oluşturun.

(Bunun, birincil anahtarları adlandırırken `classnameID` deseninin bir *dezavantajı* olduğunu unutmayın. Sınıf adını önek olmadan PRIMARY Keys ID olarak adlandırdıysanız, şu anda *yeniden adlandırma* gerekmez.)

## <a name="create-and-update-a-migrations-file"></a>Geçiş dosyası oluşturma ve güncelleştirme

Paket Yöneticisi konsolunda (PMC), aşağıdaki komutu girin:

`Add-Migration Inheritance`

PMC 'de `Update-Database` komutunu çalıştırın. Bu noktada, geçiş işlemi nasıl işleneceğini bilmez. Şu hatayı alırsınız:

*ALTER TABLE ifadesi, "FK\_dbo yabancı anahtar kısıtlaması ile çakışıyor. Departman\_dbo. Kişi\_kişisimliği ". "ContosoUniversity" veritabanında, "dbo" tablosunda çakışma oluştu. Kişi ", sütun ' PersonID '.*

*Geçişleri\&lt; timestamp&gt;\_Inheritance.cs* açın ve `Up` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=25,29-40)]

`update-database` komutunu yeniden çalıştırın.

> [!NOTE]
> Verileri geçirirken ve şema değişiklikleri yaparken başka hatalar almak mümkündür. Çözümleyemez geçiş hataları alırsanız, *Web. config* dosyasındaki bağlantı dizesini değiştirerek veya veritabanını silerek öğreticiye devam edebilirsiniz. En basit yaklaşım, *Web. config* dosyasındaki veritabanını yeniden adlandırmalıdır. Örneğin, aşağıdaki örnekte gösterildiği gibi, veritabanı adını\_test olarak değiştirin:
> 
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.xml?highlight=1-2)]
> 
> Yeni bir veritabanı ile geçirilecek veri yoktur ve `update-database` komutunun hatasız tamamlanabilmesi çok daha yüksektir. Veritabanının nasıl silineceği hakkında yönergeler için bkz. [Visual Studio 'dan bir veritabanını bırakma 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/). Öğreticiye devam etmek için bu yaklaşımla karşılaşırsanız, Bu öğreticinin sonundaki dağıtım adımını atlayın, çünkü dağıtılan site, geçişleri otomatik olarak çalıştırırken aynı hatayı alır. Bir geçiş hatasıyla ilgili sorunları gidermek istiyorsanız en iyi kaynak Entity Framework forumlarından veya StackOverflow.com biridir.

## <a name="testing"></a>Sınama

Siteyi çalıştırın ve çeşitli sayfaları deneyin. Her şey, daha önce olduğu gibi çalışmaktadır.

**Sunucu Gezgini** ' de, **SchoolContext** ve ardından **Tablolar**' ı genişletin ve **öğrenci** ve **eğitmen** tablolarının bir **kişi** tablosu ile değiştirildiğini görürsünüz. **Kişi** tablosunu genişletin ve **öğrenci** ve **eğitmen** tablolarında, kullanılan tüm sütunları olduğunu görürsünüz.

![Server_Explorer_showing_Person_table](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Kişi tablosuna sağ tıklayın ve ardından **tablo verilerini göster** ' e tıklayarak ayrıştırıcı sütununu görüntüleyin.

![](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

Aşağıdaki diyagramda, yeni okul veritabanının yapısı gösterilmektedir:

![School_database_diagram](https://asp.net/media/2578143/Windows-Live-Writer_58f5a93579b2_CC7B_School_database_diagram_6350a801-7199-413f-bbac-4a2009ed19d7.png)

## <a name="summary"></a>Özet

`Person`, `Student`ve `Instructor` sınıfları için hiyerarşi başına tablo devralma işlemi artık uygulandı. Bu ve diğer devralma yapıları hakkında daha fazla bilgi için bkz. morteza, Web günlüğü üzerinde [Devralma eşleme stratejileri](https://weblogs.asp.net/manavi/archive/2010/12/24/inheritance-mapping-strategies-with-entity-framework-code-first-ctp5-part-1-table-per-hierarchy-tph.aspx) . Sonraki öğreticide, depo ve iş deseni birimi uygulamak için bazı yollar görürsünüz.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Önceki](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [İleri](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)
