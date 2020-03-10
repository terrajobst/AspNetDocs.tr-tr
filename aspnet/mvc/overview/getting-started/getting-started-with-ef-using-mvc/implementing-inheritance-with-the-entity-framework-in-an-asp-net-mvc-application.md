---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: ASP.NET MVC 5 uygulamalarında EF ile devralma uygulama'
description: Bu öğretici, veri modelinde devralmayı nasıl uygulayacağınızı gösterir.
author: tdykstra
ms.author: riande
ms.date: 01/21/2019
ms.topic: tutorial
ms.assetid: 08834147-77ec-454a-bb7a-d931d2a40dab
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 73a01ed47b0935a1a9734c197377470defb1fe36
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583064"
---
# <a name="tutorial-implement-inheritance-with-ef-in-an-aspnet-mvc-5-app"></a>Öğretici: ASP.NET MVC 5 uygulamasında EF ile devralma uygulama

Önceki öğreticide eşzamanlılık özel durumları ele alınır. Bu öğretici, veri modelinde devralmayı nasıl uygulayacağınızı gösterir.

Nesne odaklı programlamada, [kod yeniden kullanımını](http://en.wikipedia.org/wiki/Code_reuse)kolaylaştırmak için [devralmayı](http://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)) kullanabilirsiniz. Bu öğreticide, `Instructor` ve `Student` sınıflarını, hem Eğitmenler hem de öğrenciler için ortak olan `LastName` gibi özellikleri içeren bir `Person` taban sınıftan türetireceğiz olacak şekilde değiştireceksiniz. Herhangi bir Web sayfası eklemez veya değiştirmezsiniz, ancak koddan bazılarını değiştireceksiniz ve bu değişiklikler otomatik olarak veritabanına yansıtılacaktır.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Devralmayı veritabanına eşlemeyi öğrenin
> * Kişi sınıfını oluşturma
> * Eğitmeni ve öğrenci 'yi güncelleştirme
> * Modele kişi ekleme
> * Geçişleri oluşturma ve güncelleştirme
> * Uygulamayı test etme
> * Azure’a dağıtma

## <a name="prerequisites"></a>Önkoşullar

* [Eşzamanlılığı İşleme](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="map-inheritance-to-database"></a>Devralmayı veritabanına eşle

`School` veri modelindeki `Instructor` ve `Student` sınıfları özdeş olan birkaç özelliğe sahiptir:

![Student_and_Instructor_classes](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

`Instructor` ve `Student` varlıkları tarafından paylaşılan özellikler için gereksiz kodu ortadan kaldırmak istediğinizi varsayalım. Ya da adın bir eğitmenden veya bir öğrenciye ait olup olmadığına bakılmaksızın adları biçimlendirmeden bir hizmet yazmak isteyebilirsiniz. Yalnızca bu paylaşılan özellikleri içeren `Person` bir temel sınıf oluşturabilirsiniz, sonra `Instructor` ve `Student` varlıkların aşağıdaki çizimde gösterildiği gibi bu temel sınıftan devralmasını sağlayabilirsiniz:

![Student_and_Instructor_classes_deriving_from_Person_class](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

Bu devralma yapısının veritabanında temsil edilebilmesi için birkaç yol vardır. Tek bir tabloda hem öğrenciler hem de eğitmenler hakkında bilgi içeren bir `Person` tablonuz olabilir. Bazı sütunlar yalnızca Eğitmenler (`HireDate`), bazıları yalnızca öğrencilerle (`EnrollmentDate`), bazıları ise (`LastName`, `FirstName`) uygulanabilir. Genellikle, her bir satırın temsil ettiği türü belirtmek için bir *ayrıştırıcı* sütunu vardır. Örneğin, ayrıştırıcı sütununda, Eğitmenler için "eğitmen" ve öğrenciler için "öğrenci" bulunabilir.

![Hierarchy_example başına tablo](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

Tek bir veritabanı tablosundan bir varlık devralma yapısı oluşturmanın bu düzeni, *hiyerarşi başına tablo* (TPH) devralma olarak adlandırılır.

Alternatif olarak, veritabanının devralma yapısına benzer bir şekilde görünmesini sağlayabilirsiniz. Örneğin, `Person` tablosunda yalnızca ad alanları olabilir ve Tarih alanlarıyla ayrı `Instructor` ve `Student` tabloları vardır.

![Type_inheritance başına tablo](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Her varlık sınıfı için bir veritabanı tablosu yapmanın bu düzeni, *tür başına tablo* (TPT) devralma olarak adlandırılır.

Başka bir seçenek de Özet olmayan tüm türleri tek tek tablolarla eşlemenize olanak sağlar. Devralınan özellikler de dahil olmak üzere bir sınıfın tüm özellikleri karşılık gelen tablonun sütunlarına eşlenir. Bu düzene, tablo başına somut sınıf (TPC) devralma adı verilir. Daha önce gösterildiği gibi `Person`, `Student`ve `Instructor` sınıfları için TPC devralmayı uyguladıysanız, `Student` ve `Instructor` tabloları, daha önce olduğu gibi devralma uygulandıktan sonra farklı şekilde görünür.

TPC ve TPH devralma desenleri genellikle TPT devralma desenlerinden daha iyi Entity Framework performans sağlar, çünkü TPT desenleri karmaşık JOIN sorgularına yol açabilir.

Bu öğreticide, TPH devralmanın nasıl uygulanacağı gösterilmektedir. TPH Entity Framework varsayılan devralma modelidir, bu yüzden tek yapmanız gerekir `Person` bir sınıf oluşturmak, `Person`türetmek için `Instructor` ve `Student` sınıfları değiştirmek, yeni sınıfı `DbContext`eklemek ve bir geçiş oluşturmak. (Diğer devralma düzenlerini uygulama hakkında daha fazla bilgi için, bkz. [tür başına tablo (TPT) devralmayı eşleme](https://msdn.microsoft.com/data/jj591617#2.5) ve MSDN Entity Framework belgelerinde [somut sınıf başına tablo (TPC) devralmayı](https://msdn.microsoft.com/data/jj591617#2.6) eşleme.)

## <a name="create-the-person-class"></a>Kişi sınıfını oluşturma

*Modeller* klasöründe *Person.cs* oluşturun ve şablon kodunu şu kodla değiştirin:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

## <a name="update-instructor-and-student"></a>Eğitmeni ve öğrenci 'yi güncelleştirme

Şimdi *Person.SC*değerlerini devralması için *Instructor.cs* ve *Student.cs* güncelleştirin.

*Instructor.cs*' de, `Instructor` sınıfını `Person` sınıfından türetirsiniz ve anahtar ve ad alanlarını kaldırın. Kod aşağıdaki örneğe benzer şekilde görünür:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

*Student.cs*'de benzer değişiklikler yapın. `Student` sınıfı aşağıdaki örneğe benzer şekilde görünür:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

## <a name="add-person-to-the-model"></a>Modele kişi ekleme

*SchoolContext.cs*' de, `Person` varlık türü için bir `DbSet` özelliği ekleyin:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Bu, Entity Framework hiyerarşinin devralma devralınmasını yapılandırmak için gereklidir. Gördüğünüz gibi, veritabanı güncelleştirildiği sırada `Student` ve `Instructor` tablolarının yerine bir `Person` tablosu olacaktır.

## <a name="create-and-update-migrations"></a>Geçişleri oluşturma ve güncelleştirme

Paket Yöneticisi konsolunda (PMC), aşağıdaki komutu girin:

`Add-Migration Inheritance`

PMC 'de `Update-Database` komutunu çalıştırın. Bu noktada, geçiş işlemi nasıl işleneceğini bilmez. Aşağıdakine benzer bir hata iletisi alırsınız:

> *' Dbo ' nesnesi bırakılamıyor. Eğitmen ', yabancı anahtar kısıtlaması tarafından başvurulduğu için.*

*Geçişleri\&lt; timestamp&gt;\_Inheritance.cs* açın ve `Up` yöntemini aşağıdaki kodla değiştirin:

[!code-csharp[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

Bu kod aşağıdaki veritabanı güncelleştirme görevlerini gerçekleştirir:

- Yabancı anahtar kısıtlamalarını ve öğrenci tablosuna işaret eden dizinleri kaldırır.
- Eğitmen tablosunu kişi olarak yeniden adlandırır ve öğrenci verilerini depolamak için gerekli değişiklikleri yapar:

    - Öğrenciler için Nullable kayıt tarihi ekler.
    - Bir satırın bir öğrenci mi yoksa bir eğitmen mi olduğunu göstermek için ayrıştırıcı sütunu ekler.
    - Öğrenci satırlarında işe alma tarihleri olmadığından, HireDate null yapılabilir hale gelir.
    - Öğrencilere işaret eden yabancı anahtarları güncelleştirmek için kullanılacak geçici bir alan ekler. Öğrencileri kişi tablosuna kopyaladığınızda yeni birincil anahtar değerleri alırlar.
- Öğrenci tablosundaki verileri kişi tablosuna kopyalar. Bu, öğrencilerden yeni birincil anahtar değerleri atanmasını sağlar.
- Öğrencilere işaret eden yabancı anahtar değerlerini düzeltir.
- Yabancı anahtar kısıtlamalarını ve dizinleri yeniden oluşturur, şimdi bunları kişi tablosuna işaret eder.

(Birincil anahtar türü olarak tamsayı yerine GUID kullandıysanız, öğrenci birincil anahtar değerlerinin değiştirilmesi gerekmez ve bu adımların bazıları atlanamaz.)

`update-database` komutunu yeniden çalıştırın.

(Bir üretim sisteminde, önceki veritabanı sürümüne geri dönmek için bunu kullanmak zorunda kalbilmeniz durumunda, ilgili değişiklikleri aşağı doğru yapmanız gerekir. Bu öğreticide, aşağı yöntemini kullanmayacağız.)

> [!NOTE]
> Verileri geçirirken ve şema değişiklikleri yaparken başka hatalar almak mümkündür. Çözümleyemez geçiş hataları alırsanız, *Web. config* dosyasındaki bağlantı dizesini değiştirerek veya veritabanını silerek öğreticiye devam edebilirsiniz. En basit yaklaşım, *Web. config* dosyasındaki veritabanını yeniden adlandırmalıdır. Örneğin, aşağıdaki örnekte gösterildiği gibi, veritabanı adını ContosoUniversity2 olarak değiştirin:
>
> [!code-xml[Main](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.xml?highlight=2)]
>
> Yeni bir veritabanı ile geçirilecek veri yoktur ve `update-database` komutunun hatasız tamamlanabilmesi çok daha yüksektir. Veritabanının nasıl silineceği hakkında yönergeler için bkz. [Visual Studio 'dan bir veritabanını bırakma 2012](http://romiller.com/2013/05/17/how-to-drop-a-database-from-visual-studio-2012/). Öğreticiye devam etmek için bu yaklaşımla karşılaşırsanız, Bu öğreticinin sonundaki dağıtım adımını atlayın veya yeni bir siteye ve veritabanına dağıtın. Zaten dağıtmakta olduğunuz siteye bir güncelleştirme dağıtırsanız,, geçişleri otomatik olarak çalıştırdığında EF aynı hatayı alır. Bir geçiş hatasıyla ilgili sorunları gidermek istiyorsanız en iyi kaynak Entity Framework forumlarından veya StackOverflow.com biridir.

## <a name="test-the-implementation"></a>Uygulamayı test etme

Siteyi çalıştırın ve çeşitli sayfaları deneyin. Her şey, daha önce olduğu gibi çalışmaktadır.

**Sunucu Gezgini** **veri Connections\SchoolContext** ve ardından **Tablolar**' ı genişletin ve **öğrenci** ve **eğitmen** tablolarının bir **kişi** tablosu ile değiştirildiğini görürsünüz. **Kişi** tablosunu genişletin ve **öğrenci** ve **eğitmen** tablolarında, kullanılan tüm sütunları olduğunu görürsünüz.

Kişi tablosuna sağ tıklayın ve ardından **tablo verilerini göster** ' e tıklayarak ayrıştırıcı sütununu görüntüleyin.

Aşağıdaki diyagramda, yeni okul veritabanının yapısı gösterilmektedir:

![School_database_diagram](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

## <a name="deploy-to-azure"></a>Azure’a dağıtma

Bu bölümde, bu öğretici serisinin bölüm [3, sıralama, filtreleme ve sayfalama](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md) bölümünde **Azure 'a uygulamayı** isteğe bağlı olarak dağıtma bölümünden tamamlamış olmanız gerekir. Yerel projenizde veritabanını silerek çözümladığınız hataları geçirseniz, bu adımı atlayın; ya da yeni bir site ve veritabanı oluşturup yeni ortama dağıtın.

1. Visual Studio 'da **Çözüm Gezgini** projeye sağ tıklayın ve bağlam menüsünden **Yayımla** ' yı seçin.

2. **Yayımla**’ta tıklayın.

    Web uygulaması varsayılan tarayıcınızda açılır.

3. Çalışıp çalışmadığını doğrulamak için uygulamayı test edin.

    Veritabanına erişen bir sayfayı ilk kez çalıştırdığınızda Entity Framework, geçerli veri modeliyle veritabanını güncel hale getirmek için gereken tüm geçişleri `Up` yöntemlerini çalıştırır.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET Data Access-önerilen kaynaklarda](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

Bu ve diğer devralma yapıları hakkında daha fazla bilgi için MSDN 'deki [TPT devralma deseninin](https://msdn.microsoft.com/data/jj618293) ve [TPH devralma deseninin](https://msdn.microsoft.com/data/jj618292) bölümüne bakın. Sonraki öğreticide, çeşitli görece gelişmiş Entity Framework senaryolarını nasıl işleyeceğinizi göreceksiniz.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Devralma veritabanına eşlenmeli
> * Kişi sınıfı oluşturuldu
> * Güncelleştirilmiş eğitmen ve öğrenci
> * Modele kişi eklendi
> * Geçişleri oluşturma ve güncelleştirme
> * Uygulama test edildi
> * Azure 'a dağıtıldı

Entity Framework Code First kullanan ASP.NET Web uygulamaları geliştirme hakkında temel bilgileri aşdığınızda bilmeniz gereken konular hakkında bilgi edinmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Gelişmiş Entity Framework Senaryoları](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
