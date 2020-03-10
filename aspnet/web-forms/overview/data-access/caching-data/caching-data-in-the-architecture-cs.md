---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
title: Mimaride verileri önbelleğe alma (C#) | Microsoft Docs
author: rick-anderson
description: Önceki öğreticide, sunum katmanında önbelleğe almayı nasıl uygulayacağınızı öğrendiniz. Bu öğreticide, katmanlı mimari CTU 'nin avantajlarından nasıl yararlanalabileceğinizi öğreniyoruz...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: d29a7c41-0628-4a23-9dfc-bfea9c6c1054
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
msc.type: authoredcontent
ms.openlocfilehash: 192cadb8e2f862ac2a97a36b375e247b281ece93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78551172"
---
# <a name="caching-data-in-the-architecture-c"></a>Mimaride Verileri Önbelleğe Alma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_CS.exe) veya [PDF 'yi indirin](caching-data-in-the-architecture-cs/_static/datatutorial59cs1.pdf)

> Önceki öğreticide, sunum katmanında önbelleğe almayı nasıl uygulayacağınızı öğrendiniz. Bu öğreticide, Iş mantığı katmanındaki verileri önbelleğe almak için katmanlı mimarimizden nasıl yararlanalabileceğinizi öğreniyoruz. Bunu, bir önbelleğe alma katmanı içerecek şekilde genişleterek yapacağız.

## <a name="introduction"></a>Giriş

Önceki öğreticide gördüğümüz gibi, ObjectDataSource verilerinin önbelleğe alınması, birkaç özelliği ayarlamak kadar basittir. Ne yazık ki, ObjectDataSource sunum katmanında önbelleğe alma uygular ve bu da önbelleğe alma ilkelerini ASP.NET sayfası ile sıkı bir şekilde bağar. Katmanlı mimari oluşturma nedenlerinden biri, bu tür bağların bozulmasına izin vermeleridir. Örneğin Iş mantığı katmanı, ASP.NET sayfalarından iş mantığını ayırır, ancak veri erişim katmanı veri erişim ayrıntılarını ayırır. İş mantığı ve veri erişimi ayrıntılarının bu şekilde ayrılması, sistemin daha okunabilir, daha fazla sürdürülebilir ve daha esnek bir şekilde değiştirilmesine olanak sağladığından, bölümünde tercih edilir. Ayrıca, etki alanı bilgisi ve işçiden çalışan bir geliştiricinin sunum katmanında çalışan bir geliştiricinin işini yapmak için veritabanı s ayrıntılarını öğrenme gereksinimi yoktur. Ön belleğe alma ilkesi sunum katmanından ayrılmaktadır, benzer avantajlar sunar.

Bu öğreticide, kendi önbelleğe alma ilkenizi kullanan bir *önbelleğe alma katmanı* (veya kısa için CL) dahil olmak üzere mimarimizi kullanacağız. Önbelleğe alma katmanı, `GetProducts()`, `GetProductsByCategoryID(categoryID)`, vb. gibi yöntemlerle ürün bilgilerine erişim sağlayan bir `ProductsCL` sınıfı içerir. Bu, çağrıldığında ilk olarak verileri önbellekten almaya çalışır. Önbellek boşsa, bu yöntemler BLL 'de uygun `ProductsBLL` yöntemini çağırır ve bu da verileri DAL 'ten alır. `ProductsCL` yöntemleri, BLL 'den alınan verileri döndürmeden önce önbelleğe alabilir.

Şekil 1 ' de gösterildiği gibi, CL sunum ve Iş mantığı katmanları arasında bulunur.

![Önbelleğe alma katmanı (CL) mimarimizde başka bir katmandır](caching-data-in-the-architecture-cs/_static/image1.png)

**Şekil 1**: önbelleğe alma KATMANı (CL) mimarimize ait başka bir katmandır

## <a name="step-1-creating-the-caching-layer-classes"></a>1\. Adım: önbelleğe alma katmanı sınıfları oluşturma

Bu öğreticide, tek bir sınıf olan `ProductsCL` basit bir CL oluşturacak ve yalnızca birkaç yöntem içeren bir. Tüm uygulama için tam bir önbelleğe alma katmanının oluşturulması, `CategoriesCL`, `EmployeesCL`ve `SuppliersCL` sınıfları oluşturmayı ve BLL içindeki her veri erişimi veya değiştirme yöntemi için bu önbelleğe alma katmanı sınıflarında bir yöntem sağlamayı gerektirir. BLL ve DAL gibi, önbelleğe alma katmanı ideal olarak ayrı bir sınıf kitaplığı projesi olarak uygulanmalıdır; Ancak, bunu `App_Code` klasöründe bir sınıf olarak uygulayacağız.

, DAL ve BLL sınıflarından CL sınıflarını daha temiz bir şekilde ayırmak için, s `App_Code` klasöründe yeni bir alt klasör oluşturalım. Çözüm Gezgini `App_Code` klasöre sağ tıklayın, yeni klasör ' i seçin ve yeni klasörü `CL`adlandırın. Bu klasörü oluşturduktan sonra, `ProductsCL.cs`adlı yeni bir sınıf ekleyin.

![CL adlı yeni bir klasör ve ProductsCL.cs adlı bir sınıf ekleyin](caching-data-in-the-architecture-cs/_static/image2.png)

**Şekil 2**: `CL` adlı yeni bir klasör ve `ProductsCL.cs` adlı bir sınıf ekleyin

`ProductsCL` sınıfı, karşılık gelen Iş mantığı katman sınıfında bulunan (`ProductsBLL`) aynı veri erişimi ve değiştirme yöntemleri kümesini içermelidir. Bu yöntemlerin tümünü oluşturmak yerine, yalnızca CL 'nin kullandığı desenleri almak için burada birkaç şey oluşturalım. Özellikle adım 3 ' teki `GetProducts()` ve `GetProductsByCategoryID(categoryID)` yöntemleri ve adım 4 ' te bir `UpdateProduct` aşırı yüklemesi ekleyeceğiz. Kalan `ProductsCL` yöntemleri ve `CategoriesCL`, `EmployeesCL`ve `SuppliersCL` sınıflarını boş bir şekilde ekleyebilirsiniz.

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>2\. Adım: veri önbelleğini okuma ve yazma

Önceki öğreticide araştırılan ObjectDataSource 'un önbelleğe alma özelliği, BLL 'den alınan verileri depolamak için ASP.NET veri önbelleğini dahili olarak kullanır. Veri önbelleğine Ayrıca, ASP.NET Pages arka plan kod sınıflarından veya Web uygulaması mimarisindeki sınıflardan programlı olarak erişilebilir. ASP.NET Page s arka plan kod sınıfından veri önbelleğini okumak ve yazmak için aşağıdaki kalıbı kullanın:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample1.cs)]

[`Cache` sınıf](https://msdn.microsoft.com/library/system.web.caching.cache.aspx) s [`Insert` yöntemi](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx) çok sayıda aşırı yükleme içeriyor. `Cache["key"] = value` ve `Cache.Insert(key, value)` eş anlamlı olduğundan, tanımlı süre sonu olmadan belirtilen anahtarı kullanarak önbelleğe bir öğe ekler. Genellikle, bir öğeyi bir bağımlılık, zaman tabanlı süre sonu veya her ikisi olarak önbelleğe eklerken bir süre sonu belirtmek istiyoruz. Bağımlılık veya zaman tabanlı süre sonu bilgilerini sağlamak için diğer `Insert` yöntemi aşırı yüklerinden birini kullanın.

Önbelleğe alma katmanının yöntemlerinin, öncelikle istenen verilerin önbellekte olup olmadığını denetlemesi gerekir ve varsa, buradan döndürün. İstenen veriler önbellekte değilse, uygun BLL yönteminin çağrılması gerekir. Aşağıdaki sıralı diyagramda gösterildiği gibi, dönüş değeri önbelleğe alınıp döndürülmelidir.

![Önbelleğe alma katmanı öğeleri, varsa verileri önbellekten döndürür](caching-data-in-the-architecture-cs/_static/image3.png)

**Şekil 3**: önbelleğe alma katmanı öğeleri, varsa verileri önbellekten döndürür

Şekil 3 ' te gösterilen sıra, CL sınıflarında aşağıdaki model kullanılarak gerçekleştirilir:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample2.cs)]

Burada *tür* , önbellekte depolanan verilerin türüdür `Northwind.ProductsDataTable`, örneğin, *anahtar* , önbellek öğesini benzersiz bir şekilde tanımlayan anahtardır. Belirtilen *anahtara* sahip öğe önbellekte değilse, *örnek* `null` olur ve veriler uygun BLL yönteminden alınır ve önbelleğe eklenir. `return instance` zamana ulaşıldığında, *örnek* önbellekten ya da BLL 'den çekilerek verilerin bir başvurusunu içerir.

Önbellekteki verilere erişirken yukarıdaki kalıbı kullandığınızdan emin olun. İlk bakışta eşdeğer olarak görünen aşağıdaki model, yarış koşulunu tanıtan bir hafif fark içerir. Yarış durumlarının hata ayıklaması zordur, çünkü kendilerini kendi sporlarını açığa çıkarır ve yeniden oluşturmak zordur.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample3.cs)]

Bu saniyelik fark, yanlış kod parçacığı, yerel bir değişkende önbelleğe alınmış öğeye başvuru depolamak yerine, veri önbelleğine doğrudan koşullu ifadede *ve* `return`erişildiğine göre yapılır. Bu koda ulaşıldığında, `Cache["key"]``null`olmayan, `return` bildirimine ulaşılmadan önce, sistem önbellekten çıkarılan *anahtarı* düşünün. Bu nadir durumda, kod beklenen türde bir nesne yerine bir `null` değer döndürür.

> [!NOTE]
> Veri önbelleği iş parçacığı açısından güvenlidir, bu nedenle basit okuma veya yazma işlemleri için iş parçacığı erişimini eşitlemeniz gerekmez. Ancak, atomik olması gereken önbellekteki veriler üzerinde birden çok işlem gerçekleştirmeniz gerekiyorsa, iş parçacığı güvenliğini sağlamak için bir kilit veya başka bir mekanizma uygulamaktan siz sorumlusunuz. Daha fazla bilgi için bkz. [ASP.net önbelleğine erişimi eşitleme](http://www.ddj.com/184406369) .

Bir öğe, bu gibi [`Remove` yöntemi](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx) kullanılarak veri önbelleğinden program aracılığıyla çıkartılanalabilir:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample4.cs)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>3\. Adım:`ProductsCL`sınıfından ürün bilgilerini döndürme

Bu öğreticide, s `ProductsCL` sınıfından ürün bilgilerini döndürmek için iki yöntem uygulayalim: `GetProducts()` ve `GetProductsByCategoryID(categoryID)`. Iş mantığı katmanındaki `ProductsBL` sınıfı gibi, CL 'deki `GetProducts()` yöntemi bir `Northwind.ProductsDataTable` nesnesi olarak tüm ürünlerin bilgilerini döndürür, ancak `GetProductsByCategoryID(categoryID)` belirtilen bir kategorideki tüm ürünleri döndürür.

Aşağıdaki kod `ProductsCL` sınıfındaki yöntemlerin bir parçasını gösterir:

[!code-vb[Main](caching-data-in-the-architecture-cs/samples/sample5.vb)]

İlk olarak, sınıf ve yöntemlere uygulanan `DataObject` ve `DataObjectMethodAttribute` özniteliklerini aklınızda edin. Bu öznitelikler, sihirbaz s adımlarında hangi sınıfların ve yöntemlerin görüneceğini belirten ObjectDataSource 'un sihirbazına ilişkin bilgiler sağlar. CL sınıfları ve yöntemlerine sunu katmanındaki bir ObjectDataSource 'tan erişildiğinden, tasarım zamanı deneyimini geliştirmek için bu öznitelikleri ekledik. Bu öznitelikler ve etkileri hakkında daha kapsamlı bir açıklama için [Iş mantığı katmanı oluşturma](../introduction/creating-a-business-logic-layer-cs.md) öğreticisine geri bakın.

`GetProducts()` ve `GetProductsByCategoryID(categoryID)` yöntemlerinde, `GetCacheItem(key)` yönteminden döndürülen veriler yerel bir değişkene atanır. Kısa süre içinde inceleyeceğiz `GetCacheItem(key)` yöntemi, belirtilen *anahtara*göre önbellekten belirli bir öğeyi döndürür. Önbellekte böyle bir veri bulunamazsa, karşılık gelen `ProductsBLL` Class yönteminden alınır ve `AddCacheItem(key, value)` yöntemi kullanılarak önbelleğe eklenir.

`GetCacheItem(key)` ve `AddCacheItem(key, value)` yöntemleri, veri önbelleği, sırasıyla değerleri okuma ve yazma ile arabirimidir. `GetCacheItem(key)` yöntemi iki basittir. Yalnızca geçirilen *anahtarı*kullanarak Cache sınıfından değeri döndürür:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample6.cs)]

`GetCacheItem(key)`, *anahtar* değeri sağlanan şekilde kullanmaz, ancak bunun yerine productscache-ile *anahtar* önüne geri dönüş döndüren `GetCacheKey(key)` yöntemini çağırır. ProductsCache dizesini tutan `MasterCacheKeyArray`, aynı anda kısaca göreceğiniz gibi `AddCacheItem(key, value)` yöntemi tarafından da kullanılır.

ASP.NET sayfa arka plan kod sınıfından veri önbelleğine `Page` Class s [`Cache` özelliği](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx)kullanılarak erişilebilir ve adım 2 ' de anlatıldığı gibi `Cache["key"] = value`gibi sözdizimine izin verir. Mimari içindeki bir sınıftan veri önbelleğine `HttpRuntime.Cache` veya `HttpContext.Current.Cache`kullanılarak erişilebilir. [Peter Johnson](https://weblogs.asp.net/pjohnson/default.aspx)'un blog girişi [HttpRuntime. Cache ile. HttpContext. Current. Cache](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache) , `HttpContext.Current`yerine `HttpRuntime` kullanmanın hafif performans avantajlarından yararlanır. Sonuç olarak, `ProductsCL` `HttpRuntime`kullanır.

> [!NOTE]
> Mimariniz sınıf kitaplığı projeleri kullanılarak uygulanırsa, [httpRuntime](https://msdn.microsoft.com/library/system.web.httpruntime.aspx) ve [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) sınıflarını kullanabilmeniz için `System.Web` derlemesine bir başvuru eklemeniz gerekir.

Öğe önbellekte bulunamazsa, `ProductsCL` sınıfı yöntemleri BLL 'den verileri alır ve `AddCacheItem(key, value)` metodunu kullanarak önbelleğe ekler. Önbelleğe *değer* eklemek için, 60 saniyelik zaman aşımı süresi kullanan aşağıdaki kodu kullanabiliriz:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample7.cs)]

`DateTime.Now.AddSeconds(CacheDuration)`, gelecekte zaman tabanlı süre sonu 60 saniye belirtir [`System.Web.Caching.Cache.NoSlidingExpiration`](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx) , bir on Kayan süre sonu olmadığını gösterir. Bu `Insert` yöntemi aşırı yüklemesi hem mutlak hem de kayan süre sonu için giriş parametrelerine sahip olsa da, bunlardan yalnızca birini sağlayabilirsiniz. Hem mutlak bir zaman hem de bir zaman aralığı belirtmeye çalışırsanız `Insert` yöntemi bir `ArgumentException` özel durumu oluşturur.

> [!NOTE]
> `AddCacheItem(key, value)` yönteminin bu uygulamasında şu anda bazı eksikler bulunur. 4\. adımda bu sorunları ele alacağız ve aşacağız.

## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>4\. Adım: veriler mimari aracılığıyla değiştirildiğinde önbelleğin geçersiz kılınması

Veri alma yöntemlerinin yanı sıra, önbelleğe alma katmanının verileri eklemek, güncelleştirmek ve silmek için BLL ile aynı yöntemleri sağlaması gerekir. CL verileri değiştirme yöntemleri önbelleğe alınmış verileri değiştirmez, bunun yerine BLL s ile ilgili veri değiştirme yöntemini çağırır ve sonra önbelleği geçersiz kılar. Önceki öğreticide gördüğünüz gibi bu, ObjectDataSource 'un, önbelleğe alma özellikleri etkinleştirildiğinde ve `Insert`, `Update`veya `Delete` yöntemleri çağrıldığında uyguladığı davranıştır.

Aşağıdaki `UpdateProduct` aşırı yüklemesi, veri değiştirme yöntemlerinin CL 'de nasıl uygulanacağını gösterir:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample8.cs)]

Uygun veri değişikliği Iş mantığı katmanı yöntemi çağrılır, ancak yanıtı döndürülmeden önce önbelleğin geçersiz kılması gerekir. Ne yazık ki, `ProductsCL` sınıf s `GetProducts()` ve `GetProductsByCategoryID(categoryID)` yöntemlerinin her biri farklı anahtarlarla önbelleğe öğe eklediğinden ve `GetProductsByCategoryID(categoryID)` yöntemi her benzersiz *CategoryID*için farklı bir önbellek öğesi eklediğinden, önbelleğin geçersiz kılınması basittir.

Önbelleği geçersiz kıldığınızda, `ProductsCL` sınıfı tarafından eklenmiş olabilecek *Tüm* öğeleri kaldırdık. Bu, `AddCacheItem(key, value)` yönteminde önbelleğe eklenen her öğe ile bir *önbellek bağımlılığı* ilişkilendirerek gerçekleştirilebilir. Genel olarak, bir önbellek bağımlılığı önbellekteki başka bir öğe, dosya sistemindeki bir dosya veya Microsoft SQL Server veritabanından alınan veriler olabilir. Bağımlılık değiştiğinde veya önbellekten kaldırıldığında, ilişkili olduğu önbellek öğeleri otomatik olarak önbellekten çıkarılır. Bu öğreticide, `ProductsCL` sınıfı aracılığıyla eklenen tüm öğeler için önbellek bağımlılığı görevi gören önbellekte ek bir öğe oluşturmak istiyoruz. Bu şekilde, yalnızca önbellek bağımlılığını kaldırarak bu öğelerin tümü önbellekten kaldırılabilir.

Bu yöntem aracılığıyla önbelleğe eklenen her öğenin tek bir önbellek bağımlılığı ile ilişkilendirilmesi için `AddCacheItem(key, value)` metodunu güncelleştirmesine izin verin:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample9.cs)]

`MasterCacheKeyArray`, ProductsCache tek bir değer tutan bir dize dizisidir. İlk olarak, önbelleğe bir önbellek öğesi eklenir ve geçerli tarih ve saate atanır. Önbellek öğesi zaten varsa, güncelleştirilir. Ardından, bir önbellek bağımlılığı oluşturulur. [`CacheDependency` sınıfı](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx) oluşturucusunun çok sayıda aşırı yüklemesi vardır, ancak burada kullanılmakta olan bir iki `string` dizi girişi bekler. İlki, bağımlılıklar olarak kullanılacak dosya kümesini belirtir. Dosya tabanlı herhangi bir bağımlılığı kullanmak istemediğimiz için, ilk giriş parametresi için `null` değeri kullanılır. İkinci giriş parametresi, bağımlılıklar olarak kullanılacak önbellek anahtarları kümesini belirtir. Burada tek bağlılığımız `MasterCacheKeyArray`belirttik. `CacheDependency` sonra `Insert` yöntemine geçirilir.

`AddCacheItem(key, value)`için bu değişiklik ile önbelleğin kaldırılması, bağımlılığı kaldırmak kadar basittir.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample10.cs)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>5\. Adım: önbelleğe alma katmanını sunum katmanından çağırma

Önbelleğe alma katmanı sınıfları ve yöntemleri, bu öğreticiler genelinde inceduğumuz teknikleri kullanarak verilerle çalışmak için kullanılabilir. Önbelleğe alınmış verilerle çalışmayı göstermek için, `ProductsCL` sınıfına yaptığınız değişiklikleri kaydedin ve sonra `Caching` klasörde `FromTheArchitecture.aspx` sayfasını açın ve bir GridView ekleyin. GridView s akıllı etiketinden yeni bir ObjectDataSource oluşturun. Sihirbazın ilk adımında, `ProductsCL` sınıfını açılır listedeki seçeneklerden biri olarak görmeniz gerekir.

[ProductsCL sınıfı ![, Iş nesnesi açılır listesine dahil edilmiştir](caching-data-in-the-architecture-cs/_static/image5.png)](caching-data-in-the-architecture-cs/_static/image4.png)

**Şekil 4**: `ProductsCL` sınıfı, Iş nesnesi açılır listesine dahildir ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-in-the-architecture-cs/_static/image6.png))

`ProductsCL`seçtikten sonra Ileri ' ye tıklayın. SEÇIM sekmesindeki açılan listede iki öğe vardır-`GetProducts()` ve `GetProductsByCategoryID(categoryID)` ve GÜNCELLEŞTIRME sekmesi tek `UpdateProduct` aşırı yüküne sahiptir. Seç sekmesinden `GetProducts()` yöntemini ve GÜNCELLEŞTIRME sekmesinden `UpdateProducts` yöntemini seçin ve son ' a tıklayın.

[ProductsCL sınıfı yöntemleri ![açılır listelerde listelenmiştir](caching-data-in-the-architecture-cs/_static/image8.png)](caching-data-in-the-architecture-cs/_static/image7.png)

**Şekil 5**: `ProductsCL` sınıfı yöntemleri aşağı açılan listelerde listelenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](caching-data-in-the-architecture-cs/_static/image9.png))

Sihirbazı tamamladıktan sonra, Visual Studio, ObjectDataSource `OldValuesParameterFormatString` özelliğini `original_{0}` olarak ayarlar ve GridView 'a uygun alanları ekler. `OldValuesParameterFormatString` özelliğini varsayılan değerine geri değiştirin, `{0}`ve GridView 'u sayfalama, sıralamayı ve düzenlemesini destekleyecek şekilde yapılandırın. CL tarafından kullanılan `UploadProducts` aşırı yüklemesi yalnızca düzenlenen ürün adı ve fiyatını kabul ettiğinden, GridView 'u yalnızca bu alanların düzenlenebilir olması için sınırlayın.

Önceki öğreticide, `ProductName`, `CategoryName`ve `UnitPrice` alanları için alanları eklemek üzere bir GridView tanımladık. Bu biçimlendirmeyi ve yapıyı çoğaltıp, bu durumda GridView ve ObjectDataSource 'un bildirim temelli biçimlendirmesinin aşağıdakine benzer şekilde görünmesi gerekir:

[!code-aspx[Main](caching-data-in-the-architecture-cs/samples/sample11.aspx)]

Bu noktada, önbelleğe alma katmanını kullanan bir sayfa sunuyoruz. Önbelleği eylemde görmek için `ProductsCL` sınıf s `GetProducts()` ve `UpdateProduct` yöntemlerinde kesme noktaları ayarlayın. Bir tarayıcıdaki sayfayı ziyaret edin ve önbellekten çekilen verileri görmek için sıralama ve sayfalama sırasında kodu adım adım ilerleyin. Sonra bir kaydı güncelleştirin ve önbelleğin geçersiz kılındığına ve sonuç olarak veri GridView 'a yeniden bağlandığında BLL 'den alındığını unutmayın.

> [!NOTE]
> Bu makaleye eşlik eden indirme işleminde belirtilen önbelleğe alma katmanı tamamlanmamış. Yalnızca tek bir sınıf içerir, tek bir yöntem `ProductsCL`. Üstelik, yalnızca tek bir ASP.NET sayfası CL 'yi (`~/Caching/FromTheArchitecture.aspx`) kullanır. diğer tüm diğerleri de BLL 'ye doğrudan başvurmuş. Uygulamanızda bir CL kullanmayı planlıyorsanız, sunum katmanından tüm çağrılar CL 'ye gitmelidir, bu da bu sınıfların ve yöntemlerin, sunu katmanı tarafından şu anda kullanılan BLL 'de kapsanmakta olması gerekir.

## <a name="summary"></a>Özet

Önbelleğe alma, ASP.NET 2,0 s SqlDataSource ve ObjectDataSource denetimleriyle sunum katmanında uygulanacaksa, ideal önbelleğe alma sorumluluklarına mimaride ayrı bir katman atanabilir. Bu öğreticide, sunum katmanı ve Iş mantığı katmanı arasında yer alan bir önbelleğe alma katmanı oluşturduk. Önbelleğe alma katmanının BLL 'de var olan sınıf ve yöntemlerin aynı kümesini sağlaması gerekir ve sunum katmanından çağrılır.

Bu ve önceki öğreticilerde araştırdığımız önbelleğe alma katmanı örnekleri, *reaktif yükleme*. Reaktif yükleme ile veriler yalnızca veri isteği yapıldığında ve önbellekte veriler olmadığında önbelleğe yüklenir. Veriler, gerçekten gerekli olmadan önce önbelleğe verileri belleğe yükleyen bir tekniktir ve *önbelleğe yüklenebilir.* Bir sonraki öğreticide, uygulama başlangıcında statik değerlerin önbelleğe nasıl depolanacağını göz atadığımızda bir proaktif yükleme örneği görüyoruz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için müşteri adayı gözden geçireni bir Murph idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](caching-data-with-the-objectdatasource-cs.md)
> [İleri](caching-data-at-application-startup-cs.md)
