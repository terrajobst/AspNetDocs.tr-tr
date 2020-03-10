---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
title: ASP.NET 4 Web uygulamasındaki Entity Framework 4,0 ile performansı en üst düzeye çıkarın | Microsoft Docs
author: tdykstra
description: Bu öğretici serisi, Entity Framework 4,0 öğretici serisi ile çalışmaya başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 4e43455e-dfa1-42db-83cb-c987703f04b5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 5630200a1ad1d30f6d89b38e15179f15b699fa9f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78545964"
---
# <a name="maximizing-performance-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>ASP.NET 4 Web uygulamasındaki Entity Framework 4,0 ile performansı en üst düzeye çıkarın

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Bu öğretici serisi, [Entity Framework 4,0 öğretici serisi Ile çalışmaya](https://asp.net/entity-framework/tutorials#Getting%20Started) başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. Önceki öğreticileri tamamlamadıysanız, bu öğretici için bir başlangıç noktası olarak, oluşturduğunuz [uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Ayrıca, tüm öğretici serileri tarafından oluşturulan [uygulamayı da indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) . Öğreticiler hakkında sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx)gönderebilirsiniz.

Önceki öğreticide eşzamanlılık çakışmalarını nasıl işleyeceğinizi gördünüz. Bu öğreticide, Entity Framework kullanan bir ASP.NET Web uygulamasının performansını iyileştirmeye yönelik seçenekler gösterilmektedir. Performansı en üst düzeye çıkarmak veya performans sorunlarını tanılamak için çeşitli yöntemler öğreneceksiniz.

Aşağıdaki bölümlerde sunulan bilgiler, çok çeşitli senaryolarda yararlı olabilir:

- İlgili verileri verimli bir şekilde yükleyin.
- Görünüm durumunu yönetin.

Aşağıdaki bölümlerde sunulan bilgiler, performans sorunları sunan tekil sorgulara sahipseniz yararlı olabilir:

- `NoTracking` birleştirme seçeneğini kullanın.
- LINQ sorguları ön derleme.
- Veritabanına gönderilen sorgu komutlarını inceleyin.

Aşağıdaki bölümde sunulan bilgiler, son derece büyük veri modellerine sahip uygulamalar için yararlı olabilir:

- Görünümleri önceden oluştur.

> [!NOTE]
> Web uygulaması performansı, istek ve yanıt verilerinin boyutu, veritabanı sorgularının hızı, sunucunun sıraya kaç istek yaptığı ve hatta herhangi bir verimlilik gibi birçok faktörden etkilenir. kullanmakta olabileceğiniz istemci betiği kitaplıkları. Uygulamanızda performans önemliyse veya test veya deneyim, uygulama performansının tatmin edici olmadığını gösteriyorsa, performans ayarlaması için normal Protokolü izlemeniz gerekir. Performans sorunlarının nerede oluştuğunu belirleme ve ardından Genel uygulama performansı üzerinde en yüksek etkiye sahip olan alanlara yönelik ölçüm.
> 
> Bu konu, temel olarak ASP.NET 'deki Entity Framework özellikle performansı iyileştirebilmeniz için odaklanmaktadır. Buradaki öneriler, veri erişiminin uygulamanızdaki performans darboğazların biri olduğunu tespit ediyorsanız yararlı olur. Aksi belirtilmedikçe, burada açıklanan yöntemler genel olarak&quot; en iyi uygulamalar &quot;düşünülmemelidir; bunların çoğu yalnızca olağanüstü durumlarda uygundur veya çok özel performans sorunlarını ele alınır.

Öğreticiyi başlatmak için, Visual Studio 'Yu başlatın ve önceki öğreticide birlikte çalıştığınız Contoso University Web uygulamasını açın.

## <a name="efficiently-loading-related-data"></a>Ilgili verileri verimli bir şekilde yükleme

Entity Framework bir varlığın gezinti özelliklerine ilgili verileri yükleyebilmesinin birkaç yolu vardır:

- *Yavaş yükleme*. Varlık ilk kez okunmadıysa ilgili veriler alınmadı. Ancak, bir gezinti özelliğine ilk kez erişmeye çalıştığınızda, bu gezinti özelliği için gereken veriler otomatik olarak alınır. Bu, tek bir varlığın kendisi için ve varlık için ilgili verilerin alınması gereken her seferinde veritabanına gönderilen birden çok sorguya neden olur. 

    [![Image05](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

*Eager yükleniyor*. Varlık okurken ilgili veriler onunla birlikte alınır. Bu, genellikle gereken tüm verileri alan tek bir JOIN sorgusuna neden olur. Bu öğreticilerde gördüğünüz gibi `Include` yöntemi kullanılarak Eager yüklemesi belirlersiniz.

[![Image07](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

- *Açık yükleme*. Bu, yavaş yüklemeye benzer, ancak kodda ilgili verileri açıkça almanızı sağlar; bir gezinti özelliğine eriştiğinizde otomatik olarak gerçekleşmez. Koleksiyonlar için Gezinti özelliğinin `Load` yöntemini kullanarak ilgili verileri el ile yüklersiniz veya tek bir nesneyi tutan özellikler için Reference özelliğinin `Load` yöntemini kullanırsınız. (Örneğin, bir `Department` varlığının `Person` gezinti özelliğini yüklemek için `PersonReference.Load` yöntemini çağırabilirsiniz.)

    [![Image06](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

Özellik değerlerini hemen almadıklarından, geç yükleme ve açık yükleme aynı zamanda *ertelenmiş yükleme*olarak da bilinir.

Yavaş yükleme, tasarımcı tarafından oluşturulan bir nesne bağlamı için varsayılan davranıştır. Nesne bağlamı sınıfını tanımlayan *SchoolModel.Designer.cs* dosyasını açarsanız üç Oluşturucu yöntemi bulacaksınız ve her biri aşağıdaki ifadeyi içerir:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

Genel olarak, alınan her varlık için ilgili verilerin gerekli olduğunu biliyorsanız, tek bir sorgu veritabanına gönderilen tek bir sorgu genellikle alınan her varlık için ayrı sorgulardan daha verimli olduğundan, Eager yüklemesi en iyi performansı sunar. Öte yandan, bir varlığın gezinti özelliklerine yalnızca seyrek veya yalnızca küçük bir varlık kümesi için erişmeniz gerekiyorsa, yükleme veya açık yükleme daha verimli olabilir, çünkü Eager yüklemesi gereksiniminizden daha fazla veri alacaktır.

Bir Web uygulamasında, ilgili verilerin gereksinimini etkileyen Kullanıcı eylemleri tarayıcıda gerçekleştiğinden, sayfanın oluşturulduğu nesne bağlamına bağlantısı bulunmayan bir Web uygulamasında yavaş yükleme görece küçük bir değer olabilir. Öte yandan, bir denetimi bir denetimin üzerine gönderdiğinizde, genellikle ihtiyacınız olan verileri öğrenmiş olursunuz ve bu nedenle, her bir senaryoya uygun olan öğeleri temel alarak ekip yüklemeyi veya ertelenmiş yüklemeyi seçmeniz genellikle en iyisidir.

Ayrıca, bir veri sınırlama denetimi, nesne bağlamı atıldıktan sonra bir varlık nesnesi kullanabilir. Bu durumda, bir gezinti özelliği için yavaş yükleme girişimi başarısız olur. Aldığınız hata iletisi boş: &quot;`The ObjectContext instance has been disposed and can no longer be used for operations that require a connection.`&quot;

`EntityDataSource` denetimi varsayılan olarak yavaş yüklemeyi devre dışı bırakır. Geçerli öğreticide kullandığınız `ObjectDataSource` denetimi için (veya sayfa kodundan nesne bağlamına eriştiğinizde), yavaş yüklemeyi varsayılan olarak devre dışı bırakabilirsiniz. Bir nesne bağlamını örneklediğinizde devre dışı bırakabilirsiniz. Örneğin, `SchoolRepository` sınıfının Oluşturucu yöntemine aşağıdaki satırı ekleyebilirsiniz:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Contoso Üniversitesi uygulaması için, nesne bağlamını otomatik olarak devre dışı bırakarak, bu özelliğin bir bağlam her oluşturulduğunda ayarlanması gerekmez.

*SchoolModel. edmx* veri modelini açın, tasarım yüzeyine tıklayın ve sonra Özellikler bölmesinde, **yavaş yükleme etkin** özelliğini `False`olarak ayarlayın. Veri modelini kaydedin ve kapatın.

[![Image04](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

## <a name="managing-view-state"></a>Görünüm durumunu yönetme

Güncelleştirme işlevselliği sağlamak için bir ASP.NET Web sayfası, bir sayfa işlendiğinde bir varlığın özgün özellik değerlerini depomalıdır. Geri gönderme işlemi sırasında denetim, varlığın orijinal durumunu yeniden oluşturabilir ve değişiklikleri uygulamadan önce varlığın `Attach` yöntemini çağırabilir ve `SaveChanges` metodunu çağırmaz. Varsayılan olarak, ASP.NET Web Forms veri denetimleri orijinal değerleri depolamak için görünüm durumunu kullanır. Ancak, durumu görüntüle performansı etkileyebilir, çünkü tarayıcıya gönderilen ve tarayıcıdan gönderilen sayfanın boyutunu önemli ölçüde artırabilirler.

Görünüm durumunu veya oturum durumu gibi alternatifleri yönetme teknikleri Entity Framework benzersiz değildir, bu nedenle bu öğretici bu konuya ayrıntılı olarak gidemez. Daha fazla bilgi için öğreticinin sonundaki bağlantılara bakın.

Ancak, sürüm 4 ' ün, Web Forms uygulamaların her ASP.NET geliştiricisi tarafından farkında olması gerektiğini görüntüleme durumu ile çalışma konusunda yeni bir yol sağlar: `ViewStateMode` özelliği. Bu yeni özellik sayfa veya Denetim düzeyinde ayarlanabilir ve bir sayfa için varsayılan olarak görünüm durumunu devre dışı bırakmanızı ve yalnızca bunu gerektiren denetimler için etkinleştirmenizi sağlar.

Performansın kritik olduğu uygulamalarda, her zaman sayfa düzeyinde görünüm durumunu devre dışı bırakmak ve yalnızca bunu gerektiren denetimler için etkinleştirmek iyi bir uygulamadır. Contoso Üniversitesi sayfalarındaki görünüm durumunun boyutu bu yöntem tarafından önemli ölçüde azaltılmaz, ancak nasıl çalıştığını görmek için bunu *eğitmenler. aspx* sayfası için yapmanız gerekir. Bu sayfada, Görünüm durumu devre dışı bırakılmış bir `Label` denetimi de dahil olmak üzere birçok denetim bulunur. Bu sayfadaki denetimlerin hiçbirinin görünüm durumunun etkin olması gerekmez. (`GridView` denetiminin `DataKeyNames` özelliği geri göndermeler arasında tutulması gereken durumu belirtir, ancak bu değerler denetim durumunda tutulur, bu da `ViewStateMode` özelliğinden etkilenmez.)

`Page` yönergesi ve `Label` denetim biçimlendirmesi şu anda aşağıdaki örneğe benzer:

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

Aşağıdaki değişiklikleri yapın:

- `Page` yönergesine `ViewStateMode="Disabled"` ekleyin.
- `Label` denetiminden `ViewStateMode="Disabled"` kaldırın.

Biçimlendirme şimdi aşağıdaki örneğe benzer:

[!code-aspx[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

Görünüm durumu artık tüm denetimler için devre dışı bırakıldı. Daha sonra Görünüm durumunu kullanması gereken bir denetim eklerseniz, tek yapmanız gereken, bu denetimin `ViewStateMode="Enabled"` özniteliğini içermelidir.

## <a name="using-the-notracking-merge-option"></a>NoTracking birleştirme seçeneğini kullanma

Bir nesne bağlamı veritabanı satırlarını aldığında ve bunları temsil eden varlık nesneleri oluşturduğunda, varsayılan olarak bu varlık nesnelerini de nesne durumu yöneticisini kullanarak izler. Bu izleme verileri bir önbellek görevi görür ve bir varlığı güncelleştirdiğinizde kullanılır. Bir Web uygulaması genellikle kısa süreli nesne bağlamı örneklerine sahip olduğu için sorgular genellikle izlenmesi gerekmeyen verileri döndürür çünkü bunları okuyan nesne bağlamı, okuma veya güncelleme yaptığı varlıkların herhangi biri yeniden kullanılır veya güncelleştirilir.

Entity Framework, nesne bağlamının bir *birleştirme seçeneği*belirleyerek varlık nesnelerini izleyip izlemediğini belirtebilirsiniz. Birleştirme seçeneğini tekil sorgular veya varlık kümeleri için ayarlayabilirsiniz. Bir varlık kümesi için ayarlarsanız bu, söz konusu varlık kümesi için oluşturulan tüm sorgular için varsayılan birleştirme seçeneğini ayarlamadığınızı gösterir.

Contoso University uygulaması için, depodan erişebileceğiniz varlık kümelerinin herhangi biri için izleme gerekmez, bu nedenle, depo sınıfında nesne bağlamını örneklediğinizde bu varlık kümeleri için Merge seçeneğini `NoTracking` olarak ayarlayabilirsiniz. (Bu öğreticide birleştirme seçeneğinin ayarlanması, uygulamanın performansına göre belirgin bir etkiye sahip olmayacaktır. `NoTracking` seçeneği, yalnızca belirli yüksek veri hacmi senaryolarında bir observable performans geliştirmesi yapmak olabilir.)

DAL klasöründe, *SchoolRepository.cs* dosyasını açın ve deponun eriştiği varlık kümeleri için birleştirme seçeneğini ayarlayan bir Oluşturucu yöntemi ekleyin:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

## <a name="pre-compiling-linq-queries"></a>LINQ sorgularını önceden derleme

Entity Framework, belirli bir `ObjectContext` örneğinin ömrü içinde Entity SQL bir sorgu çalıştırdığında sorgunun derlenmesi biraz zaman alır. Derlemenin sonucu önbelleğe alınır, bu da sorgunun sonraki yürütmelerinin çok daha hızlı olduğu anlamına gelir. LINQ sorguları benzer bir model izler, bu da sorguyu derlemek için gerekli olan çalışmanın bazıları sorgu her yürütüldüğünde yapılır. Diğer bir deyişle, LINQ sorguları için varsayılan olarak derleme sonuçlarının hepsi önbelleğe alınmaz.

Bir nesne bağlamının ömrü içinde defalarca çalıştırmayı düşündüğünüz bir LINQ sorgunuz varsa, derleme sonuçlarının tümünün LINQ sorgusunun ilk çalıştırıldığında önbelleğe alınmasına neden olan bir kod yazabilirsiniz.

Bir çizim olarak, bunu `SchoolRepository` sınıfında iki `Get` yöntemi için gerçekleştirirsiniz, bunlardan biri hiçbir parametre (`GetInstructorNames` yöntemi) ve bir parametre gerektirir (`GetDepartmentsByAdministrator` yöntemi). Aslında bu yöntemler, LINQ sorguları olmadıkları için derlenmek zorunda değildir.

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

Ancak, derlenmiş sorguları deneyebilmeniz için aşağıdaki LINQ sorguları olarak yazılmış gibi ilerlemeniz gerekir:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

Bu yöntemlerdeki kodu yukarıda gösterilen şekilde değiştirebilir ve devam etmeden önce çalıştığını doğrulamak için uygulamayı çalıştırabilirsiniz. Ancak aşağıdaki yönergeler, bunların önceden derlenmiş sürümlerini oluşturmak için hemen açılır.

*Dal* klasöründe bir sınıf dosyası oluşturun, *SchoolEntities.cs*olarak adlandırın ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

Bu kod, otomatik olarak oluşturulan nesne bağlamı sınıfını genişleten kısmi bir sınıf oluşturur. Kısmi sınıf, `CompiledQuery` sınıfının `Compile` yöntemini kullanarak iki derlenmiş LINQ sorgusu içerir. Ayrıca sorguları çağırmak için kullanabileceğiniz yöntemler de oluşturur. Bu dosyayı kaydedin ve kapatın.

Sonra, *SchoolRepository.cs*içinde, derlenmiş sorguları çağırmak için depo sınıfındaki mevcut `GetInstructorNames` ve `GetDepartmentsByAdministrator` yöntemlerini değiştirin:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

Daha önce olduğu gibi çalıştığını doğrulamak için *Departmanlar. aspx* sayfasını çalıştırın. `GetInstructorNames` yöntemi, yönetici açılan listesini doldurmak için çağrılır ve bir eğitmenin birden fazla departmanın yöneticisi olmadığını doğrulamak için **Güncelleştir** ' e tıkladığınızda `GetDepartmentsByAdministrator` yöntemi çağrılır.

[![Image03](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

Yalnızca nasıl yapılacağını görmek için Contoso University uygulamasındaki sorguları önceden derlediğiniz için değil, yaşamları performansını iyileştirecek. LINQ sorgularının ön derlemesi, kodunuza bir karmaşıklık düzeyi ekler. bu nedenle, yalnızca uygulamanızdaki performans sorunlarını temsil eden sorgular için bunu yaptığınızdan emin olun.

## <a name="examining-queries-sent-to-the-database"></a>Veritabanına gönderilen sorgular inceleniyor

Performans sorunlarını araştırırken, bazen Entity Framework veritabanına gönderdiği SQL komutlarının tam olarak bilmeniz yararlı olur. `IQueryable` nesnesiyle çalışıyorsanız, bunu yapmanın bir yolu `ToTraceString` metodunu kullanmaktır.

*SchoolRepository.cs*' de, `GetDepartmentsByName` yöntemindeki kodu aşağıdaki örnekle eşleşecek şekilde değiştirin:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.cs)]

`departments` değişken yalnızca bir `ObjectQuery` türüne, önceki satırın sonundaki `Where` yöntemi bir `IQueryable` nesnesi oluşturduğundan, bu tür olarak ayarlanmalıdır; `Where` yöntemi olmadan, atama gerekli değildir.

`return` satırında bir kesme noktası ayarlayın ve ardından hata ayıklayıcıda *Departmanlar. aspx* sayfasını çalıştırın. Kesme noktasına ulaştığınızda, **Yereller** penceresindeki `commandText` değişkenini inceleyin ve **metin Görselleştirici penceresinde değerini** göstermek için metin Görselleştirici ( **değer** sütununda Büyüteç Camı) kullanın. Bu kodun sonucu olan tüm SQL komutunu görebilirsiniz:

[![Image08](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

Alternatif olarak, Visual Studio Ultimate IntelliTrace özelliği, kodunuzun değiştirilmesini veya hatta bir kesme noktası ayarlamanızı gerektirmeyen Entity Framework tarafından oluşturulan SQL komutlarını görüntülemenin bir yolunu sunar.

> [!NOTE]
> Aşağıdaki yordamları yalnızca Visual Studio Ultimate sahipseniz gerçekleştirebilirsiniz.

`GetDepartmentsByName` yönteminde orijinal kodu geri yükleyin ve ardından hata ayıklayıcıda *Departmanlar. aspx* sayfasını çalıştırın.

Visual Studio 'da **Hata Ayıkla** menüsünü, ardından **IntelliTrace**' i ve sonra **IntelliTrace olayları**' nı seçin.

[![Image11](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

**IntelliTrace** penceresinde **Tümünü kes**' e tıklayın.

[![Image12](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

**IntelliTrace** penceresi, son olayların bir listesini görüntüler:

[![Image09](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

**ADO.net** satırına tıklayın. Komut metnini gösterecek şekilde genişler:

[![Image10](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

Tüm komut metni dizesini **Yereller** penceresinden panoya kopyalayabilirsiniz.

Basit `School` veritabanından daha fazla tablo, ilişki ve sütun içeren bir veritabanıyla çalıştığınızı varsayın. Birden çok `Join` yan tümcesi içeren tek bir `Select` bildiriminde ihtiyacınız olan tüm bilgileri toplayan bir sorgunun verimli bir şekilde çalışması çok karmaşık hale geldiğini fark edebilirsiniz. Bu durumda, sorguyu basitleştirmek için Eager yüklemeden açık yüklemeye geçiş yapabilirsiniz.

Örneğin, *SchoolRepository.cs*içindeki `GetDepartmentsByName` yönteminde kodu değiştirmeyi deneyin. Şu anda bu yöntemde, `Person` ve `Courses` gezinme özellikleri için `Include` yöntemlere sahip bir nesne sorgunuz vardır. `return` ifadesini, aşağıdaki örnekte gösterildiği gibi açık yüklemeyi gerçekleştiren kodla değiştirin:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

Hata ayıklayıcıda *Departmanlar. aspx* sayfasını çalıştırın ve daha önce yaptığınız gibi **IntelliTrace** penceresini tekrar denetleyin. Artık, daha önce tek bir sorgu olduğu durumlarda, uzun bir sıra görürsünüz.

[![Image13](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

Daha önce görüntülediğiniz karmaşık sorguya ne olduğunu görmek için ilk **ADO.net** satırına tıklayın.

[![Image14](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

Departmanlardan sorgu, `Join` yan tümcesi olmadan basit bir `Select` sorgusu haline geldi, ancak özgün sorgu tarafından döndürülen her bir departman için iki sorgu kümesi kullanarak ilgili Kurslar ve bir yönetici alan ayrı sorgular izlenir.

> [!NOTE]
> Geç yüklemeyi etkin bırakırsanız, burada gördüğünüz model, aynı sorgu birçok kez tekrarlandığında, yavaş yükleme işleminden kaynaklanabilir. Genellikle kaçınmak istediğiniz bir model, birincil tablonun her satırı için ilgili verilerin geç olarak yüklenmesine yöneliktir. Tek bir birleşme sorgusunun verimli olması için çok karmaşık olduğunu doğrulamadığınız müddetçe, genellikle birincil sorguyu Eager yüklemesi kullanacak şekilde değiştirerek bu gibi durumlarda performansı artırabilirsiniz.

## <a name="pre-generating-views"></a>Önceden üretilen görünümler

Yeni bir uygulama etki alanında bir `ObjectContext` nesnesi ilk oluşturulduğunda, Entity Framework, veritabanına erişmek için kullandığı bir sınıf kümesi oluşturur. Bu sınıflara *Görünümler*adı verilir ve çok büyük bir veri modeliniz varsa, bu görünümleri oluşturmak, yeni bir uygulama etki alanı başlatıldıktan sonra Web sitesinin bir sayfanın ilk isteğine yanıtını erteleyebilir. Çalışma zamanı yerine derleme zamanında görünümleri oluşturarak bu ilk istek gecikmesini azaltabilirsiniz.

> [!NOTE]
> Uygulamanızın son derece büyük bir veri modeli yoksa veya büyük bir veri modeli varsa ancak IIS geri dönüştürüldükten sonra yalnızca ilk sayfa isteğini etkileyen bir performans sorunuyla ilgilenmiyorsa, bu bölümü atlayabilirsiniz. Görünüm oluşturma, görünümler uygulama etki alanında önbelleğe alındığından, her bir `ObjectContext` nesnesi örneğini her başlattığınızda gerçekleşmez. Bu nedenle, uygulamanızı IIS 'de sık geri değiştirmediğiniz müddetçe çok az sayıda sayfa isteği önceden oluşturulmuş görünümlerden faydalanır.

*EdmGen. exe* komut satırı aracını kullanarak veya bir *metin şablonu dönüştürme araç seti* (T4) şablonu kullanarak görünümleri önceden oluşturabilirsiniz. Bu öğreticide bir T4 şablonu kullanacaksınız.

*Dal* klasöründe, **metin şablonu** şablonunu kullanarak bir dosya ekleyin (Bu, **yüklü şablonlar** listesindeki **genel** düğümüdür) ve *SchoolModel.views.tt*olarak adlandırın. Dosyadaki mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

Bu kod, şablonla aynı klasörde bulunan ve şablon dosyasıyla aynı ada sahip olan bir *. edmx* dosyası için görünümler oluşturur. Örneğin, şablon dosyanız *SchoolModel.views.tt*olarak adlandırılmışsa, *SchoolModel. edmx*adlı bir veri modeli dosyası arar.

Dosyayı kaydedin, ardından **Çözüm Gezgini** dosyasında dosyaya sağ tıklayın ve **özel aracı Çalıştır**' ı seçin.

[![Image02](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Visual Studio, şablonu temel alan *SchoolModel.views.cs* adlı görünümleri oluşturan bir kod dosyası oluşturur. (Şablon dosyasını kaydettikten hemen sonra **özel araç Çalıştır**' ı seçmeden önce bile kod dosyasının oluşturulduğunu fark etmiş olabilirsiniz.)

[![Image01](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

Şimdi uygulamayı çalıştırabilir ve daha önce olduğu gibi çalıştığını doğrulayabilirsiniz.

Önceden oluşturulmuş görünümler hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Nasıl yapılır: msdn Web sitesinde sorgu performansını artırmak Için görünümleri önceden oluşturma](https://msdn.microsoft.com/library/bb896240.aspx) . Görünümleri önceden oluşturmak için `EdmGen.exe` komut satırı aracının nasıl kullanılacağını açıklar.
- Windows Server AppFabric müşteri danışmanlığı ekip blogundan [Entity Framework 4 ' te önceden derlenmiş/önceden oluşturulmuş görünümlerle performansı yalıtma](https://blogs.msdn.com/b/appfabriccat/archive/2010/08/06/isolating-performance-with-precompiled-pre-generated-views-in-the-entity-framework-4.aspx) .

Bu, Entity Framework kullanan bir ASP.NET Web uygulamasındaki performansı iyileştirmeye giriş işlemini tamamlar. Daha fazla bilgi için aşağıdaki kaynaklara bakın:

- MSDN Web sitesindeki [performans konuları (Entity Framework)](https://msdn.microsoft.com/library/cc853327.aspx) .
- [Entity Framework ekip blogundan performansla ilgili gönderiler](https://blogs.msdn.com/b/adonet/archive/tags/performance/).
- [EF birleştirme seçenekleri ve derlenmiş sorgular](https://blogs.msdn.com/b/dsimmons/archive/2010/01/12/ef-merge-options-and-compiled-queries.aspx). Derlenmiş sorguların beklenmeyen davranışlarını ve `NoTracking`gibi birleştirme seçeneklerini açıklayan blog gönderisi. Uygulamanızda derlenmiş sorgular kullanmayı veya birleştirme seçenek ayarlarını işlemeyi planlıyorsanız, önce bunu okuyun.
- [Veri ve modelleme müşteri danışmanlığı ekip bloguna Entity Framework ilgili gönderiler](https://blogs.msdn.com/b/dmcat/archive/tags/entity+framework/). , Derlenmiş sorgularda gönderi ve Visual Studio 2010 Profiler kullanarak performans sorunlarını bulmayı içerir.
- [Son derece karmaşık sorguların performansını iyileştirmeye yönelik öneriler içeren Forum iş parçacığı Entity Framework](https://social.msdn.microsoft.com/Forums/adodotnetentityframework/thread/ffe8b2ab-c5b5-4331-8988-33a872d0b5f6).
- [ASP.NET durum yönetimi önerileri](https://msdn.microsoft.com/library/z1hkazw7.aspx).
- [Entity Framework ve ObjectDataSource 'ı kullanma: özel sayfalama](http://geekswithblogs.net/Frez/articles/using-the-entity-framework-and-the-objectdatasource-custom-paging.aspx). Bu öğreticilerde oluşturulan ContosoUniversity uygulamasında oluşturulan ve *Departmanlar. aspx* sayfasında nasıl sayfalama uygulanacağını açıklayan blog gönderisi.

Sonraki öğreticide sürüm 4 ' te yeni olan Entity Framework önemli geliştirmelerden bazıları inceedilir.

> [!div class="step-by-step"]
> [Önceki](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application.md)
> [İleri](what-s-new-in-the-entity-framework-4.md)
