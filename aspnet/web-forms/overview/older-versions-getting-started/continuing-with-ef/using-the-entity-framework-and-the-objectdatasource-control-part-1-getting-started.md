---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
title: 'Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 1. Bölüm: başlangıç | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, Entity Framework öğretici serisi ile çalışmaya başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. Yo yo...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 244278c1-fec8-4255-8a8a-13bde491c4f5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started
msc.type: authoredcontent
ms.openlocfilehash: 2f14707eb058d438495dd2bc4c17b976c471fc97
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547294"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-1-getting-started"></a>Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 1. Bölüm: Başlarken

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Bu öğretici serisi, [Entity Framework 4,0 öğretici serisi Ile çalışmaya](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. Önceki öğreticileri tamamlamadıysanız, bu öğretici için bir başlangıç noktası olarak, oluşturduğunuz [uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Ayrıca, tüm öğretici serileri tarafından oluşturulan [uygulamayı da indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) .
> 
> Contoso Üniversitesi örnek Web uygulaması, 4,0 ve Visual Studio 2010 Entity Framework kullanarak nasıl ASP.NET Web Forms uygulamalar oluşturacağınızı gösterir. Örnek uygulama, kurgusal bir Contoso Üniversitesi için bir Web sitesidir. Öğrenci giriş, kurs oluşturma ve Eğitmen atamaları gibi işlevleri içerir.
> 
> Öğreticide örnekleri gösterilir C#. [İndirilebilir örnek](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) hem C# hem de Visual Basic kod içerir.
> 
> ## <a name="database-first"></a>Database First
> 
> Entity Framework verilerle çalışmak için üç yol vardır: *Database First*, *model First*ve *Code First*. Bu öğretici Database First içindir. Bu iş akışları arasındaki farklar ve senaryonuz için en uygun olanı seçme hakkında daha fazla bilgi için bkz. [Entity Framework geliştirme Iş akışları](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="web-forms"></a>Web Forms
> 
> Başlarken serisi gibi, bu öğretici serisi ASP.NET Web Forms modelini kullanır ve Visual Studio 'da ASP.NET Web Forms ile nasıl çalışabildiğinizi varsayar. Bunu yapmazsanız, bkz. [ASP.NET 4,5 Ile çalışmaya başlama Web Forms](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). ASP.NET MVC çerçevesiyle çalışmayı tercih ediyorsanız, bkz. [ASP.NET MVC kullanarak Entity Framework](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)kullanmaya başlama.
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

`EntityDataSource` denetimi, uygulamayı çok hızlı bir şekilde oluşturmanıza olanak tanıyor, ancak genellikle *. aspx* sayfalarınızda önemli miktarda iş mantığı ve veri erişim mantığı tutmanızı gerektirir. Uygulamanızın karmaşıklığa büyümesini ve devam eden bakım gerektirmesini beklemeniz durumunda daha fazla sürdürülebilir bir *n katmanlı* veya *katmanlı* uygulama yapısı oluşturmak için daha fazla geliştirme süresi yatırmaya yatırım yapabilirsiniz. Bu mimariyi uygulamak için, sunu katmanını iş mantığı katmanından (BLL) ve veri erişim katmanından (DAL) ayırın. Bu yapıyı uygulamak için bir yol, `EntityDataSource` denetimi yerine `ObjectDataSource` denetimini kullanmaktır. `ObjectDataSource` denetimini kullandığınızda, kendi veri erişim kodunuzu uygular ve daha sonra diğer veri kaynağı denetimleriyle aynı özelliklerin birçoğunu içeren bir denetimi kullanarak *. aspx* sayfalarında bu kodu çağırabilirsiniz. Bu, bir n katmanlı yaklaşımın avantajlarını, veri erişimi için Web Forms denetimi kullanmanın avantajlarından yararlanmanızı sağlar.

`ObjectDataSource` denetimi, diğer yollarla da daha fazla esneklik sağlar. Kendi veri erişim kodunuzu yazarken, `EntityDataSource` denetiminin gerçekleştirmek üzere tasarlandığı görevler olan belirli bir varlık türünü okuma, ekleme, güncelleştirme veya silme işlemleri daha kolay olur. Örneğin, bir varlık her güncelleştirildiğinde günlük kaydı gerçekleştirebilir, bir varlık her silindiğinde verileri arşivleyebilir veya yabancı anahtar değeri olan bir satır eklerken gerektiğinde ilgili verileri otomatik olarak denetleyip güncelleştirebilirsiniz.

## <a name="business-logic-and-repository-classes"></a>İş mantığı ve depo sınıfları

`ObjectDataSource` denetim, oluşturduğunuz bir sınıfı çağırarak işe yarar. Sınıfı, verileri alan ve güncelleştiren yöntemler içerir ve bu yöntemlerin adlarını biçimlendirme içindeki `ObjectDataSource` denetimine sağlarsınız. İşleme veya geri gönderme işlemi sırasında, `ObjectDataSource` belirttiğiniz yöntemleri çağırır.

Temel CRUD işlemlerinin yanı sıra, `ObjectDataSource` denetimi ile kullanmak için oluşturduğunuz sınıfın, `ObjectDataSource` verileri okurken veya güncelleştirtığında iş mantığını yürütmesi gerekebilir. Örneğin, bir departmanı güncelleştirdiğinizde, bir kişi birden fazla departmanın yöneticisi olmadığından başka hiçbir departmanın aynı yöneticiye sahip olmadığını doğrulamanız gerekebilir.

[ObjectDataSource sınıfına genel bakış](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.aspx)gibi bazı `ObjectDataSource` belgelerde, Denetim hem iş mantığı hem de veri erişim mantığını içeren bir *iş nesnesi* olarak adlandırılan bir sınıfı çağırır. Bu öğreticide, iş mantığı ve veri erişim mantığı için ayrı sınıflar oluşturacaksınız. Veri erişim mantığını kapsülleyen sınıfına bir *Depo*denir. İş mantığı sınıfı hem iş mantığı yöntemlerini hem de veri erişim yöntemlerini içerir, ancak veri erişim yöntemleri, veri erişim görevlerini gerçekleştirmek için depoyu çağırır.

BLL ve DAL arasında BLL 'nin otomatik birim testlerini kolaylaştıran bir soyutlama katmanı da oluşturacaksınız. Bu soyutlama katmanı, bir arabirim oluşturup iş mantığı sınıfında depoyu örneklediğinizde arabirim kullanılarak uygulanır. Bu, iş mantığı sınıfını depo arabirimini uygulayan herhangi bir nesneye başvuru ile sağlamanızı mümkün kılar. Normal işlem için Entity Framework birlikte çalışarak bir depo nesnesi sağlarsınız. Test için, Koleksiyonlar olarak tanımlanan sınıf değişkenleri gibi kolayca işleyebileceğiniz bir şekilde depolanan verilerle birlikte çalışarak bir depo nesnesi sağlarsınız.

Aşağıdaki çizimde, bir depo olmadan ve bir depoyu kullanan veri erişim mantığını içeren bir iş mantığı sınıfı arasındaki fark gösterilmektedir.

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image1.png)

Yalnızca temel veri erişim görevlerini gerçekleştirdiğinden, `ObjectDataSource` denetiminin doğrudan bir depoya bağlandığı Web sayfaları oluşturarak başlarsınız. Sonraki öğreticide, doğrulama mantığı ile bir iş mantığı sınıfı oluşturacak ve `ObjectDataSource` denetimini depo sınıfı yerine bu sınıfa bağlayacaksınız. Ayrıca doğrulama mantığı için birim testleri de oluşturacaksınız. Bu serideki üçüncü öğreticide, uygulamaya sıralama ve filtreleme işlevlerini ekleyeceksiniz.

Bu öğreticide oluşturduğunuz sayfalar, [Başlarken öğretici serisinde](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md)oluşturduğunuz veri modeli `Departments` varlık kümesiyle çalışır.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image3.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image5.png)

## <a name="updating-the-database-and-the-data-model"></a>Veritabanını ve veri modelini güncelleştirme

Bu öğreticide, her ikisi de [Entity Framework ve Web Forms öğreticileri Ile çalışmaya başlama](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) bölümünde oluşturduğunuz veri modelinde ilgili değişiklikler gerektiren veritabanında iki değişiklik yaparak başlayacaksınız. Bu öğreticilerden birinde, bir veritabanı değişikliğinden sonra tasarımcıda veri modelini veritabanı ile senkronize etmek için el ile değişiklikler yaptınız. Bu öğreticide, veri modelini otomatik olarak güncelleştirmek için tasarımcı 'nın **veritabanı aracından güncelleştirme modelini** kullanacaksınız.

### <a name="adding-a-relationship-to-the-database"></a>Veritabanına Ilişki ekleme

Visual Studio 'da, [Entity Framework ve Web Forms](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) öğretici serisini kullanmaya Başlarken bölümünde oluşturduğunuz Contoso University Web uygulamasını açın ve ardından `SchoolDiagram` veritabanı diyagramını açın.

Veritabanı diyagramında `Department` tabloya bakarsanız, bir `Administrator` sütunu olduğunu görürsünüz. Bu sütun `Person` tablo için bir yabancı anahtardır, ancak veritabanında yabancı anahtar ilişkisi tanımlanmamıştır. Entity Framework ilişkiyi oluşturmanız ve veri modelini güncelleştirmeniz gerekir. böylece, bu ilişkiyi otomatik olarak işleyebilir.

Veritabanı diyagramında `Department` tablosuna sağ tıklayıp **ilişkiler**' i seçin.

[![Image80](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image7.png)

**Yabancı anahtar ilişkileri** kutusunda **Ekle**' ye tıklayın **ve ardından tablolar ve sütunlar belirtimi**için üç nokta simgesine tıklayın.

[![Image81](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image9.png)

**Tablolar ve sütunlar** iletişim kutusunda, birincil anahtar tablo ve alanı `Person` ve `PersonID`olarak ayarlayın ve yabancı anahtar tablosunu ve alanını `Department` ve `Administrator`olarak ayarlayın. (Bunu yaptığınızda, ilişki adı `FK_Department_Department` `FK_Department_Person`olarak değişir.)

[![Image82](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image11.png)

**Tablolar ve sütunlar** kutusunda **Tamam** ' a tıklayın, **yabancı anahtar ilişkileri** kutusunda **Kapat** ' a tıklayın ve değişiklikleri kaydedin. `Person` ve `Department` tabloları kaydetmek isteyip istemediğiniz sorulursa **Evet**' e tıklayın.

> [!NOTE]
> Zaten `Administrator` sütununda bulunan verilere karşılık gelen `Person` satırları sildiyseniz, bu değişikliği kaydedemezsiniz. Bu durumda, her `Department` satırdaki `Administrator` değerin `Person` tablosunda gerçekten mevcut olan bir kaydın KIMLIĞINI içerdiğinden emin olmak için **Sunucu Gezgini** ' deki tablo düzenleyicisini kullanın.
> 
> Değişikliği kaydettikten sonra, bu kişi bir Departman Yöneticisi ise `Person` tablosundan bir satırı silemezsiniz. Bir üretim uygulamasında, bir veritabanı kısıtlaması silmeyi engellediğinde veya bir geçişli silme belirttiğinizde belirli bir hata iletisi sağlarsınız. Basamaklı silme Işlemi belirtmeye ilişkin bir örnek için, [Entity Framework ve ASP.net – Başlarken Bölüm 2](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-2.md)' ye bakın.

### <a name="adding-a-view-to-the-database"></a>Veritabanına görünüm ekleme

Oluşturmakta olduğunuz yeni *Departmanlar. aspx* sayfasında, kullanıcıların departman yöneticileri seçmesini sağlamak için "son, birinci" biçimdeki adlara sahip bir-aşağı açılan liste sağlamak istiyorsunuz. Bunu daha kolay hale getirmek için veritabanında bir görünüm oluşturacaksınız. Görünüm yalnızca açılan liste için gereken verilerden oluşur: tam ad (düzgün şekilde biçimlendirildi) ve kayıt anahtarı.

**Sunucu Gezgini**, *okul. mdf*' yi genişletin, **Görünümler** klasörüne sağ tıklayın ve **Yeni Görünüm Ekle**' yi seçin.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image13.png)

**Tablo Ekle** iletişim kutusu göründüğünde **Kapat** ' a tıklayın ve aşağıdaki SQL ifadesini SQL bölmesine yapıştırın:

[!code-sql[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample1.sql)]

Görünümü `vInstructorName`olarak kaydedin.

### <a name="updating-the-data-model"></a>Veri modeli güncelleştiriliyor

*Dal* klasöründe *SchoolModel. edmx* dosyasını açın, tasarım yüzeyine sağ tıklayın ve **modeli Güncelleştir**' i seçin.

[![Image07](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image15.png)

**Veritabanı nesnelerinizi seçin** Iletişim kutusunda **Ekle** sekmesini seçin ve yeni oluşturduğunuz görünümü seçin.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image17.png)

**Son**'a tıklayın.

Tasarımcıda, aracın bir `vInstructorName` varlık oluşturduğunu ve `Department` ile `Person` varlıkları arasında yeni bir ilişki oluşturduğunu görürsünüz.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image19.png)

> [!NOTE]
> **Çıkış** ve **hata listesi** Windows 'ta, aracın yeni `vInstructorName` görünümü için otomatik olarak bir birincil anahtar oluşturduğunu bildiren bir uyarı iletisi görebilirsiniz. Bu beklenen bir davranıştır.

Koddaki yeni `vInstructorName` varlığına başvurduğunuzda, daha düşük bir "v" örneğine önek olarak eklemek istemediğiniz veritabanı kuralını kullanmak istemezsiniz. Bu nedenle, modeldeki varlık ve varlık kümesini yeniden adlandırmanız gerekir.

**Model tarayıcısını**açın. Bir varlık türü ve görünüm olarak listelenmiş `vInstructorName` görürsünüz.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image21.png)

**SchoolModel** ( **SchoolModel. Store**değil) altında **vkomutctorname** öğesine sağ tıklayın ve **Özellikler**' i seçin. **Özellikler** penceresinde, **ad** özelliğini "komutadı" olarak değiştirin ve **varlık kümesi adı** özelliğini "komutctornames" olarak değiştirin.

[![Image15](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image24.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image23.png)

Veri modelini kaydedip kapatın ve ardından projeyi yeniden derleyin.

## <a name="using-a-repository-class-and-an-objectdatasource-control"></a>Bir depo sınıfı ve ObjectDataSource denetimi kullanma

*Dal* klasöründe yeni bir sınıf dosyası oluşturun, *SchoolRepository.cs*olarak adlandırın ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample2.cs)]

Bu kod, `Departments` varlık kümesindeki tüm varlıkları döndüren tek bir `GetDepartments` yöntemi sağlar. Döndürülen her satır için `Person` gezinti özelliğine erişeceğimizi bildiğiniz için, bu özellik için `Include` metodunu kullanarak Eager yükleme belirtirsiniz. Sınıfı, nesne atıldığı zaman veritabanı bağlantısının serbest olduğundan emin olmak için `IDisposable` arabirimini de uygular.

> [!NOTE]
> Ortak bir uygulama, her varlık türü için bir depo sınıfı oluşturmaktır. Bu öğreticide, birden çok varlık türü için bir depo sınıfı kullanılır. Depo deseninin hakkında daha fazla bilgi için, [Entity Framework ekibin blogundan](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) ve [Julie Lerman 'ın blogdaki](http://thedatafarm.com/blog/data-access/agile-ef4-repository-part-3-fine-tuning-the-repository/)gönderilere bakın.

`GetDepartments` yöntemi, döndürülen koleksiyonun depo nesnesinin kendisi atıldıktan sonra bile kullanılabilir olduğundan emin olmak için bir `IQueryable` nesnesi yerine bir `IEnumerable` nesnesi döndürür. Bir `IQueryable` nesnesi, her erişildiğinde veritabanı erişimine neden olabilir, ancak depo nesnesi veri bağlama denetiminin verileri işlemeye çalıştığı zamana göre atılabilir. `IEnumerable` nesnesi yerine `IList` nesnesi gibi başka bir koleksiyon türü döndürebilirsiniz. Ancak, bir `IEnumerable` nesnesi döndürmek, `foreach` döngüleri ve LINQ sorguları gibi tipik salt okuma listesi işleme görevlerini gerçekleştirmenize olanak sağlar, ancak bu tür değişikliklerin veritabanına kalıcı olabileceğini belirten, koleksiyonda öğe ekleyemez veya kaldırabilirsiniz.

*Site. Master* ana sayfasını kullanan bir *Departmanlar. aspx* sayfası oluşturun ve `Content2`adlı `Content` denetimine aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample3.aspx)]

Bu biçimlendirme, az önce oluşturduğunuz depo sınıfını ve verileri görüntüleyen bir `GridView` denetimini kullanan bir `ObjectDataSource` denetimi oluşturur. `GridView` denetimi **Düzenle** ve **Sil** komutlarını belirtir, ancak henüz desteklemek için kod eklemediniz.

Çeşitli sütunlarda `DynamicField` denetimleri kullanılarak otomatik veri biçimlendirme ve doğrulama işlevlerinin avantajlarından yararlanabilirsiniz. Bunların çalışması için, `Page_Init` olay işleyicisinde `EnableDynamicData` yöntemini çağırmanız gerekir. (`DynamicControl` denetimleri, gezinti özellikleriyle çalışmadıklarından `Administrator` alanında kullanılmaz.)

Kılavuza iç içe `GridView` denetimine sahip bir sütun eklediğinizde `Vertical-Align="Top"` öznitelikleri daha sonra önemli hale gelir.

*Departments.aspx.cs* dosyasını açın ve aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample4.cs)]

Ardından sayfanın `Init` olayı için aşağıdaki işleyiciyi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample5.cs)]

*Dal* klasöründe, *Department.cs* adlı yeni bir sınıf dosyası oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample6.cs)]

Bu kod, veri modeline meta veri ekler. `Department` varlığının `Budget` özelliğinin, veri türü `Decimal`olsa da para birimini temsil ettiğini belirtir ve değerin 0 ile $1.000.000,00 arasında olması gerektiğini belirtir. Ayrıca, `StartDate` özelliğinin aa/gg/yyyy biçiminde bir tarih olarak biçimlendirilmesi gerektiğini belirtir.

*Departmanlar. aspx* sayfasını çalıştırın.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image26.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image25.png)

*Departmanlar. aspx* veya **Başlangıç tarihi** sütunları için bir biçim dizesi belirtmemenizin yanı sıra, *Department.cs* dosyasında sağladığınız meta veriler kullanılarak bunlara `DynamicField` denetimleri tarafından varsayılan para birimi ve Tarih biçimlendirme uygulanmış olmasına dikkat edin.

## <a name="adding-insert-and-delete-functionality"></a>INSERT ve DELETE Işlevleri ekleme

*SchoolRepository.cs*'i açın, bir `Insert` yöntemi ve bir `Delete` yöntemi oluşturmak için aşağıdaki kodu ekleyin. Kod ayrıca, `Insert` yöntemi tarafından kullanılmak üzere bir sonraki kullanılabilir kayıt anahtarı değerini hesaplayan `GenerateDepartmentID` adlı bir yöntemi içerir. Bu, veritabanı `Department` tablosu için otomatik olarak hesaplanacak şekilde yapılandırılmadığı için gereklidir.

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample7.cs)]

### <a name="the-attach-method"></a>Attach yöntemi

`DeleteDepartment` yöntemi, bellekteki varlık ve temsil ettiği veritabanı satırı arasındaki nesne bağlamının nesne durumu yöneticisinde tutulan bağlantıyı yeniden oluşturmak için `Attach` yöntemini çağırır. Bu, yöntem `SaveChanges` yöntemini çağırmadan önce oluşmalıdır.

*Nesne bağlamı* terimi, varlık kümelerinize ve varlıklarınızı erişmek için kullandığınız `ObjectContext` sınıfından türetilen Entity Framework sınıfına başvurur. Bu projenin kodunda, sınıfı `SchoolEntities`olarak adlandırılır ve bir örneği her zaman `context`olarak adlandırılır. Nesne bağlamının *nesne durumu Yöneticisi* , `ObjectStateManager` sınıfından türetilen bir sınıftır. Nesne kişisi, varlık nesnelerini depolamak ve her birinin veritabanındaki karşılık gelen tablo satırı veya satırlarıyla uyumlu olup olmadığını izlemek için nesne durumu yöneticisini kullanır.

Bir varlığı okuduğunuzda, nesne bağlamı nesneyi nesne durumu yöneticisinde depolar ve nesnenin gösteriminin veritabanıyla eşitlenmiş olup olmadığını izler. Örneğin, bir özellik değerini değiştirirseniz, değiştirdiğiniz özelliğin artık veritabanıyla eşitlenmeyeceğini belirten bir bayrak ayarlanır. Sonra, `SaveChanges` yöntemini çağırdığınızda nesne bağlamı, varlığın geçerli durumu ve veritabanının durumu arasında tam olarak nelerin farklı olduğunu bildiğinden, nesne bağlamı veritabanında ne yapılacağını bilir.

Ancak, bu işlem genellikle bir Web uygulamasında çalışmaz, çünkü bir varlığı okuyan nesne bağlamı örneği, nesne durum Yöneticisi 'ndeki her şeyi içeren bir sayfa işlendikten sonra atılmış olur. Değişiklikleri uygulamak gereken nesne bağlamı örneği, geri gönderme işlemi için oluşturulan yeni bir nesnedir. `DeleteDepartment` yöntemi söz konusu olduğunda, `ObjectDataSource` denetimi, varlığın özgün sürümünü görünüm durumundaki değerlerden yeniden oluşturur, ancak bu `Department` varlık nesne durumu yöneticisinde yok. Bu yeniden oluşturulan varlıkta `DeleteObject` yöntemini çağırdıysanız, nesne bağlamı varlığın veritabanıyla eşitlenmiş olup olmadığını bilmez, çağrı başarısız olur. Ancak `Attach` yöntemini çağırmak, yeniden oluşturulan varlık ve veritabanındaki değerler nesne bağlamının daha önceki bir örneğinde Okunmuşsa otomatik olarak gerçekleştirilen değerlerle aynı izlemeyi yeniden oluşturur.

Nesne bağlamının nesne durumu yöneticisinde varlıkları izlemesini istemediğiniz zamanlar vardır ve bunu yapmasını engellemek için bayraklar ayarlayabilirsiniz. Bunun örnekleri, bu serideki sonraki öğreticilerde gösterilmiştir.

### <a name="the-savechanges-method"></a>SaveChanges yöntemi

Bu basit depo sınıfı, CRUD işlemlerinin nasıl gerçekleştirileceğininin temel ilkelerini gösterir. Bu örnekte, `SaveChanges` yöntemi her güncelleştirmeden hemen sonra çağrılır. Bir üretim uygulamasında, veritabanının güncelleştirildiği zaman üzerinde daha fazla denetim sağlamak için `SaveChanges` yöntemini ayrı bir yöntemden çağırmak isteyebilirsiniz. (Sonraki öğreticinin sonunda, ilgili güncelleştirmeleri koordine eden bir yaklaşım olan iş deseninin birimini açıklayan bir teknik incelemeye bağlantı bulacaksınız.) Ayrıca, `DeleteDepartment` yönteminin eşzamanlılık çakışmalarını işlemek için kod içermediğinden de dikkat edin; Bunu yapılacak kod, bu serinin sonraki bir öğreticiye eklenecektir.

### <a name="retrieving-instructor-names-to-select-when-inserting"></a>Ekleme sırasında seçilecek eğitmen adlarını alma

Kullanıcılar, yeni departmanlar oluştururken açılan listede bir eğitmenler listesinden yönetici seçebilmelidir. Bu nedenle, daha önce oluşturduğunuz görünümü kullanarak eğitmenler listesini almak üzere bir yöntem oluşturmak için *SchoolRepository.cs* 'e aşağıdaki kodu ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample8.cs)]

### <a name="creating-a-page-for-inserting-departments"></a>Departmanlar eklemek için bir sayfa oluşturma

*Site. Master* sayfasını kullanan bir *DepartmentsAdd. aspx* sayfası oluşturun ve `Content2`adlı `Content` denetimine aşağıdaki biçimlendirmeyi ekleyin:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample9.aspx)]

Bu biçimlendirme, biri yeni `Department` varlıkları eklemek için bir diğeri ve bölüm yöneticileri seçmek için kullanılan `DropDownList` denetimine yönelik eğitmen adlarını almak için bir tane olmak üzere iki `ObjectDataSource` denetimi oluşturur. Biçimlendirme, yeni departmanlar girmeye yönelik bir `DetailsView` denetimi oluşturur ve `Administrator` yabancı anahtar değerini ayarlayabilmeniz için denetimin `ItemInserting` olayı için bir işleyici belirtir. Sonda, hata iletilerini göstermek için bir `ValidationSummary` denetimidir.

*DepartmentsAdd.aspx.cs* açın ve aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample10.cs)]

Aşağıdaki sınıf değişkenini ve yöntemleri ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample11.cs)]

`Page_Init` yöntemi dinamik veri işlevlerini etkin bir şekilde sunar. `DropDownList` denetiminin `Init` olayının işleyicisi denetime bir başvuru kaydeder ve `DetailsView` denetiminin `Inserting` olayı için bu başvuruyu, seçilen eğitmenin `PersonID` değerini almak ve `Administrator` varlığının `Department` yabancı anahtar özelliğini güncelleştirmek için kullanır.

Sayfayı çalıştırın, yeni bir departman için bilgi ekleyin ve sonra **Ekle** bağlantısına tıklayın.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image28.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image27.png)

Başka bir yeni departman için değerler girin. **Bütçe** alanına 1.000.000,00 'den büyük bir sayı girin ve sonraki alana sekmeye geçin. Alanda bir yıldız işareti görünür ve fare işaretçisini onun üzerine tutarsanız, bu alanın meta verilerinde girdiğiniz hata iletisini görebilirsiniz.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image30.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image29.png)

**Ekle**' ye tıklayın ve sayfanın alt kısmındaki `ValidationSummary` denetimi tarafından görüntülendiğini görürsünüz.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image32.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image31.png)

Sonra, tarayıcıyı kapatın ve *Departmanlar. aspx* sayfasını açın. `ObjectDataSource` denetimine bir `DeleteMethod` özniteliği ve `GridView` denetimine `DataKeyNames` özniteliğini ekleyerek *Departmanlar. aspx* sayfasına Delete özelliği ekleyin. Bu denetimlerin açılış etiketleri artık aşağıdaki örneğe benzeyecektir:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample12.aspx)]

Sayfayı çalıştırın.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image34.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image33.png)

*DepartmentsAdd. aspx* sayfasını çalıştırdığınızda eklediğiniz departmanı silin.

## <a name="adding-update-functionality"></a>Güncelleştirme Işlevselliği ekleniyor

*SchoolRepository.cs* 'i açın ve aşağıdaki `Update` yöntemi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample13.cs)]

*Departmanlar. aspx* sayfasında **Güncelleştir** ' e tıkladığınızda, `ObjectDataSource` denetimi `UpdateDepartment` yöntemine geçirilecek iki `Department` varlık oluşturur. Biri, Görünüm durumunda depolanan özgün değerleri içerir ve diğeri `GridView` denetimine girilen yeni değerleri içerir. `UpdateDepartment` yöntemindeki kod, varlık ve veritabanında neler olduğunu izlemek için özgün değerleri olan `Department` varlığını `Attach` yöntemine geçirir. Ardından kod, yeni değerleri olan `Department` varlığını `ApplyCurrentValues` yöntemine geçirir. Nesne bağlamı eski ve yeni değerleri karşılaştırır. Yeni bir değer eski bir değerden farklıysa, nesne bağlamı özellik değerini değiştirir. `SaveChanges` yöntemi daha sonra yalnızca veritabanında değiştirilen sütunları güncelleştirir. (Ancak, bu varlık için güncelleştirme işlevi bir saklı yordamla eşlendiyse, hangi sütunların değiştirildiğine bakılmaksızın tüm satır güncelleştirilir.)

*Departmanlar. aspx* dosyasını açın ve aşağıdaki öznitelikleri `DepartmentsObjectDataSource` denetimine ekleyin:

- `UpdateMethod="UpdateDepartment"`
- `ConflictDetection="CompareAllValues"`   
 Bu, eski değerlerin `Update` yöntemindeki yeni değerlerle karşılaştırılabilmesi için Görünüm durumunda depolanmasına neden olur.
- `OldValuesParameterFormatString="orig{0}"`   
 Bu, denetimi özgün değerler parametresinin adının `origDepartment` olduğunu bildirir.

`ObjectDataSource` denetiminin açılış etiketi için olan biçimlendirme artık aşağıdaki örneğe benzer:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample14.aspx)]

`GridView` denetimine bir `OnRowUpdating="DepartmentsGridView_RowUpdating"` özniteliği ekleyin. Bunu, kullanıcının açılan listede seçtiği satıra göre `Administrator` özellik değerini ayarlamak için kullanacaksınız. `GridView` açma etiketi artık aşağıdaki örneğe benzer:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample15.aspx)]

`GridView` denetimine, bu sütun için `ItemTemplate` denetiminden hemen sonra `Administrator` sütunu için bir `EditItemTemplate` denetimi ekleyin:

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample16.aspx)]

Bu `EditItemTemplate` denetim, *DepartmentsAdd. aspx* sayfasındaki `InsertItemTemplate` denetimine benzer. Fark, denetimin başlangıç değerinin `SelectedValue` özniteliği kullanılarak ayarlanmanızdır.

`GridView` denetiminden önce, *DepartmentsAdd. aspx* sayfasında yaptığınız gibi bir `ValidationSummary` denetimi ekleyin.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample17.aspx)]

*Departments.aspx.cs* açın ve kısmi sınıf bildiriminden hemen sonra, `DropDownList` denetimine başvurmak üzere özel bir alan oluşturmak için aşağıdaki kodu ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample18.cs)]

Sonra `DropDownList` denetimin `Init` olayı ve `GridView` denetiminin `RowUpdating` olayı için işleyiciler ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/samples/sample19.cs)]

`Init` olayının işleyicisi, sınıf alanındaki `DropDownList` denetimine bir başvuru kaydeder. `RowUpdating` olayının işleyicisi, kullanıcının girdiği değeri almak için başvurusunu kullanır ve `Department` varlığının `Administrator` özelliğine uygular.

Yeni bir departman eklemek için *DepartmentsAdd. aspx* sayfasını kullanın, sonra *Departmanlar. aspx* sayfasını çalıştırın ve eklediğiniz satırda **Düzenle** ' ye tıklayın.

> [!NOTE]
> Veritabanında geçersiz veriler nedeniyle, eklememiş olduğunuz satırları (yani veritabanında zaten var olan) düzenleyemeyeceksiniz; veritabanıyla oluşturulan satırların yöneticileri öğrencilerdir. Bunlardan birini düzenlemeye çalışırsanız, `'InstructorsDropDownList' has a SelectedValue which is invalid because it does not exist in the list of items.` gibi bir hata raporlayan bir hata sayfası alacaksınız

[![Image10](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image36.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image35.png)

Geçersiz bir **Bütçe** miktarı girip **Güncelleştir**' e tıklarsanız, *Departmanlar. aspx* sayfasında gördüğünüz yıldız ve hata iletisinin aynısını görürsünüz.

Bir alan değerini değiştirin veya farklı bir yönetici seçip **Güncelleştir**' e tıklayın. Değişiklik görüntülenir.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image38.png)](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started/_static/image37.png)

Bu, Entity Framework ile temel CRUD (oluşturma, okuma, güncelleştirme, silme) işlemleri için `ObjectDataSource` denetimini kullanmaya giriş işlemini tamamlar. Basit n katmanlı bir uygulama oluşturdunuz, ancak iş mantığı katmanı, otomatik birim testini karmaşıklaştırır ve veri erişim katmanına sıkı bir şekilde bağlanmış. Aşağıdaki öğreticide, birim testini kolaylaştırmak için depo deseninin nasıl uygulanacağını göreceksiniz.

> [!div class="step-by-step"]
> [Next](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests.md)
