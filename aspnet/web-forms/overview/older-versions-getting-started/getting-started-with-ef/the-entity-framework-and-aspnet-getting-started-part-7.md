---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 7 ' yi kullanmaya başlama | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: f8afb245-b705-419c-8790-0b295e90d5e2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-7
msc.type: authoredcontent
ms.openlocfilehash: 18d4b44c5e23fd6942c3adf48a33a5602e6df6d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603434"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-7"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms-Bölüm 7 ' yi kullanmaya başlama

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](the-entity-framework-and-aspnet-getting-started-part-1.md) bakın

## <a name="using-stored-procedures"></a>Saklı Yordamları Kullanma

Önceki öğreticide, bir hiyerarşi başına devralma düzeni uygulamış olursunuz. Bu öğreticide, veritabanı erişimi üzerinde daha fazla denetim kazanmak için saklı yordamların nasıl kullanılacağı gösterilir.

Entity Framework, veritabanı erişimi için saklı yordamları kullanması gerektiğini belirtmenize olanak tanır. Herhangi bir varlık türü için, bu türdeki varlıkları oluşturmak, güncelleştirmek veya silmek için kullanmak üzere bir saklı yordam belirtebilirsiniz. Ardından, veri modelinde varlık kümelerini alma gibi görevleri gerçekleştirmek için kullanabileceğiniz saklı yordamlara başvurular ekleyebilirsiniz.

Saklı yordamları kullanmak, veritabanı erişimi için yaygın bir gereksinimdir. Bazı durumlarda, bir veritabanı yöneticisi tüm veritabanı erişiminin güvenlik nedenleriyle saklı yordamlar üzerinden gitmesini gerektirebilir. Diğer durumlarda, veritabanını güncelleştirdiğinde Entity Framework kullandığı işlemlerden bazılarına iş mantığı oluşturmak isteyebilirsiniz. Örneğin, bir varlık silindiğinde bir arşiv veritabanına kopyalamak isteyebilirsiniz. Ya da bir satır güncelleştirildiğinde değişikliği yapan bir günlüğe kaydetme tablosuna bir satır yazmak isteyebilirsiniz. Bu tür görevleri, Entity Framework bir varlığı sildiği veya bir varlığı güncelleştiren her seferinde çağrılan bir saklı yordamda gerçekleştirebilirsiniz.

Önceki öğreticide olduğu gibi, yeni sayfa oluşturabileceksiniz. Bunun yerine, Entity Framework zaten oluşturduğunuz bazı sayfalardan veritabanına erişim şeklini değiştirirsiniz.

Bu öğreticide, `Student` ve `Instructor` varlıkları eklemek için veritabanında saklı yordamlar oluşturacaksınız. Bunları veri modeline ekleyeceksiniz ve Entity Framework veritabanına `Student` ve `Instructor` varlıkları eklemek için onları kullanması gerektiğini belirtirsiniz. Ayrıca, `Course` varlıkları almak için kullanabileceğiniz bir saklı yordam oluşturacaksınız.

## <a name="creating-stored-procedures-in-the-database"></a>Veritabanında saklı yordamlar oluşturma

(Bu öğreticide, projedeki *okul. mdf* dosyasını kullanıyorsanız, saklı yordamlar zaten mevcut olduğundan bu bölümü atlayabilirsiniz.)

**Sunucu Gezgini**, *okul. mdf*' yi genişletin, **saklı yordamlar**' a sağ tıklayın ve **Yeni saklı yordam Ekle**' yi seçin.

[![image15](the-entity-framework-and-aspnet-getting-started-part-7/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image1.png)

Aşağıdaki SQL deyimlerini kopyalayıp, çatı saklı yordamını değiştirerek saklı yordam penceresine yapıştırın.

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample1.sql)]

[![image14](the-entity-framework-and-aspnet-getting-started-part-7/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image3.png)

`Student` varlıkların dört özelliği vardır: `PersonID`, `LastName`, `FirstName`ve `EnrollmentDate`. Veritabanı KIMLIK değerini otomatik olarak oluşturur ve saklı yordam diğer üç için parametreleri kabul eder. Saklı yordam, Entity Framework, yeni satırın kayıt anahtarı değerini döndürür, böylece, bellekte devam eden varlığın sürümünde bunu takip edebilir.

Saklı yordam penceresini kaydedin ve kapatın.

Aşağıdaki SQL deyimlerini kullanarak `InsertInstructor` saklı yordamı aynı şekilde oluşturun:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample2.sql)]

`Student` ve `Instructor` varlıkları için de `Update` saklı yordamlar oluşturun. (Veritabanı zaten `Instructor` ve `Student` varlıkları için çalışacak `DeletePerson` saklı bir yordama sahiptir.)

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample3.sql)]

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample4.sql)]

Bu öğreticide, her varlık türü için üç işlevi (INSERT, Update ve Delete--) eşlersiniz. Entity Framework sürüm 4, bu işlevlerden yalnızca birini veya ikisini, diğerlerini eşleştirmeden saklı yordamlara eşlemenizi sağlar, tek bir özel durum: güncelleştirme işlevini eşleştirmeniz ancak Delete işlevini belirtmezseniz, bu işlem yaptığınızda Entity Framework bir özel durum oluşturur bir varlığı silmeyi deneyin. Entity Framework sürüm 3,5 ' de, saklı yordamları eşleme konusunda bu çok esnekliğe sahip değilsiniz: bir işlevi eşleştirdiyseniz, üçünü eşlemek için gerekli olan

Güncelleştirme verileri yerine okuyan bir saklı yordam oluşturmak için aşağıdaki SQL deyimlerini kullanarak tüm `Course` varlıklarını seçen bir tane oluşturun:

[!code-sql[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample5.sql)]

## <a name="adding-the-stored-procedures-to-the-data-model"></a>Saklı yordamları veri modeline ekleme

Saklı yordamlar artık veritabanında tanımlanmıştır, ancak Entity Framework için kullanılabilir hale getirmek üzere veri modeline eklenmelidir. *SchoolModel. edmx*' i açın, tasarım yüzeyine sağ tıklayın ve **modeli veritabanından Güncelleştir**' i seçin. **Veritabanı nesnelerinizi seçin** Iletişim kutusundaki **Ekle** sekmesinde, **saklı yordamlar**' ı genişletin, yeni oluşturulan saklı yordamları ve `DeletePerson` saklı yordamını seçin ve ardından **son**' a tıklayın.

[![image20](the-entity-framework-and-aspnet-getting-started-part-7/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image5.png)

## <a name="mapping-the-stored-procedures"></a>Saklı yordamları eşleme

Veri modeli tasarımcısında `Student` varlığına sağ tıklayıp **saklı yordam eşlemesi**' ni seçin.

[![image21](the-entity-framework-and-aspnet-getting-started-part-7/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image7.png)

**Eşleme ayrıntıları** penceresi görüntülenir, burada Entity Framework bu türden varlıkları eklemek, güncelleştirmek ve silmek için kullanması gereken saklı yordamları belirtebilirsiniz.

[![image22](the-entity-framework-and-aspnet-getting-started-part-7/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image9.png)

**Insert** Işlevini **ınsertstudent**olarak ayarlayın. Pencere, her birinin bir varlık özelliğine eşlenmesi gereken saklı yordam parametrelerinin bir listesini gösterir. Adların ikisi de aynı olduğundan, bunlar otomatik olarak eşlenir. `FirstName`adlı bir varlık özelliği yoktur, bu nedenle kullanılabilir varlık özelliklerini gösteren bir açılan listeden `FirstMidName` el ile seçmeniz gerekir. (Bunun nedeni, `FirstName` özelliğinin adını ilk öğreticideki `FirstMidName` olarak değiştirdiniz.)

[![image23](the-entity-framework-and-aspnet-getting-started-part-7/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image11.png)

Aynı **eşleme ayrıntıları** penceresinde, `Update` işlevini `UpdateStudent` saklı yordamla eşleyin (`Insert` saklı yordamı için yaptığınız gibi `FirstName`parametre değeri olarak `FirstMidName` belirttiğinizden emin olun) ve `Delete` işlevi `DeletePerson` saklı yordamına.

[![image01](the-entity-framework-and-aspnet-getting-started-part-7/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image13.png)

`Instructor` varlığı için Eğitmenler için INSERT, Update ve delete saklı yordamlarını eşlemek için aynı yordamı izleyin.

[![image02](the-entity-framework-and-aspnet-getting-started-part-7/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image15.png)

Verileri güncelleştirmek yerine okunan saklı yordamlar için, saklı yordamı döndürdüğü varlık türüne eşlemek için **Model tarayıcı** penceresini kullanın. Veri modeli tasarımcısında, tasarım yüzeyine sağ tıklayıp **model tarayıcısı**' nı seçin. **SchoolModel. Store** düğümünü açın ve sonra **saklı yordamlar** düğümünü açın. Ardından `GetCourses` saklı yordamına sağ tıklayıp **Işlev Içeri aktarma Ekle**' yi seçin.

[![image24](the-entity-framework-and-aspnet-getting-started-part-7/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image17.png)

**Işlev Içeri aktarma Ekle** iletişim kutusunda, bir SELECT **varlıklarının** **koleksiyonunu döndürür** ve döndürülen varlık türü olarak `Course` öğesini seçin. İşiniz bittiğinde, **Tamam**’a tıklayın. *. Edmx* dosyasını kaydedin ve kapatın.

[![image25](the-entity-framework-and-aspnet-getting-started-part-7/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image19.png)

## <a name="using-insert-update-and-delete-stored-procedures"></a>INSERT, Update ve delete saklı yordamlarını kullanma

Verileri ekleme, güncelleştirme ve silmeye yönelik saklı yordamlar, veri modeline eklendikten ve bunları uygun varlıklarla eşleştirdikten sonra otomatik olarak Entity Framework tarafından kullanılır. Artık *StudentsAdd. aspx* sayfasını çalıştırabilirsiniz ve yeni bir öğrenci oluşturduğunuzda Entity Framework, yeni bir satırı `Student` tablosuna eklemek için `InsertStudent` saklı yordamını kullanır.

[![image03](the-entity-framework-and-aspnet-getting-started-part-7/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image21.png)

*Öğrenciler. aspx* sayfasını çalıştırın ve listede yeni öğrenci görüntülenir.

[![image04](the-entity-framework-and-aspnet-getting-started-part-7/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image23.png)

Update işlevinin çalıştığını doğrulamak için adı değiştirin ve ardından DELETE işlevinin çalıştığını doğrulamak için öğrenci 'yi silin.

[![image05](the-entity-framework-and-aspnet-getting-started-part-7/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-7/_static/image25.png)

## <a name="using-select-stored-procedures"></a>SELECT saklı yordamlarını kullanma

Entity Framework, `GetCourses`gibi saklı yordamları otomatik olarak çalıştırmaz ve bunları `EntityDataSource` denetimiyle kullanamazsınız. Bunları kullanmak için, bunları koddan çağırabilirsiniz.

*InstructorsCourses.aspx.cs* dosyasını açın. `PopulateDropDownLists` yöntemi, tüm kurs varlıklarını almak için bir LINQ-Entities sorgusu kullanır ve bu sayede bir eğitmenin ne olduğunu ve hangilerinin atanmamış olduğunu belirleyebilir:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample6.cs)]

Bunu şu kodla değiştirin:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-7/samples/sample7.cs)]

Sayfa artık tüm kursların listesini almak için `GetCourses` saklı yordamını kullanır. Daha önce olduğu gibi çalıştığını doğrulamak için sayfayı çalıştırın.

(Saklı yordam tarafından alınan varlıkların gezinti özellikleri, `ObjectContext` varsayılan ayarlarına bağlı olarak bu varlıklarla ilgili verilerle otomatik olarak doldurulmayabilir. Daha fazla bilgi için, MSDN Kitaplığı 'nda [Ilgili nesneleri yükleme](https://msdn.microsoft.com/library/bb896272.aspx) bölümüne bakın.)

Sonraki öğreticide, veri biçimlendirmeyi ve doğrulama kurallarını programlamayı ve test yapmayı kolaylaştırmak için dinamik veri işlevselliğini nasıl kullanacağınızı öğreneceksiniz. Veri biçimi dizeleri ve bir alanın gerekli olup olmadığı gibi her bir Web sayfası kuralı için belirtmek yerine, veri modeli meta verilerinde bu tür kuralları belirtebilirsiniz ve bunlar her sayfada otomatik olarak uygulanır.

> [!div class="step-by-step"]
> [Önceki](the-entity-framework-and-aspnet-getting-started-part-6.md)
> [İleri](the-entity-framework-and-aspnet-getting-started-part-8.md)
