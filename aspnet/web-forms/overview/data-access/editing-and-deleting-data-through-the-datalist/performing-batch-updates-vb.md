---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
title: Toplu güncelleştirmeler gerçekleştirme (VB) | Microsoft Docs
author: rick-anderson
description: Tüm öğeleri düzenleme modunda olduğu ve içindeki ' Tümünü Güncelleştir ' düğmesine tıklayarak değerlerinin kaydedilebileceği tam düzenlenebilir bir DataList oluşturmayı öğrenin...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 8dac22a7-91de-4e3b-888f-a4c438b03851
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
msc.type: authoredcontent
ms.openlocfilehash: e54c9fc12da278492b54164cf657eea142a3dae6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74632577"
---
# <a name="performing-batch-updates-vb"></a>Toplu Güncelleştirmeler Gerçekleştirme (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe) veya [PDF 'yi indirin](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)

> Tüm öğeleri düzenleme modunda olduğu ve sayfadaki "Tümünü Güncelleştir" düğmesine tıklanarak değerlerinin kaydedilebileceği tam düzenlenebilir bir DataList oluşturmayı öğrenin.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md) , öğe düzeyi DataList oluşturmayı inceledik. Standart düzenlenebilir GridView gibi, DataList 'teki her öğe tıklandığı zaman öğeyi düzenlenebilir hale getirmek için bir Düzenle düğmesi içeriyordu. Bu öğe düzeyi düzenleme yalnızca zaman zaman güncellenen veriler için uygun olsa da, bazı kullanım örneği senaryoları kullanıcının birçok kaydı düzenlemesini gerektirir. Bir kullanıcının onlarca kayıt düzenlemesi gerekiyorsa ve Düzenle ' ye tıkladıktan sonra değişiklikleri yapıp, her biri için Güncelleştir ' e tıkladığınızda, tıklama miktarı üretkenliği görebilir. Bu tür durumlarda daha iyi bir seçenek, *Tüm* öğelerinin düzenleme modunda olduğu ve içindeki tüm öğeleri bir Update Tümünü Güncelleştir düğmesine tıklanarak düzenlenebildiği bir tam düzenlenebilir DataList sağlamaktır (bkz. Şekil 1).

[Tamamen düzenlenebilir bir DataList 'teki her öğe ![değiştirilebilir](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)

**Şekil 1**: tamamen düzenlenebilir bir DataList 'Teki her öğe değiştirilebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-batch-updates-vb/_static/image3.png))

Bu öğreticide, kullanıcıların tamamen düzenlenebilir bir DataList kullanarak tedarikçi adres bilgilerini güncelleştirmesine nasıl olanak sağlayacağız.

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>1\. Adım: DataList 'te Düzenlenek Kullanıcı arabirimini oluşturma

Yukarıdaki öğreticide, standart, öğe düzeyi düzenlenebilir bir DataList oluşturduğumuz iki şablon kullandık:

- `ItemTemplate` salt okunurdur Kullanıcı arabirimini içeriyordu (her bir ürün adı ve fiyatını görüntülemek için Web denetimleri etiketi).
- `EditItemTemplate`, düzenleme modu kullanıcı arabirimini içeriyordu (iki metin kutusu Web denetimi).

DataList `EditItemIndex` özelliği, `EditItemTemplate`kullanılarak `DataListItem` (varsa) işleneceğini belirler. Özellikle, `ItemIndex` değeri DataList s `EditItemIndex` özelliği ile eşleşen `DataListItem` `EditItemTemplate`kullanılarak işlenir. Tek seferde yalnızca bir öğe düzenlenebilir olduğunda, ancak tamamen düzenlenebilir bir DataList oluşturulurken bu model iyi bir şekilde geçerlidir.

Tamamen düzenlenebilir bir DataList için, *tüm* `DataListItem` öğeleri düzenlenebilir arabirim kullanarak işlemesini istiyoruz. Bunu gerçekleştirmenin en kolay yolu `ItemTemplate`düzenlenebilir arabirimini tanımlamaktır. Tedarikçiler adres bilgilerini değiştirmek için, düzenlenebilir arabirim, satıcı adını metin olarak ve ardından Adres, şehir ve ülke değerleri için metin kutuları içerir.

`BatchUpdate.aspx` sayfasını açıp bir DataList denetimi ekleyin ve `ID` özelliğini `Suppliers`olarak ayarlayın. DataList s akıllı etiketinden `SuppliersDataSource`adlı yeni bir ObjectDataSource denetimi eklemeyi tercih edin.

[SuppliersDataSource adlı yeni bir ObjectDataSource oluşturma ![](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)

**Şekil 2**: `SuppliersDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-batch-updates-vb/_static/image6.png))

`SuppliersBLL` sınıf s `GetSuppliers()` metodunu kullanarak verileri almak için ObjectDataSource 'ı yapılandırın (bkz. Şekil 3). Önceki öğreticide olduğu gibi, ObjectDataSource aracılığıyla Tedarikçi bilgilerini güncelleştirmek yerine doğrudan Iş mantığı katmanı ile çalışacağız. Bu nedenle, GÜNCELLEŞTIRME sekmesinde açılan listeyi (yok) olarak ayarlayın (bkz. Şekil 4).

[GetSuppliers () yöntemini kullanarak Tedarikçi bilgilerini alma ![](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)

**Şekil 3**: `GetSuppliers()` yöntemi kullanarak Tedarikçi bilgilerini alma ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-batch-updates-vb/_static/image9.png))

[![GÜNCELLEŞTIRME sekmesinde açılan listeyi (yok) olarak ayarlayın](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)

**Şekil 4**: güncelleştirme sekmesinde açılan listeyi (yok) olarak ayarlayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-batch-updates-vb/_static/image12.png))

Sihirbaz tamamlandıktan sonra Visual Studio, bir etiket Web denetimindeki veri kaynağı tarafından döndürülen her bir veri alanını göstermek için otomatik olarak `ItemTemplate` DataList 'i oluşturur. Bunun yerine, düzen arabirimini sağlamak için bu şablonu değiştirmemiz gerekiyor. `ItemTemplate`, DataList ' akıllı etiketindeki veya doğrudan bildirim temelli söz dizimi aracılığıyla Şablonları Düzenle seçeneği kullanılarak tasarımcı aracılığıyla özelleştirilebilir.

Tedarikçinin adını metin olarak görüntüleyen bir düzen arabirimi oluşturmak için bir dakikanızı ayırın, ancak Tedarikçi s adresi, şehir ve ülke değerleri için metin kutuları içerir. Bu değişiklikleri yaptıktan sonra, sayfa bildirimli sözdizimi aşağıdaki gibi görünmelidir:

[!code-aspx[Main](performing-batch-updates-vb/samples/sample1.aspx)]

> [!NOTE]
> Önceki öğreticide olduğu gibi, bu öğreticideki DataList 'in görünüm durumunun etkin olması gerekir.

`ItemTemplate`, `Styles.css` sınıfına eklenen ve `ProductPropertyLabel` ve `ProductPropertyValue` CSS sınıflarıyla aynı stil ayarlarını kullanacak şekilde yapılandırılan `SupplierPropertyLabel` ve `SupplierPropertyValue`iki yeni CSS sınıfı kullandım.

[!code-css[Main](performing-batch-updates-vb/samples/sample2.css)]

Bu değişiklikleri yaptıktan sonra bu sayfayı bir tarayıcı aracılığıyla ziyaret edin. Şekil 5 ' i gösterdiği gibi, her bir DataList öğesi tedarikçi adını metin olarak görüntüler ve adres, şehir ve ülkeyi göstermek için metin kutuları kullanır.

[DataList 'teki her tedarikçi ![düzenlenebilir](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)

**Şekil 5**: DataList 'teki her bir tedarikçi düzenlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](performing-batch-updates-vb/_static/image15.png))

## <a name="step-2-adding-an-update-all-button"></a>2\. Adım: Tümünü Güncelleştir düğmesi ekleme

Şekil 5 ' teki her tedarikçinin adres, şehir ve ülke alanları bir metin kutusunda görüntülenirken, şu anda bir güncelleştirme düğmesi yok demektir. Tamamen düzenlenebilir veri bilgileriyle her öğe için bir güncelleştirme düğmesine sahip olmak yerine, bir sayfada genellikle tek bir güncelleştir düğmesi vardır ve tıklandığı zaman DataList 'teki *Tüm* kayıtları günceller. Bu öğretici için, her biri sayfanın üst kısmına ve diğeri alta doğru bir şekilde iki güncelleştirme ekleyelim (iki düğmeyi de aynı etkiye sahip olur).

DataList 'in üzerine bir düğme web denetimi ekleyerek başlayın ve `ID` özelliğini `UpdateAll1`olarak ayarlayın. Sonra, DataList 'in altına ikinci düğme web denetimini ekleyin, `ID` `UpdateAll2`olarak ayarlar. Tümünü güncelleştirmek için iki düğme için `Text` özelliklerini ayarlayın. Son olarak, olaylar `Click` her iki düğme için de olay işleyicileri oluşturun. Her olay işleyicilerindeki güncelleştirme mantığını çoğaltmak yerine, bu mantığı üçüncü bir yöntemle yeniden düzenleme, `UpdateAllSupplierAddresses`, olay işleyicilerinin bu üçüncü yöntemi çağırma.

[!code-vb[Main](performing-batch-updates-vb/samples/sample3.vb)]

Şekil 6, Tümünü Güncelleştir düğmeleri eklendikten sonra sayfayı gösterir.

[Sayfaya Iki güncelleştirme ![tüm düğmeler eklendi](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)

**Şekil 6**: sayfaya Iki güncelleştirme tüm düğmeler eklenmiş ([tam boyutlu görüntüyü görüntülemek için tıklatın](performing-batch-updates-vb/_static/image18.png))

## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>3\. Adım: tüm tedarikçiler adres bilgilerini güncelleştirme

Tüm DataList öğeleri, düzen arabirimini görüntüleyen ve Tümünü Güncelleştir düğmelerinin eklenmesiyle birlikte, her durumda kalan, toplu güncelleştirmeyi gerçekleştirmek için kod yazıyor. Özellikle, DataList öğeleri arasında döngü yapmanız ve her biri için `SuppliersBLL` sınıf s `UpdateSupplierAddress` metodunu çağırmanız gerekir.

DataList 'i oluşturan `DataListItem` örneklerinin koleksiyonuna DataList s [`Items` özelliği](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx)aracılığıyla erişilebilir. Bir `DataListItem`başvurusu ile `DataKeys` koleksiyonundan ilgili `SupplierID` alabilir ve aşağıdaki kodun gösterildiği gibi `ItemTemplate` içindeki TextBox Web denetimlerine programlı bir şekilde başvurabilir:

[!code-vb[Main](performing-batch-updates-vb/samples/sample4.vb)]

Kullanıcı Update All düğmelerinden birine tıkladığında `UpdateAllSupplierAddresses` yöntemi `Suppliers` DataList 'teki her bir `DataListItem` üzerinden yinelenir ve ilgili değerleri geçirerek `SuppliersBLL` sınıf s `UpdateSupplierAddress` yöntemini çağırır. Adres, şehir veya ülke geçişleri için girilen olmayan bir değer, `UpdateSupplierAddress` (boş bir dize yerine) `Nothing` bir değerdir ve bu, temel kayıt alanları için bir veritabanı `NULL` sonuçlanır.

> [!NOTE]
> Geliştirme olarak, toplu güncelleştirme gerçekleştirildikten sonra bazı onay iletisi sağlayan sayfaya bir durum etiketi Web denetimi eklemek isteyebilirsiniz.

## <a name="updating-only-those-addresses-that-have-been-modified"></a>Yalnızca değiştirilen adresler güncelleştiriliyor

Bu öğretici için kullanılan Batch güncelleştirme algoritması, kendi adres bilgilerinin değiştirilip değiştirilmediğini bağımsız olarak DataList 'teki *her* tedarikçide `UpdateSupplierAddress` yöntemini çağırır. Bu görünmeyen güncelleştirmeler genellikle bir performans sorunu olsa da, veritabanı tablosunda yapılan değişiklikleri yeniden denetlebiliyorsanız, bu değişiklikler gereksiz kayıtlara yol açabilir. Örneğin, tüm `UPDATE` `Suppliers` öğeleri bir denetim tablosuna kaydetmek için Tetikleyiciler kullanırsanız, Kullanıcı tüm değişiklikleri Güncelleştir düğmesine her tıkladığında, kullanıcının herhangi bir değişiklik yapıp yapmadığına bakılmaksızın, sistemdeki her bir sağlayıcı için yeni bir denetim kaydı oluşturulur.

ADO.NET DataTable ve DataAdapter sınıfları, yalnızca değiştirilen, silinen ve yeni kayıtların herhangi bir veritabanı iletişimine neden olduğu durumlarda toplu güncelleştirmeleri destekleyecek şekilde tasarlanmıştır. DataTable 'daki her satır, satırın DataTable 'a eklenip eklenmeyeceğini, onun içinden silindiğini veya değiştirildiğini belirten bir [`RowState` özelliğine](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) sahiptir. Bir DataTable başlangıçta doldurulduktan sonra tüm satırlar değiştirilmeden işaretlenir. Satır s sütunlarının herhangi birinin değerini değiştirmek satırı değiştirilmiş olarak işaretler.

`SuppliersBLL` sınıfında, ilk olarak tek tedarikçide bir `SuppliersDataTable` ve ardından aşağıdaki kodu kullanarak `Address`, `City`ve `Country` sütun değerlerini ayarlayarak belirtilen tedarikçinin s adres bilgilerini güncelleştirdik:

[!code-vb[Main](performing-batch-updates-vb/samples/sample5.vb)]

Bu kod, geçirilen adres, şehir ve ülke değerlerini, değerlerin değiştirilip değiştirilmediğini bakılmaksızın `SuppliersDataTable` `SuppliersRow` atar. Bu değişiklikler `SuppliersRow` s `RowState` özelliğinin değiştirilmiş olarak işaretlenmesine neden olur. Veri erişim katmanı s `Update` yöntemi çağrıldığında, `SupplierRow` değiştirildiğini görür ve bu nedenle veritabanına bir `UPDATE` komutu gönderir.

Bununla birlikte, yalnızca `SuppliersRow` s mevcut değerlerinden farklıysa, yalnızca geçirilen adres, şehir ve ülke değerlerini atamak için bu yönteme kod ekledik. Adres, şehir ve ülkenin mevcut verilerle aynı olduğu durumlarda, hiçbir değişiklik yapılmaz ve `SupplierRow` s `RowState` değiştirilmemiş olarak işaretlenir. Ağ sonucu, DAL s `Update` yöntemi çağrıldığında, `SuppliersRow` değiştirilmediği için hiçbir veritabanı çağrısının yapılmaması durumunda olur.

Bu değişikliği yapmak için, şu kodla, geçen adres, şehir ve ülke değerlerini etkileyen deyimleri değiştirin:

[!code-vb[Main](performing-batch-updates-vb/samples/sample6.vb)]

Bu eklenen kodla, DAL s `Update` yöntemi veritabanına yalnızca adresle ilgili değerler değiştirilen kayıtlar için bir `UPDATE` ifade gönderir.

Alternatif olarak, geçilen adres alanları ve veritabanı verileri arasında herhangi bir farklılık olup olmadığını ve yoksa yalnızca DAL s `Update` metoduna olan çağrıyı atlayabilirsiniz. Bu yaklaşım, veritabanı doğrudan yöntemi bir veritabanı çağrısının gerçekten gerekli olup olmadığını tespit etmek üzere `RowState` denetlenebileceği bir `SuppliersRow` örneği geçirdiğinden, DB Direct yöntemini yeniden kullandığınızda iyi bir şekilde çalışabilir.

> [!NOTE]
> `UpdateSupplierAddress` yöntemi her çağrıldığında, güncelleştirilmiş kayıt hakkında bilgi almak için veritabanına bir çağrı yapılır. Daha sonra verilerde değişiklik olursa tablo satırını güncelleştirmek için başka bir veritabanına yapılan çağrı yapılır. Bu iş akışı, `BatchUpdate.aspx` sayfasındaki *Tüm* değişikliklere sahip bir `EmployeesDataTable` örneğini kabul eden bir `UpdateSupplierAddress` yöntemi aşırı yüklemesi oluşturularak iyileştirilebilir. Daha sonra, `Suppliers` tablodaki tüm kayıtları almak için veritabanına bir çağrı yapabilir. Bu durumda, iki sonuç kümeleri numaralandırılır ve yalnızca değişikliklerin gerçekleştiği kayıtlar güncelleştirilemeyebilir.

## <a name="summary"></a>Özet

Bu öğreticide, tam olarak düzenlenebilir bir DataList oluşturmayı, kullanıcının birden çok tedarikçi için adres bilgilerini hızlı bir şekilde değiştirmesine izin vermeyi gördük. Bir metin kutusu Web denetimi oluşturma arabirimini, DataList s `ItemTemplate`içindeki Tedarikçi adresi, şehir ve ülke değerleri için tanımlayarak başladık. Daha sonra, DataList 'in üzerinde ve altındaki tüm düğmeleri güncelleştirme ekledik. Bir Kullanıcı değişiklikleri yaptıktan ve Tümünü Güncelleştir düğmelerinden birine tıkladıktan sonra, `DataListItem` s numaralandırılır ve `SuppliersBLL` sınıfı s `UpdateSupplierAddress` yöntemine bir çağrı yapılır.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

## <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğreticiye ilişkin müşteri adayı gözden geçirenler Zack Jones ve Ken ön PISA ' dir. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, benimitchell@4GuysFromRolla.combir satır bırakın [.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Önceki](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
> [İleri](handling-bll-and-dal-level-exceptions-vb.md)
