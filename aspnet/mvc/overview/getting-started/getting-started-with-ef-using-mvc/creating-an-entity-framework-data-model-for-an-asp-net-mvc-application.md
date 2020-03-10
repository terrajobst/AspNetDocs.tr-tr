---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 'Öğretici: MVC 5 kullanarak Entity Framework 6 Code First kullanmaya başlama | Microsoft Docs'
description: Bu öğretici dizisinde, veri erişimi için Entity Framework 6 kullanan bir ASP.NET MVC 5 uygulaması oluşturma hakkında bilgi edineceksiniz.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616132"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a>Öğretici: MVC 5 kullanarak Entity Framework 6 Code First kullanmaya başlama

> [!NOTE]
> Yeni geliştirme için ASP.NET MVC denetleyicileri ve görünümleri üzerinde [ASP.NET Core Razor Pages](/aspnet/core/razor-pages) önerilir. Razor Pages ile benzer bir öğretici serisi için bkz. [öğretici: ASP.NET Core Razor Pages kullanmaya başlama](/aspnet/core/tutorials/razor-pages/razor-pages-start). Yeni öğretici:
> * Daha kolay hale gelmelidir.
> * Daha fazla EF Core en iyi yöntem sağlar.
> * Daha verimli sorgular kullanır.
> * En son API ile daha güncel.
> * Daha fazla özellik içerir.
> * , Yeni uygulama geliştirmesi için tercih edilen yaklaşımdır.

Bu öğretici dizisinde, veri erişimi için Entity Framework 6 kullanan bir ASP.NET MVC 5 uygulaması oluşturma hakkında bilgi edineceksiniz. Bu öğretici Code First iş akışını kullanır. Code First, Database First ve Model First arasında seçim yapma hakkında daha fazla bilgi için bkz. [model oluşturma](/ef/ef6/modeling/).

Bu öğretici serisinde, Contoso Üniversitesi örnek uygulamasının nasıl oluşturulacağı açıklanmaktadır. Örnek uygulama, basit bir üniversite web sitesidir. Bununla birlikte öğrenciye, kursa ve eğitmen bilgilerini görüntüleyebilir ve güncelleştirebilirsiniz. Oluşturduğunuz ekranlardan ikisi şunlardır:

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![Öğrenci Düzenle](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * MVC web uygulaması oluşturma
> * Site stili Ayarla
> * Entity Framework 6 ' yı yükler
> * Veri modeli oluşturma
> * Veritabanı bağlamını oluşturma
> * Test verileriyle VERITABANıNı başlatma
> * LocalDB kullanmak için EF 6 ayarlama
> * Denetleyici ve görünüm oluşturma
> * Veritabanını görüntüleme

## <a name="prerequisites"></a>Önkoşullar

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a>MVC web uygulaması oluşturma

1. Visual Studio 'Yu açın ve C# **ASP.NET web uygulaması (.NET Framework)** şablonunu kullanarak bir Web projesi oluşturun. Projeyi *Contosouniversity* olarak adlandırın ve **Tamam**' ı seçin.

   ![Visual Studio 'da yeni proje iletişim kutusu](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. **Yeni ASP.NET Web uygulaması-ContosoUniversity**içinde **MVC**' yi seçin.

   ![Visual Studio 'da yeni Web uygulaması iletişim kutusu](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > Varsayılan olarak, **kimlik doğrulama** seçeneği **kimlik doğrulaması yok**olarak ayarlanır. Bu öğreticide, Web uygulaması kullanıcıların oturum açmasını gerektirmez. Ayrıca, erişimi kimin oturum açanlar temelinde kısıtlayamaz.

1. Projeyi oluşturmak için **Tamam**'ı seçin.

## <a name="set-up-the-site-style"></a>Site stili Ayarla

Birkaç basit değişiklik, site menüsünü, düzeni ve giriş sayfasını ayarlar.

1. *Views\shared\\_Layout. cshtml*dosyasını açın ve aşağıdaki değişiklikleri yapın:

   - "My ASP.NET Application" ve "Application Name" gibi her bir oluşumu "Contoso Üniversitesi" olarak değiştirin.
   - Öğrenciler, kurslar, Eğitmenler ve departmanlar için menü girişleri ekleyin ve kişi girişini silin.

   Değişiklikler aşağıdaki kod parçacığında vurgulanır:

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. *Views\home\ındex.cshtml*içinde, ASP.net ve MVC hakkındaki metni bu uygulamayla ilgili metinle değiştirmek için dosyanın içeriğini aşağıdaki kodla değiştirin:

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. Web sitesini çalıştırmak için CTRL + F5 tuşlarına basın. Ana menünün bulunduğu giriş sayfasını görürsünüz.

## <a name="install-entity-framework-6"></a>Entity Framework 6 ' yı yükler

1. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.

2. **Paket Yöneticisi konsolu** penceresinde, aşağıdaki komutu girin:

   ```text
   Install-Package EntityFramework
   ```

Bu adım, Bu öğreticinin el ile yaptığınız, ancak ASP.NET MVC scafkatlama özelliği tarafından otomatik olarak gerçekleştirilen birkaç adımdan biridir. Entity Framework (EF) kullanmak için gereken adımları görebilmeniz için bunları el ile yapabilirsiniz. MVC denetleyicisi ve görünümleri oluşturmak için daha sonra yapı iskelesi kullanacaksınız. Alternatif olarak, yapı iskelesi 'nin EF NuGet paketini otomatik olarak yüklemesini, veritabanı bağlamı sınıfını oluşturmasını ve bağlantı dizesini oluşturmasını sağlar. Bu şekilde başlamaya hazırsanız, tüm yapmanız gereken adımları atlayın ve varlık sınıflarınızı oluşturduktan sonra MVC denetleyicinizi dolandırıcılara katlayın.

## <a name="create-the-data-model"></a>Veri modeli oluşturma

Daha sonra Contoso Üniversitesi uygulaması için varlık sınıfları oluşturacaksınız. Aşağıdaki üç varlıkla başlayacaksınız:

**Kurs** <-> **kayıt** <-> **öğrenci**

| Varlıklar | İlişki |
| -------- | ------------ |
| Kayıt kursu | Bire çok |
| Kayıt için öğrenci | Bire çok |

`Student` ve `Enrollment` varlıkları arasında bire çok ilişki vardır ve `Course` ile `Enrollment` varlıkları arasında bire çok bir ilişki vardır. Diğer bir deyişle, bir öğrenci herhangi bir sayıda kursa kaydedilebilir ve bir kurs, kayıtlı sayıda öğrenciye sahip olabilir.

Aşağıdaki bölümlerde, bu varlıkların her biri için bir sınıf oluşturacaksınız.

> [!NOTE]
> Projeyi bu varlık sınıflarının tümünü oluşturmayı bitirmeden önce derlemeye çalışırsanız derleyici hatalarıyla karşılaşırsınız.

### <a name="the-student-entity"></a>Öğrenci varlık

- *Modeller* klasöründe, **Çözüm Gezgini** klasöre sağ tıklayıp > **sınıfı** **Ekle** ' yi seçerek *Student.cs* adlı bir sınıf dosyası oluşturun. Şablon kodunu aşağıdaki kodla değiştirin:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` özelliği, bu sınıfa karşılık gelen veritabanı tablosunun birincil anahtar sütunu olacak. Varsayılan olarak, Entity Framework `ID` veya *classname* `ID` birincil anahtar olarak adlandırılan bir özelliği yorumlar.

`Enrollments` özelliği bir *Gezinti özelliğidir*. Gezinti özellikleri, bu varlıkla ilgili diğer varlıkları tutar. Bu durumda, bir `Student` varlığının `Enrollments` özelliği, bu `Student` varlıkla ilgili `Enrollment` varlıkların tümünü tutacaktır. Diğer bir deyişle, veritabanındaki belirli bir `Student` satırı, iki ilişkili `Enrollment` satırına sahiptir (Bu, `StudentID` yabancı anahtar sütununda öğrencinin birincil anahtar değerini içeren satırlar), bu `Student` varlığın `Enrollments` gezinti özelliği bu iki `Enrollment` varlığını içerir.

Gezinti özellikleri genellikle `virtual` olarak tanımlanır ve bu sayede, *geç yükleme*gibi belirli Entity Framework işlevsellikten yararlanabilir. (Bu serinin ilerleyen kısımlarında [Ilgili verileri okuma](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) öğreticisinde daha sonra geç yükleme açıklanmaktadır.)

Bir gezinti özelliği birden çok varlığı tutabileceiyorsa (çok-çok veya bire çok ilişkilerde olduğu gibi), türü `ICollection`gibi girişlerin eklenebileceği, silinebileceği ve güncelleştirilemeyebilir bir liste olmalıdır.

### <a name="the-enrollment-entity"></a>Kayıt varlık

- *Modeller* klasöründe *enrollment.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` özelliği birincil anahtar olacaktır; Bu varlık, `Student` varlığında gördüğünüz gibi, kendisini `ID` yerine *classname* `ID` modelini kullanır. Normalde tek bir model seçip veri modeliniz genelinde kullanabilirsiniz. Burada, değişim, her iki stili de kullanabileceğinizi gösterir. Daha sonraki bir öğreticide, `classname` olmadan `ID` kullanmanın, veri modelinde devralma uygulamayı daha kolay hale getiren bir durum görürsünüz.

`Grade` özelliği bir [sabit listesi](/ef/ef6/modeling/code-first/data-types/enums). `Grade` türü bildiriminden sonraki soru işareti, `Grade` özelliğinin [null yapılabilir](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)olduğunu gösterir. Null olan bir sınıf sıfır bir sınıfta farklılık gösterir. null, henüz bir sınıf bilinmediğini veya henüz atanmadığını belirtir.

`StudentID` özelliği bir yabancı anahtardır ve ilgili gezinti özelliği `Student`. `Enrollment` bir varlık bir `Student` varlığıyla ilişkilendirilir, bu nedenle özellik yalnızca tek bir `Student` varlığı tutabilir (daha önce gördüğünüz `Student.Enrollments` gezinti özelliğinden farklı olarak, birden çok `Enrollment` varlığı tutabilir).

`CourseID` özelliği bir yabancı anahtardır ve ilgili gezinti özelliği `Course`. Bir `Enrollment` varlığı bir `Course` varlığıyla ilişkilendirilir.

Entity Framework, *&lt;gezinti özelliği adı&gt;&lt;birincil anahtar özellik adı&gt;* (`StudentID` varlığın birincil anahtarı `Student` olduğundan `Student` gezinti özelliği için `ID`) olarak adlandırılmışsa, bir özelliği yabancı anahtar özelliği olarak yorumlar. Yabancı anahtar özelliklerine aynı zamanda *&lt;birincil anahtar özellik adı&gt;* aynı şekilde adlandırılabilir (örneğin, `Course` varlığının birincil anahtarı `CourseID`olduğundan `CourseID`).

### <a name="the-course-entity"></a>Kurs varlık

- *Modeller* klasöründe, şablon kodunu aşağıdaki kodla değiştirerek *Course.cs*oluşturun:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` özelliği bir gezinti özelliğidir. `Course` bir varlık, herhangi bir sayıda `Enrollment` varlıkla ilişkili olabilir.

Bu serinin sonraki bir öğreticide <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> özniteliği hakkında daha fazla bilgi edineceksiniz. Temel olarak bu öznitelik, veritabanının oluşturması yerine kursa ait birincil anahtarı girmenize olanak sağlar.

## <a name="create-the-database-context"></a>Veritabanı bağlamını oluşturma

Belirli bir veri modeli için Entity Framework işlevselliğini koordine eden ana sınıf *veritabanı bağlamı* sınıfıdır. Bu sınıfı [System. Data. Entity. DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx) sınıfından türeterek oluşturursunuz. Kodunuzda, veri modeline hangi varlıkların ekleneceğini belirtirsiniz. Ayrıca, belirli Entity Framework davranışlarını özelleştirebilirsiniz. Bu projede, sınıfı `SchoolContext`olarak adlandırılır.

- ContosoUniversity projesinde bir klasör oluşturmak için **Çözüm Gezgini** ' de projeye sağ tıklayın ve **Ekle**' ye ve ardından **Yeni klasör**' e tıklayın. Yeni klasörü *dal* olarak adlandırın (veri erişim katmanı için). Bu klasörde, *SchoolContext.cs*adlı yeni bir sınıf dosyası oluşturun ve şablon kodunu şu kodla değiştirin:

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>Varlık kümelerini belirtme

Bu kod, her varlık kümesi için bir [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx) özelliği oluşturur. Entity Framework terimlerinde, genellikle bir *varlık kümesi* bir veritabanı tablosuna karşılık gelir ve bir *varlık* tablodaki bir satıra karşılık gelir.

> [!NOTE]
>
> `DbSet<Enrollment>` ve `DbSet<Course>` deyimlerini atlayabilirsiniz ve aynı şekilde çalışır. Entity Framework, `Student` varlık `Enrollment` varlığına başvurduğundan ve `Enrollment` varlığı `Course` varlığına başvurduğundan bunları örtülü olarak içerebilir.

### <a name="specify-the-connection-string"></a>Bağlantı dizesini belirtin

Bağlantı dizesinin adı (daha sonra Web. config dosyasına ekleyeceğiniz) oluşturucuya geçirilir.

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

Ayrıca, Web. config dosyasında depolanan birinin adı yerine bağlantı dizesinin kendisini de geçirebilirsiniz. Kullanılacak veritabanını belirtme seçenekleri hakkında daha fazla bilgi için bkz. [bağlantı dizeleri ve modeller](/ef/ef6/fundamentals/configuring/connection-strings).

Bir bağlantı dizesi veya bir adı belirtmezseniz, Entity Framework bağlantı dizesi adının sınıf adı ile aynı olduğunu varsayar. Bu örnekteki varsayılan bağlantı dizesi adı, açıkça belirtdiklerinize göre `SchoolContext`.

### <a name="specify-singular-table-names"></a>Tekil tablo adlarını belirtin

[Onmodeloluþturma](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) yöntemindeki `modelBuilder.Conventions.Remove` deyimleri, tablo adlarının plmasını önler. Bunu yapmadıysanız, veritabanındaki oluşturulan tablolar `Students`, `Courses`ve `Enrollments`olarak adlandırılır. Bunun yerine, tablo adları `Student`, `Course`ve `Enrollment`olacaktır. Geliştiriciler tablo adlarının plmış olup olmayacağını kabul etmez. Bu öğretici tekil formunu kullanır, ancak önemli nokta bu kod satırını dahil ederek veya atlayarak tercih ettiğiniz formdan seçim yapabilirsiniz.

## <a name="initialize-db-with-test-data"></a>Test verileriyle VERITABANıNı başlatma

Entity Framework, uygulama çalışırken otomatik olarak bir veritabanı oluşturabilir (veya bırakıp yeniden oluşturabilir). Bu işlem, uygulamanız her çalıştığında veya yalnızca modelin var olan veritabanıyla eşitlenmemiş olması durumunda yapılması gerektiğini belirtebilirsiniz. Ayrıca, verileri test verileriyle doldurmak üzere veritabanını oluşturduktan sonra otomatik olarak çağıran bir `Seed` Entity Framework yöntemi yazabilirsiniz.

Varsayılan davranış yalnızca var olmayan bir veritabanı oluşturmaktır (ve model değiştirildiyse ve veritabanı zaten varsa bir özel durum oluşturur). Bu bölümde, veritabanının bırakılması ve model her değiştiğinde yeniden oluşturulması gerektiğini belirtirsiniz. Veritabanının düşürülmesi tüm verilerinizin kaybedilmesine neden olur. Bu genellikle geliştirme sırasında, `Seed` yöntemi veritabanı yeniden oluşturulduğunda çalışır ve test verilerinizi yeniden oluşturur. Ancak üretimde, her zaman veritabanı şemasını değiştirmeniz gerektiğinde tüm verilerinizi kaybetmek istemezsiniz. Daha sonra, veritabanını bırakıp yeniden oluşturmak yerine veritabanı şemasını değiştirmek için Code First Migrations kullanarak model değişikliklerini nasıl işleyeceğinizi göreceksiniz.

1. DAL klasöründe, *SchoolInitializer.cs* adlı yeni bir sınıf dosyası oluşturun ve şablon kodunu, gerektiğinde bir veritabanının oluşturulmasına neden olan aşağıdaki kodla değiştirin ve test verilerini yeni veritabanına yükler.

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   `Seed` yöntemi, bir giriş parametresi olarak veritabanı bağlamı nesnesini alır ve yöntemdeki kod, veritabanına yeni varlıklar eklemek için bu nesneyi kullanır. Her varlık türü için, kod yeni varlıkların bir koleksiyonunu oluşturur, bunları uygun `DbSet` özelliğine ekler ve değişiklikleri veritabanına kaydeder. Burada yapılan her bir varlık grubundan sonra `SaveChanges` yöntemini çağırmak gerekmez, ancak bunu yapmak, kod veritabanına yazılırken bir özel durum oluşursa bir sorunun kaynağını bulmanıza yardımcı olur.

2. Entity Framework Başlatıcı sınıfınızı kullanmasını söylemek için, aşağıdaki örnekte gösterildiği gibi uygulama *Web. config* dosyasındaki (kök proje klasöründeki) `entityFramework` öğesine bir öğe ekleyin:

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   `context type` tam bağlam sınıfı adını ve içindeki derlemeyi belirtir ve `databaseinitializer type` Başlatıcı sınıfının ve içindeki derlemenin tam adını belirtir. (EF 'in başlatıcıyı kullanmasını istemiyorsanız, `context` öğesinde bir öznitelik ayarlayabilirsiniz: `disableDatabaseInitialization="true"`.) Daha fazla bilgi için bkz. [yapılandırma dosyası ayarları](/ef/ef6/fundamentals/configuring/config-file).

   *Web. config* dosyasında başlatıcıyı ayarlamaya bir alternatif, *Global.asax.cs* dosyasındaki `Application_Start` yöntemine `Database.SetInitializer` bir ifade ekleyerek kodda kullanmaktır. Daha fazla bilgi için bkz. [Entity Framework Code First veritabanı başlatıcıları anlama](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm).

Uygulama, bir uygulamanın belirli bir çalıştırmasında veritabanına ilk kez eriştiğinizde Entity Framework, veritabanını modelle (`SchoolContext` ve varlık sınıflarınız) karşılaştırdığında bu şekilde ayarlanır. Fark varsa, uygulama veritabanını bırakır ve yeniden oluşturur.

> [!NOTE]
> Bir uygulamayı bir üretim Web sunucusuna dağıttığınızda, veritabanını bırakan ve yeniden oluşturan kodu kaldırmanız veya devre dışı bırakmanız gerekir. Bu, bu serinin sonraki bir öğreticide bunu yapacaksınız.

## <a name="set-up-ef-6-to-use-localdb"></a>LocalDB kullanmak için EF 6 ayarlama

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017) , SQL Server Express veritabanı altyapısının basit bir sürümüdür. Yüklemek ve yapılandırmak kolaydır, isteğe bağlı olarak başlar ve kullanıcı modunda çalışır. LocalDB, veritabanlarıyla *. mdf* dosyaları olarak çalışmanıza olanak sağlayan SQL Server Express özel bir yürütme modunda çalışır. Veritabanını projeyle kopyalayabilmek istiyorsanız, Web projesinin *App\_Data* klasörüne LocalDB veritabanı dosyalarını koyabilirsiniz. SQL Server Express ' deki Kullanıcı örneği özelliği ayrıca *. mdf* dosyalarıyla çalışmanıza olanak sağlar ancak kullanıcı örneği özelliği kullanım dışıdır; Bu nedenle, LocalDB *. mdf* dosyalarıyla çalışma için önerilir. LocalDB, Visual Studio ile varsayılan olarak yüklenir.

Genellikle, SQL Server Express üretim Web uygulamaları için kullanılmaz. LocalDB 'nin IIS ile çalışmak üzere tasarlanmadığı için, bir Web uygulamasıyla üretim kullanımı önerilmez.

- Bu öğreticide LocalDB ile çalışacaksınız. Uygulama *Web. config* dosyasını açın ve aşağıdaki örnekte gösterildiği gibi `appSettings` öğesinden önce bir `connectionStrings` öğesi ekleyin. ( *Web. config* dosyasını kök proje klasöründe güncelleştirdiğinizden emin olun. Ayrıca, *Görünümler* alt klasöründe, güncelleştirmeniz gerekmeyen bir *Web. config* dosyası da vardır.)

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

Eklediğiniz bağlantı dizesi Entity Framework, *ContosoUniversity1. mdf*adlı bir LocalDB veritabanı kullanacağınızı belirtir. (Veritabanı henüz yok ancak EF onu oluşturacak.) Veritabanını *App\_veri* klasörünüzde oluşturmak istiyorsanız bağlantı dizesine `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` ekleyebilirsiniz. Bağlantı dizeleri hakkında daha fazla bilgi için bkz. [ASP.NET Web uygulamaları için SQL Server bağlantı dizeleri](/previous-versions/aspnet/jj653752(v=vs.110)).

Aslında *Web. config* dosyasında bir bağlantı dizesine ihtiyacınız yoktur. Bir bağlantı dizesi vermezseniz Entity Framework, bağlam sınıfınızı temel alan varsayılan bir bağlantı dizesi kullanır. Daha fazla bilgi için bkz. [Yeni bir veritabanına Code First](/ef/ef6/modeling/code-first/workflows/new-database).

## <a name="create-controller-and-views"></a>Denetleyici ve görünüm oluşturma

Artık verileri göstermek için bir Web sayfası oluşturacaksınız. Verileri isteme işlemi, veritabanının oluşturulmasını otomatik olarak tetikler. Yeni bir denetleyici oluşturarak başlarsınız. Ancak bunu yapmadan önce modeli ve bağlam sınıflarını MVC denetleyici yapı iskelesi için kullanılabilir hale getirmek için projeyi derleyin.

1. **Çözüm Gezgini**' de **denetleyiciler** klasörüne sağ tıklayın, **Ekle**' yi seçin ve ardından **yeni yapı iskelesi öğesine**tıklayın.
2. **Yapı Iskelesi Ekle** iletişim kutusunda, **Entity Framework kullanarak, görünümler Içeren MVC 5 denetleyici**' yi seçin ve ardından **Ekle**' yi seçin.

     ![Visual Studio 'da Scaffold iletişim kutusu ekleme](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. **Denetleyici Ekle** iletişim kutusunda aşağıdaki seçimleri yapın ve ardından **Ekle**' yi seçin:

   - Model Sınıfı: **öğrenci (ContosoUniversity. modeller)** . (Açılan listede bu seçeneği görmüyorsanız projeyi derleyin ve yeniden deneyin.)
   - Veri bağlamı sınıfı: **SchoolContext (ContosoUniversity. dal)** .
   - Denetleyici adı: **Studentcontroller** (StudentsController).
   - Diğer alanlar için varsayılan değerleri bırakın.

     **Ekle**' ye tıkladığınızda, desteği bir *StudentController.cs* dosyası ve denetleyicisiyle birlikte çalışan bir dizi görünüm ( *. cshtml* dosyası) oluşturur. Entity Framework kullanan projeler oluşturduğunuzda, scaffolder 'ın bazı ek işlevlerinden de yararlanabilirsiniz: ilk model sınıfınızı oluşturma, bağlantı dizesi oluşturma ve ardından **Denetleyici Ekle** kutusunda **veri bağlam sınıfının**yanındaki **+** düğmesini seçerek **Yeni veri bağlamı** belirtme. Desteği, `DbContext` sınıfınızı ve Bağlantı dizenizi, ayrıca denetleyiciyi ve görünümleri oluşturacaktır.
4. Visual Studio, *Controllers\studentcontroller.cs* dosyasını açar. Bir veritabanı bağlamı nesnesini örnekleyen bir sınıf değişkeninin oluşturulduğunu görürsünüz:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` Action yöntemi, veritabanı bağlamı örneğinin `Students` özelliğini okuyarak *öğrenciler* varlık kümesinden öğrencilerin bir listesini alır:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     *Student\ındex.cshtml* görünümü bu listeyi bir tabloda görüntüler:

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. Projeyi çalıştırmak için CTRL + F5 tuşlarına basın. ("Gölge kopya oluşturulamıyor" hatası alırsanız, tarayıcıyı kapatın ve yeniden deneyin.)

     `Seed` yönteminin eklendiği test verilerini görmek için **öğrenciler** sekmesine tıklayın. Tarayıcı pencerenizin ne kadar dar olduğuna bağlı olarak, üst adres çubuğunda öğrenci sekmesi bağlantısını görürsünüz veya bağlantıyı görmek için sağ üst köşeye tıklamanız gerekir.

     ![Menü düğmesi](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a>Veritabanını görüntüleme

Öğrenciler sayfasını çalıştırdığınızda ve uygulama veritabanına erişmeyi denediğinde, bir veritabanı olmadığını ve bir tane oluşturduğunu tespit edin. EF daha sonra veritabanını verilerle doldurmak için çekirdek yöntemini çalıştırdı.

Visual Studio 'da veritabanını görüntülemek için **Sunucu Gezgini** ya da **SQL Server Nesne Gezgini** (ssox) kullanabilirsiniz. Bu öğretici için **Sunucu Gezgini**kullanacaksınız.

1. Tarayıcıyı kapatın.
2. **Sunucu Gezgini**, **veri bağlantıları** ' nı genişletin (önce Yenile düğmesini seçmeniz gerekebilir), **okul bağlamını (contosouniversity)** genişletin ve sonra **tabloları genişleterek yeni veritabanınızdaki tabloları görebilirsiniz** .

3. Oluşturulan sütunları ve tabloya eklenmiş satırları görmek için **öğrenci** tablosuna sağ tıklayın ve **tablo verilerini göster** ' e tıklayın.

4. **Sunucu Gezgini** bağlantısını kapatın.

*ContosoUniversity1. mdf* ve *. ldf* veritabanı dosyaları *% USERPROFILE%* klasöründedir.

`DropCreateDatabaseIfModelChanges` başlatıcısı kullandığınızdan, artık `Student` sınıfında bir değişiklik yapabilirsiniz, uygulamayı yeniden çalıştırabilirsiniz ve veritabanı, değişikliklerinizi eşleştirmek için otomatik olarak yeniden oluşturulur. Örneğin, `Student` sınıfına bir `EmailAddress` özelliği eklerseniz, öğrenciler sayfasını yeniden çalıştırın ve ardından tabloya bir daha göz atın, yeni bir `EmailAddress` sütunu görürsünüz.

## <a name="conventions"></a>Kurallar

*Kurallar*nedeniyle en az bir veritabanı oluşturmak için Entity Framework yazmanız gereken kod miktarı veya Entity Framework varsayımlar sağlar. Bunlardan bazıları zaten belirtilmiştir veya farkında olmadıklarınız olmadan kullanılmıştır:

- Varlık sınıfı adlarının plurar biçimleri tablo adı olarak kullanılır.
- Varlık özelliği adları, sütun adları için kullanılır.
- `ID` veya *classname* `ID` adlı varlık özellikleri birincil anahtar özellikler olarak tanınır.
- Bir özellik, bir yabancı anahtar özelliği olarak yorumlanır *&lt;gezinti özelliği adı&gt;&lt;birincil anahtar özellik adı&gt;* (örneğin, `StudentID`, birincil anahtarı `Student` olduğundan `Student` gezinti özelliği için `ID`). Yabancı anahtar özelliklerine aynı zamanda &lt;birincil anahtar özellik adı&gt; aynı şekilde adlandırılabilir (örneğin, `Enrollment` varlığının birincil anahtarı `EnrollmentID`olduğundan `EnrollmentID`).

Kuralların geçersiz kılınabileceğini gördünüz. Örneğin, tablo adlarının plurulmamalıdır ve daha sonra bir özelliği bir yabancı anahtar özelliği olarak nasıl açıkça işaretleneceğini göreceksiniz.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

EF 6 hakkında daha fazla bilgi için şu makalelere bakın:

* [ASP.NET Veri Erişimi - Önerilen Kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md)

* [Code First kuralları](/ef/ef6/modeling/code-first/conventions/built-in)

* [Daha Karmaşık Bir Veri Modeli Oluşturma](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * MVC web uygulaması oluşturuldu
> * Site stili Ayarla
> * Entity Framework yüklendi 6
> * Veri modeli oluşturuldu
> * Veritabanı bağlamı oluşturuldu
> * Test verileriyle VERITABANı başlatıldı
> * LocalDB kullanmak için EF 6 ayarlama
> * Denetleyici ve görünümler oluşturuldu
> * Veritabanı görüntüleniyor

Denetleyicilerinizdeki ve görünümlerindeki oluşturma, okuma, güncelleştirme, silme (CRUD) kodunu incelemeyi ve özelleştirmeyi öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Temel CRUD işlevlerini uygulama](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)