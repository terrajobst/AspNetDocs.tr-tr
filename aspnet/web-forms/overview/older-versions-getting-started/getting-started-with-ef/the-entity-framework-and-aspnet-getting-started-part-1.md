---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms ile çalışmaya başlama | Microsoft Docs
author: tdykstra
description: Contoso University örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: fd88b32ad2a65e5b4c7ead15f0d6dc5dc6e97e75
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630461"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>Entity Framework 4,0 Database First ve ASP.NET 4 Web Forms ile çalışmaya başlama

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama, kurgusal bir Contoso Üniversitesi için bir Web sitesidir. Öğrenci giriş, kurs oluşturma ve Eğitmen atamaları gibi işlevleri içerir.
> 
> Öğreticide örnekleri gösterilir C#. [İndirilebilir örnek](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) hem C# hem de Visual Basic kod içerir.
> 
> ## <a name="database-first"></a>Database First
> 
> Entity Framework verilerle çalışmak için üç yol vardır: *Database First*, *model First*ve *Code First*. Bu öğretici Database First içindir. Bu iş akışları arasındaki farklar ve senaryonuz için en uygun olanı seçme hakkında daha fazla bilgi için bkz. [Entity Framework geliştirme Iş akışları](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="web-forms"></a>Web Forms
> 
> Bu öğretici serisi, ASP.NET Web Forms modelini kullanır ve Visual Studio 'da ASP.NET Web Forms ile nasıl çalışabildiğinizi varsayar. Bunu yapmazsanız, bkz. [ASP.NET 4,5 Ile çalışmaya başlama Web Forms](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). ASP.NET MVC çerçevesiyle çalışmayı tercih ediyorsanız, bkz. [ASP.NET MVC kullanarak Entity Framework](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)kullanmaya başlama.
> 
> ## <a name="software-versions"></a>Yazılım sürümleri
> 
> | **Öğreticide gösterilen** | **İle de birlikte çalışarak** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Web için Visual Studio 2010 Express. Öğretici, Visual Studio 'nun sonraki sürümleriyle test edilmemiştir. Menü seçimleri, iletişim kutuları ve şablonlarda birçok fark vardır. |
> | .NET 4 | .NET 4,5, .NET 4 ile geriye dönük olarak uyumludur, ancak öğretici .NET 4,5 ile sınanmamıştır. |
> | Entity Framework 4 | Öğretici, daha sonraki Entity Framework sürümleriyle sınanmamıştır. Entity Framework 5 ' den başlayarak EF, EF 4,1 ile tanıtılan `DbContext API` varsayılan olarak kullanır. EntityDataSource denetimi, `ObjectContext` API 'sini kullanacak şekilde tasarlandı. EntityDataSource denetimini `DbContext` API ile kullanma hakkında daha fazla bilgi için [Bu blog gönderisine](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx)bakın. |
> 
> ## <a name="questions"></a>UL
> 
> Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx), [Entity Framework ve LINQ to Entities forumuna](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

## <a name="overview"></a>Genel bakış

Bu öğreticilerde oluşturacağınız uygulama basit bir üniversite web sitesidir.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

Kullanıcılar görüntüleyebilir ve Öğrenci, kurs ve Eğitmen bilgileri güncelleştirin. Oluşturacağınız ekranların bazıları aşağıda gösterilmiştir.

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>Web uygulaması oluşturma

Öğreticiyi başlatmak için Visual Studio 'Yu açın ve **ASP.NET Web uygulaması** şablonunu kullanarak yeni bir ASP.NET Web uygulaması projesi oluşturun:

[![Image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

Bu şablon, zaten bir stil sayfası ve ana sayfalar içeren bir Web uygulaması projesi oluşturur:

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

*Site. Master* dosyasını açın ve "My ASP.NET Application" öğesini "Contoso Üniversitesi" olarak değiştirin.

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

`NavigationMenu` adlı *menü* denetimini bulun ve oluşturacağınız sayfalara menü öğeleri ekleyen aşağıdaki biçimlendirme ile değiştirin.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

*Default. aspx* sayfasını açın ve `BodyContent` adlı `Content` denetimini bu şekilde değiştirin:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

Artık oluşturmakta olduğunuz çeşitli sayfaların bağlantılarını içeren basit bir giriş sayfanız vardır:

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>Veritabanı oluşturma

Bu öğreticiler için Entity Framework veri modeli tasarımcısını kullanarak, mevcut bir veritabanına (genellikle *veritabanı ilk* yaklaşımı olarak adlandırılır) göre veri modelini otomatik olarak oluşturabilirsiniz. Bu öğretici serisinde kapsanmayan bir alternatif, veri modelini el ile oluşturmak ve tasarımcı 'nın veritabanını oluşturan betikler oluşturmasını ( *model ilk* yaklaşımı) sağlar.

Bu öğreticide kullanılan veritabanı ilk yöntemi için, bir sonraki adım siteye bir veritabanı eklemektir. En kolay yol, ilk olarak bu öğreticiyle ilgili projeyi indirmesidir. Ardından, *uygulama\_veri* klasörüne sağ tıklayın, **Varolan öğe Ekle**' yi seçin ve indirilen projeden *okul. mdf* veritabanı dosyasını seçin.

Diğer bir seçenek de [okul örnek veritabanını oluşturma yönergelerini Izleyeceğiz](https://msdn.microsoft.com/library/bb399731.aspx). Veritabanını indirmeniz veya oluşturmanız durumunda, *okul. mdf* dosyasını aşağıdaki klasörden uygulamanızın uygulama *\_veri* klasörüne kopyalayın:

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

( *. Mdf* dosyasının bu konumu SQL Server 2008 Express kullandığınızı varsayar.)

Veritabanını bir betikten oluşturursanız, veritabanı diyagramı oluşturmak için aşağıdaki adımları gerçekleştirin:

1. **Sunucu Gezgini**, **veri bağlantıları**' nı genişletin, *okul. mdf*' yi genişletin, **veritabanı diyagramları**' na sağ tıklayın ve **Yeni Diyagram Ekle**' yi seçin.

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. Tüm tabloları seçip **Ekle**' ye tıklayın.

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server tabloları, tablolardaki sütunları ve tablolar arasındaki ilişkileri gösteren bir veritabanı diyagramı oluşturur. Tabloları, daha sonra istediğiniz şekilde düzenlemek için taşıyabilirsiniz.
3. Diyagramı "SchoolDiagram" olarak kaydedin ve kapatın.

Bu öğreticide yer alan *okul. mdf* dosyasını indirdiğinizde, **Sunucu Gezgini**veritabanı **diyagramları** altında **SchoolDiagram** ' ye çift tıklayarak veritabanı diyagramını görüntüleyebilirsiniz.

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

Diyagram şuna benzer (tablolar burada gösterilenden farklı konumlarda olabilir):

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>Entity Framework veri modeli oluşturma

Artık bu veritabanından bir Entity Framework veri modeli oluşturabilirsiniz. Veri modelini uygulamanın kök klasöründe oluşturabilirsiniz, ancak bu öğreticide *dal* adlı bir klasöre (veri erişim katmanı için) yerleştirebilirsiniz.

**Çözüm Gezgini**, *dal* adlı bir proje klasörü ekleyin (çözümün altında değil, projenin altında olduğundan emin olun).

*Dal* klasörüne sağ tıklayın ve ardından **Ekle** ve **Yeni öğe**' yi seçin. **Yüklü şablonlar**altında, **veriler**' i seçin, **ADO.net varlık veri modeli** şablonunu seçin, *SchoolModel. edmx*olarak adlandırın ve ardından **Ekle**' ye tıklayın.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

Bu, Varlık Veri Modeli Sihirbazı 'Nı başlatır. İlk sihirbaz adımında, **veritabanından oluştur** seçeneği varsayılan olarak seçilidir. **İleri**'ye tıklayın.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

**Veri bağlantınızı seçin** adımında, varsayılan değerleri bırakın ve **İleri**' ye tıklayın. Okul veritabanı varsayılan olarak seçilidir ve bağlantı ayarı *Web. config* dosyasında **Sseçlentities**olarak kaydedilir.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

**Veritabanı nesnelerinizi seçin** Sihirbazı adımında, `sysdiagrams` dışındaki tüm tabloları (daha önce oluşturduğunuz diyagram için oluşturulmuş) seçin ve ardından **son**' a tıklayın.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

Model oluşturma işlemi tamamlandıktan sonra Visual Studio, veritabanı tablolarınıza karşılık gelen Entity Framework nesnelerinin (varlıkların) grafik gösterimini gösterir. (Veritabanı diyagramında olduğu gibi, tek tek öğelerin konumu Bu çizimde gördüklerden farklı olabilir. İsterseniz çizimi eşleştirmek için öğeleri etrafında sürükleyebilirsiniz.)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>Entity Framework veri modelini keşfetme

Varlık diyagramının veritabanı diyagramına çok benzer şekilde göründüğünü, birkaç farklı farklılık olduğunu görebilirsiniz. Tek fark, ilişkilendirmenin türünü gösteren her bir ilişkilendirmenin sonundaki simgelerin eklenmesidir (tablo ilişkileri, veri modelindeki varlık ilişkilendirmeleri olarak adlandırılır):

- Bire sıfır veya-bir ilişkilendirme "1" ve "0.. 1" ile temsil edilir.

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    Bu durumda, bir `Person` varlığı bir `OfficeAssignment` varlığıyla ilişkili olabilir veya olmayabilir. Bir `OfficeAssignment` varlık bir `Person` varlığıyla ilişkilendirilmelidir. Diğer bir deyişle, bir eğitmen bir ofise veya atanmayabilir ve herhangi bir Office yalnızca bir eğitmene atanabilir.
- Bire çok ilişkilendirmesi "1" ve "\*" ile temsil edilir.

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    Bu durumda, `Person` bir varlık ilişkili `StudentGrade` varlıklara sahip olabilir veya olmayabilir. Bir `StudentGrade` varlık bir `Person` varlığıyla ilişkilendirilmelidir. `StudentGrade` varlıklar, aslında bu veritabanındaki kayıtlı kursları temsil eder; bir öğrenci kursa kaydedildiyse ve henüz bir sınıf yoksa, `Grade` özelliği null olur. Diğer bir deyişle, bir öğrenci henüz hiçbir kursa kaydedilmeyebilir, bir kursa kaydedilebilir veya birden çok kursa kaydedilebilir. Kayıtlı bir Kurstaki her bir sınıf yalnızca bir öğrenci için geçerlidir.
- Çok-çok ilişkilendirmesi "\*" ve "\*" ile temsil edilir.

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    Bu durumda, bir `Person` varlığının ilişkili `Course` varlıkları olabilir veya bulunmayabilir, tersi de geçerlidir: bir `Course` varlığının ilişkili `Person` varlıkları olabilir veya olmayabilir. Diğer bir deyişle, bir eğitmen birden çok kurs öğretebilir ve bir kurs birden fazla eğitmen tarafından tada gelebilir. (Bu veritabanında, bu ilişki yalnızca Eğitmenler için geçerlidir; öğrencileri kurslara bağlamaz. Öğrenciler, Studentnotlar tablosunun kurslarına bağlanır.)

Veritabanı diyagramı ve veri modeli arasındaki diğer bir farklılık, her varlık için ek **Gezinti özellikleri** bölümüdür. Bir varlığın gezinti özelliği ilgili varlıklara başvurur. Örneğin, bir `Person` varlığındaki `Courses` özelliği, bu `Person` varlıkla ilgili `Course` varlıkların bir koleksiyonunu içerir.

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

Veritabanı ve veri modeli arasında başka bir farklılık da, veritabanında kullanılan `CourseInstructor` ilişkilendirme tablosunun, `Person` ve `Course` tabloları çoktan çoğa ilişkiye bağlamadır. Gezinti özellikleri, `Course` varlığındaki `Person` varlık ve ilgili `Person` varlıklarından ilgili `Course` varlıkları almanızı sağlar; bu nedenle, veri modelindeki ilişkilendirme tablosunu temsil etmeniz gerekmez.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

Bu öğreticinin amaçları doğrultusunda, `Person` tablosunun `FirstName` sütununun aslında kişinin adı ve ikinci adı içerdiğini varsayalım. Alanın adını bunu yansıtacak şekilde değiştirmek istersiniz, ancak veritabanı Yöneticisi (DBA) veritabanını değiştirmek istememeyebilir. Veri modelindeki `FirstName` özelliğinin adını değiştirebilirsiniz, ancak veritabanı eşdeğerini değişmeden bırakabilirsiniz.

Tasarımcıda `Person` varlığındaki **adı** ' na sağ tıklayın ve ardından **Yeniden Adlandır**' ı seçin.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

"FirstMidName" adlı yeni adı yazın. Bu, veritabanını değiştirmeden koddaki sütuna başvurma şeklini değiştirir.

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

Model tarayıcısı, veritabanı yapısını, veri modeli yapısını ve aralarındaki eşlemeyi görüntülemek için başka bir yol sağlar. Görmek için varlık Tasarımcısı 'nda boş bir alana sağ tıklayın ve ardından **model tarayıcısı**' na tıklayın.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

**Model tarayıcı** bölmesinde bir ağaç görünümü görüntülenir. ( **Model tarayıcı** bölmesi **Çözüm Gezgini** bölmesi ile yerleştirilmiş olabilir.) **SchoolModel** düğümü, veri modeli yapısını temsil eder ve **SchoolModel. Store** düğümü veritabanı yapısını temsil eder.

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

Tabloları görmek için **SchoolModel. Store** ' u genişletin, tabloları görmek için **tablolar/görünümler** ' i genişletin ve ardından tablodaki sütunları görmek için **kursu** genişletin.

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

**SchoolModel**' ı genişletin, **varlık türleri**' ni genişletin ve ardından varlıklar içindeki varlıkları ve özellikleri görmek için **Kurs** düğümünü genişletin.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

Tasarımcı ya da **model tarayıcısı** bölmesinde, Entity Framework iki modelin nesnelerini nasıl ilişkilendirir? bölümüne bakabilirsiniz. `Person` varlığına sağ tıklayıp **Tablo eşleme**' yi seçin.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

Bu, **eşleme ayrıntıları** penceresini açar. Bu pencerenin, veritabanı sütununun `FirstName` `FirstMidName`eşlenmiş olduğunu görmenize, bu da veri modelinde olarak yeniden adlandırdıklarınız olduğunu görürsünüz.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

Entity Framework, veritabanı, veri modeli ve aralarında eşlemeler hakkında bilgi depolamak için XML kullanır. *SchoolModel. edmx* dosyası aslında bu bilgileri IÇEREN bir XML dosyasıdır. Tasarımcı, bilgileri bir grafik biçiminde işler, ancak aynı zamanda dosyayı XML olarak görüntüleyebilir **Çözüm Gezgini**, **birlikte Aç**' a tıklayıp **XML (metin) Düzenleyicisi**' ni *seçebilirsiniz.* (Veri modeli Tasarımcısı ve bir XML Düzenleyicisi, aynı dosyayı açmak ve bunlarla çalışmak için iki farklı yol olduğundan, tasarımcı 'yı açabilir ve dosyayı aynı anda bir XML düzenleyicisinde açabilirsiniz.)

Artık bir Web sitesi, bir veritabanı ve bir veri modeli oluşturdunuz. Sonraki izlenecek yolda, veri modeli ve ASP.NET `EntityDataSource` denetimini kullanarak verilerle çalışmaya başlayacaksınız.

> [!div class="step-by-step"]
> [Next](the-entity-framework-and-aspnet-getting-started-part-2.md)
