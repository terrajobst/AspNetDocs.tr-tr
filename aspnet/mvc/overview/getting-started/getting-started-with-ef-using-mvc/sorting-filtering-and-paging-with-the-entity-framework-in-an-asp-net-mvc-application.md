---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: bir ASP.NET MVC uygulamasındaki Entity Framework sıralama, filtreleme ve sayfalama ekleme | Microsoft Docs'
author: tdykstra
description: Bu öğreticide, **öğrenciler** dizin sayfasına sıralama, filtreleme ve sayfalama işlevselliği eklersiniz. Ayrıca basit bir gruplama sayfası da oluşturursunuz.
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616041"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>Öğretici: bir ASP.NET MVC uygulamasındaki Entity Framework sıralama, filtreleme ve sayfalama ekleme

[Önceki öğreticide](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), `Student` varlıkların temel CRUD işlemleri için bir dizi Web sayfası uyguladık. Bu öğreticide, **öğrenciler** dizin sayfasına sıralama, filtreleme ve sayfalama işlevselliği eklersiniz. Ayrıca basit bir gruplama sayfası da oluşturursunuz.

Aşağıdaki görüntüde, işiniz bittiğinde sayfanın nasıl görüneceğine ilişkin bir gösterilmektedir. Sütun başlıkları, kullanıcının sütuna göre sıralamak için tıkladığı bağlantılardır. Sütun başlığına tıklanması artan ve azalan sıralama düzeni arasında sürekli olarak geçiş yapar.

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Sütun sıralama bağlantıları Ekle
> * Arama kutusu ekleme
> * Sayfalama Ekle
> * Hakkında bir sayfa oluşturun

## <a name="prerequisites"></a>Önkoşullar

* [Temel CRUD İşlevselliği Uygulama](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>Sütun sıralama bağlantıları Ekle

Öğrenci dizini sayfasına sıralama eklemek için `Student` denetleyicisinin `Index` yöntemini değiştireceksiniz ve `Student` dizin görünümüne kod eklersiniz.

### <a name="add-sorting-functionality-to-the-index-method"></a>Dizin yöntemine sıralama işlevi ekleme

- *Controllers\studentcontroller.cs*içinde `Index` yöntemini aşağıdaki kodla değiştirin:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

Bu kod, URL 'deki sorgu dizesinden bir `sortOrder` parametresi alır. Sorgu dizesi değeri, ASP.NET MVC tarafından eylem yöntemine bir parametre olarak sağlanır. Parametresi, "Name" veya "Date" adlı bir dizedir, isteğe bağlı olarak alt çizgi ve azalan sıra belirtmek için "desc" dizesi gelir. Varsayılan sıralama düzeni artan.

Dizin sayfası ilk kez istendiğinde sorgu dizesi yoktur. Öğrenciler `LastName`göre artan sırada görüntülenir. Bu, varsayılan olarak, `switch` deyimindeki karşı bir durum tarafından oluşturulmuştur. Kullanıcı bir sütun başlığı köprüsüne tıkladığında, sorgu dizesinde uygun `sortOrder` değeri sağlanır.

İki `ViewBag` değişkeni, görünümün sütun başlığı köprülerini uygun sorgu dizesi değerleriyle yapılandırabilmesi için kullanılır:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Bunlar Üçlü ifadelerdir. Birincisi, `sortOrder` parametresi null veya boş ise `ViewBag.NameSortParm` "ad\_desc" olarak ayarlanmalıdır; Aksi takdirde, boş bir dizeye ayarlanmalıdır. Bu iki deyim, görünümün sütun başlığı köprülerini şu şekilde ayarlamaya olanak tanır:

| Geçerli sıralama düzeni | Son ad Köprüsü | Tarih Köprüsü |
| --- | --- | --- |
| Artan son ad | descending | ascending |
| Azalan son ad | ascending | ascending |
| Artan Tarih | ascending | descending |
| Azalan Tarih | ascending | ascending |

Yöntemi, sıralama yapılacak sütunu belirtmek için [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) kullanır. Kod, `switch` ifadesinden önce bir <xref:System.Linq.IQueryable%601> değişkeni oluşturur, `switch` ifadesinde değiştirir ve `switch` deyimden sonra `ToList` yöntemini çağırır. `IQueryable` değişkenleri oluşturup değiştirirken veritabanına hiçbir sorgu gönderilmez. Sorgu, `ToList`gibi bir yöntemi çağırarak `IQueryable` nesnesini bir koleksiyona dönüştürene kadar yürütülmez. Bu nedenle, bu kod `return View` ifadeye kadar Yürütülmeyen tek bir sorgu ile sonuçlanır.

Her sıralama düzeni için farklı LINQ deyimleri yazmanın alternatif olarak, dinamik olarak bir LINQ deyimi oluşturabilirsiniz. Dinamik LINQ hakkında daha fazla bilgi için bkz. [DYNAMIC LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>Öğrenci dizini görünümüne sütun başlığı köprüleri ekleme

1. *Views\student\ındex.cshtml*içinde, başlık satırı için `<tr>` ve `<th>` öğelerini vurgulanan kodla değiştirin:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   Bu kod, uygun sorgu dizesi değerleriyle köprüler ayarlamak için `ViewBag` özelliklerindeki bilgileri kullanır.

2. Sıralamayı doğrulamak için sayfayı çalıştırın ve **son ad** ve **kayıt tarihi** sütun başlıklarına tıklayın.

   **Son ad** başlığına tıkladıktan sonra, öğrenciler azalan son ad sırasıyla görüntülenir.

## <a name="add-a-search-box"></a>Arama kutusu ekleme

Öğrenciler dizin sayfasına filtre eklemek için, görünüme bir metin kutusu ve Gönder düğmesi ekleyeceksiniz ve `Index` yönteminde ilgili değişiklikleri yapmanız gerekir. Metin kutusu, ilk ad ve soyadı alanlarında arama yapmak için bir dize girmenize olanak sağlar.

### <a name="add-filtering-functionality-to-the-index-method"></a>Dizin yöntemine filtreleme işlevi ekleme

- *Controllers\studentcontroller.cs*içinde `Index` yöntemini aşağıdaki kodla değiştirin (değişiklikler vurgulanır):

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

Kod, `Index` yöntemine bir `searchString` parametresi ekler. Arama dizesi değeri, dizin görünümüne ekleyeceğiniz bir metin kutusundan alınır. Ayrıca, LINQ ifadesine yalnızca adı veya soyadı olan, arama dizesini içeren öğrencileri seçen bir `where` yan tümcesi ekler. <xref:System.Linq.Queryable.Where%2A> yan tümcesini ekleyen deyimi, yalnızca aranacak bir değer varsa yürütülür.

> [!NOTE]
> Çoğu durumda, bir Entity Framework varlık kümesinde veya bir bellek içi koleksiyonda uzantı yöntemi olarak aynı yöntemi çağırabilirsiniz. Sonuçlar normalde aynıdır, ancak bazı durumlarda farklı olabilir.
>
> Örneğin, `Contains` yönteminin .NET Framework uygulanması, buna boş bir dize geçirdiğinizde tüm satırları döndürür, ancak SQL Server Compact 4,0 Entity Framework sağlayıcısı boş dizeler için sıfır satır döndürür. Bu nedenle örnekteki kod (`Where` deyimin `if` bir deyimin içine yerleştirilmesi), tüm SQL Server sürümleri için aynı sonuçları elde ettiğinizden emin olmanızı sağlar. Ayrıca, `Contains` yönteminin .NET Framework uygulanması, varsayılan olarak büyük/küçük harfe duyarlı bir karşılaştırma gerçekleştirir, ancak Entity Framework SQL Server sağlayıcılar varsayılan olarak büyük/küçük harfe duyarsız karşılaştırmalar yapar. Bu nedenle, testi açık büyük/küçük harfe duyarsız hale getirmek için `ToUpper` yöntemini çağırmak, daha sonra kodu bir `IQueryable` nesnesi yerine `IEnumerable` bir koleksiyon döndürecek şekilde değiştirdiğinizde sonuçların değişmemesini sağlar. (Bir `IEnumerable` koleksiyonunda `Contains` yöntemini çağırdığınızda .NET Framework uygulamasını alırsınız; bunu bir `IQueryable` nesnesi üzerinde çağırdığınızda, veritabanı sağlayıcısı uygulamasını alırsınız.)
>
> Null işleme, farklı veritabanı sağlayıcıları için veya bir `IEnumerable` koleksiyonu kullandığınızda ile karşılaştırıldığında `IQueryable` bir nesne kullandığınızda da farklı olabilir. Örneğin, bazı senaryolarda `table.Column != 0` gibi `Where` bir koşul, değer olarak `null` olan sütunları döndürmeyebilir. Varsayılan olarak, null değerler arasındaki eşitlik, bellekte çalışır şekilde veritabanında çalışır, ancak bu davranışı yapılandırmak için, EF6 içinde [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) bayrağını ayarlayabilir veya EF Core [Userelationalnulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) metodunu çağırabilirsiniz.

### <a name="add-a-search-box-to-the-student-index-view"></a>Öğrenci dizini görünümüne arama kutusu ekleme

1. *Views\student\ındex.cshtml*içinde, bir başlık, metin kutusu ve bir **arama** düğmesi oluşturmak için, açılan `table` etiketinden hemen önce vurgulanan kodu ekleyin.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. Sayfayı çalıştırın, bir arama dizesi girin ve filtreleme 'nin çalıştığını doğrulamak için **Ara** ' ya tıklayın.

   URL 'nin "bir" arama dizesi içermediğini, yani bu sayfaya yer işareti eklerseniz, yer işaretini kullandığınızda filtrelenmiş listeyi almadığına dikkat edin. Bu, tüm listeyi sıralacağından, sütun sıralama bağlantıları için de geçerlidir. **Arama** düğmesini daha sonra öğreticide daha sonra filtre ölçütlerine yönelik Sorgu dizelerini kullanacak şekilde değiştirirsiniz.

## <a name="add-paging"></a>Sayfalama Ekle

Öğrenciler dizin sayfasına sayfalama eklemek için **Pagedlist. Mvc** NuGet paketini yükleyerek başlayacaksınız. Daha sonra `Index` yönteminde başka değişiklikler yapar ve `Index` görünümüne sayfalama bağlantıları ekleyebilirsiniz. **Pagedlist. Mvc** , ASP.NET MVC için çok iyi sayfalama ve sıralama paketlerinden biridir ve burada kullanılması, diğer seçeneklerin bir önerisi olarak değil yalnızca örnek olarak tasarlanmıştır.

### <a name="install-the-pagedlistmvc-nuget-package"></a>PagedList. MVC NuGet paketini yükler

NuGet **pagedlist. Mvc** paketi, **pagedlist** paketini otomatik olarak bir bağımlılık olarak yüklüyor. **Pagedlist** paketi, `IQueryable` ve `IEnumerable` koleksiyonları için `PagedList` bir koleksiyon türü ve genişletme yöntemleri yüklüyor. Uzantı yöntemleri `IQueryable` veya `IEnumerable``PagedList` koleksiyonda tek bir veri sayfası oluşturur ve `PagedList` koleksiyonu, sayfalama işlemini kolaylaştıran çeşitli özellikler ve yöntemler sağlar. **Pagedlist. Mvc** paketi, sayfalama düğmelerini görüntüleyen bir sayfalama Yardımcısı yüklüyor.

1. **Araçlar** menüsünde, **NuGet Paket Yöneticisi** ' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin.

2. **Paket Yöneticisi konsol** penceresinde, **paket kaynağının** **NuGet.org** olduğundan ve **varsayılan projenin** **contosouniversity**olduğundan emin olun ve ardından şu komutu girin:

   ```text
   Install-Package PagedList.Mvc
   ```

3. Projeyi oluşturun.

### <a name="add-paging-functionality-to-the-index-method"></a>Dizin yöntemine sayfalama işlevselliği ekleme

1. *Controllers\studentcontroller.cs*içinde, `PagedList` ad alanı için `using` bir ifade ekleyin:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. `Index` yöntemini aşağıdaki kod ile değiştirin:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   Bu kod bir `page` parametresi, geçerli bir sıralama düzeni parametresi ve Yöntem imzasına geçerli bir filtre parametresi ekler:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   Sayfa ilk kez görüntülenirken veya Kullanıcı bir sayfalama veya sıralama bağlantısına tıklamamışsa, tüm parametreler null olur. Bir sayfalama bağlantısına tıklandıysanız, `page` değişkeni görüntülenecek sayfa numarasını içerir.

   `ViewBag` özelliği geçerli sıralama düzeni ile görünüm sağlar, çünkü bu sıralama sırasını sayfalama sırasında aynı tutmak için disk belleği bağlantılarına dahil edilmesi gerekir:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   `ViewBag.CurrentFilter`başka bir özellik, geçerli filtre dizesiyle görünüm sağlar. Bu değer, disk belleği sırasında filtre ayarlarını korumak için disk belleği bağlantılarına dahil olmalıdır ve sayfa yeniden görüntülenirken metin kutusuna geri yüklenmesi gerekir. Arama dizesi sayfalama sırasında değiştirilmişse, yeni filtre farklı verilerin görüntülenmesini sağladığından sayfanın 1 olarak sıfırlanması gerekir. Metin kutusuna bir değer girildiğinde ve Gönder düğmesine basıldığında arama dizesi değişir. Bu durumda `searchString` parametresi null değildir.

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   Yöntemin sonunda, öğrenciler `IQueryable` nesnesindeki `ToPagedList` uzantısı yöntemi, öğrenci sorgusunu, sayfalama destekleyen bir koleksiyon türünde tek bir öğrenciler sayfasına dönüştürür. Bu tek bir öğrenci sayfası daha sonra görünüme geçirilir:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   `ToPagedList` yöntemi bir sayfa numarası alır. İki soru işareti, [null birleşim işlecini](/dotnet/csharp/language-reference/operators/null-coalescing-operator)temsil eder. Null birleşim işleci, Nullable bir tür için varsayılan değeri tanımlar; `(page ?? 1)` ifadesi bir değere sahipse `page` değerini döndürür veya `page` null ise 1 döndürür.

### <a name="add-paging-links-to-the-student-index-view"></a>Öğrenci dizini görünümüne sayfalama bağlantıları ekleme

1. *Views\student\ındex.cshtml*içinde, var olan kodu aşağıdaki kodla değiştirin. Değişiklikler vurgulanır.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   Sayfanın üst kısmındaki `@model` ifade, görünümün artık `List` nesnesi yerine `PagedList` bir nesne aldığından emin olarak belirtir.

   `PagedList.Mvc` için `using` deyimleri, sayfalama düğmelerinin MVC Yardımcısı 'na erişim sağlar.

   Kod, bir [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) aşırı yüklemesi kullanarak [FormMethod. Get](/previous-versions/aspnet/dd460179(v=vs.100))belirlemesine izin verir.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   Varsayılan [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) , form VERILERINI bir gönderiyle gönderir, yani Parametreler, URL 'de sorgu dizeleri olarak değil http ileti gövdesinde geçirilir. HTTP GET belirttiğinizde, form verileri URL 'ye sorgu dizeleri olarak geçirilir ve bu da kullanıcıların URL 'ye yer işareti eklemesini sağlar. [Http get kullanımı Için W3C yönergeleri](http://www.w3.org/2001/tag/doc/whenToUseGet.html) , eylem bir güncelleştirmeye neden olmadığında Al ' ın kullanılması önerilir.

   Metin kutusu geçerli arama dizesiyle başlatılır, böylece yeni bir sayfaya tıkladığınızda geçerli arama dizesini görebilirsiniz.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   Sütun üst bilgisi bağlantıları, kullanıcının filtre sonuçları içinde sıralama yapabilmesi için geçerli arama dizesini denetleyiciye geçirmek için sorgu dizesini kullanır:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   Geçerli sayfa ve toplam sayfa sayısı görüntülenir.

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   Görüntülenecek sayfa yoksa, "sayfa 0/0" görüntülenir. (Bu durumda, `Model.PageNumber` 1 olduğu ve `Model.PageCount` 0 olduğu için sayfa numarası sayfa sayısından daha büyük olur.)

   Sayfalama düğmeleri `PagedListPager` Yardımcısı tarafından görüntülenir:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   `PagedListPager` Yardımcısı, URL 'Ler ve stil oluşturma da dahil olmak üzere özelleştirebilmeniz gereken birkaç seçenek sağlar. Daha fazla bilgi için GitHub sitesindeki [Troyıgocode/PagedList](https://github.com/TroyGoode/PagedList) bölümüne bakın.

2. Sayfayı çalıştırın.

   Disk belleğinin çalıştığından emin olmak için farklı sıralama emirlerindeki disk belleği bağlantılarına tıklayın. Daha sonra bir arama dizesi girin ve sayfalama ve filtreleme ile doğru şekilde çalıştığını doğrulamak için sayfalama işlemi yeniden deneyin.

## <a name="create-an-about-page"></a>Hakkında bir sayfa oluşturun

Contoso Üniversitesi web sitesinin hakkında sayfasında, her bir kayıt tarihi için kaç öğrenciye kaydolduğunu görüntüleyeceksiniz. Bu, gruplar üzerinde gruplandırma ve basit hesaplamalar gerektirir. Bunu gerçekleştirmek için aşağıdakileri yapmanız gerekir:

- Görünüme geçirmeniz gereken veriler için bir görünüm modeli sınıfı oluşturun.
- `Home` denetleyicisindeki `About` yöntemini değiştirin.
- `About` görünümünü değiştirin.

### <a name="create-the-view-model"></a>Görünüm modeli oluşturma

Proje klasöründe bir *Viewmodeller* klasörü oluşturun. Bu klasörde, *EnrollmentDateGroup.cs* bir sınıf dosyası ekleyin ve şablon kodunu şu kodla değiştirin:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>Ana denetleyiciyi değiştirme

1. *HomeController.cs*' de, dosyanın en üstüne aşağıdaki `using` deyimlerini ekleyin:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. Sınıf için açma küme ayracından hemen sonra veritabanı bağlamı için bir sınıf değişkeni ekleyin:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. `About` yöntemini aşağıdaki kod ile değiştirin:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   LINQ deyimleri, öğrenci varlıklarını kayıt tarihine göre gruplandırır, her bir gruptaki varlıkların sayısını hesaplar ve sonuçları bir `EnrollmentDateGroup` View model nesneleri koleksiyonunda depolar.

4. `Dispose` yöntemi ekleyin:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>Hakkında görünümünü değiştirme

1. *Views\home\about.exe* dosyasındaki kodu aşağıdaki kodla değiştirin:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. Uygulamayı çalıştırın ve **hakkında** bağlantısına tıklayın.

   Her kayıt tarihi için öğrenci sayısı bir tabloda görüntülenir.

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indirin](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Ek kaynaklar

Diğer Entity Framework kaynaklarına bağlantılar, [ASP.NET Data Access-önerilen kaynaklar](../../../../whitepapers/aspnet-data-access-content-map.md)bölümünde bulunabilir.

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Sütun sıralama bağlantıları Ekle
> * Arama kutusu ekleme
> * Sayfalama Ekle
> * Hakkında bir sayfa oluşturun

Bağlantı dayanıklılığı ve komut yakalaşmayı nasıl kullanacağınızı öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Bağlantı dayanıklılığı ve komut yakaalımı](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
