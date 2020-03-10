---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: Verimli veri sayfalamayı uygulama | Microsoft Docs
author: microsoft
description: 8\. adım, her seferinde 1000 ' in bir kez görüntülenmesini sağlamak yerine,/Dınyalar URL 'imize sayfalama desteğinin nasıl ekleneceğini gösterir.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601054"
---
# <a name="implement-efficient-data-paging"></a>Verimli Veri Sayfalama Uygulama

[Microsoft](https://github.com/microsoft) tarafından

[PDF 'YI indir](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Bu, ASP.NET MVC 1 kullanarak küçük, ancak tam bir Web uygulamasının nasıl oluşturulacağını gösteren ücretsiz bir ["Nerdakşam yemeği" uygulama öğreticisinin](introducing-the-nerddinner-tutorial.md) adım 8 ' idir.
> 
> Adım 8 ' de, her seferinde 1000 ' in çıkarılabilmesini sağlamak yerine, bir kerede yalnızca 10 ' dan fazla dinlemei görüntülemek ve son kullanıcıların bir SEO kolay bir şekilde, tüm listenin geri ve ileri doğru bir şekilde görüntülenmesini sağlamak için/Dınyalar URL 'imize disk belleği desteğinin nasıl ekleneceği gösterilmektedir.
> 
> ASP.NET MVC 3 kullanıyorsanız, [MVC 3 Ile çalışmaya başlama](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) veya [MVC müzik mağazası](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) öğreticilerini izlemeniz önerilir.

## <a name="nerddinner-step-8-paging-support"></a>Nerdakşam yemeği adım 8: sayfalama desteği

Sitemiz başarılı olursa, binlerce yaklaşan yemek olacaktır. Kullanıcı arabirimimizin tüm bu duyanlar için ölçeklendirirken emin olmak ve kullanıcıların onlara gözatmalarına izin vermek istiyoruz. Bunu etkinleştirmek için, */dınyalar* URL 'imize disk belleği desteği ekleyeceğiz. bu sayede, bir kerede yalnızca 10 adet yaklaşan dinlemeler görüntülenir ve son KULLANıCıLARıN bir SEO kolay bir şekilde tüm liste üzerinde geri ve ileri doğru bir şekilde gezinmesini sağlar.

### <a name="index-action-method-recap"></a>Index () eylem yöntemi yeniden üst sınırı

DinnersController sınıfımızda bulunan Index () eylem yöntemi şu anda aşağıdaki gibi görünüyor:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

*/Dınanlar* URL 'sine bir istek yapıldığında, tüm yaklaşan geri alanlar listesini alır ve bunların tümünün bir listesini oluşturur:

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>IQueryable&lt;T&gt; anlama

*IQueryable&lt;t&gt;* , .NET 3,5 'nin bir PARÇASı olarak LINQ ile tanıtılan bir arabirimdir. Disk belleği desteğini uygulamak için avantajlarından yararlanabildiğimiz güçlü "ertelenmiş yürütme" senaryolarına olanak sağlar.

DinnerRepository ' de, Findupcomingdıntik () yönteminden bir IQueryable&lt;akşam&gt; sırası döndürüyoruz:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

Findupcomingdınlayıcılar () yöntemi tarafından döndürülen IQueryable&lt;akşam&gt; nesnesi, LINQ to SQL kullanarak veritabanımızdan akşam yemeği nesnelerini almak için bir sorgu saklar. Önemli bir deyişle, sorgudaki verilere erişmeye/yineleme yapmaya ya da ToList () yöntemini çağırana kadar, sorguyu veritabanına karşı yürütmez. Findupcomingdinlerimizin () yöntemini çağıran kod, isteğe bağlı olarak, sorguyu yürütmeden önce IQueryable&lt;akşam&gt; nesnesine ek "zincirleme" işlemleri/filtreler eklemeyi tercih edebilir. LINQ to SQL, veriler istendiğinde birleştirilmiş sorguyu veritabanına karşı yürütmek için yeterince akıllı olur.

Disk belleği mantığını uygulamak için, DinnersController 'in dizin () eylem yöntemini, döndürülen IQueryable&lt;akşam&gt; sırasıyla ToList () çağrılmadan önce ek "Skip" ve "Take" işleçlerini uygulayacak şekilde güncelleştirebiliriz:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

Yukarıdaki kod, veritabanında ilk 10 yaklaşan geri dönüşlerin üzerine atlar ve ardından 20 dinsini döndürür. LINQ to SQL, SQL veritabanında bu atlama mantığını gerçekleştiren ve Web sunucusunda değil, iyileştirilmiş bir SQL sorgusu oluşturmaya yetecek kadar akıllı bir değer. Bu, veritabanında milyonlarca dinleyici olsa bile, bu isteğin bir parçası olarak yalnızca istediğimiz 10 ' un alınması (verimli ve ölçeklenebilir hale getirilmesi) anlamına gelir.

### <a name="adding-a-page-value-to-the-url"></a>URL 'ye bir "Page" değeri ekleniyor

Belirli bir sayfa aralığını sabit kodlamak yerine, URL 'lerimizi bir kullanıcının istediği akşam yemeği aralığını belirten bir "Page" parametresi içermesini istiyoruz.

#### <a name="using-a-querystring-value"></a>QueryString değeri kullanma

Aşağıdaki kod, bir QueryString parametresini desteklemek ve */Dıntik? Page = 2*gibi URL 'leri etkinleştirmek için dizin () eylem yönteminizi nasıl güncelleştirebileceğinizi göstermektedir.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

Yukarıdaki Index () eylem yönteminde "Page" adlı bir parametre bulunur. Parametre null yapılabilir bir tamsayı (yani, int) olarak belirtilir. Bu, */Dınsin? Page = 2* URL 'sinin "2" değerinin parametre değeri olarak geçirilmesine neden olacağı anlamına gelir. */Dınanlar* URL 'si (QueryString değeri olmadan) null değer geçirilmesine neden olur.

Sayfa boyutunu sayfa boyutu (Bu durumda 10 satır) ile çarpıyoruz. Null yapılabilir türlerle ilgilenirken faydalı olan ["birleştirme" işleci (??) kullanılıyor. C# ](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) Yukarıdaki kod, sayfa parametresi null ise 0 değerini atar.

#### <a name="using-embedded-url-values"></a>Gömülü URL değerlerini kullanma

Bir QueryString değeri kullanmanın alternatifi, sayfa parametresini gerçek URL 'nin içine eklemek olacaktır. Örneğin: */Dinners/Page/2* veya */Dinners/2*. ASP.NET MVC, bu gibi senaryoları desteklemeyi kolaylaştıran güçlü bir URL yönlendirme altyapısı içerir.

İstediğiniz herhangi bir denetleyici sınıfına veya eylem yöntemine herhangi bir gelen URL veya URL biçimi eşleyen özel yönlendirme kuralları kaydedebiliriz. Tüm yapmanız gereken, Global. asax dosyasını projemiz:

![](implement-efficient-data-paging/_static/image2.png)

Ve ardından yollar için ilk çağrı gibi MapRoute () yardımcı yöntemini kullanarak yeni bir eşleme kuralı kaydedin. MapRoute ():

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

Yukarıdaki "Upcomingdıntik" adlı yeni bir yönlendirme kuralı kaydettiriyoruz. "Dinetleri/sayfa/{Page}" URL biçiminde olduğunu ve {Page} URL içinde gömülü bir parametre değeri olduğunu belirledik. MapRoute () yönteminin üçüncü parametresi, bu biçimle eşleşen URL 'Leri DinnersController sınıfındaki Index () eylem yöntemiyle eşlemenizi gerektiğini gösterir.

QueryString senaryoumuzdan önce sahip olduğumuz aynı dizin () kodunu ("Page" parametresi, QueryString değil URL 'den gelecek şekilde) kullanabiliriz:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

Şimdi de uygulamayı çalıştırdığımızda ve */ınıza* yazdığınızda, ilk 10 yaklaşan dinetleri görüyoruz:

![](implement-efficient-data-paging/_static/image3.png)

*/Dinners/Page/1* ' ye yazarken, dinetleri 'nin sonraki sayfasını görürsünüz:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>Sayfa gezintisi kullanıcı arabirimi ekleme

Sayfalama senaryoumuzu tamamlamaya yönelik son adım, kullanıcıların akşam yemeği verilerini kolayca atlamasına olanak tanımak için görünüm şablonumuzdaki "ileri" ve "önceki" Gezinti Kullanıcı arabirimini uygulamak olacaktır.

Bunu doğru şekilde uygulamak için, veritabanındaki tüm Dinetleri ve ne kadar veri sayfası olduğunu bilmemiz gerekir. Daha sonra, şu anda istenen "sayfa" değerinin verilerin başlangıcında veya sonunda olup olmadığını hesaplamakta ve "önceki" ve "sonraki" Kullanıcı arabirimini uygun şekilde gösterip gizleyebilmemiz gerekir. Dizin () eylemi yöntemi içinde bu mantığı uygulayabiliriz. Alternatif olarak, projenize bu mantığı daha yeniden kullanılabilir bir şekilde kapsülleyen bir yardımcı sınıf ekleyebiliriz.

Aşağıda .NET Framework yerleşik&lt;T&gt; koleksiyon sınıfından türetilen basit bir "Sayfalılı liste" yardımcı sınıfı verilmiştir. IQueryable verilerinin herhangi bir dizisini sayfalamak için kullanılabilecek yeniden kullanılabilir bir koleksiyon sınıfı uygular. Nerdakşam yemeği uygulamamız, IQueryable&lt;akşam yemeği&gt; sonuçları üzerinden çalışacağız, ancak IQueryable&lt;ürün&gt; veya IQueryable&lt;müşteri&gt; diğer uygulama senaryolarında bu sonuçlara karşı kolayca kullanılabilir.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

"PageIndex", "PageSize", "TotalCount" ve "TotalPages" gibi özellikleri nasıl hesaplayacağını ve daha sonra ortaya çıkaran hakkında dikkat edin. Ayrıca, koleksiyondaki veri sayfasının orijinal sıranın başlangıcında veya sonunda olup olmadığını gösteren "HasPreviousPage" ve "HasNextPage" iki yardımcı özelliğini kullanıma sunar. Yukarıdaki kod iki SQL sorgusunun çalışmasına neden olur. Bu, ilk olarak akşam yemeği nesnelerinin sayısını alır (yani, bir tamsayı döndüren "SELECT COUNT" ifadesini yerine getirmek için) ve ikincisi yalnızca şu satırları alır: geçerli veri sayfası için veritabanımız gereken veriler.

Daha sonra DinnersController. Index () yardımcı yönteminizi, DinnerRepository. Findupcomingdıntik () sonucundan akşam yemeği&gt;&lt;.

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

Daha sonra, \Views\Dinners\Index.aspx View şablonunu ViewPage&lt;Nerdakşam yemeği. yardımcılar. disk belleği&lt;Dinner&gt;&gt; ve daha sonra&lt;bir sonraki ve önceki Gezinti Kullanıcı arabirimini göstermek veya gizlemek için görünümümüzün en altına aşağıdaki kodu ekleyerek güncelleştirebilirsiniz:&lt;&gt;&gt;

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

Köprülerimizi oluşturmak için HTML. RouteLink () yardımcı yöntemini nasıl kullandığınızı öğrenin. Bu yöntem, daha önce kullandığımız HTML. ActionLink () yardımcı yöntemine benzer. Bu fark, "Upcomingdintik" yönlendirme kuralını kullanarak, Global. asax dosyanız içinde kurduğumuz URL 'YI oluşturmamız. Bu, Şu biçimdeki dizin () eylem yöntemine URL 'Ler oluşturacağız: */Dinners/Page/{Page}* – burada {Page} değeri, geçerli pageIndex temel alınarak yukarıdaki sağlamamız gereken bir değişkendir.

Şimdi uygulamamızı yeniden çalıştırdığımızda tarayıcımızda her seferinde 10 dinde görüyoruz:

![](implement-efficient-data-paging/_static/image5.png)

Ayrıca, arama motoru erişilebilir URL 'Leri kullanarak verilerimize iletme ve geri doğru atlama olanağı sunan sayfanın alt kısmında &lt;&lt;&lt; ve &gt;&gt;Gezinti Kullanıcı arabirimine sahip olduğumuz:&gt;

![](implement-efficient-data-paging/_static/image6.png)

| **Kenar konusu: IQueryable&lt;T&gt; etkilerini anlama** |
| --- |
| IQueryable&lt;T&gt;, çeşitli ilginç yürütme senaryolarına (sayfalama ve bileşim tabanlı sorgular gibi) olanak tanıyan çok güçlü bir özelliktir. Tüm güçlü özelliklerde olduğu gibi, bunu nasıl kullandığınız ile ilgili dikkatli olmak istersiniz. Deponuzdan bir IQueryable&lt;T&gt; sonucu döndürmesinin, kodun zincirleme operatör yöntemlerine çağrı yapmasına ve bu nedenle nihai sorgu yürütmeye katılmasını sağlayan bir sonuç olduğunu bilmek önemlidir. Bu özellik için çağrı kodu sağlamak istemiyorsanız, daha önce yürütülmüş bir sorgunun sonuçlarını içeren&lt;T&gt; veya IEnumerable&lt;T&gt; sonuçları geri döndürmelisiniz. Sayfalandırma senaryolarında, bu durum gerçek veri sayfalandırma mantığını çağrılan depo yöntemine itmeniz gerekir. Bu senaryoda, bir Sayfaıo listesi döndüren bir imzaya sahip olmak için Findupcomingdıntik () Bulucu yönteminizi güncelleştirebiliriz: Sayfaınan liste&lt; akşam yemeği&gt; Findupcomingdınanlar (int pageIndex, INT pageSize) {} veya bir IList&lt;akşam yemeği&gt;geri döndürür ve bir "totalCount" out parametresi kullanarak toplam dinde: IList&lt;akşam yemeği&gt; Findupcomingdınanlar (int pageIndex, INT pageSize, Out int totalCount) {} |

### <a name="next-step"></a>Sonraki adım

Şimdi uygulamamıza kimlik doğrulaması ve yetkilendirme desteği ekleyebilmemiz için bakalım.

> [!div class="step-by-step"]
> [Önceki](re-use-ui-using-master-pages-and-partials.md)
> [İleri](secure-applications-using-authentication-and-authorization.md)
