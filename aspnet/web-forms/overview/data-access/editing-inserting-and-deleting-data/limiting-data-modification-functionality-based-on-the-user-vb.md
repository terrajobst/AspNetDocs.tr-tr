---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
title: Kullanıcıya göre veri değişikliği Işlevselliğini sınırlama (VB) | Microsoft Docs
author: rick-anderson
description: Kullanıcıların verileri düzenlemelerine izin veren bir Web uygulamasında farklı Kullanıcı hesapları farklı veri düzenleme ayrıcalıklarına sahip olabilir. Bu öğreticide t...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 9dc264a6-feb8-474b-8b91-008c50708065
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/limiting-data-modification-functionality-based-on-the-user-vb
msc.type: authoredcontent
ms.openlocfilehash: c257a930e4d27fcd42591a541e700786bf413bf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78607396"
---
# <a name="limiting-data-modification-functionality-based-on-the-user-vb"></a>Kullanıcıya Bağlı Olarak Veri Değişikliği İşlevselliğini Sınırlama (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek uygulamayı indirin](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_23_VB.exe) veya [PDF 'yi indirin](limiting-data-modification-functionality-based-on-the-user-vb/_static/datatutorial23vb1.pdf)

> Kullanıcıların verileri düzenlemelerine izin veren bir Web uygulamasında farklı Kullanıcı hesapları farklı veri düzenleme ayrıcalıklarına sahip olabilir. Bu öğreticide, ziyaret eden kullanıcıya göre veri değiştirme yeteneklerini dinamik olarak ayarlamayı inceleyeceğiz.

## <a name="introduction"></a>Giriş

Kullanıcı hesaplarını destekleyen bir dizi Web uygulaması, oturum açmış kullanıcıya göre farklı seçenekler, raporlar ve işlevler sağlar. Örneğin, öğreticilerimiz sayesinde, tedarikçi şirketlerinden kullanıcıların sitede oturum açmasına ve ürünleri hakkındaki genel bilgileri (Belki de şirket adı gibi Tedarikçi bilgileriyle birlikte) güncelleştirmesine izin vermek isteyebilir. Adres, ilgili kişi bilgileri, vb. Ayrıca, şirketinizdeki kişiler için bazı Kullanıcı hesaplarını dahil etmek ve stok, yeniden sipariş düzeyi vb. birimler gibi ürün bilgilerini oturum açabilmeleri ve güncelleştirmek isteyebilirsiniz. Web uygulamamız, anonim kullanıcıların (oturum açmamış kişiler) ziyaret etmesini de sağlayabilir, ancak bunları yalnızca verileri görüntülemesi için sınırlayabilir. Böyle bir kullanıcı hesabı sistemi söz konusu olduğunda, ASP.NET sayfalarımızda bulunan veri Web denetimlerinin, şu anda oturum açmış kullanıcı için uygun olan ekleme, düzenlemesi ve silme yeteneklerini sunmamız istiyoruz.

Bu öğreticide, ziyaret eden kullanıcıya göre veri değiştirme yeteneklerini dinamik olarak ayarlamayı inceleyeceğiz. Özellikle, tedarikçi tarafından sunulan ürünleri listeleyen bir GridView ile birlikte, düzenlenebilir bir DetailsView içinde tedarikçiler bilgilerini görüntüleyen bir sayfa oluşturacağız. Sayfayı ziyaret eden Kullanıcı şirkeemiz ise, her türlü tedarikçinin bilgilerini görüntüleyebilir; adreslerini düzenleyin; ve tedarikçinin sunduğu ürünlerin bilgilerini düzenleyin. Ancak, Kullanıcı belirli bir şirketten ise, yalnızca kendi adres bilgilerini görüntüleyebilir ve düzenleyebilir ve yalnızca üretimi durdurulmuş olarak işaretlenmemiş ürünlerini düzenleyebilir.

[Şirketimizdeki bir Kullanıcı ![tüm tedarikçilere ilişkin bilgileri düzenleyebilir](limiting-data-modification-functionality-based-on-the-user-vb/_static/image2.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image1.png)

**Şekil 1**: şirketimizdeki bir Kullanıcı herhangi bir tedarikçi bilgisini düzenleyebilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image3.png))

[Belirli bir tedarikçiden bir Kullanıcı ![, bilgilerini yalnızca görüntüleyebilir ve düzenleyebilir](limiting-data-modification-functionality-based-on-the-user-vb/_static/image5.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image4.png)

**Şekil 2**: belirli bir tedarikçiden gelen bir Kullanıcı, bilgilerini görüntüleyebilir ve düzenleyebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image6.png))

Haydi başlayın!

> [!NOTE]
> ASP.NET 2,0 s üyelik sistemi, Kullanıcı hesaplarını oluşturmak, yönetmek ve doğrulamak için standartlaştırılmış, genişletilebilir bir platform sağlar. Üyelik sisteminin bir incelemesi Bu öğreticilerin kapsamının ötesinde, anonim ziyaretçilerin belirli bir tedarikçiden mi yoksa şirketim mi olduğunu seçebilmesine izin vererek, bu öğretici "Fakes" üyelik yerine bu öğretici. Üyelik hakkında daha fazla bilgi için [inceleme ASP.NET 2,0 s üyelik, roller ve profil](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx) makale serisini inceleyin.

## <a name="step-1-allowing-the-user-to-specify-their-access-rights"></a>1\. Adım: kullanıcının erişim haklarını belirtmesini sağlar

Gerçek dünyada bir Web uygulamasında, Kullanıcı hesabı bilgileri şirketimize veya belirli bir tedarikçiye yönelik olarak çalıştıkseler ve kullanıcı sitede oturum açtıktan sonra bu bilgilere ASP.NET sayfalarımızdan program aracılığıyla erişilebilmesini sağlar. Bu bilgiler, ASP.NET 2,0 s rol sistemi aracılığıyla, profil sistemi üzerinden kullanıcı düzeyindeki hesap bilgileri olarak veya bazı özel yollarla yakalanamaz.

Bu öğreticinin amacı, oturum açmış kullanıcıya bağlı olarak veri değiştirme yeteneklerini ayarlamayı göstermektir ve ASP.NET 2,0 s üyeliğini, rollerini ve profil sistemlerini göstermek üzere tasarlanmamıştır, Bu sayfayı ziyaret eden kullanıcı için özellikler-kullanıcının, tedarikçiler bilgilerini görüntüleyip düzenleyebilmeleri veya düzenleyebileceği bir DropDownList veya neleri görüntüleyebileceklerini ve düzenleyebileceklerini gösteren bir DropDownList. Kullanıcı tüm Tedarikçi bilgilerini görüntüleyip düzenleyebileceğini gösteriyorsa (varsayılan), tüm tedarikçilerle bir sayfa oluşturabilir, tüm tedarikçilere ait adres bilgilerini düzenleyebilir ve seçilen tedarikçinin sunduğu herhangi bir ürün için birim başına adı ve miktarı düzenleyebilirsiniz. Kullanıcı yalnızca belirli bir tedarikçiyi görüntüleyip düzenleyebileceğini gösteriyorsa, yalnızca söz konusu tedarikçideki ayrıntıları ve ürünleri görüntüleyebilir ve *artık Discontinued olmayan* ürünlere yönelik olarak yalnızca ad ve birim bilgilerini güncelleştirebilir.

Bu öğreticideki ilk adımımız, bu DropDownList 'i oluşturmak ve bunu sistemdeki tedarikçilerle doldurmaktır. `EditInsertDelete` klasöründeki `UserLevelAccess.aspx` sayfasını açın, `ID` özelliği `Suppliers`olarak ayarlanmış bir DropDownList ekleyin ve bu DropDownList 'i `AllSuppliersDataSource`adlı yeni bir ObjectDataSource 'a bağlayın.

[AllSuppliersDataSource adlı yeni bir ObjectDataSource oluşturma ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image8.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image7.png)

**Şekil 3**: `AllSuppliersDataSource` adlı yeni bir ObjectDataSource oluşturun ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image9.png))

Bu DropDownList 'in tüm tedarikçileri içermesini istediğimize ait olduğundan, `SuppliersBLL` sınıf s `GetSuppliers()` metodunu çağırmak için ObjectDataSource 'u yapılandırın. Ayrıca, ObjectDataSource 'un adım 2 ' de ekleyeceğiniz DetailsView tarafından da kullanıldığı için, ObjectDataSource `Update()` yönteminin `SuppliersBLL` sınıf s `UpdateSupplierAddress` yöntemiyle eşlendiğinden emin olun.

ObjectDataSource sihirbazını tamamladıktan sonra, `Suppliers` DropDownList 'i yapılandırarak `CompanyName` veri alanını gösterir ve `SupplierID` veri alanını her bir `ListItem`için değer olarak kullanır.

[Suppliers DropDownList 'i CompanyName ve TedarikçiKimliği veri alanlarını kullanacak şekilde yapılandırma ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image11.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image10.png)

**Şekil 4**: `Suppliers` DropDownList 'i `CompanyName` ve `SupplierID` veri alanlarını kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image12.png))

Bu noktada, DropDownList, veritabanındaki tedarikçilerin şirket adlarını listeler. Ancak, DropDownList 'e "tüm tedarikçileri göster/Düzenle" seçeneğini de dahil etmemiz gerekir. Bunu gerçekleştirmek için `Suppliers` DropDownList s `AppendDataBoundItems` özelliğini `true` olarak ayarlayın ve ardından `Text` özelliği "tüm tedarikçileri göster/Düzenle" ve değeri `-1`olan bir `ListItem` ekleyin. Bu, doğrudan bildirim yoluyla veya Özellikler penceresi gidip DropDownList s `Items` özelliğindeki üç noktaya tıklanarak eklenebilir.

> [!NOTE]
> Bir veri bağlama DropDownList 'e Select All öğesi ekleme hakkında daha ayrıntılı bir tartışma için bir [*DropDownList öğreticisi Ile ana/ayrıntı filtrelemesine*](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) geri bakın.

`AppendDataBoundItems` özelliği ayarlandıktan ve `ListItem` eklendikten sonra, DropDownList s bildirim temelli işaretleme şöyle görünmelidir:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample1.aspx)]

Şekil 5 ' te, bir tarayıcıdan görüntülendiklerinde geçerli ilerimizin ekran görüntüsü gösterilmektedir.

[![DropDownList, tüm ListItem ve her tedarikçi için bir göster Içerir](limiting-data-modification-functionality-based-on-the-user-vb/_static/image14.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image13.png)

**Şekil 5**: `Suppliers` DropDownList tüm `ListItem`bir göster ve her bir tedarikçi Için bir tane içerir ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image15.png))

Kullanıcı arabirimini Kullanıcı seçimini değiştirdikten hemen sonra güncelleştirmek istediğimiz için, `Suppliers` DropDownList s `AutoPostBack` özelliğini `true`olarak ayarlayın. 2\. adımda, DropDownList seçimine dayalı olarak tedarikçilere ilişkin bilgileri gösteren bir DetailsView denetimi oluşturacağız. Daha sonra, 3. adımda bu DropDownList s `SelectedIndexChanged` olayı için bir olay işleyicisi oluşturacağız, burada, ilgili tedarikçi bilgilerini seçili tedarikçiye göre DetailsView 'a bağlayan bir kod ekleyeceğiz.

## <a name="step-2-adding-a-detailsview-control"></a>2\. Adım: bir DetailsView denetimi ekleme

Tedarikçi bilgilerini göstermek için bir DetailsView kullanalım. Tüm tedarikçileri görüntüleyebilecek ve düzenleyebilen Kullanıcı için, DetailsView disk belleğini destekler ve kullanıcının aynı anda Tedarikçi bilgilerini tek bir kayıtta görüntülemesine olanak tanır. Ancak, Kullanıcı belirli bir tedarikçi için çalışıyorsa, DetailsView yalnızca söz konusu tedarikçinin s bilgilerini gösterir ve bir sayfalama arabirimi içermez. Her iki durumda da, DetailsView 'un kullanıcının Tedarikçi adresini, şehir ve ülke alanlarını düzenlemesine izin verilmesi gerekir.

Sayfaya `Suppliers` DropDownList altında bir DetailsView ekleyin, `ID` özelliğini `SupplierDetails`olarak ayarlayın ve önceki adımda oluşturulan `AllSuppliersDataSource` ObjectDataSource 'a bağlayın. Sonra, "Sayfalamayı Etkinleştir" onay kutularını işaretleyin ve DetailsView ' ın akıllı etiketinde Düzenle onay kutularını etkinleştirin.

> [!NOTE]
> `Update()`, `SuppliersBLL` sınıf s `UpdateSupplierAddress` yöntemiyle ObjectDataSource s yöntemini eşleştirmediğinden, DetailsView 'un akıllı etiketinde Düzenle özelliğini etkinleştir seçeneğini görmüyorsanız. Geri dönüp bu yapılandırma değişikliğini yapmanız gereken bir zaman ayırın ve sonra, DetailsView 'un akıllı etiketinde Düzenle özelliğini etkinleştir seçeneğinin görünmesi gerekir.

`SuppliersBLL` Class s `UpdateSupplierAddress` yöntemi yalnızca dört parametre kabul ettiğinden-`supplierID`, `address`, `city`ve `country`, DetailsView s BoundFields alanlarını `CompanyName` ve `Phone` BoundFields salt okunurdur. Ayrıca, `SupplierID` BoundField öğesini tamamen kaldırın. Son olarak, `AllSuppliersDataSource` ObjectDataSource Şu anda `OldValuesParameterFormatString` özelliği `original_{0}`olarak ayarlanmıştır. Bu özellik ayarını bildirime dayalı sözdiziminden tamamen kaldırmak veya `{0}`varsayılan değere ayarlamak için bir dakikanızı ayırın.

`SupplierDetails` DetailsView ve `AllSuppliersDataSource` ObjectDataSource yapılandırıldıktan sonra, aşağıdaki bildirim temelli işaretlemeleri olacaktır:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample2.aspx)]

Bu noktada, DetailsView ' ın üzerinden disk belleğine alınabilir ve seçilen tedarikçinin s adres bilgileri `Suppliers` DropDownList ' de yapılan seçime bakılmaksızın güncelleştirilemeyebilir (bkz. Şekil 6).

[Herhangi bir üretici bilgisinin görüntülenebileceği ve adresinin güncelleştirilebilmesi ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image17.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image16.png)

**Şekil 6**: tüm tedarikçiler bilgileri görüntülenebilir ve adresi güncelleştirilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image18.png))

## <a name="step-3-displaying-only-the-selected-supplier-s-information"></a>3\. Adım: yalnızca seçili sağlayıcı bilgilerini görüntüleme

Sayfamız Şu anda, belirli bir tedarikçinin `Suppliers` DropDownList 'den seçilmesinden bağımsız olarak tüm tedarikçilerle ilgili bilgileri görüntüler. Seçili tedarikçinin yalnızca Tedarikçi bilgilerini görüntülemesi için, sayfanıza başka bir ObjectDataSource eklemek istiyoruz. Bu, belirli bir tedarikçi hakkındaki bilgileri alır.

Sayfaya `SingleSupplierDataSource`adlandırarak yeni bir ObjectDataSource ekleyin. Akıllı etiketinden veri kaynağını Yapılandır bağlantısına tıklayın ve `SuppliersBLL` sınıf s `GetSupplierBySupplierID(supplierID)` metodunu kullanın. `AllSuppliersDataSource` ObjectDataSource ile olduğu gibi, `SingleSupplierDataSource` ObjectDataSource s `Update()` yöntemi `SuppliersBLL` sınıf s `UpdateSupplierAddress` yöntemine eşlenir.

[![SingleSupplierDataSource ObjectDataSource 'ı Getsupplierbysupplierıd (SupplierID) metodunu kullanacak şekilde yapılandırın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image20.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image19.png)

**Şekil 7**: `SingleSupplierDataSource` ObjectDataSource 'ı `GetSupplierBySupplierID(supplierID)` metodunu kullanacak şekilde yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image21.png))

Sonra, `GetSupplierBySupplierID(supplierID)` Method s `supplierID` giriş parametresi için parametre kaynağını belirtmemiz istenir. DropDownList 'den seçilen tedarikçinin bilgilerini göstermek istediğinizden, parametre kaynağı olarak `Suppliers` DropDownList s `SelectedValue` özelliğini kullanın.

[TedarikçiKimliği parametre kaynağı olarak Suppliers DropDownList 'i kullanmak ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image23.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image22.png)

**Şekil 8**: `supplierID` parametre kaynağı olarak `Suppliers` DropDownList kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image24.png))

Bu İkinci ObjectDataSource da eklendiğinde, DetailsView denetimi şu anda `AllSuppliersDataSource` ObjectDataSource 'u her zaman kullanacak şekilde yapılandırılmıştır. Seçili `Suppliers` DropDownList öğesine bağlı olarak, DetailsView tarafından kullanılan veri kaynağını ayarlamak için mantık eklememiz gerekiyor. Bunu gerçekleştirmek için, üreticiler DropDownList için bir `SelectedIndexChanged` olay işleyicisi oluşturun. Bu, tasarımcıda DropDownList 'e çift tıklanarak en kolay şekilde oluşturulabilir. Bu olay işleyicisinin hangi veri kaynağını kullanacağını belirlemesi gerekir ve verileri DetailsView 'a yeniden bağlamanız gerekir. Bu, aşağıdaki kodla gerçekleştirilir:

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample3.vb)]

Olay işleyicisi, "tüm tedarikçileri göster/Düzenle" seçeneğinin seçili olup olmadığını belirleyerek başlar. Bu durumda, DetailsView `SupplierDetails` `DataSourceID` `AllSuppliersDataSource` olarak ayarlar ve kullanıcıyı `PageIndex` özelliğini 0 olarak ayarlayarak Üreticiler kümesindeki ilk kayda döndürür. Ancak, Kullanıcı DropDownList 'den belirli bir tedarikçiyi seçmiştir, DetailsView `DataSourceID` `SingleSuppliersDataSource`atanır. Veri kaynağı ne olursa olsun, `SuppliersDetails` modu salt okuma moduna geri döndürülür ve veriler `SuppliersDetails` denetim s `DataBind()` yöntemine yapılan bir çağrı ile DetailsView 'a yeniden bağlanır.

Bu olay işleyicisindeki bir yerde, "tüm tedarikçileri göster/Düzenle" seçeneği işaretli değilse, DetailsView denetimi artık seçili tedarikçiyi gösterir. Bu durumda, tüm tedarikçiler disk belleği arabiriminden görüntülenebilir. Şekil 9 ' da "tüm tedarikçileri göster/Düzenle" seçeneğinin belirlenmiş olduğu sayfa gösterilir; sayfalama arabiriminin mevcut olduğuna ve kullanıcının herhangi bir tedarikçiyi ziyaret edip güncelleştirmesine izin vermesini unutmayın. Şekil 10 ' da Ma Maison tedarikçinin seçtiği sayfa görüntülenir. Bu durumda yalnızca Ma Maison bilgileri görüntülenebilir ve düzenlenebilir.

[Tüm tedarikçiler bilgilerinin görüntülenebilmesi ve düzenlenebilmesini ![](limiting-data-modification-functionality-based-on-the-user-vb/_static/image26.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image25.png)

**Şekil 9**: tüm tedarikçiler bilgileri görüntülenebilir ve düzenlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image27.png))

[![yalnızca seçili sağlayıcı bilgileri görüntülenebilir ve düzenlenebilir](limiting-data-modification-functionality-based-on-the-user-vb/_static/image29.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image28.png)

**Şekil 10**: yalnızca seçili sağlayıcı bilgileri görüntülenebilir ve düzenlenebilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image30.png))

> [!NOTE]
> Bu öğretici için, hem DropDownList 'ler hem de DetailsView denetim `EnableViewState` `true` (varsayılan) olarak ayarlanmalıdır, çünkü DropDownList s `SelectedIndex` ve DetailsView 'un `DataSourceID` özellikleri değişiklikleri geri göndermeler arasında hatırlanmalıdır.

## <a name="step-4-listing-the-suppliers-products-in-an-editable-gridview"></a>4\. Adım: tedarikçiler ürünlerini düzenlenebilir bir GridView 'da listeleme

DetailsView tamamlanarak bir sonraki adımınız, seçili tedarikçinin sunduğu ürünleri listeleyen düzenlenebilir bir GridView içermelidir. Bu GridView yalnızca `ProductName` ve `QuantityPerUnit` alanlarında düzenlemelere izin vermeyi bilmelidir. Üstelik, sayfayı ziyaret eden Kullanıcı belirli bir tedarikçiden ise, *yalnızca kullanımdan kaldırılmıştır olan ürünlere* yönelik güncelleştirmelere izin verilmelidir. Bunu gerçekleştirmek için öncelikle yalnızca `ProductID`, `ProductName`ve `QuantityPerUnit` alanları giriş olarak alan `ProductsBLL` sınıf s `UpdateProducts` yönteminin bir aşırı yüklemesini eklememiz gerekir. Çok sayıda öğreticilerde bu süreci geliştirdik. bu nedenle, `ProductsBLL`eklenmesi gereken koda yalnızca buradan göz atalım:

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample4.vb)]

Bu aşırı yükleme oluşturulduktan sonra GridView denetimini ve ilişkili ObjectDataSource 'u eklemeye hazırız. Sayfaya yeni bir GridView ekleyin, `ID` özelliğini `ProductsBySupplier`olarak ayarlayın ve `ProductsBySupplierDataSource`adlı yeni bir ObjectDataSource kullanacak şekilde yapılandırın. Bu GridView 'un bu ürünleri seçili tedarikçiye göre listelemediğinden, `ProductsBLL` sınıf s `GetProductsBySupplierID(supplierID)` metodunu kullanın. `Update()` yöntemini yeni oluşturduğumuz yeni `UpdateProduct` aşırı yüklemeye de eşleyin.

[![, yeni oluşturulan UpdateProduct Overload 'ı kullanmak üzere ObjectDataSource 'u yapılandırmak için](limiting-data-modification-functionality-based-on-the-user-vb/_static/image32.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image31.png)

**Şekil 11**: yeni oluşturulan `UpdateProduct` aşırı yüklemeyi kullanmak için ObjectDataSource 'ı yapılandırın ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image33.png))

`GetProductsBySupplierID(supplierID)` Method s `supplierID` giriş parametresi için parametre kaynağını seçmeniz istenir. DetailsView 'da seçilen tedarikçinin ürünlerini göstermek istediğimiz için, parametre kaynağı olarak `SuppliersDetails` DetailsView denetim s `SelectedValue` özelliğini kullanın.

[![, parametre kaynağı olarak SuppliersDetails DetailsView s SelectedValue özelliğini kullanın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image35.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image34.png)

**Şekil 12**: `SuppliersDetails` DetailsView s `SelectedValue` özelliğini parametre kaynağı olarak kullanın ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image36.png))

GridView 'a dönerek, `ProductName`, `QuantityPerUnit`ve `Discontinued`dışındaki tüm GridView alanlarını kaldırarak `Discontinued` CheckBoxField salt okunurdur. Ayrıca, GridView s akıllı etiketinde Düzenle özelliğini etkinleştir seçeneğini işaretleyin. Bu değişiklikler yapıldıktan sonra, GridView ve ObjectDataSource için bildirim temelli biçimlendirme aşağıdakine benzer olmalıdır:

[!code-aspx[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample5.aspx)]

Önceki ObjectDataSources 'larımızda olduğu gibi, bu tek s `OldValuesParameterFormatString` özelliği `original_{0}`olarak ayarlanır, bu da birim başına bir ürün adı veya miktar güncelleştirilmeye çalışıldığında sorun oluşmasına neden olur. Bu özelliği bildirime dayalı sözdiziminden tamamen kaldırın veya varsayılan değer olan `{0}`ayarlayın.

Bu yapılandırma tamamlandıktan sonra sayfamız artık GridView 'da seçilen tedarikçinin sunduğu ürünleri listeler (bkz. Şekil 13). Şu anda birim başına *herhangi bir* ürün adı veya miktarı güncelleştirilebilen olabilir. Bununla birlikte, belirli bir tedarikçi ile ilişkili kullanıcılar için bu tür işlevlerin Discontinued ürünleri için izin verilmeyen şekilde, sayfa mantığımızı güncelleştirmemiz gerekir. 5\. adımda bu son parçayı içeceğiz.

[Seçili tedarikçinin sunduğu ürünlerin ![görüntülenir](limiting-data-modification-functionality-based-on-the-user-vb/_static/image38.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image37.png)

**Şekil 13**: seçili tedarikçinin sunduğu ürünler görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image39.png))

> [!NOTE]
> Bu düzenlenebilir GridView 'un eklenmesiyle birlikte `Suppliers` DropDownList s `SelectedIndexChanged` olay işleyicisi, GridView 'un salt okunurdur bir duruma döndürülmesi için güncelleştirilmeleri gerekir. Aksi halde, ürün bilgilerinin düzenlenmesinin ortasında farklı bir sağlayıcı seçilirse, yeni tedarikçi için GridView 'daki karşılık gelen dizin de düzenlenebilir olur. Bunu engellemek için GridView s `EditIndex` özelliğini `SelectedIndexChanged` olay işleyicisindeki `-1` olarak ayarlamanız yeterlidir.

Ayrıca, GridView s görünüm durumunun etkin olması önemli olduğunu (varsayılan davranış) unutmayın. GridView s `EnableViewState` özelliğini `false`olarak ayarlarsanız, eşzamanlı kullanıcıların kayıtları yanlışlıkla silmesini veya düzenlemesini sağlamak için bir risk çalıştırırsınız. Daha fazla bilgi için bkz. [Uyarı: ASP.NET 2,0 GridViews/DetailsView/formviews ile, görüntüleme ve/veya silme ve görünüm durumunu devre dışı bırakma desteği](http://scottonwriting.net/sowblog/posts/10054.aspx) .

## <a name="step-5-disallow-editing-for-discontinued-products-when-showedit-all-suppliers-is-not-selected"></a>5\. Adım: tüm tedarikçileri göster/Düzenle seçili olmadığında, üretimi durdurulmuş ürünler için düzenlemeye Izin verme

`ProductsBySupplier` GridView tamamen işlevsel olsa da, o anda belirli bir tedarikçiden bu kullanıcılara çok fazla erişim veriyor. İş kurallarımıza göre, bu gibi kullanıcılar, Discontinued ürünlerini güncelleştirebilmelidir. Bunu zorlamak için, sayfa bir tedarikçiden Kullanıcı tarafından ziyaret edildiğinde, bu GridView satırlarındaki Düzenle düğmesini, üretimi durdurulmuş ürünlerle gizleyebilir (veya devre dışı bırakabiliriz).

GridView s `RowDataBound` olayı için bir olay işleyicisi oluşturun. Bu olay işleyicisinde, kullanıcının belirli bir tedarikçiyle ilişkilendirilip ilişkilendirilmediğini belirlememiz gerekir. Bu öğreticide,-1 ' den başka bir şey varsa, Kullanıcı belirli bir tedarikçi ile ilişkilendiriliyorsa, bu öğreticide, tedarikçiler DropDownList s `SelectedValue` özelliği denetlenerek belirlenebilir. Bu tür kullanıcılar için, ürünün sonlandıranıp üretilmediğini belirlememiz gerekir. [*GridView s altbilgisi öğreticisindeki Özet bilgileri görüntüleme*](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) bölümünde açıklandığı gibi, GridView satırına bağlantılı gerçek `ProductRow` örneğine bir başvuru elde etmemiz için `e.Row.DataItem` özelliğini kullanabilirsiniz. Ürün kullanımdan kaldırılmıştır, önceki öğreticide ele alınan teknikleri kullanarak, [*silme sırasında Istemci tarafı onayı ekleyerek*](adding-client-side-confirmation-when-deleting-vb.md)GridView s Commandalanındaki Düzenle düğmesine programlı bir başvuru elde edebilirsiniz. Bir başvuruya ulaştıktan sonra düğmeyi gizleyebilir veya devre dışı bırakabiliriz.

[!code-vb[Main](limiting-data-modification-functionality-based-on-the-user-vb/samples/sample6.vb)]

Bu olay işleyicisiyle, bu sayfayı belirli bir tedarikçiden bir kullanıcı olarak ziyaret ederken, bu ürünler için Düzenle düğmesi gizlendiğinden, Discontinued olan ürünler düzenlenebilir değildir. Örneğin, Chef Anton s Gumbo karışımı, yeni Orleans Cajun Delights tedarikçisine yönelik üretimi durdurulmuş bir üründür. Bu Tedarikçiye ait sayfayı ziyaret ederken, bu ürünün düzenleme düğmesi görüş açısından gizlenir (bkz. Şekil 14). Bununla birlikte, "tüm tedarikçileri göster/Düzenle" seçeneğini kullanarak ziyaret edildiğinde Düzenle düğmesi kullanılabilir (bkz. Şekil 15).

[Tedarikçiye özgü kullanıcılar Için ![Chef Anton s Gumbo Mix için düzenleme düğmesi gizlenir](limiting-data-modification-functionality-based-on-the-user-vb/_static/image41.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image40.png)

**Şekil 14**: tedarikçiye özgü kullanıcılar Için Düzenle düğmesi Chef Anton s Gumbo Mix gizlenir ([tam boyutlu görüntüyü görüntülemek için tıklatın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image42.png))

[TÜM tedarikçiler kullanıcılarını göstermek/düzenlemek Için ![, Chef Anton s Gumbo Mix için Düzenle düğmesi görüntülenir](limiting-data-modification-functionality-based-on-the-user-vb/_static/image44.png)](limiting-data-modification-functionality-based-on-the-user-vb/_static/image43.png)

**Şekil 15**: tüm tedarikçiler kullanıcılarını göster/Düzenle Için, Chef Anton s Gumbo Mix Için Düzenle düğmesi görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](limiting-data-modification-functionality-based-on-the-user-vb/_static/image45.png))

## <a name="checking-for-access-rights-in-the-business-logic-layer"></a>Iş mantığı katmanında erişim hakları denetleniyor

Bu öğreticide, ASP.NET sayfası, kullanıcının neleri görebileceğini ve neleri güncelleştirebileceklerini ve hangi ürünlerin güncelleştirebileceklerini, tüm mantığı işler. İdeal olarak, bu mantık Iş mantığı katmanında da mevcuttur. Örneğin, `SuppliersBLL` sınıf s `GetSuppliers()` yöntemi (tüm tedarikçileri döndüren), şu anda oturum açmış kullanıcının belirli bir tedarikçi ile *ilişkilendirilmediğinden* emin olmak için bir denetim içerebilir. Benzer şekilde, `UpdateSupplierAddress` yöntemi, şu anda oturum açmış olan kullanıcının şirketim için çalıştığından emin olmak için bir denetim içerebilir (Bu nedenle tüm tedarikçiler adres bilgilerini güncelleştirebilir) veya veriler güncelleştirilmekte olan tedarikçiyle ilişkilendirilir.

Bu tür BLL katmanı, kullanıcı haklarının, sayfada BLL sınıflarının erişemediği bir DropDownList tarafından belirlendiği için buradaki BLL-Layer denetimlerini içermiyordu. Üyelik sistemini veya ASP.NET tarafından (Windows kimlik doğrulaması gibi) sunulan kullanıma hazır kimlik doğrulama düzenlerinden birini kullanırken, şu anda oturum açmış olan Kullanıcı bilgileri ve rol bilgilerine BLL 'den erişilebilir ve bu sayede erişim haklar, hem sunuda hem de BLL katmanlarında mümkün olup olmadığını denetler.

## <a name="summary"></a>Özet

Kullanıcı hesapları sağlayan çoğu sitenin, oturum açmış kullanıcıya göre veri değiştirme arabirimini özelleştirmesi gerekir. Yönetici kullanıcılar herhangi bir kaydı silebilir ve düzenleyebilir, ancak yönetici olmayan kullanıcılar yalnızca oluşturdukları kayıtları güncelleştirmek veya silmek için sınırlı olabilir. Senaryo ne olursa olsun, veri Web denetimleri, ObjectDataSource ve Iş mantığı katman sınıfları, oturum açmış kullanıcıya göre belirli işlevleri eklemek veya reddetmek için genişletilebilir. Bu öğreticide, kullanıcının belirli bir tedarikçiyle mi ilişkili olduğuna ya da şirketim için çalıştıysa, görüntülenebilir ve düzenlenebilir verilerin nasıl sınırlandıralınacağını gördük.

Bu öğreticide GridView, DetailsView ve FormView denetimleri kullanılarak veri ekleme, güncelleştirme ve silme hakkında inceleme yapılır. Sonraki öğreticiden başlayarak, sayfalama ve sıralama desteği eklemek için dikkat çekeceğiz.

Programlamanın kutlu olsun!

## <a name="about-the-author"></a>Yazar hakkında

4GuysFromRolla.com 'in, [Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), yedi ASP/ASP. net books ve [](http://www.4guysfromrolla.com)'in yazarı, 1998 sürümünden bu yana Microsoft Web teknolojileriyle çalışmaktadır. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, [*24 saat içinde ASP.NET 2,0 kendi kendinize eğitim*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)ister. mitchell@4GuysFromRolla.comadresinden erişilebilir [.](mailto:mitchell@4GuysFromRolla.com) ya da blog aracılığıyla [http://ScottOnWriting.NET](http://ScottOnWriting.NET)bulabilirsiniz.

> [!div class="step-by-step"]
> [Öncekini](adding-client-side-confirmation-when-deleting-vb.md)
