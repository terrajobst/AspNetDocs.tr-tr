---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
title: Özel disk belleğine alınan verileriC#sıralama () | Microsoft Docs
author: rick-anderson
description: Önceki öğreticide, verileri bir Web sayfasında sunarken özel sayfalama uygulamayı öğrendiniz. Bu öğreticide, önceki bir genişletmeyi nasıl genişlettireceğiz...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 778baa4e-4af8-4665-947e-7a01d1a4dff2
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e55ed9b92814753e95bdfdf26c2f051df6f2630d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642384"
---
# <a name="sorting-custom-paged-data-c"></a>Özel Sayfalanmış Verileri Sıralama (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_CS.exe) veya [PDF 'yi indirin](sorting-custom-paged-data-cs/_static/datatutorial26cs1.pdf)

> Önceki öğreticide, verileri bir Web sayfasında sunarken özel sayfalama uygulamayı öğrendiniz. Bu öğreticide, önceki örneği özel sayfalama sıralama desteğini dahil etmek için nasıl genişletebileceğinizi görüyoruz.

## <a name="introduction"></a>Giriş

Özel sayfalama, varsayılan sayfalama ile karşılaştırıldığında, çok sayıda boyuta göre verileri kullanarak sayfalama performansını iyileştirebilir, bu da büyük miktarlarda veri aracılığıyla sayfalandığında, özel sayfalama uygulama seçimini bir şekilde gerçekleştirebilir. Özel sayfalama uygulamak, varsayılan sayfalama uygulamaktan daha karmaşıktır, ancak özellikle de karışıma sıralama ekliyoruz. Bu öğreticide, sıralama *ve* özel sayfalama desteği dahil olmak üzere önceki bir örnekten örnek genişleteceğiz.

> [!NOTE]
> Bu öğretici önceki bir üzerinde oluşturulduğundan, önceki öğretici s Web sayfasından (`EfficientPaging.aspx`) `<asp:Content>` öğesi içinde bildirime dayalı sözdizimini kopyalamak ve `SortParameter.aspx` sayfasındaki `<asp:Content>` öğesi arasına yapıştırmak için biraz zaman ayırın. Bir ASP.NET sayfasının işlevselliğini başka bir şekilde çoğaltmaya yönelik daha ayrıntılı bir tartışma için, oluşturma [ve arabirim ekleme öğreticisine doğrulama denetimlerini ekleme](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) adım 1 ' e geri bakın.

## <a name="step-1-reexamining-the-custom-paging-technique"></a>1\. Adım: özel sayfalama tekniğini yeniden Inceleme

Özel sayfalama işleminin düzgün çalışması için, başlangıç satırı dizini ve en fazla satır parametreleri verilen belirli bir kayıt alt kümesini verimli bir şekilde alan bir teknik uygulamamız gerekir. Bu amacı elde etmek için kullanılabilecek birkaç teknik vardır. Önceki öğreticide, Microsoft SQL Server 2005 s yeni `ROW_NUMBER()` derecelendirme işlevini kullanarak bunu gerçekleştirmeye baktık. Kısacası `ROW_NUMBER()` derecelendirme işlevi, belirtilen sıralama düzeni tarafından derecelendirilen bir sorgu tarafından döndürülen her satıra bir satır numarası atar. İlgili kayıtların alt kümesi daha sonra numaralandırılmış sonuçların belirli bir bölümü döndürülerek elde edilir. Aşağıdaki sorgu, `ProductName`alfabetik olarak sıralanan sonuçları derecelendirerek 11 ' den 20 ' ye kadar numaralandırılmış ürünleri döndürmek için bu tekniği nasıl kullanacağınızı gösterir:

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample1.sql)]

Bu teknik, belirli bir sıralama düzeni (Bu örnekte alfabetik olarak sıralanmış`ProductName`) kullanılarak sayfalama için iyi bir sonuç verir, ancak sorgunun farklı bir sıralama ifadesine göre sıralanmış sonuçları gösterecek şekilde değiştirilmesi gerekir. İdeal olarak, yukarıdaki sorgu `OVER` yan tümcesinde bir parametre kullanmak için yeniden yazılabilir, örneğin:

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample2.sql)]

Ne yazık ki parametreli `ORDER BY` yan tümcelerlerine izin verilmez. Bunun yerine, `@sortExpression` giriş parametresini kabul eden bir saklı yordam oluşturuyoruz, ancak aşağıdaki geçici çözümlerden birini kullanır:

- Kullanılabilecek sıralama ifadelerinin her biri için sabit kodlanmış sorgular yazın; ardından, hangi sorgunun çalıştırılacağını öğrenmek için `IF/ELSE` T-SQL deyimlerini kullanın.
- `@sortExpressio` n giriş parametresine göre dinamik `ORDER BY` ifadeleri sağlamak için bir `CASE` deyimi kullanın; daha fazla bilgi için [SQL `CASE` deyimlerinin gücüyle](http://www.4guysfromrolla.com/webtech/102704-1.shtml) sorgu sonuçlarını dinamik olarak sıralamak için kullanılan bölümüne bakın.
- Saklı yordamda uygun sorguyu bir dize olarak oluşturun ve ardından dinamik sorguyu yürütmek için [`sp_executesql` sistem saklı yordamını](https://msdn.microsoft.com/library/ms188001.aspx) kullanın.

Bu geçici çözümlerin her biri bir dezavantaja sahiptir. İlk seçenek, olası her bir sıralama ifadesi için bir sorgu oluşturmanızı gerektirdiğinden diğer iki ikisi için de sürdürülebilir değildir. Bu nedenle, daha sonra GridView 'a yeni, sıralanabilir alanlar eklemeye karar verirseniz, geri dönüp saklı yordamı güncelleştirmeniz gerekir. İkinci yaklaşım, dize olmayan veritabanı sütunlarına göre sıralama yaparken performans sorunlarını ortaya çıkaracak ve ayrıca ilk olarak aynı bakım sorunlarından de sahip olan bazı alt tlelikler vardır. Ve dinamik SQL kullanan üçüncü seçenek, bir saldırgan kendi seçtikleri giriş parametresi değerlerini geçen saklı yordamı yürütebilise, bir SQL ekleme saldırılarına karşı riski ortaya çıkarır.

Bu yaklaşımlardan hiçbiri kusursuz olsa da, üçüncü seçeneği üçünün en iyisi olduğunu düşünüyorum. Dinamik SQL kullanımıyla, diğer iki ikisi de olmadığı bir esneklik düzeyi sağlar. Ayrıca, bir SQL ekleme saldırısına yalnızca, bir saldırgan tercih ettiği giriş parametrelerinde geçen saklı yordamı yürütebilmesi durumunda kullanılabilir. DAL parametreli sorgular kullandığından, ADO.NET veritabanına gönderilen bu parametreleri mimari üzerinden korur, yani SQL ekleme saldırısı güvenlik açığının yalnızca saldırgan, saklı yordamı doğrudan yürütebileceği durumlarda vardır.

Bu işlevi uygulamak için `GetProductsPagedAndSorted`adlı Northwind veritabanında yeni bir saklı yordam oluşturun. Bu saklı yordam üç giriş parametresini kabul etmelidir: `@sortExpression`, sonuçların nasıl sıralanması gerektiğini belirten ve `OVER` yan tümcesindeki `ORDER BY` metinden sonra doğrudan nasıl ekleneceğini belirten, `nvarchar(100`türünde bir giriş parametresi. ve `@startRowIndex` ve `@maximumRows`önceki öğreticide incelenen `GetProductsPaged` saklı yordamından aynı iki tamsayı giriş parametresini. Aşağıdaki betiği kullanarak `GetProductsPagedAndSorted` saklı yordamını oluşturun:

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample3.sql)]

Saklı yordam, `@sortExpression` parametresi için bir değer belirtilmesini sağlayarak başlar. Eksik ise, sonuçlar `ProductID`göre sıralanır. Ardından, dinamik SQL sorgusu oluşturulur. Burada dinamik SQL sorgusunun, Products tablosundan tüm satırları almak için kullanılan önceki sorgulardan biraz farklı olduğunu unutmayın. Önceki örneklerde, bir alt sorgu kullanarak her bir ürüne ilişkin ilişkili kategori ve sağlayıcı adlarını elde ediyoruz. Bu karar, [veri erişim katmanı oluşturma](../introduction/creating-a-data-access-layer-cs.md) öğreticisinde geri yapılmıştır ve TableAdapter bu tür sorgular için ilişkili Insert, Update ve DELETE yöntemlerini otomatik olarak oluşturamadığı için `JOIN` s kullanımı yerine oluşturulmuştur. Ancak, `GetProductsPagedAndSorted` saklı yordamı, sonuçlar kategorisi veya tedarikçi adlarına göre sıralanmak için `JOIN` s kullanmalıdır.

Bu dinamik sorgu statik sorgu bölümleri ve `@sortExpression`, `@startRowIndex`ve `@maximumRows` parametreleri birleştirerek oluşturulur. `@startRowIndex` ve `@maximumRows` tamsayı parametreleri olduğundan, doğru bir şekilde birleştirmek için bunların nvarchars içine dönüştürülmesi gerekir. Bu dinamik SQL sorgusu oluşturulduktan sonra, `sp_executesql`aracılığıyla yürütülür.

Bu saklı yordamı `@sortExpression`, `@startRowIndex`ve `@maximumRows` parametrelerine ait farklı değerlerle test etmek için bir dakikanızı ayırın. Sunucu Gezgini, saklı yordam adına sağ tıklayın ve Yürüt ' ü seçin. Bu işlem, giriş parametrelerini girebileceğiniz saklı yordamı Çalıştır iletişim kutusunu getirir (bkz. Şekil 1). Sonuçları kategori adına göre sıralamak için, `@sortExpression` parametresi değeri için CategoryName kullanın; tedarikçinin şirket adına göre sıralamak için CompanyName ' i kullanın. Parametre değerlerini sağladıktan sonra, Tamam ' a tıklayın. Sonuçlar çıkış penceresinde görüntülenir. Şekil 2 ' de, azalan düzende `UnitPrice` göre derecelendirilen 11 ' den 20 ' ye kadar dönen sonuçları gösterir.

![Saklı yordamın üç giriş parametresi için farklı değerler deneyin](sorting-custom-paged-data-cs/_static/image1.png)

**Şekil 1**: saklı yordamın üç giriş parametresi Için farklı değerler deneyin

[![saklı yordam sonuçları Çıkış Penceresi gösterilir](sorting-custom-paged-data-cs/_static/image3.png)](sorting-custom-paged-data-cs/_static/image2.png)

**Şekil 2**: saklı yordam sonuçları çıkış penceresi gösterilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-custom-paged-data-cs/_static/image4.png))

> [!NOTE]
> `OVER` yan tümcesindeki belirtilen `ORDER BY` sütununa göre sonuçları derecelendirerek SQL Server sonuçları sıralaması gerekir. Bu işlem, sonuçların tarafından sıralanan sütunlar üzerinde kümelenmiş bir dizin varsa veya kapsayan bir dizin varsa, ancak başka maliyetli olabilir. Yeterince büyük sorguların performansını artırmak için, sonuçların sıralandığı sütun için kümelenmemiş bir dizin eklemeyi göz önünde bulundurun. Daha fazla ayrıntı için [SQL Server 2005 ' de derecelendirme işlevleri ve performans](http://www.sql-server-performance.com/ak_ranking_functions.asp) bölümüne bakın.

## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>2\. Adım: veri erişimini ve Iş mantığı katmanlarını genişleterek

`GetProductsPagedAndSorted` saklı yordam oluşturulduktan sonra, bir sonraki adımınız uygulama mimarimiz tarafından bu saklı yordamı yürütmek için bir yol sağlamaktır. Bu, hem DAL hem de BLL 'ye uygun bir yöntem eklenmesini gerektirir. DAL için bir yöntem ekleyerek başlayalım. `Northwind.xsd` türü belirtilmiş veri kümesini açın, `ProductsTableAdapter`sağ tıklayın ve bağlam menüsünden sorgu Ekle seçeneğini belirleyin. Önceki öğreticide yaptığımız gibi, bu yeni DAL yöntemini mevcut bir saklı yordamı kullanacak şekilde yapılandırmak istiyoruz-`GetProductsPagedAndSorted`, bu durumda. Yeni TableAdapter yönteminin varolan bir saklı yordamı kullanmasını istediğinizi belirterek başlayın.

![Mevcut bir saklı yordam kullanmayı seçin](sorting-custom-paged-data-cs/_static/image5.png)

**Şekil 3**: varolan bir saklı yordam kullanmayı seçin

Kullanılacak saklı yordamı belirtmek için, sonraki ekranda bulunan aşağı açılan listeden `GetProductsPagedAndSorted` saklı yordamını seçin.

![Getproductspagedandsıralanmış saklı yordamını kullanın](sorting-custom-paged-data-cs/_static/image6.png)

**Şekil 4**: Getproductspagedandsıralanmış saklı yordamını kullanın

Bu saklı yordam, sonuçları olarak bir dizi kayıt döndürür. bu nedenle, sonraki ekranda tablo verileri döndüren anlamına gelir.

![Saklı yordamın tablo verilerini döndürdüğünü belirtir](sorting-custom-paged-data-cs/_static/image7.png)

**Şekil 5**: saklı yordamın tablo verilerini döndürdüğünü belirtin

Son olarak, hem bir DataTable doldur hem de bir DataTable desenleri döndüren DAL yöntemleri oluşturun ve sırasıyla `FillPagedAndSorted` ve `GetProductsPagedAndSorted`yöntemlerini adlandırarak bir DataTable deseni döndürün.

![Yöntemlerin adlarını seçin](sorting-custom-paged-data-cs/_static/image8.png)

**Şekil 6**: yöntem adlarını seçin

Artık DAL genişlettiğimiz için BLL 'ye yeniden başlamaya hazırız. `ProductsBLL` sınıf dosyasını açın ve `GetProductsPagedAndSorted`yeni bir yöntem ekleyin. Bu yöntemin `sortExpression`, `startRowIndex`ve `maximumRows` üç giriş parametresini kabul etmesi gerekir ve bunun gibi DAL s `GetProductsPagedAndSorted` yöntemine çağrı yapmanız gerekir:

[!code-csharp[Main](sorting-custom-paged-data-cs/samples/sample4.cs)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>3\. Adım: SortExpression parametresinde geçirilecek ObjectDataSource yapılandırma

`GetProductsPagedAndSorted` saklı yordamı kullanan Yöntemler dahil olmak üzere DAL ve BLL 'yi genişletmeden, her şey yeni BLL metodunu kullanmak ve kullanıcının sonuçları sıralamayı istediği sütuna göre `SortExpression` parametresini geçirmek için `SortParameter.aspx` sayfasındaki ObjectDataSource 'u yapılandırmaktır.

`GetProductsPaged` `SelectMethod` ObjectDataSource 'ı `GetProductsPagedAndSorted`olarak değiştirerek başlayın. Bu işlem, veri kaynağı Yapılandırma Sihirbazı ile Özellikler penceresi veya doğrudan bildirime dayalı sözdizimi aracılığıyla yapılabilir. Sonra, ObjectDataSource s [`SortParameterName` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)için bir değer sağlamamız gerekir. Bu özellik ayarlandıysa, ObjectDataSource, GridView s `SortExpression` özelliğini `SelectMethod`geçirmeye çalışır. Özellikle, ObjectDataSource, adı `SortParameterName` özelliğinin değerine eşit olan bir giriş parametresi arar. BLL s `GetProductsPagedAndSorted` yöntemi `sortExpression`adlı sıralama ifadesi giriş parametresine sahip olduğundan, ObjectDataSource s `SortExpression` özelliğini sortExpression olarak ayarlayın.

Bu iki değişikliği yaptıktan sonra, ObjectDataSource 'un bildirime dayalı sözdizimi aşağıdakine benzer şekilde görünmelidir:

[!code-aspx[Main](sorting-custom-paged-data-cs/samples/sample5.aspx)]

> [!NOTE]
> Önceki öğreticide olduğu gibi, ObjectDataSource 'un SelectParameters koleksiyonunda sortExpression, StartRowIndex veya maximumRows giriş *parametrelerini içermediğinden emin* olun.

GridView 'da sıralamayı etkinleştirmek için GridView s akıllı etiketinde sıralama etkinleştir onay kutusunu işaretleyin. Bu, GridView s `AllowSorting` özelliğini `true` olarak ayarlayan ve her sütun için üst bilgi metninin bir LinkButton olarak işlenmesine neden olur. Son Kullanıcı üst bilgi bağlantı düğmelerinden birine tıkladığında, geri gönderme ve aşağıdaki adımları transpire:

1. GridView, [`SortExpression` özelliğini](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) üst bilgi bağlantısına tıklanan alanın `SortExpression` değerine güncelleştirir
2. ObjectDataSource, BLL s `GetProductsPagedAndSorted` yöntemini çağırır. Bu, GridView s `SortExpression` özelliğini yöntem s `sortExpression` giriş parametresinin değeri olarak geçirerek (uygun `startRowIndex` ve `maximumRows` giriş parametresi değerleriyle birlikte)
3. BLL, DAL s `GetProductsPagedAndSorted` yöntemini çağırır
4. DAL, `@sortExpression` parametresini geçirerek (`@startRowIndex` ve `@maximumRows` giriş parametresi değerleriyle birlikte) `GetProductsPagedAndSorted` saklı yordamını yürütür
5. Saklı yordam, veri alt kümesini BLL 'ye döndürür; bu, ObjectDataSource 'a döndürür; Bu veriler daha sonra GridView 'a bağlanır, HTML olarak işlenir ve son kullanıcıya gönderilir

Şekil 7 ' de `UnitPrice` göre artan sırada sıralanan ilk sonuç sayfasını gösterir.

[![sonuçlar BirimFiyat 'a göre sıralanır](sorting-custom-paged-data-cs/_static/image10.png)](sorting-custom-paged-data-cs/_static/image9.png)

**Şekil 7**: sonuçlar BirimFiyat öğesine göre sıralanır ([tam boyutlu görüntüyü görüntülemek için tıklayın](sorting-custom-paged-data-cs/_static/image11.png))

Geçerli uygulama, sonuçları ürün adına, kategori adına, birim başına miktar 'a ve birim fiyata göre doğru bir şekilde sıralayabilse de, sonuçları Tedarikçi adına göre sıralamaya çalışırken çalışma zamanı özel durumu oluşur (bkz. Şekil 8).

![Sonuçları tedarikçiye göre sıralamaya çalışırken aşağıdaki çalışma zamanı özel durumu oluşur](sorting-custom-paged-data-cs/_static/image12.png)

**Şekil 8**: sonuçları tedarikçiye göre sıralamaya çalışırken aşağıdaki çalışma zamanı özel durumu oluşur

Bu özel durum, `SortExpression` GridView `SupplierName` BoundField `SupplierName`olarak ayarlandığı için oluşur. Ancak, `Suppliers` tablodaki tedarikçinin adı, bu sütun adının `SupplierName`olarak diğer adı verilir `CompanyName`. Ancak, `ROW_NUMBER()` işlevi tarafından kullanılan `OVER` yan tümcesi diğer adı kullanamaz ve gerçek sütun adını kullanmalıdır. Bu nedenle, `SortExpression` `SupplierName` BoundField ' dan CompanyName olarak değiştirin (bkz. Şekil 9). Şekil 10 ' da gösterildiği gibi, bu değişiklikten sonra sonuçlar tedarikçiye göre sıralanabilir.

![SupplierName BoundField, SortExpression 'ı CompanyName olarak değiştirme](sorting-custom-paged-data-cs/_static/image13.png)

**Şekil 9**: SupplierName BoundField, SortExpression 'ı CompanyName olarak değiştirme

[![sonuçlar artık tedarikçiye göre sıralanabilecek](sorting-custom-paged-data-cs/_static/image15.png)](sorting-custom-paged-data-cs/_static/image14.png)

**Şekil 10**: sonuçlar artık tedarikçiye göre sıralanabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](sorting-custom-paged-data-cs/_static/image16.png))

## <a name="summary"></a>Özet

Önceki öğreticide incelenen özel sayfalama uygulamasına, sonuçların sıralama sırasında, tasarım zamanında belirtilmesi gerekir. Kısacası bu, uyguladığımız özel sayfalama uygulamasının aynı anda, sıralama özellikleri sunduğumuz anlamına gelir. Bu öğreticide, sonuçların sıralanabileceği bir `@sortExpression` giriş parametresi dahil olmak üzere, saklı yordamı birinciden genişleterek bu sınırlamanın üstesinden geldik.

Bu saklı yordamı oluşturduktan ve DAL ve BLL 'de yeni yöntemler oluşturduktan sonra, ObjectDataSource 'un geçerli `SortExpression` özelliğini BLL `SelectMethod`geçirilecek şekilde yapılandırarak hem sıralama hem de özel disk belleği sunan bir GridView uygulayacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren, Carlos Santos idi. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](efficiently-paging-through-large-amounts-of-data-cs.md)
> [İleri](creating-a-customized-sorting-user-interface-cs.md)
