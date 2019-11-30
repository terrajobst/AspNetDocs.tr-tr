---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: ASP.NET MVC uygulaması için Entity Framework veri modeli oluşturma (1/10) | Microsoft Docs
author: tdykstra
description: Visual Studio 2013, Entity Framework 6 ve MVC 5 için bu öğretici serisinin daha yeni bir sürümü kullanılabilir. Contoso Üniversitesi örnek Web uygulaması da...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8ee5aa22b6b2329b01d41437f30508e28a2288b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595966"
---
# <a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>ASP.NET MVC uygulaması için Entity Framework veri modeli oluşturma (1/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > Visual Studio 2013, Entity Framework 6 ve MVC 5 için [Bu öğretici serisinin daha yeni bir sürümü](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) kullanılabilir.
> 
> 
> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 ve Visual Studio 2012 kullanılarak ASP.NET MVC 4 uygulamalarının nasıl oluşturulacağını gösterir. Örnek uygulama, kurgusal bir Contoso Üniversitesi için bir Web sitesidir. Öğrenci giriş, kurs oluşturma ve eğitmen atamaları gibi işlevleri içerir. Bu öğretici serisinde, Contoso Üniversitesi örnek uygulamasının nasıl oluşturulacağı açıklanmaktadır. [Tamamlanmış uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8).
> 
> ## <a name="code-first"></a>Code First
> 
> Entity Framework verilerle çalışmak için üç yol vardır: *Database First*, *model First*ve *Code First*. Bu öğretici Code First içindir. Bu iş akışları arasındaki farklar ve senaryonuz için en uygun olanı seçme hakkında daha fazla bilgi için bkz. [Entity Framework geliştirme Iş akışları](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="mvc"></a>MVC
> 
> Örnek uygulama, [ASP.NET MVC](../../../index.md)üzerine kurulmuştur. ASP.NET Web Forms modeliyle çalışmayı tercih ediyorsanız, [model bağlama ve Web Forms](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md) öğretici serisi ve [ASP.NET veri erişimi içerik haritasına](../../../../whitepapers/aspnet-data-access-content-map.md)bakın.
> 
> ## <a name="software-versions"></a>Yazılım sürümleri
> 
> | **Öğreticide gösterilen** | **İle de birlikte çalışarak** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | Web için Visual Studio 2012 Express. Bu, Web için VS 2012 veya VS 2012 Express henüz yoksa Windows Azure SDK tarafından otomatik olarak yüklenir. Visual Studio 2013 çalışır, ancak öğretici onunla test edilmemiştir ve bazı menü seçimleri ve iletişim kutuları farklıdır. Windows Azure dağıtımı için [Windows Azure SDK 'Sının VS 2013 sürümü](https://go.microsoft.com/fwlink/p/?linkid=323510) gereklidir. |
> | .NET 4.5 | Gösterilen özelliklerin çoğu .NET 4 ' te çalışır, ancak bazıları bu şekilde çalışmaz. Örneğin, EF 'teki enum desteği .NET 4,5 gerektirir. |
> | Entity Framework 5 |  |
> | [Microsoft Azure SDK 2,1](https://go.microsoft.com/fwlink/p/?linkid=323511) | Windows Azure dağıtım adımlarını atlarsanız SDK 'ya ihtiyacınız yoktur. SDK 'nın yeni bir sürümü kullanıma sunulduktan sonra bağlantı daha yeni sürümü yükler. Bu durumda, bazı yönergeleri yeni kullanıcı arabirimi ve özelliklere uyarlamanız gerekebilir. |
> 
> ## <a name="questions"></a>UL
> 
> Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx), [Entity Framework ve LINQ to Entities forumuna](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.
> 
> ## <a name="acknowledgments"></a>Bilgilendirme
> 
> Bildirimler için serideki son öğreticiye [ve vb hakkında bir nota](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)bakın.
> 
> ## <a name="original-version-of-the-tutorial"></a>Öğreticinin orijinal sürümü
> 
> Öğreticinin orijinal sürümü [EF 4,1/MVC 3 e-book](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)' da kullanılabilir.

## <a name="the-contoso-university-web-application"></a>Contoso Üniversitesi web uygulaması

Bu öğreticilerde oluşturacağınız uygulama basit bir üniversite web sitesidir.

Kullanıcılar öğrenci, kurs ve eğitmen bilgilerini görüntüleyebilir ve güncelleştirebilir. Oluşturacağınız ekranların bazıları aşağıda verilmiştir.

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

Bu sitenin kullanıcı arabirimi stili, yerleşik şablonlar tarafından üretilerek, öğreticinin Entity Framework kullanımı konusunda temel olarak odaklanabilmesi için, yerleşik şablonlar tarafından üretilmeden yakın tutulur.

## <a name="prerequisites"></a>Prerequisites

Bu öğreticideki yönergeler ve ekran görüntüleri, .NET için [Visual studio 2012](https://www.microsoft.com/visualstudio/eng/downloads) veya [Visual Studio 2012 Express](https://go.microsoft.com/fwlink/?LinkID=275131)kullandığınızı, 2013 Haziran ayında .NET için en son güncelleştirme ve Azure SDK 'sını kullandığınızı varsayar. Bunu aşağıdaki bağlantıyı kullanarak edinebilirsiniz:

[.NET için Azure SDK (Visual Studio 2012)](https://go.microsoft.com/fwlink/?LinkId=254364)

Visual Studio yüklüyse, yukarıdaki bağlantıda eksik bileşenler yüklenir. Visual Studio yoksa, bu bağlantı Web için Visual Studio 2012 Express 'i yükler. Visual Studio 2013 kullanabilirsiniz, ancak bazı gerekli yordamlar ve ekranlar farklı olur.

## <a name="create-an-mvc-web-application"></a>MVC web uygulaması oluşturma

Visual Studio 'Yu açın ve C# **ASP.NET MVC 4 Web uygulaması** şablonunu kullanarak "contosouniversity" adlı yeni bir proje oluşturun. **.NET Framework 4,5** ' i hedeflediğinizden emin olun ( [`enum` özellikleri](https://msdn.microsoft.com/data/hh859576.aspx)kullanıyorsunuz ve .NET 4,5 gerektirir).

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

**Yeni ASP.NET MVC 4 projesi** Iletişim kutusunda **Internet uygulaması** şablonunu seçin.

**Razor** görünüm altyapısını seçili bırakın ve **birim testi projesi oluştur** onay kutusunu işaretsiz bırakın.

**Tamam**'a tıklayın.

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>Site stilini ayarlayın

Birkaç basit değişiklik, site menüsünü, düzeni ve giriş sayfasını ayarlar.

*Views\shared\\_Layout. cshtml*dosyasını açın ve dosyanın içeriğini aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

Bu kod aşağıdaki değişiklikleri yapar:

- "My ASP.NET MVC uygulaması" ve "logonuz" adlı şablon örneklerini "Contoso Üniversitesi" ile değiştirir.
- Öğreticide daha sonra kullanılacak çeşitli eylem bağlantıları ekler.

*Views\home\ındex.cshtml*içinde, ASP.net ve MVC hakkındaki şablon paragraflarını ortadan kaldırmak için dosyanın içeriğini aşağıdaki kodla değiştirin:

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

*Controllers\homecontroller.cs*içinde, aşağıdaki örnekte gösterildiği gibi, `Index` eylemi yönteminde `ViewBag.Message` değerini "Contoso University 'e hoş geldiniz" olarak değiştirin:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

Siteyi çalıştırmak için CTRL + F5 tuşlarına basın. Ana menünün bulunduğu giriş sayfasını görürsünüz.

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>Veri modeli oluşturma

Daha sonra Contoso Üniversitesi uygulaması için varlık sınıfları oluşturacaksınız. Aşağıdaki üç varlıkla başlayacaksınız:

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

`Student` ve `Enrollment` varlıkları arasında bire çok ilişki vardır ve `Course` ile `Enrollment` varlıkları arasında bire çok bir ilişki vardır. Diğer bir deyişle, bir öğrenci herhangi bir sayıda kursa kaydedilebilir ve bir kurs, kayıtlı sayıda öğrenciye sahip olabilir.

Aşağıdaki bölümlerde, bu varlıkların her biri için bir sınıf oluşturacaksınız.

> [!NOTE]
> Projeyi bu varlık sınıflarının tümünü oluşturmayı bitirmeden önce derlemeye çalışırsanız derleyici hatalarıyla karşılaşırsınız.

### <a name="the-student-entity"></a>Öğrenci varlığı

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

*Modeller* klasöründe *Student.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` özelliği, bu sınıfa karşılık gelen veritabanı tablosunun birincil anahtar sütunu olacak. Varsayılan olarak, Entity Framework `ID` veya *classname* `ID` birincil anahtar olarak adlandırılan bir özelliği yorumlar.

`Enrollments` özelliği bir *Gezinti özelliğidir*. Gezinti özellikleri, bu varlıkla ilgili diğer varlıkları tutar. Bu durumda, bir `Student` varlığının `Enrollments` özelliği, bu `Student` varlıkla ilgili `Enrollment` varlıkların tümünü tutacaktır. Diğer bir deyişle, veritabanındaki belirli bir `Student` satırı, iki ilişkili `Enrollment` satırına sahiptir (Bu, `StudentID` yabancı anahtar sütununda öğrencinin birincil anahtar değerini içeren satırlar), bu `Student` varlığın `Enrollments` gezinti özelliği bu iki `Enrollment` varlığını içerir.

Gezinti özellikleri genellikle `virtual` olarak tanımlanır ve bu sayede, *geç yükleme*gibi belirli Entity Framework işlevsellikten yararlanabilir. (Geç yükleme daha sonra bu serinin ilerleyen bölümlerinde [Ilgili verileri okuma](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) öğreticisinde açıklanacaktır.

Bir gezinti özelliği birden çok varlığı tutabileceiyorsa (çok-çok veya bire çok ilişkilerde olduğu gibi), türü `ICollection`gibi girişlerin eklenebileceği, silinebileceği ve güncelleştirilemeyebilir bir liste olmalıdır.

### <a name="the-enrollment-entity"></a>Kayıt varlığı

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

*Modeller* klasöründe *enrollment.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

Sınıf özelliği bir [sabit listesi](https://msdn.microsoft.com/data/hh859576.aspx). `Grade` türü bildiriminden sonraki soru işareti, `Grade` özelliğinin [null yapılabilir](https://msdn.microsoft.com/library/2cf62fcy.aspx)olduğunu gösterir. Null olan bir sınıf sıfır bir sınıfta farklılık gösterir. null, henüz bir sınıf bilinmediğini veya henüz atanmadığını belirtir.

`StudentID` özelliği bir yabancı anahtardır ve ilgili gezinti özelliği `Student`. `Enrollment` bir varlık bir `Student` varlığıyla ilişkilendirilir, bu nedenle özellik yalnızca tek bir `Student` varlığı tutabilir (daha önce gördüğünüz `Student.Enrollments` gezinti özelliğinden farklı olarak, birden çok `Enrollment` varlığı tutabilir).

`CourseID` özelliği bir yabancı anahtardır ve ilgili gezinti özelliği `Course`. Bir `Enrollment` varlığı bir `Course` varlığıyla ilişkilendirilir.

### <a name="the-course-entity"></a>Kurs varlığı

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

*Modeller* klasöründe, mevcut kodu şu kodla değiştirerek *Course.cs*oluşturun:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` özelliği bir gezinti özelliğidir. `Course` bir varlık, herhangi bir sayıda `Enrollment` varlıkla ilişkili olabilir.

[[Databasegenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)([DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)) hakkında daha fazla bilgi edineceksiniz. None)] bir sonraki öğreticide özniteliği. Temel olarak bu öznitelik, veritabanının oluşturması yerine kursa ait birincil anahtarı girmenize olanak sağlar.

## <a name="create-the-database-context"></a>Veritabanı bağlamını oluşturma

Belirli bir veri modeli için Entity Framework işlevselliğini koordine eden ana sınıf *veritabanı bağlamı* sınıfıdır. Bu sınıfı [System. Data. Entity. DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) sınıfından türeterek oluşturursunuz. Kodunuzda, veri modeline hangi varlıkların ekleneceğini belirtirsiniz. Ayrıca, belirli Entity Framework davranışlarını özelleştirebilirsiniz. Bu projede, sınıfı `SchoolContext`olarak adlandırılır.

*Dal* adlı bir klasör oluşturun (veri erişim katmanı için). Bu klasörde, *SchoolContext.cs*adlı yeni bir sınıf dosyası oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

Bu kod, her varlık kümesi için bir [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx) özelliği oluşturur. Entity Framework terimlerinde, genellikle bir *varlık kümesi* bir veritabanı tablosuna karşılık gelir ve bir *varlık* tablodaki bir satıra karşılık gelir.

[Onmodeloluþturma](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx) yöntemindeki `modelBuilder.Conventions.Remove` deyimleri, tablo adlarının plmasını önler. Bunu yapmadıysanız, oluşturulan tablolar `Students`, `Courses`ve `Enrollments`olarak adlandırılır. Bunun yerine, tablo adları `Student`, `Course`ve `Enrollment`olacaktır. Geliştiriciler tablo adlarının plmış olup olmayacağını kabul etmez. Bu öğretici tekil formunu kullanır, ancak önemli nokta bu kod satırını dahil ederek veya atlayarak tercih ettiğiniz formdan seçim yapabilirsiniz.

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx) , kullanıcı modunda isteğe bağlı ve çalışır durumda başlayan SQL Server Express veritabanı altyapısının hafif bir sürümüdür. LocalDB, veritabanlarıyla *. mdf* dosyaları olarak çalışmanıza olanak sağlayan SQL Server Express özel bir yürütme modunda çalışır. Genellikle, LocalDB veritabanı dosyaları bir Web projesinin *App\_Data* klasöründe tutulur. SQL Server Express ' deki Kullanıcı örneği özelliği ayrıca *. mdf* dosyalarıyla çalışmanıza olanak sağlar ancak kullanıcı örneği özelliği kullanım dışıdır; Bu nedenle, LocalDB *. mdf* dosyalarıyla çalışma için önerilir.

Genellikle SQL Server Express üretim Web uygulamaları için kullanılmaz. LocalDB 'nin IIS ile çalışmak üzere tasarlanmadığı için, bir Web uygulamasıyla üretim kullanımı önerilmez.

Visual Studio 2012 ve sonraki sürümlerinde, LocalDB varsayılan olarak Visual Studio ile yüklenir. Visual Studio 2010 ve önceki sürümlerde SQL Server Express (LocalDB olmadan), Visual Studio ile varsayılan olarak yüklenir; Visual Studio 2010 kullanıyorsanız el ile yüklemelisiniz.

Bu öğreticide, veritabanının *App\_Data* klasöründe bir *. mdf* dosyası olarak depolanabilmesi için LocalDB ile birlikte çalışacaksınız. Kök *Web. config* dosyasını açın ve aşağıdaki örnekte gösterildiği gibi `connectionStrings` koleksiyonuna yeni bir bağlantı dizesi ekleyin. ( *Web. config* dosyasını kök proje klasöründe güncelleştirdiğinizden emin olun. Ayrıca, güncelleştirilmesi gerekmeyen *Görünümler* alt klasöründe bir *Web. config* dosyası bulunmaktadır.)

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

Entity Framework, varsayılan olarak, `DbContext` sınıfıyla aynı adlı bir bağlantı dizesi arar (`SchoolContext` bu proje için). Eklediğiniz bağlantı dizesi, *App\_Data* klasöründe bulunan *contosouniversity. mdf* adlı bir LocalDB veritabanını belirtir. Daha fazla bilgi için bkz. [ASP.NET Web uygulamaları Için bağlantı dizelerini SQL Server](https://msdn.microsoft.com/library/jj653752.aspx).

Aslında bağlantı dizesini belirtmeniz gerekmez. Bir bağlantı dizesi vermezseniz Entity Framework sizin için bir tane oluşturur; Ancak, veritabanı uygulamanızın *app\_Data* klasöründe olmayabilir. Veritabanının oluşturulacağı hakkında bilgi için, bkz. [Yeni bir veritabanına Code First](https://msdn.microsoft.com/data/jj193542).

`connectionStrings` koleksiyonda ayrıca, üyelik veritabanı için kullanılan `DefaultConnection` adlı bir bağlantı dizesi vardır. Bu öğreticide üyelik veritabanını kullanmayacağız. İki bağlantı dizesi arasındaki tek fark veritabanı adı ve ad özniteliği değeridir.

## <a name="set-up-and-execute-a-code-first-migration"></a>Code First geçişini ayarlama ve yürütme

Bir uygulamayı geliştirmeye ilk kez başladığınızda, veri modeliniz sıklıkla değişir ve model her değiştiğinde, veritabanı ile eşitlenmemiş olur. Veri modelini her değiştirişinizde veritabanını otomatik olarak bırakıp yeniden oluşturmak için Entity Framework yapılandırabilirsiniz. Test verileri kolayca yeniden oluşturulduğundan bu bir sorun değildir, ancak üretime dağıtıldıktan sonra veritabanını bırakmadan veritabanı şemasını güncelleştirmek istersiniz. Geçişler özelliği Code First veritabanını bırakıp yeniden oluşturmadan güncelleştirilmesini sağlar. Yeni bir projenin geliştirme döngüsünün başlarında, her modelin her değiştirilişinde veritabanını bırakmak, yeniden oluşturmak ve yeniden çekirdek yapmak için [Dropcreatedatabaseifmodelchanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx) kullanmak isteyebilirsiniz. Uygulamanızı dağıtmaya hazırsanız geçiş yaklaşımına dönüştürebilirsiniz. Bu öğreticide yalnızca geçişleri kullanacaksınız. Daha fazla bilgi için bkz. [Code First Migrations](https://msdn.microsoft.com/data/jj591621) ve [geçişleri ekran kaydı serisi](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx).

### <a name="enable-code-first-migrations"></a>Code First Migrations etkinleştir

1. **Araçlar** menüsünde, **NuGet Paket Yöneticisi** ' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. `PM>` istemine şu komutu girin:

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![geçişleri Etkinleştir komutu](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    Bu komut, ContosoUniversity projesinde bir *geçişler* klasörü oluşturur ve bu klasöre geçişleri yapılandırmak için düzenleyebileceğiniz bir *Configuration.cs* dosyası koyar.

    ![Geçişler klasörü](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    `Configuration` sınıfı, veritabanı oluşturulduğunda ve bir veri modeli değişikliğinden sonra her güncelleştirildiği zaman çağrılan bir `Seed` yöntemi içerir.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    Bu `Seed` yönteminin amacı, test verilerini Code First oluşturduktan veya güncelleştirdikten sonra veritabanına ekleme olanağı sağlamaktır.

### <a name="set-up-the-seed-method"></a>Çekirdek yöntemi ayarlama

[Çekirdek](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yöntemi, Code First Migrations veritabanını oluşturduğunda ve veritabanını en son geçişe her güncelleştirilişinde çalışır. Çekirdek yönteminin amacı, uygulama veritabanına ilk kez erişmeden önce tablolarınıza veri ekleme olanağı sağlamaktır.

Önceki Code First sürümlerinde, geçişler yayınlanmadan önce, geliştirme sırasında her model değiştikçe, veritabanının tamamen silinmesi ve sıfırdan yeniden oluşturulması gerekiyordu çünkü bu, test verilerini eklemek için `Seed` metotlarından yaygındır. Code First Migrations ile test verileri, veritabanı değişikliklerinden sonra tutulur, bu nedenle [temel](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yöntemde test verilerinin dahil edilmesi genellikle gerekli değildir. Aslında, `Seed` yöntemi üretimde çalışacağı için veritabanını üretime dağıtmak üzere geçişler kullanacaksanız, `Seed` yönteminin test verileri eklemesini istemezsiniz. Bu durumda, `Seed` yönteminin yalnızca üretime eklenmesini istediğiniz verileri veritabanına eklemesini istersiniz. Örneğin, uygulama üretimde kullanılabilir hale geldiğinde, veritabanının `Department` tablosuna gerçek bölüm adlarını içermesini isteyebilirsiniz.

Bu öğreticide, dağıtım için geçişler kullanacaksınız, ancak `Seed` yöntemi test verilerini el ile çok sayıda veri eklemek zorunda kalmadan nasıl çalıştığını görmenizi kolaylaştırmak için de test verileri ekleyecektir.

1. *Configuration.cs* dosyasının içeriğini aşağıdaki kodla değiştirin ve bu, test verilerini yeni veritabanına yükler. 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    [Çekirdek](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) yöntemi, veritabanı bağlamı nesnesini bir giriş parametresi olarak alır ve yöntemdeki kod bu nesneyi veritabanına yeni varlıklar eklemek için kullanır. Her varlık türü için, kod yeni varlıkların bir koleksiyonunu oluşturur, bunları uygun [Dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) özelliğine ekler ve değişiklikleri veritabanına kaydeder. Burada yapılan her bir varlık grubundan sonra [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) yöntemini çağırmak gerekmez, ancak bu, kod veritabanına yazılırken bir özel durum oluşursa bir sorunun kaynağını bulmanıza yardımcı olur.

    Veri ekleyen deyimlerden bazıları, "upsert" bir işlem gerçekleştirmek için [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) yöntemini kullanır. `Seed` yöntemi her geçişte çalıştığı için, eklemeye çalıştığınız satırlar veritabanını oluşturan ilk geçişten sonra zaten mevcut olacağı için yalnızca veri ekleyemezsiniz. "Upsert" işlemi, zaten var olan bir satır eklemeye çalışırsanız, ancak uygulamayı test ederken yapmış olduğunuz verilerde yapılan değişiklikleri ***geçersiz kılar*** . Bazı tablolardaki test verileri ile bu durum oluşmasını istemeyebilirsiniz: bazı durumlarda verileri değiştirirken değişiklikler veritabanı güncelleştirmelerinden sonra kalmasını istiyor. Bu durumda, bir koşullu ekleme işlemi yapmak istiyorsanız, yalnızca mevcut değilse bir satır ekleyin. Çekirdek yöntemi her iki yaklaşımı kullanır.

    [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) metoduna geçirilen ilk parametre, bir satırın zaten var olup olmadığını denetlemek için kullanılacak özelliği belirtir. Sağladınız test öğrenci verileri için, listedeki her bir ad benzersiz olduğundan bu amaçla `LastName` özelliği kullanılabilir:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    Bu kod, son adların benzersiz olduğunu varsayar. Yinelenen son ada sahip bir öğrenci el ile eklerseniz, bir sonraki geçiş işlemi yaptığınızda aşağıdaki özel durumu alırsınız.

    Sıra birden fazla öğe içeriyor

    `AddOrUpdate` yöntemi hakkında daha fazla bilgi için bkz. Julie Lerman 'ın blogundan [EF 4,3 AddOrUpdate yöntemiyle dikkatli olunmalıdır](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/) .

    `Enrollment` varlıkları ekleyen kod `AddOrUpdate` metodunu kullanmaz. Bir varlığın zaten var olup olmadığını denetler ve varlık yoksa varlığı ekler. Bu yaklaşım, geçişler çalıştırıldığında bir kayıt durumunda yaptığınız değişiklikleri korur. Kod `Enrollment`[listesinin](https://msdn.microsoft.com/library/6sh2ey19.aspx) her bir üyesi boyunca döngü yapar ve kayıt veritabanında bulunamazsa kaydı veritabanına ekler. Veritabanını ilk güncelleştirdiğinizde, veritabanı boş olur, bu nedenle her bir kayıt eklenir.

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    `Seed` yönteminde hata ayıklama ve "Alexander Carson" adlı iki öğrenci gibi gereksiz verileri işleme hakkında daha fazla bilgi için, bkz. Rick Anderson 'ın blogu üzerinde [dağıtım ve hata ayıklama Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) .
2. Projeyi oluşturun.

### <a name="create-and-execute-the-first-migration"></a>Ilk geçişi oluşturma ve yürütme

1. Paket Yöneticisi konsolu penceresinde aşağıdaki komutları girin: 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration` komutu, veritabanını oluşturan kodu içeren bir *[dateStamp]\_InitialCreate.cs* dosyası geçişleri klasörüne ekler. İlk parametre (`InitialCreate)` dosya adı için kullanılır ve istediğiniz her şey olabilir; genellikle geçiş sırasında nelerin yapıldığını özetleyen bir sözcük veya tümcecik seçersiniz. Örneğin, daha sonraki bir geçişe &quot;AddDepartmentTable&quot;adını yazabilirsiniz.

    ![İlk geçiş ile geçişler klasörü](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `InitialCreate` sınıfının `Up` yöntemi, veri modeli varlık kümelerine karşılık gelen veritabanı tablolarını oluşturur ve `Down` yöntemi onları siler. Geçişler, bir geçiş için veri modeli değişikliklerini uygulamak üzere `Up` yöntemini çağırır. Güncelleştirmeyi geri almak için bir komut girdiğinizde, geçişler `Down` yöntemini çağırır. Aşağıdaki kod `InitialCreate` dosyanın içeriğini gösterir:

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    `update-database` komutu veritabanını oluşturmak için `Up` yöntemini çalıştırır ve sonra veritabanını doldurmak için `Seed` metodunu çalıştırır.

Veri modeliniz için bir SQL Server veritabanı oluşturuldu. Veritabanı adı *Contosouniversity*'dir ve *. mdf* dosyası, bağlantı dizeniz içinde Belirtidikleriniz olduğundan projenizin *App\_Data* klasöründedir.

Visual Studio 'da veritabanını görüntülemek için **Sunucu Gezgini** ya da **SQL Server Nesne Gezgini** (ssox) kullanabilirsiniz. Bu öğreticide **Sunucu Gezgini**kullanacaksınız. Web için Visual Studio Express 2012 ' de **Sunucu Gezgini** **veritabanı Gezgini**olarak adlandırılır.

1. **Görünüm** menüsünden **Sunucu Gezgini**' ye tıklayın.
2. **Bağlantı ekle** simgesine tıklayın.

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. **Veri kaynağı seç** iletişim kutusunda istenirse, **Microsoft SQL Server**' a ve ardından **devam**' a tıklayın.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. **Bağlantı ekle** Iletişim kutusunda **sunucu adı**için **(LocalDB) \v11.0** girin. **Bir veritabanı adı Seç veya gir**altında **contosouniversity** ' i seçin.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. **Tamam**'a tıklayın.
6. **SchoolContext** öğesini genişletin ve ardından **Tablolar**' ı genişletin.  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. Oluşturulan sütunları ve tabloya eklenmiş satırları görmek için **öğrenci** tablosuna sağ tıklayın ve **tablo verilerini göster** ' e tıklayın.

    ![Öğrenci tablosu](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>Öğrenci denetleyicisi ve görünümleri oluşturma

Sonraki adım, uygulamanızda bu tablolardan biriyle çalışan bir ASP.NET MVC denetleyicisi ve görünümleri oluşturmaktır.

1. `Student` denetleyicisi oluşturmak için, **Çözüm Gezgini**içindeki **denetleyiciler** klasörüne sağ tıklayın, **Ekle**' yi seçin ve ardından **Denetleyici**' ye tıklayın. **Denetleyici Ekle** iletişim kutusunda aşağıdaki seçimleri yapın ve ardından **Ekle**' ye tıklayın: 

   - Denetleyici adı: **Studentcontroller**.
   - Şablon: **Entity Framework kullanarak okuma/yazma eylemleri ve görünümleri olan MVC denetleyicisi**.
   - Model Sınıfı: **öğrenci (ContosoUniversity. modeller)** . (Açılan listede bu seçeneği görmüyorsanız projeyi derleyin ve yeniden deneyin.)
   - Veri bağlamı sınıfı: **SchoolContext (ContosoUniversity. modeller)** .
   - Görünümler: **Razor (cshtml)** . (Varsayılan.)

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio, *Controllers\studentcontroller.cs* dosyasını açar. Bir veritabanı bağlamı nesnesini örnekleyen bir sınıf değişkeni oluşturulduğunu görürsünüz:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     `Index` Action yöntemi, veritabanı bağlamı örneğinin `Students` özelliğini okuyarak *öğrenciler* varlık kümesinden öğrencilerin bir listesini alır:

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     *Student\ındex.cshtml* görünümü bu listeyi bir tabloda görüntüler:

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. Projeyi çalıştırmak için CTRL + F5 tuşlarına basın.

     `Seed` yönteminin eklendiği test verilerini görmek için **öğrenciler** sekmesine tıklayın.

     ![Öğrenci Dizin sayfası](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>Kurallar

Entity Framework, kuralların kullanımı veya Entity Framework varsayımlarıyla *ilgili olarak en*az bir veritabanı oluşturabilmesini sağlamak için yazmanız gereken kod miktarı. Bunlardan bazıları zaten belirtilmiştir:

- Varlık sınıfı adlarının plurar biçimleri tablo adı olarak kullanılır.
- Varlık özelliği adları, sütun adları için kullanılır.
- `ID` veya *classname* `ID` adlı varlık özellikleri birincil anahtar özellikler olarak tanınır.

Kuralların geçersiz kılınabileceğini (örneğin, tablo adlarının çoğullendirilmemelidir) gördünüz ve bu serinin ilerleyen kısımlarında daha [karmaşık veri modeli oluşturma](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md) öğreticisinde daha fazla bilgi edinebilirsiniz. Daha fazla bilgi için bkz. [Code First kuralları](https://msdn.microsoft.com/data/jj679962).

## <a name="summary"></a>Özet

Artık Entity Framework ve SQL Server Express kullanarak verileri depolayıp görüntüleyen basit bir uygulama oluşturdunuz. Aşağıdaki öğreticide, temel CRUD (oluşturma, okuma, güncelleştirme, silme) işlemlerini nasıl gerçekleştireceğinizi öğreneceksiniz. Bu sayfanın en altında geri bildirim bırakabilirsiniz. Lütfen öğreticinin bu bölümünü nasıl Beğeneceğimizi ve nasıl iyileştirebileceğimizi bize bildirin.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Next](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
