---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
title: Iş mantığı katmanı oluşturma (C#) | Microsoft Docs
author: rick-anderson
description: Bu öğreticide, iş kurallarınızı t... ile veri değişimi için bir aracı görevi gören bir Iş mantığı katmanına (BLL) merkezileştirmeyi inceleyeceğiz.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 85554606-47cb-4e4f-9848-eed9da579056
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: df96f3e7422a0537bf1b003a33fe8d71a671ac33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78605625"
---
# <a name="creating-a-business-logic-layer-c"></a>İş Mantığı Katmanı Oluşturma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_2_CS.exe) veya [PDF 'yi indirin](creating-a-business-logic-layer-cs/_static/datatutorial02cs1.pdf)

> Bu öğreticide, iş kurallarınızı, sunum katmanı ve DAL arasındaki veri değişimi için bir aracı olarak işlev gören bir Iş mantığı katmanına (BLL) nasıl merkezileştireceğiz.

## <a name="introduction"></a>Giriş

[İlk öğreticide](creating-a-data-access-layer-cs.md) oluşturulan veri erişim KATMANı (dal), veri erişim mantığını sunum mantığındaki düzgün şekilde ayırır. Ancak DAL, veri erişim ayrıntılarını sunu katmanından düzgün bir şekilde ayırırken, uygulanabilecek iş kurallarını zorlamaz. Örneğin, uygulamamız için, `Discontinued` alanı 1 olarak ayarlandığında `Products` tablosunun `CategoryID` veya `SupplierID` alanlarının değiştirilmesine izin vermemek isteyebilir veya kıdem kurallarını zorlamak isteyebilir ve bir çalışanın, bundan sonra işe alınan bir kişi tarafından yönetilmekte olduğu durumları yasaklayabilir. Diğer bir yaygın senaryo yetkilendirme yalnızca belirli bir roldeki kullanıcılar ürünleri silebilir veya `UnitPrice` değerini değiştirebilir.

Bu öğreticide, bu iş kurallarını sunum katmanı ve DAL arasında veri değişimi için bir aracı görevi gören bir Iş mantığı katmanına (BLL) merkezileştirmeyi inceleyeceğiz. Gerçek dünyada bir uygulamada BLL 'nin ayrı bir sınıf kitaplığı projesi olarak uygulanması gerekir; Ancak, bu öğreticiler için, proje yapısını basitleştirmek üzere `App_Code` klasörümüzü bir dizi sınıf olarak uygulayacağız. Şekil 1 ' de sunum katmanı, BLL ve DAL arasındaki mimari ilişkiler gösterilmektedir.

![BLL, sunu katmanını veri erişim katmanından ayırır ve Iş kurallarını uygular](creating-a-business-logic-layer-cs/_static/image1.png)

**Şekil 1**: BLL, sunu katmanını veri erişim katmanından ayırır ve Iş kurallarını uygular

## <a name="step-1-creating-the-bll-classes"></a>Adım 1: BLL sınıfları oluşturma

BLL 'larımız, DAL içindeki her TableAdapter için bir tane olmak üzere dört sınıftan oluşacaktır; Bu BLL sınıflarının her biri, uygun iş kurallarını uygulayarak DAL içinde ilgili TableAdapter 'tan alma, ekleme, güncelleştirme ve silme yöntemlerine sahip olacaktır.

DAL ve BLL ile ilgili sınıfları daha düzgün bir şekilde ayırmak için `App_Code` klasöründe iki alt klasör oluşturalım `DAL` ve `BLL`. Çözüm Gezgini `App_Code` klasöre sağ tıklayıp yeni klasör ' ü seçin. Bu iki klasörü oluşturduktan sonra, ilk öğreticide oluşturulan türü belirtilmiş veri kümesini `DAL` alt klasörüne taşıyın.

Sonra, `BLL` alt klasöründe dört BLL sınıf dosyasını oluşturun. Bunu gerçekleştirmek için `BLL` alt klasörüne sağ tıklayın, yeni öğe Ekle ' yi seçin ve sınıf şablonunu seçin. `ProductsBLL`, `CategoriesBLL`, `SuppliersBLL`ve `EmployeesBLL`olmak üzere dört sınıfı adlandırın.

![App_Code klasöre dört yeni sınıf ekleyin](creating-a-business-logic-layer-cs/_static/image2.png)

**Şekil 2**: `App_Code` klasöre dört yeni sınıf ekleyin

Sonra, yalnızca ilk öğreticiden TableAdapters için tanımlanan yöntemleri kaydırmak üzere sınıfların her birine Yöntemler ekleyelim. Şimdilik, bu yöntemler doğrudan DAL içine çağrı görür; daha sonra gerekli iş mantığını eklemek için daha sonra döneceğiz.

> [!NOTE]
> Visual Studio Standard Edition veya üstünü kullanıyorsanız (yani, Visual Web *Developer kullanmıyorsanız)* , isteğe bağlı olarak [Sınıf Tasarımcısı](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp)kullanarak sınıflarınızı görsel şekilde tasarlayabilirsiniz. Visual Studio 'daki bu yeni özellik hakkında daha fazla bilgi için [Sınıf Tasarımcısı bloguna](https://blogs.msdn.com/classdesigner/default.aspx) bakın.

`ProductsBLL` sınıfı için toplam yedi yöntem eklemesi gerekir:

- `GetProducts()` tüm ürünleri döndürür
- `GetProductByProductID(productID)` belirtilen ürün KIMLIĞI ile ürünü döndürür
- `GetProductsByCategoryID(categoryID)` belirtilen Kategorideki tüm ürünleri döndürür
- `GetProductsBySupplier(supplierID)` belirtilen tedarikçiden tüm ürünleri döndürür
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` geçirilen değerleri kullanarak veritabanına yeni bir ürün ekler; Yeni girilen kaydın `ProductID` değerini döndürür
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)`, geçirilen değerleri kullanarak veritabanında var olan bir ürünü güncelleştirir; tam olarak bir satır güncelleştirilirse `true` döndürür, aksi takdirde `false`
- `DeleteProduct(productID)`, belirtilen ürünü veritabanından siler

ProductsBLL.cs

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample1.cs)]

Yalnızca veri `GetProducts`, `GetProductByProductID`, `GetProductsByCategoryID`ve `GetProductBySuppliersID` döndüren yöntemler yalnızca DAL içine çağırdıkları için oldukça basittir. Bazı senaryolarda, bu düzeyde uygulanması gereken iş kuralları olabilir (oturum açmış olan kullanıcıya veya kullanıcının ait olduğu role göre yetkilendirme kuralları gibi), bu yöntemleri olduğu gibi bırakmalısınız. Bu yöntemler için BLL, yalnızca sunum katmanının veri erişim katmanından temel alınan verilere eriştiği bir ara sunucu olarak işlev görür.

`AddProduct` ve `UpdateProduct` yöntemlerinin her ikisi de çeşitli ürün alanlarının değerlerini parametre olarak alır ve yeni bir ürün ekler ya da mevcut bir ürünü güncelleştirir. `Product` tablonun sütunlarının birçoğu `NULL` değerlerini kabul edebileceğinizden (`CategoryID`, `SupplierID`ve `UnitPrice`), bu tür sütunlara eşlenen `AddProduct` ve `UpdateProduct` için bu giriş parametreleri [null yapılabilir türler](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx)kullanır. Null yapılabilir türler .NET 2,0 ' de yenidir ve bir değer türünün `null`olması gerektiğini belirten bir teknik sağlar. ' C# De, türden sonra `?` (`int? x;`gibi) ekleyerek bir değer türü null yapılabilir bir tür olarak bayrak atayabilirsiniz. Daha fazla bilgi için [ C# programlama kılavuzundaki](https://msdn.microsoft.com/library/67ef8sbd%28VS.80%29.aspx) [null yapılabilir türler](https://msdn.microsoft.com/library/1t3y8s4s.aspx) bölümüne bakın.

Her üç yöntem de, işlem etkilenen bir satırla sonuçlanabileceğinden, bir satırın eklenip eklenmeyeceğini, güncelleştirildiğini veya silindiğini belirten bir Boole değeri döndürür. Örneğin, sayfa geliştiricisi mevcut olmayan bir ürün için `ProductID` geçirmek `DeleteProduct` çağırırsa, veritabanına verilen `DELETE` ifadesinin etkisi olmaz ve bu nedenle `DeleteProduct` yöntemi `false`döndürür.

Yeni bir ürün eklerken veya mevcut bir ürünü güncelleştirirken yeni veya değiştirilmiş ürünün alan değerlerinde bir `ProductsRow` örneği kabul etmenin aksine, yeni veya değiştirilmiş ürünün alan değerlerinde yaptığımız bir değer. `ProductsRow` sınıfı, varsayılan parametresiz oluşturucusu olmayan ADO.NET `DataRow` sınıfından türetildiğinden bu yaklaşım seçildi. Yeni bir `ProductsRow` örneği oluşturmak için, önce bir `ProductsDataTable` örneği oluşturmalı ve ardından `NewProductRow()` metodunu (`AddProduct`' de yaptığımız) çağırmalıdır. Bu Short, ObjectDataSource 'ı kullanarak ürün ekleme ve güncelleştirme yaparken baş başlarından daha fazla yer açın. Kısacası, ObjectDataSource giriş parametrelerinin bir örneğini oluşturmaya çalışacaktır. BLL yöntemi bir `ProductsRow` örneği bekliyorsa, ObjectDataSource bir tane oluşturmayı dener, ancak varsayılan parametresiz oluşturucunun olmaması nedeniyle başarısız olur. Bu sorun hakkında daha fazla bilgi için şu iki ASP.NET Forum gönderilerine bakın: [türü kesin belirlenmiş veri kümeleriyle ObjectDataSources](https://forums.asp.net/1098630/ShowPost.aspx)ve [ObjectDataSource ve kesin olarak belirlenmiş veri kümesiyle sorun](https://forums.asp.net/1048212/ShowPost.aspx).

Ardından, hem `AddProduct` hem de `UpdateProduct`, kod bir `ProductsRow` örneği oluşturur ve bunu yeni geçirilen değerlerle doldurur. Bir DataRow 'ın DataColumns sütunlarına değer atarken çeşitli alan düzeyi doğrulama denetimleri meydana gelebilir. Bu nedenle, geçirilen değerlerin el ile bir DataRow 'a yerleştirilmesi BLL yöntemine geçirilen verilerin geçerliliğini sağlamaya yardımcı olur. Ne yazık ki Visual Studio tarafından oluşturulan kesin türü belirtilmiş DataRow sınıfları null yapılabilir türler kullanmaz. Bunun yerine, bir DataRow içindeki belirli bir DataColumn 'un bir `NULL` veritabanı değerine karşılık gelmesi gerektiğini belirtmek için `SetColumnNameNull()` metodunu kullanmanız gerekir.

`UpdateProduct`, `GetProductByProductID(productID)`kullanarak güncelleştirmek için öncelikle ürüne yükleniriz. Bu, veritabanına gereksiz bir seyahat gibi görünse de, bu ek seyahat, gelecekteki öğreticilerde iyimser eşzamanlılık keşfetirken sizi kanıtlayacaktır. İyimser eşzamanlılık, aynı verilerde eşzamanlı olarak çalışan iki kullanıcının başka bir değişikliğin yanlışlıkla üzerine yazmamasını sağlayan bir tekniktir. Yakalayıp tüm kayıt Ayrıca, BLL 'de yalnızca DataRow 'ın sütunlarının bir alt kümesini değiştiren güncelleştirme yöntemleri oluşturmayı kolaylaştırır. `SuppliersBLL` sınıfı araştırırken böyle bir örnek görüyoruz.

Son olarak, `ProductsBLL` sınıfında [DataObject özniteliği](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx) (dosyanın üst kısmına yakın olan Class ifadesinden önce `[System.ComponentModel.DataObject]` sözdizimi) ve yöntemlerin [DataObjectMethodAttribute özniteliklerine](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx)sahip olduğunu unutmayın. `DataObject` öznitelik, sınıfı bir [ObjectDataSource denetimine](https://msdn.microsoft.com/library/9a4kyhcx.aspx)bağlamak için uygun bir nesne olarak işaretler, ancak `DataObjectMethodAttribute` yöntemin amacını gösterir. Gelecek öğreticilerde göreceğiniz gibi, ASP.NET 2.0 'ın ObjectDataSource, bir sınıftan verilere bildirimli olarak erişmeyi kolaylaştırır. ObjectDataSource 'un sihirbazda bağlanacak olası sınıfların listesini filtrelemeye yardımcı olmak için, varsayılan olarak yalnızca `DataObjects` olarak işaretlenen sınıflar sihirbazın açılan listesinde gösterilir. `ProductsBLL` sınıfı bu öznitelikler olmadan aynı zamanda çalışır, ancak bunları eklemek, ObjectDataSource 'un Sihirbazı 'nda ile çalışmayı kolaylaştırır.

## <a name="adding-the-other-classes"></a>Diğer sınıfları ekleme

`ProductsBLL` sınıfı tamamlandığımızda Kategoriler, tedarikçiler ve çalışanlar ile çalışmaya yönelik sınıfları eklememiz gerekir. Yukarıdaki örnekteki kavramları kullanarak aşağıdaki sınıfları ve yöntemleri oluşturmak için bir dakikanızı ayırın:

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

Bir yöntemi, `SuppliersBLL` sınıfının `UpdateSupplierAddress` yöntemi olduğunu belirtmekte. Bu yöntem, yalnızca tedarikçinin adres bilgilerini güncelleştirmek için bir arabirim sağlar. Bu yöntem, iç olarak belirtilen `supplierID` (`GetSupplierBySupplierID`kullanarak) `SupplierDataRow` nesnesini okur, adresle ilgili özellikleri ayarlar ve sonra `SupplierDataTable``Update` yöntemine çağrı yapar. `UpdateSupplierAddress` yöntemi şöyledir:

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample2.cs)]

BLL sınıflarının tüm uygulamam için bu makalenin karşıdan yükleme bölümüne bakın.

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>2\. Adım: tür veri kümelerine BLL sınıfları aracılığıyla erişme

İlk öğreticide, program aracılığıyla doğrudan yazılan veri kümesiyle çalışma örnekleri gördünüz, ancak BLL sınıflarımızın eklenmesiyle, sunum katmanının bunun yerine BLL ile çalışması gerekir. İlk öğreticiden `AllProducts.aspx` örnekte, `ProductsTableAdapter` aşağıdaki kodda gösterildiği gibi ürün listesini bir GridView 'a bağlamak için kullanılmıştır:

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample3.cs)]

Yeni BLL sınıflarını kullanmak için, her bir kodun ilk satırı, yalnızca `ProductsTableAdapter` nesnesini bir `ProductBLL` nesnesiyle değiştirecek.

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample4.cs)]

BLL sınıflarına Ayrıca, ObjectDataSource kullanılarak bildirimli olarak (yazılan veri kümesi gibi) erişilebilir. Aşağıdaki öğreticilerde, ObjectDataSource daha ayrıntılı bir şekilde ele alacağız.

[![ürünlerin listesi bir GridView içinde görüntülenir](creating-a-business-logic-layer-cs/_static/image4.png)](creating-a-business-logic-layer-cs/_static/image3.png)

**Şekil 3**: ürünlerin listesi bir GridView 'da görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-business-logic-layer-cs/_static/image5.png))

## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>3\. Adım: DataRow sınıflarına alan düzeyinde doğrulama ekleme

Alan düzeyi doğrulama, ekleme veya güncelleştirme sırasında iş nesnelerinin özellik değerleriyle ilgili olup olmadığını denetler. Ürünlerin bazı alan düzeyi doğrulama kuralları şunları içerir:

- `ProductName` alan 40 karakter uzunluğunda veya daha az olmalıdır
- `QuantityPerUnit` alanın uzunluğu 20 karakter veya daha az olmalıdır
- `ProductID`, `ProductName`ve `Discontinued` alanları gereklidir, ancak diğer tüm alanlar isteğe bağlıdır
- `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`ve `ReorderLevel` alanları sıfırdan büyük veya sıfıra eşit olmalıdır

Bu kurallar, ve veritabanı düzeyinde ifade edilmelidir. `ProductName` ve `QuantityPerUnit` alanlarındaki karakter sınırı `Products` tablosundaki bu sütunların veri türleri tarafından yakalanır (sırasıyla`nvarchar(40)` ve `nvarchar(20)`). Alanların gerekli olup olmadığı ve isteğe bağlı olarak, veritabanı tablosu sütunu `NULL` s 'ye izin veriyorsa ifade edilir. Yalnızca sıfırdan büyük veya sıfıra eşit değerlerin `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`veya `ReorderLevel` sütunlarına göre olmasını sağlamak için dört [Denetim kısıtlaması](https://msdn.microsoft.com/library/ms188258.aspx) vardır.

Bu kuralların veritabanında zorlanmaya ek olarak, veri kümesi düzeyinde de zorunlu kılınmaları gerekir. Aslında, alan uzunluğu ve değerin gerekli veya isteğe bağlı olup olmadığı her DataTable 'ın veri sütunları kümesi için zaten yakalandı. Mevcut Alan düzeyi doğrulamayı otomatik olarak temin etmek için, veri kümesi tasarımcısına gidin, DataTable 'lerden birindeki bir alanı seçin ve ardından Özellikler penceresi gidin. Şekil 4 ' te gösterildiği gibi, `ProductsDataTable` `QuantityPerUnit` DataColumn en fazla 20 karakter uzunluğunda ve `NULL` değerlere izin veriyor. `ProductsDataRow``QuantityPerUnit` özelliğini 20 karakterden daha uzun bir dize değeri olarak ayarlamaya çalışarız, bir `ArgumentException` oluşturulur.

[DataColumn ![temel alan düzeyi doğrulaması sağlar](creating-a-business-logic-layer-cs/_static/image7.png)](creating-a-business-logic-layer-cs/_static/image6.png)

**Şekil 4**: DataColumn, temel alan düzeyi doğrulaması sağlar ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-business-logic-layer-cs/_static/image8.png))

Ne yazık ki, Özellikler penceresi üzerinden `UnitPrice` değeri sıfırdan büyük veya sıfıra eşit olması gibi sınır denetimleri belirtemezsiniz. Bu tür alan düzeyinde doğrulama sağlamak için DataTable 'ın [ColumnChanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx) olayı için bir olay işleyicisi oluşturulması gerekir. [Önceki öğreticide](creating-a-data-access-layer-cs.md)belirtildiği gibi, yazılan veri kümesi tarafından oluşturulan veri kümesi, DataTable ve DataRow nesneleri, kısmi sınıfların kullanımı aracılığıyla Genişletilebilir. Bu tekniği kullanarak `ProductsDataTable` sınıfı için `ColumnChanging` olay işleyicisi oluşturabiliriz. `ProductsDataTable.ColumnChanging.cs`adlı `App_Code` klasörde bir sınıf oluşturarak başlayın.

[![App_Code klasöre yeni bir sınıf ekleyin](creating-a-business-logic-layer-cs/_static/image10.png)](creating-a-business-logic-layer-cs/_static/image9.png)

**Şekil 5**: `App_Code` klasöre yeni bir sınıf ekleyin ([tam boyutlu görüntüyü görüntülemek için tıklayın](creating-a-business-logic-layer-cs/_static/image11.png))

Sonra, `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`ve `ReorderLevel` sütun değerlerinin (`NULL`değilse) sıfırdan büyük veya sıfıra eşit olmasını sağlayan `ColumnChanging` olayı için bir olay işleyicisi oluşturun. Böyle bir sütun Aralık dışında ise, bir `ArgumentException`oluşturun.

ProductsDataTable.ColumnChanging.cs

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample5.cs)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>4\. Adım: BLL 'nin sınıflarına özel Iş kuralları ekleme

Alan düzeyi doğrulamaya ek olarak, tek sütunlu düzeyde ifade edilen farklı varlıklar veya kavramlar içeren üst düzey özel iş kuralları olabilir, örneğin:

- Bir ürün kullanımdan kaldırılmıştır, `UnitPrice` güncelleştirilemez
- Bir çalışanın yer aldığı ülke, yöneticisinin ait olduğu ülke ile aynı olmalıdır
- Ürün, tedarikçi tarafından sunulan tek ürün ise kullanımdan kaldırılmıştır

BLL sınıfları, uygulamanın iş kurallarına uyulması için denetimler içermelidir. Bu denetimler, uygulandıkları yöntemlere doğrudan eklenebilir.

İş kurallarımızın bir ürünün belirli bir tedarikçiden tek ürün olması halinde Discontinued olarak işaretlenmediğini dikte etmediğini düşünün. Diğer bir deyişle, ürün *X* , tedarikçinin *Y*'den satın aldığımız tek ürün ise, *x* olarak Discontinued olarak işaretliyoruz; Bununla birlikte *, tedarikçimiz* üç ürün, *A*, *B*ve *C*ile sağlandıysa, bunların tümünü ve bunların tümünü Discontinued olarak işaretleriz. Tek iş kuralı, ancak iş kuralları ve yaygın anlamda her zaman hizalanmaz!

Bu iş kuralını, `Discontinued` `true` olarak ayarlanmış olup olmadığını denetleyerek başlayacağız `UpdateProducts` yöntemde zorlamak için, bu ürünün tedarikçiden satın aldığımız ürünlerin sayısını öğrenmek üzere `GetProductsBySupplierID` çağırıyoruz. Bu tedarikçiden yalnızca bir ürün satın aldıysanız bir `ApplicationException`oluşturacağız.

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample6.cs)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>Sunu katmanındaki doğrulama hatalarına yanıt verme

Sunu katmanından BLL 'yi çağırırken, ortaya çıkan tüm özel durumları işlemeye veya ASP.NET (`HttpApplication``Error` olayını harekete geçirme) kadar balonculara kadar olan bir özel durum olup istemediğinize karar verebilirsiniz. BLL ile programlı olarak çalışırken bir özel durumu işlemek için, bir TRY kullanabiliriz [... ](https://msdn.microsoft.com/library/0yd65esw.aspx)aşağıdaki örnekte gösterildiği gibi catch bloğu:

[!code-csharp[Main](creating-a-business-logic-layer-cs/samples/sample7.cs)]

Gelecekteki öğreticilerde göreceğiniz gibi, verileri eklemek, güncelleştirmek veya silmek için veri Web denetimi kullanırken BLL 'den kabarcık yapan özel durumların işlenmesi, kodu `try...catch` bloklarda kaydırmak zorunda kalmadan doğrudan bir olay işleyicisinde ele alınabilir.

## <a name="summary"></a>Özet

İyi tasarlanmış bir uygulama, her biri belirli bir rolü kapsülleyen ayrı katmanlara oluşturulur. Bu makale serisinin ilk öğreticisinde, yazılan veri kümelerini kullanarak bir veri erişim katmanı oluşturduk; Bu öğreticide, bir Iş mantığı katmanını, uygulama `App_Code` klasörü içinde DAL olarak çağıran bir dizi sınıf olarak geliştirdik. BLL, uygulamamız için alan düzeyi ve iş düzeyi mantığı uygular. Ayrı bir BLL oluşturmaya ek olarak, bu öğreticide yaptığımız gibi, TableAdapters ' yöntemlerini kısmi sınıfların kullanımı aracılığıyla genişletmenin yanı sıra başka bir seçenek de vardır. Ancak, bu tekniğin kullanılması, mevcut yöntemleri geçersiz kılmamızı veya bu makalede gerçekleştirdiğimiz yaklaşımdan, DAL ve BLL 'lerimizi ayrı olarak ayırmamıza izin vermez.

DAL ve BLL, sunum katmanımızda başlamaya hazırız. Bir [sonraki öğreticide](master-pages-and-site-navigation-cs.md) , veri erişimi konularından kısa bir turtur ve öğreticiler genelinde kullanılmak üzere tutarlı bir sayfa düzeni tanımlayacağız.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticide lider gözden geçirenler Liz Shulok, dennıs Patterson, Carlos Santos ve Tepton Giesenow. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](creating-a-data-access-layer-cs.md)
> [İleri](master-pages-and-site-navigation-cs.md)
