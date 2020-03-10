---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
title: Bir ASP.NET MVC uygulamasında depo ve Iş deseni birimi uygulama (9/10) | Microsoft Docs
author: tdykstra
description: Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 44761193-04ba-4990-9f90-145d3c10a716
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 18de9b125ee5d10795b9ce1a366918dadf4fc4e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540266"
---
# <a name="implementing-the-repository-and-unit-of-work-patterns-in-an-aspnet-mvc-application-9-of-10"></a>Bir ASP.NET MVC uygulamasında depo ve Iş deseni birimi uygulama (9/10)

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso Üniversitesi örnek Web uygulaması, Entity Framework 5 Code First ve Visual Studio 2012 kullanarak nasıl ASP.NET MVC 4 uygulamaları oluşturacağınızı gösterir. Öğretici serisi hakkında daha fazla bilgi için, [serideki ilk öğreticiye](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)bakın. Öğretici serisini başlangıçtan başlatabilir veya [Bu bölüm için bir başlangıç projesi indirebilir](building-the-ef5-mvc4-chapter-downloads.md) ve buradan başlayabilirsiniz.
> 
> > [!NOTE] 
> > 
> > Giderebileceğiniz bir sorunla karşılaşırsanız, [Tamamlanan bölümü indirin](building-the-ef5-mvc4-chapter-downloads.md) ve sorununuzu yeniden oluşturmaya çalışın. Sorunu, kodunuzun tamamlanan kodla karşılaştırarak genellikle soruna çözüm olarak ulaşabilirsiniz. Bazı yaygın hatalar ve bunların nasıl çözüleceği için bkz [. hatalar ve geçici çözümler.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

Önceki öğreticide, `Student` ve `Instructor` varlık sınıflarında gereksiz kodu azaltmak için devralmayı kullandınız. Bu öğreticide, CRUD işlemleri için depoyu ve iş desenleri birimini kullanmanın bazı yollarını görürsünüz. Önceki öğreticide olduğu gibi, bu, kodunuzun yeni sayfalar oluşturmak yerine zaten oluşturduğunuz sayfalarla çalışma biçimini değiştireceksiniz.

## <a name="the-repository-and-unit-of-work-patterns"></a>Depo ve Iş birimi düzenleri

Depo ve çalışma birimi düzenleri, veri erişim katmanı ve bir uygulamanın iş mantığı katmanı arasında bir soyutlama katmanı oluşturmak için tasarlanmıştır. Bu desenleri uygulamak, uygulamanızın veri deposundaki değişikliklerden yalıtılmış hale getirmenize yardımcı olabilir ve otomatik birim testi veya test odaklı geliştirmeyi (TDD) kolaylaştırabilir.

Bu öğreticide, her varlık türü için bir depo sınıfı uygulayacaksınız. `Student` varlık türü için bir depo arabirimi ve bir depo sınıfı oluşturacaksınız. Denetleyiciyi denetleyicinizde başlattığınızda, denetleyicinin, depo arabirimini uygulayan herhangi bir nesneye yönelik bir başvuruyu kabul edeceği şekilde arabirimini kullanacaksınız. Denetleyici bir Web sunucusu altında çalıştığında, Entity Framework ile çalışan bir depoyu alır. Denetleyici bir birim testi sınıfı altında çalıştığında, bir bellek içi koleksiyon gibi test için kolayca işleyebileceğiniz şekilde depolanan verilerle çalışan bir depo alır.

Öğreticide daha sonra, `Course` denetleyicisindeki `Course` ve `Department` varlık türleri için birden çok depo ve bir çalışma birimi sınıfı kullanacaksınız. Çalışma birimi sınıfı, hepsi tarafından paylaşılan tek bir veritabanı bağlam sınıfı oluşturarak birden çok depodaki çalışmayı koordine eder. Otomatik birim testi gerçekleştirebilmek istiyorsanız, bu sınıflar için `Student` deposunda yaptığınız gibi arabirimler oluşturup kullanacaksınız. Ancak, Öğreticiyi bir şekilde korumak için bu sınıfları arabirimler olmadan oluşturup kullanacaksınız.

Aşağıdaki çizimde, denetleyici ve bağlam sınıfları arasındaki ilişkileri, bir veya daha fazla iş deseninin kullanıldığı bir şekilde kullanmayın.

![Repository_pattern_diagram](https://asp.net/media/2578149/Windows-Live-Writer_8c4963ba1fa3_CE3B_Repository_pattern_diagram_1df790d3-bdf2-4c11-9098-946ddd9cd884.png)

Bu öğretici serisinde birim testlerini oluşturmayacağız. Depo deseninin kullanıldığı bir MVC uygulamasıyla TDD 'ye giriş için bkz. [Walkthrough: ASP.NET MVC Ile TDD kullanma](https://msdn.microsoft.com/library/ff847525.aspx). Depo düzeniyle ilgili daha fazla bilgi için aşağıdaki kaynaklara bakın:

- MSDN 'deki [Depo deseninin](https://msdn.microsoft.com/library/ff649690.aspx) .
- Entity Framework ekibi blogu üzerinde [Entity Framework 4,0 Ile depo ve çalışma birimi biçimlerini kullanma](https://blogs.msdn.com/b/adonet/archive/2009/06/16/using-repository-and-unit-of-work-patterns-with-entity-framework-4-0.aspx) .
- Julie Lerman 'ın blogdaki [çevik Entity Framework 4 depo](http://thedatafarm.com/blog/data-access/agile-entity-framework-4-repository-part-1-model-and-poco-classes/) serisi.
- Hesabı, dan Wahlin blogundan [bir BAKıŞTA HTML5/jQuery uygulamasında oluşturma](https://weblogs.asp.net/dwahlin/archive/2011/08/15/building-the-account-at-a-glance-html5-jquery-application.aspx) .

> [!NOTE]
> Depoyu ve iş deseni birimini uygulamak için birçok yol vardır. Depo sınıflarını, çalışma birimi sınıfı olmadan veya bunlarla birlikte kullanabilirsiniz. Tüm varlık türleri veya her tür için tek bir depo uygulayabilirsiniz. Her tür için bir tane uygularsanız, ayrı sınıflar, genel bir temel sınıf ve türetilmiş sınıflar ya da bir soyut temel sınıf ve türetilmiş sınıflar kullanabilirsiniz. Deponuza iş mantığı ekleyebilir veya onu veri erişim mantığı ile kısıtlayabilirsiniz. Ayrıca, varlık kümeleriniz için [dbset](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx) türleri yerine, [ıdbset](https://msdn.microsoft.com/library/gg679233(v=vs.103).aspx) arabirimlerini kullanarak veritabanı bağlamı sınıfınızda bir soyutlama katmanı da oluşturabilirsiniz. Bu öğreticide gösterilen bir soyutlama katmanını uygulamaya yönelik yaklaşım, tüm senaryolar ve ortamların önerisi değil dikkate almanız gereken tek seçenektir.

## <a name="creating-the-student-repository-class"></a>Öğrenci deposu sınıfı oluşturma

*Dal* klasöründe, *IStudentRepository.cs* adlı bir sınıf dosyası oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample1.cs)]

Bu kod, iki okuma `Student` yöntemi de dahil olmak üzere tipik bir CRUD yöntemi kümesi bildirir ve tek bir `Student` varlığı KIMLIĞE göre bulur.

*Dal* klasöründe, *StudentRepository.cs* dosyası adlı bir sınıf dosyası oluşturun. Mevcut kodu, `IStudentRepository` arabirimini uygulayan aşağıdaki kodla değiştirin:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample2.cs)]

Veritabanı bağlamı bir sınıf değişkeninde tanımlanır ve Oluşturucu çağıran nesnenin bağlam örneğine geçirilmesini bekler:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample3.cs)]

Depoda yeni bir bağlam örneği oluşturabilirsiniz, ancak daha sonra bir denetleyicide birden çok depo kullandıysanız, her biri ayrı bir bağlam ile sona erdir. Daha sonra `Course` denetleyicisinde birden çok depo kullanacaksınız ve iş sınıfının bir biriminin tüm depoların aynı bağlamı kullanmasını nasıl sağlayabilecekleri hakkında bilgi edineceksiniz.

Depo, [IDisposable](https://msdn.microsoft.com/library/system.idisposable.aspx) 'yi uygular ve daha önce denetleyicide gördüğünüz şekilde veritabanı bağlamını bırakır ve CRUD yöntemleri, daha önce gördüğünüz gibi veritabanı bağlamına çağrı yapar.

## <a name="change-the-student-controller-to-use-the-repository"></a>Öğrenci denetleyicisini depoyu kullanacak şekilde değiştirme

*StudentController.cs*içinde, şu anda sınıfındaki kodu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=13-18,44,75,77,102-103,120,137-138,159,172-174,186)]

Denetleyici artık bağlam sınıfı yerine `IStudentRepository` arabirimini uygulayan bir nesne için bir sınıf değişkeni bildiriyor:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample5.cs)]

Varsayılan (parametresiz) Oluşturucu yeni bir bağlam örneği oluşturur ve isteğe bağlı bir Oluşturucu çağıranın bir bağlam örneğine geçmesini sağlar.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample6.cs)]

( *Bağımlılık ekleme*veya di kullanıyorsanız, varsayılan oluşturucuya ihtiyacınız yoktur, çünkü dı yazılımı doğru depo nesnesinin her zaman sağlanması gerekir.)

CRUD yöntemlerinde, depo artık bağlam yerine çağırılır:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample7.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample8.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample9.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample10.cs)]

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample11.cs)]

`Dispose` yöntemi artık bağlamı yerine depoyu ortadan kaldırmıştır:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample12.cs)]

Siteyi çalıştırın ve **öğrenciler** sekmesine tıklayın.

![Students_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image1.png)

Sayfa, depoyu kullanmak üzere kodu değiştirmeden önce olduğu gibi görünür ve aynı şekilde çalışır ve diğer öğrenci sayfaları da aynı şekilde çalışır. Ancak, denetleyicinin `Index` yönteminin filtrelenmesini ve sıralanmasını sağlamanın önemli bir farkı vardır. Bu yöntemin orijinal sürümü aşağıdaki kodu içeriyordu:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample13.cs?highlight=1)]

Güncelleştirilmiş `Index` yöntemi aşağıdaki kodu içerir:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample14.cs?highlight=1)]

Yalnızca vurgulanan kod değiştirilmiştir.

Kodun orijinal sürümünde `students` bir `IQueryable` nesnesi olarak yazılır. Sorgu, `ToList`gibi bir yöntem kullanılarak bir koleksiyona dönüştürülene kadar, dizin görünümü öğrenci modeline erişene kadar gerçekleşmeyen veritabanına gönderilmez. Yukarıdaki özgün koddaki `Where` yöntemi veritabanına gönderilen SQL sorgusunda bir `WHERE` yan tümcesi haline gelir. Bu da, veritabanı tarafından yalnızca seçili varlıkların döndürüldüğü anlamına gelir. Ancak, `context.Students` `studentRepository.GetStudents()`değiştirme sonucu olarak, bu deyimden sonraki `students` değişkeni, veritabanındaki tüm öğrencileri içeren bir `IEnumerable` koleksiyonudur. `Where` yöntemi uygulamanın nihai sonucu aynıdır, ancak artık iş, veritabanı tarafından değil Web sunucusunda bellekte yapılır. Büyük hacimli veriler döndüren sorgular için bu verimsiz olabilir.

> [!TIP]
> 
> **IQueryable vs. IEnumerable**
> 
> Depoyu burada gösterildiği gibi uyguladıktan sonra, **arama** kutusuna gönderilen sorgu SQL Server, arama ölçütlerinizi Içermediğinden tüm öğrenci satırlarını döndürür.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image2.png)
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample15.sql)]
> 
> Bu sorgu, depo Sorgu ölçütlerini bilmeden sorguyu yürütülebildiğinden tüm öğrenci verilerini döndürür. Sıralama, arama ölçütlerini uygulama ve sayfalama için verilerin bir alt kümesini seçme işlemi (Bu durumda yalnızca 3 satır gösteriliyor), daha sonra `IEnumerable` koleksiyonunda `ToPagedList` yöntemi çağrıldığında bellekte yapılır.
> 
> Kodun önceki sürümünde (Depoyu uygulamadan önce), `IQueryable` nesnesi üzerinde `ToPagedList` çağrıldığında, sorgu, arama ölçütlerini Uygulamadıktan sonra veritabanına gönderilmez.
> 
> ![](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image3.png)
> 
> ToPagedList bir `IQueryable` nesnesinde çağrıldığında, SQL Server gönderilen sorgu arama dizesini belirtir ve sonuç olarak yalnızca arama ölçütlerine uyan satırlar döndürülür ve bellekte hiçbir filtreleme yapılması gerekmez.
> 
> [!code-sql[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample16.sql)]
> 
> (Aşağıdaki öğreticide SQL Server gönderilen sorguların nasıl inceleneceği açıklanmaktadır.)

Aşağıdaki bölümde, bu çalışmanın veritabanı tarafından yapılması gerektiğini belirtmenize olanak tanıyan depo yöntemlerinin nasıl uygulanacağı gösterilmektedir.

Artık denetleyici ve Entity Framework veritabanı bağlamı arasında bir soyutlama katmanı oluşturdunuz. Bu uygulamayla otomatik birim testi gerçekleştirecekseniz, `IStudentRepository`uygulayan bir birim testi projesinde alternatif bir depo sınıfı oluşturabilirsiniz *.* Verileri okumak ve yazmak için bağlam çağırmak yerine, bu sahte havuz sınıfı, denetleyici işlevlerini test etmek için bellek içi koleksiyonları işleyebilir.

## <a name="implement-a-generic-repository-and-a-unit-of-work-class"></a>Genel bir depo ve Iş sınıfı birimi uygulama

Her varlık türü için bir depo sınıfı oluşturmak, çok fazla sayıda kod oluşmasına neden olabilir ve bu da kısmi güncelleştirmelere neden olabilir. Örneğin, aynı işlemin parçası olarak iki farklı varlık türünü güncelleştirmeniz gerektiğini varsayalım. Her biri ayrı bir veritabanı bağlamı örneği kullanıyorsa, biri başarılı olabilir ve diğeri başarısız olabilir. Gereksiz kodu en aza indirecek bir yol, genel bir depoyu ve tüm depoların aynı veritabanı bağlamını kullandığından emin olmanın bir yoludur (ve bu nedenle tüm güncelleştirmeleri koordine etmek) bir iş sınıfı birimi kullanmaktır.

Öğreticinin bu bölümünde, hem `Department` hem de `Course` varlık kümelerine erişmek için bir `GenericRepository` sınıfı ve `UnitOfWork` sınıfı oluşturacak ve bunları `Course` denetleyicide kullanacaksınız. Daha önce açıklandığı gibi, öğreticinin bu bölümünü basit tutmak için, bu sınıflar için arabirim oluşturulmazlar. Ancak bunları, TDD 'yi kolaylaştırmak için kullanacaksanız, genellikle bunları `Student` depoyu yaptığınız şekilde arayüzlerle birlikte uygulamalısınız.

### <a name="create-a-generic-repository"></a>Genel depo oluşturma

*Dal* klasöründe *GenericRepository.cs* oluşturun ve mevcut kodu şu kodla değiştirin:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample17.cs)]

Sınıf değişkenleri, veritabanı bağlamı ve deponun örneklendiği varlık kümesi için bildirilmiştir:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample18.cs)]

Oluşturucu bir veritabanı bağlamı örneğini kabul eder ve varlık kümesi değişkenini başlatır:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample19.cs)]

`Get` yöntemi, çağıran kodun bir filtre koşulu ve sonuçları sıralamak için bir sütun belirtmesini sağlamak üzere lambda ifadeleri kullanır ve bir dize parametresi, çağıranın, yükleme için bir virgülle ayrılmış gezinti özellikleri listesi sağlamasına imkan tanır:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample20.cs)]

Kod `Expression<Func<TEntity, bool>> filter`, çağıranın `TEntity` türüne göre bir lambda ifadesi sağlayacağı ve bu ifade bir Boolean değer döndürecek anlamına gelir. Örneğin, `Student` varlık türü için depo örneği oluşturulduğunda, çağıran yöntemdeki kod `filter` parametresi için `student => student.LastName == "Smith`&quot; belirtebilir.

Kod `Func<IQueryable<TEntity>, IOrderedQueryable<TEntity>> orderBy` Ayrıca çağıranın bir lambda ifadesi sağlayacağı anlamına gelir. Ancak bu durumda, ifadeye giriş, `TEntity` türü için bir `IQueryable` nesnesidir. İfade, bu `IQueryable` nesnesinin sıralı bir sürümünü döndürür. Örneğin, `Student` varlık türü için depo örneği oluşturulduğunda, çağıran yöntemdeki kod `orderBy` parametresi için `q => q.OrderBy(s => s.LastName)` belirtebilir.

`Get` yöntemindeki kod bir `IQueryable` nesnesi oluşturur ve sonra filtre ifadesini uygular:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample21.cs)]

Daha sonra, virgülle ayrılmış listeyi ayrıştırdıktan sonra Eager yükleme ifadelerini uygular:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample22.cs)]

Son olarak, bir tane varsa `orderBy` ifadesini uygular ve sonuçları döndürür; Aksi halde, sıralanmamış sorgunun sonuçlarını döndürür:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample23.cs)]

`Get` yöntemini çağırdığınızda, bu işlevler için parametreler sağlamak yerine yöntemi tarafından döndürülen `IEnumerable` koleksiyonunda filtreleme ve sıralama yapabilirsiniz. Ancak sıralama ve filtreleme işi Web sunucusunda bellekte yapılır. Bu parametreleri kullanarak, işin Web sunucusu yerine veritabanı tarafından yapıldığından emin olursunuz. Diğer bir seçenek de belirli varlık türleri için türetilmiş sınıflar oluşturmak ve `GetStudentsInNameOrder` veya `GetStudentsByName`gibi özelleştirilmiş `Get` Yöntemler eklemektir. Ancak, karmaşık bir uygulamada bu, çok sayıda türetilmiş sınıfa ve özel yöntemlere neden olabilir ve bu da sürdürmek için daha fazla iş olabilir.

`GetByID`, `Insert`ve `Update` yöntemlerindeki kod, genel olmayan depoda gördüğünüzle benzerdir. (`Find` yöntemiyle birlikte yükleme yapamıyorsanız `GetByID` imzasında bir Eager yükleme parametresi sağlamamazsınız.)

`Delete` yöntemi için iki aşırı yükleme sağlanır:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample24.cs)]

Bunlardan biri, yalnızca silinecek varlığın KIMLIĞINI ve bir varlık örneği almanızı sağlar. Eşzamanlılık öğreticisini [gerçekleştirirken](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) , eşzamanlılık işleme için, bir izleme özelliğinin orijinal değerini içeren bir varlık örneği alan `Delete` bir yönteme ihtiyacınız vardır.

Bu genel depo, normal CRUD gereksinimlerini işleyecek. Belirli bir varlık türünün daha karmaşık filtre veya sıralama gibi özel gereksinimleri olduğunda, bu tür için ek yöntemlere sahip türetilmiş bir sınıf oluşturabilirsiniz.

## <a name="creating-the-unit-of-work-class"></a>Iş sınıfı birimi oluşturma

İş sınıfı birimi bir amaca hizmet eder: birden çok depo kullandığınızda emin olmak için, tek bir veritabanı bağlamını paylaşır. Bu şekilde, bir iş birimi tamamlandığında, bağlam örneği üzerinde `SaveChanges` yöntemini çağırabilir ve ilgili tüm değişikliklerin koordine olmasını sağlayabilirsiniz. Sınıfın ihtiyaç duyacağı her bir depo için bir `Save` yöntemi ve bir özelliktir. Her depo özelliği, diğer depo örnekleriyle aynı veritabanı bağlamı örneği kullanılarak oluşturulan bir depo örneği döndürür.

*Dal* klasöründe, *UnitOfWork.cs* adlı bir sınıf dosyası oluşturun ve şablon kodunu şu kodla değiştirin:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample25.cs)]

Kod, veritabanı bağlamı ve her depo için sınıf değişkenleri oluşturur. `context` değişkeni için yeni bir bağlam örneği oluşturulur:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample26.cs)]

Her depo özelliği, deponun zaten var olup olmadığını denetler. Aksi takdirde, içerik örneğini geçirerek depoyu başlatır. Sonuç olarak, tüm depolar aynı bağlam örneğini paylaşır.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample27.cs)]

`Save` yöntemi, veritabanı bağlamına `SaveChanges` çağırır.

Bir sınıf değişkeninde bir veritabanı bağlamını örnekleyen herhangi bir sınıf gibi, `UnitOfWork` sınıfı `IDisposable` uygular ve bağlamı ortadan kaldırmaktadır.

### <a name="changing-the-course-controller-to-use-the-unitofwork-class-and-repositories"></a>Kurs denetleyicisini UnitOfWork sınıfını ve depoları kullanacak şekilde değiştirme

*CourseController.cs* içinde bulunan kodu şu kodla değiştirin:

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample28.cs?highlight=15,20,22,31,54-55,70,85-86,101-102,122-124,130)]

Bu kod, `UnitOfWork` sınıfı için bir sınıf değişkeni ekler. (Burada arabirimleri kullanıyorsanız, değişkeni burada başlatmadınız. bunun yerine, `Student` deposu için yaptığınız gibi iki oluşturucuların bir modelini uygulamalısınız.)

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample29.cs)]

Sınıfın geri kalanında, veritabanı bağlamına yapılan tüm başvurular, depoya erişmek için `UnitOfWork` özellikleri kullanılarak uygun depoya başvurularla değiştirilmiştir. `Dispose` yöntemi `UnitOfWork` örneğini ortadan kaldırır.

[!code-csharp[Main](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/samples/sample30.cs)]

Siteyi çalıştırın ve **Kurslar** sekmesine tıklayın.

![Courses_Index_page](implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application/_static/image4.png)

Sayfa, yaptığınız değişikliklerle aynı şekilde görünür ve çalışır ve diğer kurs sayfaları da aynı şekilde çalışır.

## <a name="summary"></a>Özet

Artık hem depoyu hem de iş düzeni birimini uyguladık. Genel depoda Yöntem parametreleri olarak lambda ifadeleri kullandınız. Bu ifadelerin `IQueryable` nesne ile nasıl kullanılacağı hakkında daha fazla bilgi için MSDN Kitaplığı 'nda [IQueryable (t) arabirimi (System. LINQ)](https://msdn.microsoft.com/library/bb351562.aspx) konusuna bakın. Sonraki öğreticide, bazı gelişmiş senaryoları nasıl işleyeceğinizi öğreneceksiniz.

Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET veri erişimi Içerik haritasında](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.

> [!div class="step-by-step"]
> [Önceki](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [İleri](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)
