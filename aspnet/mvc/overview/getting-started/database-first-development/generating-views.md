---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 'Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümler oluşturma'
description: Bu öğretici, denetleyicileri ve görünümleri oluşturmak için ASP.NET Scafkatlarını kullanmaya odaklanır.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616209"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a>Öğretici: ASP.NET MVC uygulamasıyla EF Database First için görünümler oluşturma

MVC, Entity Framework ve ASP.NET Scafkatı kullanarak var olan bir veritabanına arabirim sağlayan bir Web uygulaması oluşturabilirsiniz. Bu öğretici serisinde, kullanıcıların bir veritabanı tablosunda yer alan verileri görüntülemesini, düzenlemesini, oluşturmasını ve silmesini sağlayan nasıl otomatik olarak kod üretileyeceğiniz gösterilmektedir. Oluşturulan kod, veritabanı tablosundaki sütunlara karşılık gelir.

Bu öğretici, denetleyicileri ve görünümleri oluşturmak için ASP.NET Scafkatlarını kullanmaya odaklanır.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Yapı iskelesi Ekle
> * Yeni görünümlere bağlantı ekleme
> * Öğrenci görünümlerini görüntüle
> * Kayıt görünümlerini görüntüle

## <a name="prerequisite"></a>Önkoşul

* [Web uygulaması ve veri modellerini oluşturma](creating-the-web-application.md)

## <a name="add-scaffold"></a>Yapı iskelesi Ekle

Model sınıfları için standart veri işlemleri sağlayacak kod oluşturmaya hazırsınızdır. Bir yapı iskelesi öğesi ekleyerek kodu eklersiniz. Ekleyebileceğiniz yapı iskelesi türü için birçok seçenek vardır; Bu öğreticide, scafkatlama, önceki bölümde oluşturduğunuz öğrenci ve kayıt modellerine karşılık gelen bir denetleyiciyi ve görünümleri içerir.

Projenizde tutarlılığı sürdürmek için, yeni denetleyiciyi var olan **denetleyiciler** klasörüne ekleyeceksiniz. **Denetleyiciler** klasörüne sağ tıklayın ve > **yeni yapı Iskelesi öğesi** **Ekle** ' yi seçin.

Entity Framework seçeneğini **kullanarak, görünümler Içeren MVC 5 denetleyiciyi** seçin. Bu seçenek, modelinizdeki verileri güncelleştirme, silme, oluşturma ve görüntülemeye yönelik denetleyiciyi ve görünümleri oluşturacaktır.

![MVC denetleyicisi Ekle](generating-views/_static/image2.png)

Model sınıfı için **öğrenci (ContosoSite. modeller)** öğesini seçin ve bağlam sınıfı Için **Contosoüniversıtydataentities (Contososite. modeller)** öğesini seçin. Denetleyici adını **Studentscontroller**olarak tutun.

**Ekle**'yi tıklatın.

Bir hata alırsanız, bunun nedeni, önceki bölümde projeyi derlemeniz olabilir. Bu durumda projeyi oluşturmayı deneyin ve ardından yapı iskelesi öğesini yeniden ekleyin.

Kod oluşturma işlemi tamamlandıktan sonra, projenizin **denetleyicileri** ve **görünümleri** > **öğrenciler** klasörlerinde yeni bir denetleyici ve görünümler görürsünüz.

Aynı adımları yeniden gerçekleştirin, ancak **kayıt** sınıfı için bir yapı iskelesi ekleyin. İşiniz bittiğinde, bir **EnrollmentsController.cs** dosyanız ve oluşturma, silme, ayrıntılar, düzenleme ve dizin görünümleri ile **kayıtlar adlı** **Görünümler** altında bir klasör vardır.

## <a name="add-links-to-new-views"></a>Yeni görünümlere bağlantı ekleme

Yeni görünümleriniz üzerinde gezinmenize daha kolay hale getirmek için öğrenciler ve kayıtlar için Dizin görünümlerine birkaç köprü ekleyebilirsiniz. Dosyayı, sitenizin ana sayfası olan > **home** > *Index. cshtml* **' de açın** . Aşağıdaki kodu jumbotron altına ekleyin.

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

ActionLink yöntemi için ilk parametre, bağlantıda görüntülenecek metindir. İkinci parametre eylemdir ve üçüncü parametre denetleyicinin adıdır. Örneğin, ilk bağlantı, StudentsController içindeki dizin eylemine işaret eder. Gerçek köprü bu değerlerden oluşturulur. İlk bağlantı, kullanıcıları **Görünümler/öğrenciler** klasörü içindeki **Index. cshtml** dosyasına alır.

## <a name="display-student-views"></a>Öğrenci görünümlerini görüntüle

Projenize eklenen kodun öğrencilerinin bir listesini görüntüleyeceğini ve kullanıcıların veritabanındaki öğrenci kayıtlarını düzenlemesini, oluşturmasını veya silmesini sağlayan bir kod görürsünüz.

**Görünümler** > **giriş** > *Index. cshtml* dosyasına sağ tıklayın ve **Tarayıcıda görüntüle**' yi seçin. Uygulama giriş sayfasında, **öğrenci listesi**' ni seçin.

![](generating-views/_static/image6.png)

**Dizin** sayfasında, bu verileri değiştirmek için öğrenciler ve bağlantılar listesine dikkat edin. **Yeni oluştur** bağlantısını seçin ve yeni bir öğrenci için bazı değerler sağlayın. **Oluştur**' a tıklayın ve yeni öğrencinin listenize eklendiğini unutmayın.

**Dizin** sayfasında, **Düzenle** bağlantısını seçin ve bir öğrenci için bazı değerleri değiştirin. **Kaydet**' e tıklayın ve Öğrenci kaydının değiştirildiğini unutmayın.

Son olarak, **Sil** bağlantısını seçin ve **Sil** düğmesine tıklayarak kaydı silmek istediğinizi onaylayın.

Herhangi bir kod yazmadan, öğrenci tablosundaki veriler üzerinde yaygın işlemler gerçekleştiren görünümler eklediniz.

Bir alanın metin etiketinin, Web sayfasında görüntülenmesini istediğiniz zaman olmayan veritabanı özelliğine ( **LastName**gibi) göre olduğunu fark etmiş olabilirsiniz. Örneğin, etiketi **Soyadı**olacak şekilde tercih edebilirsiniz. Bu görüntü sorunu öğreticide daha sonra düzeltilecektir.

## <a name="display-enrollment-views"></a>Kayıt görünümlerini görüntüle

Veritabanınız, öğrenci ve kayıt tabloları arasında bire çok bir ilişki ve kurs ve kayıt tabloları arasında bire çok ilişki içerir. Kayıt görünümleri bu ilişkileri doğru bir şekilde işler. Sitenizin ana sayfasına gidin ve kayıt **listesi** bağlantısı ' nı ve ardından **Yeni bağlantı oluştur** ' u seçin.

Görünüm yeni bir kayıt kaydı oluşturmak için bir form görüntüler. Özellikle, formun bir **CourseID** açılır listesi ve bir **studentid** açılır listesi içerdiğine dikkat edin. Her ikisi de ilgili tablolardaki değerlerle doldurulur.

Ayrıca, girilen değerlerin doğrulanması alanın veri türüne göre otomatik olarak uygulanır. **Sınıf** için bir sayı gerekir, bu nedenle uyumsuz bir değer sağlamaya çalışırsanız bir hata iletisi görüntülenir: *alan sınıfı bir sayı olmalıdır.*

Otomatik olarak oluşturulan görünümlerin, kullanıcıların veritabanındaki verilerle çalışmasını olanaklı olduğunu doğruladınız. Bu serinin sonraki öğreticide, veritabanını güncelleştirecek ve ilgili değişiklikleri Web uygulamasında yapacaksınız.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Yapı iskelesi eklendi
> * Yeni görünümlere bağlantılar eklendi
> * Görünen öğrenci görünümleri
> * Görüntülenmiş kayıt görünümleri

Veritabanını değiştirme hakkında bilgi edinmek için sonraki öğreticiye ilerleyin.
> [!div class="nextstepaction"]
> [Veritabanını değiştirme](changing-the-database.md)