---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
title: 'Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 2. Bölüm: Iş mantığı katmanı ve birim testleri ekleme | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, Entity Framework 4,0 öğretici serisi ile çalışmaya başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: efb0e677-10b8-48dc-93d3-9ba3902dd807
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests
msc.type: authoredcontent
ms.openlocfilehash: 24344cc33d7c26d7c408db26c0530ef2c708a7d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546769"
---
# <a name="using-the-entity-framework-40-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests"></a>Entity Framework 4,0 ve ObjectDataSource denetimini kullanma, 2. Bölüm: Iş mantığı katmanı ve birim testleri ekleme

[Tom Dykstra](https://github.com/tdykstra) tarafından

> Bu öğretici serisi, [Entity Framework 4,0 öğretici serisi Ile çalışmaya](https://asp.net/entity-framework/tutorials#Getting%20Started) başlama tarafından oluşturulan Contoso University Web uygulamasında oluşturulur. Önceki öğreticileri tamamlamadıysanız, bu öğretici için bir başlangıç noktası olarak, oluşturduğunuz [uygulamayı indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Ayrıca, tüm öğretici serileri tarafından oluşturulan [uygulamayı da indirebilirsiniz](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) . Öğreticiler hakkında sorularınız varsa, bunları [ASP.NET Entity Framework forumuna](https://forums.asp.net/1227.aspx)gönderebilirsiniz.

Önceki öğreticide, Entity Framework ve `ObjectDataSource` denetimini kullanarak n katmanlı bir Web uygulaması oluşturdunuz. Bu öğreticide iş mantığı ekleme, iş mantığı katmanını (BLL) ve veri erişim katmanını (DAL) ayrı tutarken ve BLL için otomatik birim testlerinin nasıl oluşturulacağı gösterilmektedir.

Bu öğreticide aşağıdaki görevleri tamamlayacaksınız:

- İhtiyaç duyduğunuz veri erişim yöntemlerini bildiren bir depo arabirimi oluşturun.
- Depo sınıfında depo arabirimini uygulayın.
- Veri erişimi işlevlerini gerçekleştirmek için depo sınıfını çağıran bir iş mantığı sınıfı oluşturun.
- `ObjectDataSource` denetimini depo sınıfı yerine iş mantığı sınıfına bağlayın.
- Bir birim test projesi ve veri deposu için bellek içi koleksiyonları kullanan bir depo sınıfı oluşturun.
- İş mantığı sınıfına eklemek istediğiniz iş mantığı için bir birim testi oluşturun, ardından testi çalıştırın ve başarısız olarak görüntüleyin.
- İş mantığını iş mantığı sınıfında uygulayın, ardından birim testini yeniden çalıştırın ve ardından geçti.

Önceki öğreticide oluşturduğunuz *Departmanlar. aspx* ve *DepartmentsAdd. aspx* sayfalarıyla çalışacaksınız.

## <a name="creating-a-repository-interface"></a>Depo arabirimi oluşturma

Depo arabirimini oluşturarak başlarsınız.

[![Image08](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image2.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image1.png)

*Dal* klasöründe, yeni bir sınıf dosyası oluşturun, *ISchoolRepository.cs*olarak adlandırın ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample1.cs)]

Arabirim, depo sınıfında oluşturduğunuz CRUD (oluşturma, okuma, güncelleştirme, silme) yöntemlerinin her biri için bir yöntemi tanımlar.

*SchoolRepository.cs*içindeki `SchoolRepository` sınıfında, bu sınıfın `ISchoolRepository` arabirimini uyguladığını belirtir:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample2.cs)]

## <a name="creating-a-business-logic-class"></a>Iş mantığı sınıfı oluşturma

Ardından, iş mantığı sınıfını oluşturacaksınız. Bunu, `ObjectDataSource` denetimi tarafından yürütülecek iş mantığını ekleyebilmeniz, ancak bunu henüz yapamasanız da yapmanız gerekir. Şimdilik, yeni iş mantığı sınıfı yalnızca deponun gerçekleştirdiği CRUD işlemlerini gerçekleştirir.

[![Image09](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image4.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image3.png)

Yeni bir klasör oluşturun ve *BLL*olarak adlandırın. (Gerçek bir uygulamada, iş mantığı katmanı genellikle ayrı bir proje olmak üzere bir sınıf kitaplığı olarak uygulanır, ancak bu öğreticiyi tutmak için BLL sınıfları bir proje klasöründe tutulur.)

*BLL* klasöründe, yeni bir sınıf dosyası oluşturun, *SchoolBL.cs*olarak adlandırın ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample3.cs)]

Bu kod, daha önce depo sınıfında gördüğünüz CRUD yöntemlerini oluşturur, ancak Entity Framework yöntemlerine doğrudan erişmek yerine, depo Sınıfı yöntemlerini çağırır.

Depo sınıfına bir başvuruyu tutan sınıf değişkeni bir arabirim türü olarak tanımlanır ve depo sınıfını örnekleyen kod iki Oluşturucu içinde bulunur. Parametresiz Oluşturucu `ObjectDataSource` denetimi tarafından kullanılır. Daha önce oluşturduğunuz `SchoolRepository` sınıfının bir örneğini oluşturur. Diğer Oluşturucu, iş mantığı sınıfının, depo arabirimini uygulayan herhangi bir nesnede geçmesini sağlayan herhangi bir koda izin verir.

Depo sınıfını ve iki Oluşturucu çağıran CRUD yöntemleri, tercih ettiğiniz herhangi bir arka uç veri deposunda iş mantığı sınıfını kullanmayı mümkün kılar. İş mantığı sınıfının, çağırma sınıfının verileri nasıl devam ettiğini farkında olması gerekmez. (Bu genellikle *Kalıcılık Ignorance*olarak adlandırılır.) Bu, birim testini kolaylaştırır, çünkü iş mantığı sınıfını, verileri depolamak için bellek içi `List` koleksiyonlarında basit olarak bir şeyi kullanan bir depo uygulamasına bağlayabilirsiniz.

> [!NOTE]
> Teknik olarak, varlık nesneleri, Entity Framework `EntityObject` sınıfından kalıtımla alan sınıflardan örneklendiklerinden, hala Kalıcılık olmaya devam etmez. Tamamen kalıcılığı tahmin etmek için, `EntityObject` sınıfından kalıtımla alan nesnelerin yerine *düz eskı clr nesneleri*veya *Pocos*kullanabilirsiniz. POCOs kullanmanın Bu öğreticinin kapsamı dışındadır. Daha fazla bilgi için bkz. MSDN Web sitesinde [Test edilebilirlik ve Entity Framework 4,0](https://msdn.microsoft.com/library/ff714955.aspx) .)

Artık `ObjectDataSource` denetimlerini depoya değil iş mantığı sınıfına bağlayabilirsiniz ve her şeyin daha önce olduğu gibi çalıştığını doğrulayabilirsiniz.

*Departmanlar. aspx* ve *DepartmentsAdd. aspx*' de `TypeName="ContosoUniversity.DAL.SchoolRepository"` her oluşumunu `TypeName="ContosoUniversity.BLL.SchoolBL`"olarak değiştirin. (Tümünde dört örnek vardır.)

Daha önce olduğu gibi çalıştığını doğrulamak için *Departmanlar. aspx* ve *DepartmentsAdd. aspx* sayfalarını çalıştırın.

[![Image01](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image6.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image5.png)

[![Image02](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image8.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image7.png)

## <a name="creating-a-unit-test-project-and-repository-implementation"></a>Birim testi projesi ve depo uygulama oluşturma

**Test projesi** şablonunu kullanarak çözüme yeni bir proje ekleyin ve `ContosoUniversity.Tests`adlandırın.

Test projesinde, `System.Data.Entity` bir başvuru ekleyin ve `ContosoUniversity` projesine bir proje başvurusu ekleyin.

Artık birim testleriyle kullanacağınız depo sınıfını oluşturabilirsiniz. Bu depo için veri deposu sınıf içinde olacaktır.

[![Image12](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image10.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image9.png)

Test projesinde, yeni bir sınıf dosyası oluşturun, *MockSchoolRepository.cs*olarak adlandırın ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample4.cs)]

Bu depo sınıfı, doğrudan Entity Framework erişen aynı CRUD yöntemlerine sahiptir, ancak bir veritabanı yerine `List` koleksiyonlarıyla bellekte çalışır. Bu, bir test sınıfının iş mantığı sınıfına yönelik birim testlerini ayarlamayı ve doğrulamasını kolaylaştırır.

## <a name="creating-unit-tests"></a>Birim testleri oluşturma

**Test** projesi şablonu sizin için bir saplama birimi test sınıfı oluşturdu ve bir sonraki göreviniz, iş mantığı sınıfına eklemek istediğiniz iş mantığı için birim testi yöntemleri ekleyerek bu sınıfı değiştirmektir.

[![Image13](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image12.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image11.png)

Contoso University 'de, her bir eğitmen yalnızca tek bir departmanın yöneticisi olabilir ve bu kuralı zorlamak için iş mantığı eklemeniz gerekir. Testleri ekleyerek ve başarısız olduğunu görmek için testleri çalıştırarak başlayacaksınız. Daha sonra kodu ekleyecek ve testleri yeniden çalıştırabileceksiniz.

*UnitTest1.cs* dosyasını açın ve contosouniversity projesinde oluşturduğunuz iş mantığı ve veri erişim katmanları için `using` deyimlerini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample5.cs)]

`TestMethod1` yöntemini aşağıdaki yöntemlerle değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample6.cs)]

`CreateSchoolBL` yöntemi, daha sonra iş mantığı sınıfının yeni bir örneğine geçen birim test projesi için oluşturduğunuz depo sınıfının bir örneğini oluşturur. Yöntemi daha sonra, test yöntemlerinde kullanabileceğiniz üç departman eklemek için iş mantığı sınıfını kullanır.

Test yöntemleri, birisi mevcut bir departmanla aynı yöneticiye sahip yeni bir departman eklemeye çalışırsa veya bir kişinin KIMLIĞINI belirleyerek bir departmanın yöneticisini güncelleştirmeye çalışırsa, iş mantığı sınıfının bir özel durum oluşturduğundan emin olun. zaten başka bir departmanın yöneticisi.

Özel durum sınıfını henüz oluşturmadınız, bu nedenle bu kod derlenmeyecektir. Derlemek için, `DuplicateAdministratorException` sağ tıklayın ve **Oluştur**' u ve ardından **sınıf**' ı seçin.

[![Image14](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image14.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image13.png)

Bu, Test projesinde, ana projede özel durum sınıfını oluşturduktan sonra silebilmeniz için bir sınıf oluşturur. ve iş mantığını uyguladık.

Test projesini çalıştırın. Beklenen şekilde testler başarısız olur.

[![Image03](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image16.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image15.png)

## <a name="adding-business-logic-to-make-a-test-pass"></a>Test geçişi yapmak için Iş mantığı ekleme

Daha sonra, başka bir departmanı zaten yönetici olan bir departmanın yöneticisi olarak ayarlamayı olanaksız kılan iş mantığını uygulayacaksınız. İş mantığı katmanından bir özel durum oluşturacaksınız ve bir Kullanıcı bir departmanı düzenleip zaten yönetici olan birini seçtikten sonra **Güncelleştir** ' e tıkladıysanız sunu katmanında bu işlemi gerçekleştirebilirsiniz. (Ayrıca, sayfayı oluşturmadan önce yönetici olan açılan listeden da eğitmen 'i kaldırabilirsiniz, ancak buradaki amaç iş mantığı katmanıyla birlikte çalışır.)

Bir Kullanıcı bir eğitmeni bir taneden fazla departmanın yöneticisine kurmaya çalıştığında oluşturacağınız özel durum sınıfını oluşturarak başlayın. Ana projede *BLL* klasöründe yeni bir sınıf dosyası oluşturun, *DuplicateAdministratorException.cs*olarak adlandırın ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample7.cs)]

Şimdi derlemek için, daha önce test projesinde oluşturduğunuz geçici *DuplicateAdministratorException.cs* dosyasını silin.

Ana projede, *SchoolBL.cs* dosyasını açın ve doğrulama mantığını içeren aşağıdaki yöntemi ekleyin. (Kod, daha sonra oluşturacağınız bir yönteme başvurur.)

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample8.cs)]

Başka bir departmanın aynı yöneticiye sahip olup olmadığını denetlemek için `Department` varlıkları eklerken veya güncelleştirirken bu yöntemi çağıracaksınız.

Kod, eklenen veya güncellenen varlıkla aynı `Administrator` özellik değerine sahip bir `Department` varlığı için veritabanını aramak üzere bir yöntemi çağırır. Bir tane bulunursa, kod bir özel durum oluşturur. Eklenen veya güncellenen varlık `Administrator` değerine sahip değilse ve bu yöntem bir güncelleştirme sırasında çağrılırsa ve bulunan `Department` varlığı güncelleştirilmekte olan `Department` varlıkla eşleşiyorsa doğrulama denetimi gerekmez.

`Insert` ve `Update` metotlarından yeni yöntemi çağırın:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample9.cs)]

*ISchoolRepository.cs*' de, yeni veri erişim yöntemi için aşağıdaki bildirimi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample10.cs)]

*SchoolRepository.cs*' de aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample11.cs)]

*SchoolRepository.cs*' de, aşağıdaki yeni veri erişim yöntemini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample12.cs)]

Bu kod, belirtilen bir yöneticiye sahip `Department` varlıklarını alır. Yalnızca bir departman bulunması gerekir (varsa). Ancak, veritabanında bir kısıtlama bulunmadığından, birden çok departmanın bulunduğu durumlarda dönüş türü bir koleksiyondur.

Varsayılan olarak, nesne bağlamı veritabanından varlıkları aldığında, bunların nesne durumu yöneticisinde izlenmesini önler. `MergeOption.NoTracking` parametresi bu sorgu için bu izlemenin yapılmayacak olduğunu belirtir. Bu gereklidir çünkü sorgu, güncelleştirmeye çalıştığınız varlığı tam olarak döndürebilir ve bu varlığı iliştiremeyeceksiniz. Örneğin, *Departmanlar. aspx* sayfasında geçmiş departmanı düzenler ve yöneticiyi değiştirmeden bırakırsanız, bu sorgu geçmiş departmanı döndürür. `NoTracking` ayarlanmamışsa, nesne bağlamının, nesne durumu yöneticisinde geçmiş departmanı varlığı zaten vardır. Daha sonra, görünüm durumundan yeniden oluşturulan geçmiş departmanı varlığı iliştirildiğinde, nesne bağlamı `"An object with the same key already exists in the ObjectStateManager. The ObjectStateManager cannot track multiple objects with the same key"`belirten bir özel durum oluşturur.

(`MergeOption.NoTracking`belirtmeye alternatif olarak, yalnızca bu sorgu için yeni bir nesne bağlamı oluşturabilirsiniz. Yeni nesne bağlamı kendi nesne durumu yöneticisine sahip olacağından, `Attach` yöntemini çağırdığınızda hiçbir çakışma olmaz. Yeni nesne bağlamı, özgün nesne bağlamı ile meta veri ve veritabanı bağlantısı paylaşır, bu nedenle bu alternatif yaklaşımın performans cezası en düşük düzeyde olacaktır. Ancak burada gösterilen yaklaşım, diğer bağlamlarda yararlı bulacağınız `NoTracking` seçeneğini tanıtır. `NoTracking` seçeneği, bu serideki sonraki bir öğreticide daha ayrıntılı bir şekilde ele alınmıştır.)

Test projesinde, *MockSchoolRepository.cs*'e yeni veri erişim yöntemini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample13.cs)]

Bu kod, `ContosoUniversity` proje deposunun LINQ to Entities kullandığı aynı veri seçimini gerçekleştirmek için LINQ kullanır.

Test projesini yeniden çalıştırın. Testlerin geçişi bu kez yapılır.

[![Image04](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image18.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image17.png)

## <a name="handling-objectdatasource-exceptions"></a>ObjectDataSource özel durumlarını işleme

`ContosoUniversity` projesinde, *Departmanlar. aspx* sayfasını çalıştırın ve bir departmanın yöneticisini başka bir departman için zaten yönetici olan birisine değiştirmeyi deneyin. (Veritabanı geçersiz verilerle önceden yüklenmiş olarak geldiğinden, bu öğreticide yalnızca eklediğiniz departmanları düzenleyedeğiştirebileceğinizi unutmayın.) Aşağıdaki sunucu hata sayfasını alırsınız:

[![Image05](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image20.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image19.png)

Kullanıcıların bu tür bir hata sayfasını görmesini istemezsiniz, bu nedenle hata işleme kodu eklemeniz gerekir. *Departmanlar. aspx* ' i açın ve `DepartmentsObjectDataSource``OnUpdated` olayı için bir işleyici belirtin. `ObjectDataSource` açma etiketi artık aşağıdaki örneğe benzer.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample14.aspx)]

*Departments.aspx.cs*' de aşağıdaki `using` ifadesini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample15.cs)]

`Updated` olayı için aşağıdaki işleyiciyi ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample16.cs)]

`ObjectDataSource` denetimi, güncelleştirmeyi gerçekleştirmeye çalıştığında bir özel durumu yakalarsa, bu işleyicide olay bağımsız değişkeninde (`e`) özel durumu geçirir. İşleyicisindeki kod, özel durumun yinelenen yönetici özel durumu olup olmadığını denetler. Eğer ise, kod `ValidationSummary` denetimin görüntülemesi için bir hata iletisi içeren bir doğrulayıcı denetimi oluşturur.

Sayfayı çalıştırın ve birini iki bölümün yöneticisine tekrar yapmayı deneyin. Bu kez `ValidationSummary` denetiminde bir hata iletisi görüntülenir.

[![Image06](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image22.png)](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/_static/image21.png)

*DepartmentsAdd. aspx* sayfasında benzer değişiklikler yapın. *DepartmentsAdd. aspx*içinde, `DepartmentsObjectDataSource``OnInserted` olayı için bir işleyici belirtin. Ortaya çıkan biçimlendirme aşağıdaki örneğe benzeyecektir.

[!code-aspx[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample17.aspx)]

*DepartmentsAdd.aspx.cs*' de aynı `using` ifadesini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample18.cs)]

Aşağıdaki olay işleyicisini ekleyin:

[!code-csharp[Main](using-the-entity-framework-and-the-objectdatasource-control-part-2-adding-a-business-logic-layer-and-unit-tests/samples/sample19.cs)]

Artık *DepartmentsAdd.aspx.cs* sayfasını test edebilir ve aynı zamanda bir kişiye birden fazla departmanın yönetici yapma girişimlerini doğru bir şekilde işlediğini doğrulayabilirsiniz.

Bu işlem, Entity Framework `ObjectDataSource` denetimini kullanmak için depo deseninin uygulanması için giriş işlemini tamamlar. Depo deseninin ve test edilebilirlik hakkında daha fazla bilgi için bkz. MSDN teknik incelemesi [ve Entity Framework 4,0](https://msdn.microsoft.com/library/ff714955.aspx).

Aşağıdaki öğreticide, uygulamaya sıralama ve filtreleme işlevlerinin nasıl ekleneceğini göreceksiniz.

> [!div class="step-by-step"]
> [Önceki](using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md)
> [İleri](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
