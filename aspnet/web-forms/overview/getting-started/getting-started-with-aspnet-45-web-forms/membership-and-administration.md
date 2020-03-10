---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
title: Üyelik ve yönetim | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 732a2316-e49f-4f72-becd-0cd72f14457e
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/membership-and-administration
msc.type: authoredcontent
ms.openlocfilehash: ab00bc90bfc767d06e747be6dfb973245b5aae88
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546741"
---
# <a name="membership-and-administration"></a>Üyelik ve Yönetim

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğreticide, özel bir rol eklemek ve ASP.NET Identity kullanmak için Wingtip Toys örnek uygulamasını güncelleştirme yöntemi gösterilmektedir. Ayrıca, özel bir rolün bulunduğu kullanıcının Web sitesinden ürün ekleyip kaldırabileceği bir Yönetim sayfasının nasıl uygulanacağını gösterir.

[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md) , ASP.NET Web uygulaması oluşturmak için kullanılan üyelik sistemidir ve ASP.NET 4,5 ' de kullanılabilir. ASP.NET Identity, Visual Studio 2013 Web Forms proje şablonunda ve ayrıca [ASP.NET MVC](../../../../mvc/index.md), [ASP.NET Web apı 'Si](../../../../web-api/index.md)ve [ASP.net tek sayfalı uygulama](../../../../single-page-application/index.md)için şablonlar kullanılır. Ayrıca, boş bir Web uygulamasıyla başladığınızda NuGet kullanarak ASP.NET Identity sistemini özel olarak yükleyebilirsiniz. Ancak, bu öğretici serisinde ASP.NET Identity sistemini içeren **Web Forms**ProjectTemplate kullanın. ASP.NET Identity, kullanıcıya özel profil verilerini uygulama verileriyle tümleştirmeyi kolaylaştırır. Ayrıca, ASP.NET Identity uygulamanızdaki Kullanıcı profillerinin Kalıcılık modelini seçmenizi sağlar. Verileri bir SQL Server veritabanında veya Microsoft Azure depolama tabloları gibi *NoSQL* veri depoları dahil olmak üzere başka bir veri deposunda saklayabilirsiniz.

Bu öğretici, Wingtip Toys öğretici serisi ' nde, "PayPal ile kullanıma alma ve ödeme" başlıklı önceki öğreticide oluşturulur.

## <a name="what-youll-learn"></a>Öğrenecekleriniz:

- Uygulamaya özel bir rol ve Kullanıcı eklemek için kod kullanma.
- Yönetim klasörü ve sayfasına erişimi kısıtlama.
- Özel role ait olan kullanıcı için gezinti sağlama.
- Bir [DropDownList](https://msdn.microsoft.com/library/system.web.ui.webcontrols.dropdownlist(v=vs.110).aspx) denetimini ürün kategorileriyle doldurmak için model bağlamayı kullanma.
- Dosya [yükleme](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload(v=vs.110).aspx) denetimini kullanarak Web uygulamasına bir dosya yükleme.
- Giriş doğrulamasını uygulamak için doğrulama denetimlerini kullanma.
- Uygulamadan ürün ekleme ve kaldırma.

## <a name="these-features-are-included-in-the-tutorial"></a>Bu özellikler öğreticiye dahil edilmiştir:

- ASP.NET Kimlik
- Yapılandırma ve yetkilendirme
- Model bağlama
- Unobtrusive doğrulaması

ASP.NET Web Forms üyelik özellikleri sağlar. Varsayılan şablonu kullanarak, uygulama çalışırken hemen kullanabileceğiniz yerleşik üyelik işlevselliğine sahip olursunuz. Bu öğreticide, özel bir rol eklemek ve bu role bir kullanıcı atamak için ASP.NET Identity nasıl kullanılacağı gösterilmektedir. Yönetim klasörüne erişimi nasıl kısıtlayacağınızı öğreneceksiniz. Yönetim klasörüne, ürün ekleme ve kaldırma ve bir ürünün eklendikten sonra önizlemesi için özel bir rol sağlayan bir sayfa ekleyeceksiniz.

## <a name="adding-a-custom-role"></a>Özel rol ekleme

ASP.NET Identity kullanarak özel bir rol ekleyebilir ve kodu kullanarak bu role bir kullanıcı atayabilirsiniz.

1. **Çözüm Gezgini**, *Logic* Folder öğesine sağ tıklayın ve yeni bir sınıf oluşturun.
2. Yeni sınıfı *RoleActions.cs*olarak adlandırın.
3. Kodu aşağıdaki şekilde görünecek şekilde değiştirin:  

    [!code-csharp[Main](membership-and-administration/samples/sample1.cs?highlight=8)]
4. **Çözüm Gezgini**, *Global.asax.cs* dosyasını açın.
5. *Global.asax.cs* dosyasını, sarı renkle vurgulanmış kodu ekleyerek değiştirin, böylece şöyle görünür:  

    [!code-csharp[Main](membership-and-administration/samples/sample2.cs?highlight=11,26-28)]
6. `AddUserAndRole` kırmızı renkte altı çizili olduğuna dikkat edin. AddUserAndRole koduna çift tıklayın.  
   Vurgulanan yöntemin başındaki "A" harfinin altı çizili olacaktır.
7. "A" harfinin üzerine gelin ve `AddUserAndRole` yöntemi için bir yöntem saplaması oluşturmanıza izin veren kullanıcı arabirimine tıklayın. 

    ![Üyelik ve yönetim-Yöntem saplaması oluştur](membership-and-administration/_static/image1.png)
8. Başlıklı seçeneğe tıklayın:  
    `Generate method stub for "AddUserAndRole" in "WingtipToys.Logic.RoleActions"`
9. *Mantıksal* klasörden *RoleActions.cs* dosyasını açın.  
   `AddUserAndRole` yöntemi sınıf dosyasına eklenmiştir.
10. `NotImplementedException` kaldırarak ve vurgulanmış kodu sarı olarak ekleyerek *RoleActions.cs* dosyasını değiştirin, böylece şöyle görünür:  

    [!code-csharp[Main](membership-and-administration/samples/sample3.cs?highlight=5-7,15-51)]

Yukarıdaki kod, üyelik veritabanı için ilk olarak bir veritabanı bağlamı oluşturur. Üyelik veritabanı, *App\_Data* klasöründe bir *. mdf* dosyası olarak da depolanır. İlk Kullanıcı bu Web uygulamasında oturum açtıktan sonra bu veritabanını görüntüleyebileceksiniz. 

> [!NOTE] 
> 
> Üyelik verilerini ürün verileriyle birlikte depolamak istiyorsanız, yukarıdaki kodda ürün verilerini depolamak için kullandığınız **DbContext** 'i kullanmayı göz önünde bulundurun.

 *İnternal* anahtar sözcüğü, türler (sınıflar gibi) ve tür üyeleri (örneğin, Yöntemler veya Özellikler) için bir erişim değiştiricisidir. İç türlere veya üyelere yalnızca aynı derlemede *(. dll* dosyasında) bulunan dosyalar içinde erişilebilir. Uygulamanızı oluşturduğunuzda, uygulamanızı çalıştırdığınızda yürütülen kodu içeren bir derleme dosyası *(. dll*) oluşturulur. 

Rol yönetimi sağlayan `RoleStore` nesnesi veritabanı bağlamına göre oluşturulur.

> [!NOTE] 
> 
> `RoleStore` nesnesi oluşturulduğunda, genel bir `IdentityRole` türü kullandığını unutmayın. Bu, `RoleStore` yalnızca `IdentityRole` nesneleri içerme iznine sahip olduğu anlamına gelir. Ayrıca, genel türler kullanılarak bellekteki kaynaklar daha iyi işlenir.

Ardından `RoleManager` nesnesi, az önce oluşturduğunuz `RoleStore` nesnesine göre oluşturulur. `RoleManager` nesnesi, `RoleStore`değişiklikleri otomatik olarak kaydetmek için kullanılabilecek role ilgili API 'YI kullanıma sunar. `RoleManager`, yalnızca `IdentityRole` nesneleri içermesine izin verilir çünkü kod `<IdentityRole>` genel türünü kullanır.

Üyelik veritabanında "canEdit" rolünün bulunup bulunmadığını anlamak için `RoleExists` yöntemini çağırın. Aksi takdirde, rolünü oluşturursunuz.

`UserManager` nesnesinin oluşturulması `RoleManager` denetiminden daha karmaşık görünüyor, ancak neredeyse aynı. Tek bir satırda birden çok olarak kodlanır. Burada, geçirdiğiniz parametre Parantezde bulunan yeni bir nesne olarak örnekleniyor.

Daha sonra yeni bir `ApplicationUser` nesnesi oluşturarak "canEditUser" kullanıcısını oluşturursunuz. Ardından, kullanıcıyı başarıyla oluşturursanız, kullanıcıyı yeni role eklersiniz.

> [!NOTE] 
> 
> Hata işleme, bu öğretici serisinin ilerleyen kısımlarında "ASP.NET hata Işleme" öğreticisi sırasında güncelleştirilecektir.

Uygulama bir sonraki sefer başlatıldığında, "canEditUser" adlı Kullanıcı, uygulamanın "canEdit" adlı rol olarak eklenir. Bu öğreticide daha sonra, bu öğreticide eklediğiniz ek özellikleri göstermek için "canEditUser" kullanıcısı olarak oturum açabileceksiniz. ASP.NET Identity hakkında API ayrıntıları için bkz. [Microsoft. Aspnet. Identity Ad alanı](https://msdn.microsoft.com/library/microsoft.aspnet.identity(v=vs.111).aspx). ASP.NET Identity sistemi başlatma hakkında daha fazla bilgi için bkz. [Aspnetıdentitysample](https://github.com/rustd/AspnetIdentitySample/blob/master/AspnetIdentitySample/App_Start/IdentityConfig.cs).

### <a name="restricting-access-to-the-administration-page"></a>Yönetim sayfasına erişimi sınırlandırma

Wingtip Toys örnek uygulaması, hem anonim kullanıcıların hem de oturum açan kullanıcıların ürünleri görüntülemesine ve satın almasına izin verir. Ancak, özel "canEdit" rolüne sahip oturum açmış olan Kullanıcı, ürün eklemek ve kaldırmak için sınırlı bir sayfaya erişebilir.

#### <a name="add-an-administration-folder-and-page"></a>Bir yönetim klasörü ve sayfası ekleme

Daha sonra, Wingtip Toys örnek uygulamasının özel rolüne ait olan "canEditUser" kullanıcısı için *yönetici* adlı bir klasör oluşturacaksınız.

1. **Çözüm Gezgini** ' de proje adına (**Wingtip Toys**) sağ tıklayın ve **Yeni klasör**&gt; -**Ekle** ' yi seçin.
2. Yeni klasör *yöneticisini*adlandırın.
3. *Yönetici* klasörüne sağ tıklayın ve ardından **yeni öğe**&gt; -**Ekle** ' yi seçin.   
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
4. Sol taraftaki <strong>Visual C#</strong> -&gt; <strong>Web</strong> şablonları grubunu seçin. Orta listeden, <strong>Ana sayfa ile Web formu</strong>' nu seçin, <em>adminpage. aspx</em><strong>olarak</strong> adlandırın ve <strong>Ekle</strong>' yi seçin.
5. Ana sayfa olarak *site. Master* dosyasını seçin ve ardından **Tamam**' ı seçin.

#### <a name="add-a-webconfig-file"></a>Web. config dosyası Ekle

*Yönetici* klasörüne bir *Web. config* dosyası ekleyerek, klasörde bulunan sayfaya erişimi kısıtlayabilirsiniz.

1. *Yönetici* klasörüne sağ tıklayın ve **yeni öğe**&gt; -**Ekle** ' yi seçin.  
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Visual C# Web şablonları listesinden ortadaki listeden <strong>Web yapılandırma dosyası</strong>' nı seçin, <em>Web. config</em>dosyasının varsayılan adını kabul edin ve <strong>Ekle</strong><strong>'</strong> yi seçin.
3. *Web. config* DOSYASıNDAKI mevcut XML içeriğini aşağıdakiler ile değiştirin:  

    [!code-xml[Main](membership-and-administration/samples/sample4.xml)]

*Web. config* dosyasını kaydedin. *Web. config* dosyası, yalnızca uygulamanın "CanEdit" rolüne ait olan kullanıcının, *yönetici* klasöründe bulunan sayfaya erişebileceğini belirtir.

### <a name="including-custom-role-navigation"></a>Özel rol gezintisi dahil

Özel "canEdit" rolü kullanıcısının, uygulamanın Yönetim bölümüne gitmesini sağlamak için, *site. Master* sayfasına bir bağlantı eklemeniz gerekir. Yalnızca "canEdit" rolüne ait olan kullanıcılar **yönetici** bağlantısını görebilir ve Yönetim bölümüne erişebilir.

1. Çözüm Gezgini, *site. Master* sayfasını bulup açın.
2. "CanEdit" rolü kullanıcısına ilişkin bir bağlantı oluşturmak için, vurgulanan biçimlendirmeyi aşağıdaki sıralanmamış liste `<ul>` öğesine ekleyerek listenin aşağıdaki gibi görünmesini sağlayın:  

    [!code-html[Main](membership-and-administration/samples/sample5.html?highlight=2-3)]
3. *Site.Master.cs* dosyasını açın. Sarı renkle `Page_Load` işleyicisine eklenen kodu ekleyerek **yönetici** bağlantısını yalnızca "canEditUser" kullanıcısına görünür hale getirin. `Page_Load` işleyicisi şu şekilde görünür:   

    [!code-csharp[Main](membership-and-administration/samples/sample6.cs?highlight=3-6)]

Sayfa yüklendiğinde, kod, oturum açmış kullanıcının "canEdit" rolüne sahip olup olmadığını denetler. Kullanıcı "canEdit" rolüne aitse, *adminpage. aspx* sayfasına olan bağlantıyı içeren span öğesi (ve sonuç olarak yayılma içindeki bağlantı) görünür hale getirilir.

### <a name="enabling-product-administration"></a>Ürün yönetimini etkinleştirme

Şimdiye kadar, "canEdit" rolünü oluşturdunuz ve bir "canEditUser" kullanıcısı, bir yönetim klasörü ve bir yönetim sayfası eklediniz. Yönetim klasörü ve sayfası için erişim hakları ayarlamış ve uygulamaya "canEdit" rolü için bir gezinti bağlantısı ekledik. Daha sonra, *adminpage. aspx* sayfasına ve koduna, ürünü eklemek ve kaldırmak Için "CanEdit" rolüne sahip kullanıcıyı etkinleştiren *AdminPage.aspx.cs* arka plan kod dosyasına biçimlendirme ekleyeceksiniz.

1. **Çözüm Gezgini**, *yönetici* klasöründen *adminpage. aspx* dosyasını açın.
2. Varolan biçimlendirmeyi aşağıdaki kodla değiştirin:  

    [!code-aspx[Main](membership-and-administration/samples/sample7.aspx)]
3. Ardından, *Adminpage. aspx* ' i sağ tıklayıp **kodu görüntüle**' ye tıklayarak *AdminPage.aspx.cs* arka plan kod dosyasını açın.
4. *AdminPage.aspx.cs* arka plan kod dosyasındaki mevcut kodu şu kodla değiştirin:  

    [!code-csharp[Main](membership-and-administration/samples/sample8.cs)]

*AdminPage.aspx.cs* arka plan kodu dosyası için girdiğiniz kodda, `AddProducts` adlı bir sınıf, veritabanına ürün ekleme işinin gerçek işini yapar. Bu sınıf henüz yok, bu nedenle şimdi oluşturacaksınız.

1. **Çözüm Gezgini**, *Logic* klasörüne sağ tıklayın ve sonra **Yeni öğe**&gt; -**Ekle** ' yi seçin.   
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Sol taraftaki **görsel C#**  -&gt; **kod** şablonları grubunu seçin. Ardından, orta listeden **sınıf**' ı seçin ve *AddProducts.cs*olarak adlandırın.   
   Yeni sınıf dosyası görüntülenir.
3. Mevcut kodu şu kodla değiştirin:  

    [!code-csharp[Main](membership-and-administration/samples/sample9.cs)]

*Adminpage. aspx* sayfası, kullanıcının ürünleri eklemek ve kaldırmak Için "CanEdit" rolüne ait olmasına olanak sağlar. Yeni bir ürün eklendiğinde, ürünle ilgili ayrıntılar onaylanır ve veritabanına girilir. Yeni ürün, Web uygulamasının tüm kullanıcıları tarafından hemen kullanılabilir.

#### <a name="unobtrusive-validation"></a>Unobtrusive doğrulaması

Kullanıcının *adminpage. aspx* sayfasında sağladığı ürün ayrıntıları, doğrulama denetimleri (`RequiredFieldValidator` ve `RegularExpressionValidator`) kullanılarak onaylanır. Bu denetimler otomatik olarak kaldıruntrusive doğrulamasını kullanır. Unobtrusive doğrulaması, doğrulama denetimlerinin istemci tarafı doğrulama mantığı için JavaScript kullanmasına izin verir, bu da sayfanın doğrulanacak sunucuya bir seyahat gerektirmeyeceği anlamına gelir. Varsayılan olarak, unobtrusive doğrulaması, aşağıdaki yapılandırma ayarına göre *Web. config* dosyasına dahil edilmiştir:

[!code-xml[Main](membership-and-administration/samples/sample10.xml)]

#### <a name="regular-expressions"></a>Normal İfadeler

*Adminpage. aspx* sayfasındaki ürün fiyatı bir **RegularExpressionValidator** denetimi kullanılarak onaylanır. Bu denetim, ilişkili giriş denetiminin ("AddProductPrice" TextBox) değerinin normal ifade tarafından belirtilen Düzenle eşleşip eşleşmediğini doğrular. Normal ifade, belirli karakter düzenlerini hızlı bir şekilde bulmanıza ve eşleştirmenize olanak tanıyan bir desen eşleştirme gösterimidir. **RegularExpressionValidator** denetimi aşağıda gösterildiği gibi, Fiyat girişini doğrulamak için kullanılan normal ifadeyi içeren `ValidationExpression` adlı bir özellik içerir:

[!code-aspx[Main](membership-and-administration/samples/sample11.aspx)]

#### <a name="fileupload-control"></a>Dosya karşıya yükleme denetimi

Giriş ve doğrulama denetimlerine ek olarak, *adminpage. aspx* sayfasına **dosya yükleme** denetimini eklediniz. Bu denetim, dosyaları karşıya yükleme özelliğini sağlar. Bu durumda, yalnızca görüntü dosyalarının karşıya yüklenmesine izin vermiş olursunuz. Arka plan kod dosyasında (*AdminPage.aspx.cs*) `AddProductButton` tıklandığında, kod dosya **yükleme** denetiminin `HasFile` özelliğini denetler. Denetimde bir dosya varsa ve dosya türüne (dosya uzantısına göre) izin veriliyorsa, görüntü *görüntüler* klasörüne ve uygulamanın *Images/thumbs* klasörüne kaydedilir.

#### <a name="model-binding"></a>Model bağlama

Bu öğretici serisinin başlarında, bir **ListView** denetimini, bir **formsview** denetimini, bir **GridView** denetimini ve bir **detailview** denetimini doldurmak için model bağlamayı kullandınız. Bu öğreticide, bir **DropDownList** denetimini ürün kategorilerinin bir listesiyle doldurmak için model bağlamayı kullanırsınız.

*Adminpage. aspx* dosyasına eklediğiniz biçimlendirme `DropDownAddCategory`adlı bir **DropDownList** denetimi içerir:

[!code-aspx[Main](membership-and-administration/samples/sample12.aspx)]

`ItemType` özniteliğini ve `SelectMethod` özniteliğini ayarlayarak bu **DropDownList** 'i doldurmak için model bağlamayı kullanırsınız. `ItemType` özniteliği, denetimi doldururken `WingtipToys.Models.Category` türünü kullanacağınızı belirtir. Bu türü, `Category` sınıfını (aşağıda gösterilmiştir) oluşturarak bu öğretici serisinin başlangıcında tanımlamış olursunuz. `Category` sınıfı, *category.cs* dosyasının içindeki *modeller* klasöründedir.

[!code-csharp[Main](membership-and-administration/samples/sample13.cs)]

**DropDownList** denetiminin `SelectMethod` özniteliği, arka plan kod dosyasında (*AdminPage.aspx.cs*) yer alan `GetCategories` yöntemini (aşağıda gösterilen) kullanacağınızı belirtir.

[!code-csharp[Main](membership-and-administration/samples/sample14.cs)]

Bu yöntem bir `IQueryable` arabiriminin, bir sorguyu bir `Category` türüne karşı değerlendirmek için kullanıldığını belirtir. Döndürülen değer, sayfa biçimlendirmesinde (*Adminpage. aspx*), **DropDownList** 'i doldurmak için kullanılır.

Listedeki her öğe için gösterilecek metin, `DataTextField` özniteliği ayarlanarak belirtilir. `DataTextField` özniteliği, **DropDownList** denetimindeki her bir kategoriyi göstermek için `Category` sınıfının `CategoryName` (yukarıda gösterilen) kullanır. **DropDownList** denetimindeki bir öğe seçildiğinde geçirilen gerçek değer `DataValueField` özniteliğine dayalıdır. `DataValueField` özniteliği, `Category` sınıfında (yukarıda gösterilen) tanımlamak üzere `CategoryID` olarak ayarlanır.

### <a name="how-the-application-will-work"></a>Uygulamanın nasıl çalışacaksınız

"CanEdit" rolüne ait olan kullanıcı sayfaya ilk kez gittiğinde, `DropDownAddCategory`**DropDownList** denetimi yukarıda açıklanan şekilde doldurulur. `DropDownRemoveProduct`**DropDownList** denetimi aynı yaklaşımı kullanan ürünlerle de doldurulur. "CanEdit" rolüne ait olan Kullanıcı kategori türünü seçer ve ürün ayrıntılarını (**ad**, **Açıklama**, **Fiyat**ve **resim dosyası**) ekler. "CanEdit" rolüne ait Kullanıcı, **Ürün Ekle** düğmesine tıkladığında `AddProductButton_Click` olay işleyicisi tetiklenir. Arka plan kod dosyasında (*AdminPage.aspx.cs*) bulunan `AddProductButton_Click` olay işleyicisi, izin verilen dosya türleriyle *(. gif*, *. png*, *. jpeg*veya *. jpg*) eşleştiğinden emin olmak için görüntü dosyasını denetler. Daha sonra, görüntü dosyası Wingtip Toys örnek uygulamasının bir klasörüne kaydedilir. Ardından, yeni ürün veritabanına eklenir. Yeni ürün eklemeyi tamamlamak için `AddProducts` sınıfının yeni bir örneği oluşturulur ve bu ürünler adlandırılır. `AddProducts` sınıfı `AddProduct`adlı bir yönteme sahiptir ve Products nesnesi, bu yöntemi veritabanına ürün eklemek için çağırır.

[!code-csharp[Main](membership-and-administration/samples/sample15.cs)]

Kod başarıyla yeni ürünü veritabanına eklerse, sayfa `ProductAction=add`sorgu dizesi değeri ile yeniden yüklenir.

[!code-csharp[Main](membership-and-administration/samples/sample16.cs)]

Sayfa yeniden yüklediğinde sorgu dizesi URL 'ye dahil edilir. Sayfayı yeniden yükleyerek, "canEdit" rolüne ait olan Kullanıcı, *adminpage. aspx* sayfasındaki **DropDownList** denetimlerindeki güncelleştirmeleri hemen görebilir. Ayrıca, URL ile sorgu dizesi eklenerek, sayfa "canEdit" rolüne ait olan kullanıcıya bir başarı iletisi görüntüleyebilir.

*Adminpage. aspx* sayfası yeniden yüklediğinde, `Page_Load` olayı çağrılır.

[!code-csharp[Main](membership-and-administration/samples/sample17.cs)]

`Page_Load` olay işleyicisi sorgu dizesi değerini denetler ve bir başarı iletisi gösterilip gösterilmeyeceğini belirler.

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Alışveriş sepetindeki öğeleri nasıl ekleyebileceğiniz, silebildiğini ve güncelleştirecağınızı görmek için uygulamayı şimdi çalıştırabilirsiniz. Alışveriş sepeti toplamı, alışveriş sepetindeki tüm öğelerin toplam maliyetini yansıtır.

1. Çözüm Gezgini ' de, Wingtip Toys örnek uygulamasını çalıştırmak için **F5** ' e basın.  
   Tarayıcı açılır ve *default. aspx* sayfasını gösterir.
2. Sayfanın üst kısmındaki **oturum aç** bağlantısına tıklayın. 

    ![Üyelik ve yönetim-oturum açma bağlantısı](membership-and-administration/_static/image2.png)

   *Login. aspx* sayfası görüntülenir.
3. Aşağıdaki Kullanıcı adını ve parolayı kullanın:  
   Kullanıcı adı: canEditUser@wingtiptoys.com  
   Password: Pa$$word1 

    ![Üyelik ve yönetim-oturum açma sayfası](membership-and-administration/_static/image3.png)
4. Sayfanın alt tarafında **bulunan oturum aç** düğmesine tıklayın.
5. Sonraki sayfanın üst kısmında, *adminpage. aspx* sayfasına gitmek için **yönetici** bağlantısını seçin. 

    ![Üyelik ve yönetim-yönetici bağlantısı](membership-and-administration/_static/image4.png)
6. Giriş doğrulamasını test etmek için herhangi bir ürün ayrıntısı eklemeden **Ürün Ekle** düğmesine tıklayın. 

    ![Üyelik ve yönetim-yönetici sayfası](membership-and-administration/_static/image5.png)

   Gerekli alan iletilerinin görüntülendiğini unutmayın.
7. Yeni bir ürünün ayrıntılarını ekleyin ve ardından **Ürün Ekle** düğmesine tıklayın. 

    ![Üyelik ve yönetim-ürün ekleme](membership-and-administration/_static/image6.png)
8. Eklediğiniz yeni ürünü görüntülemek için üst gezinti menüsünde **Ürünler** ' i seçin. 

    ![Üyelik ve yönetim-yeni ürünü göster](membership-and-administration/_static/image7.png)
9. Yönetim sayfasına dönmek için **yönetici** bağlantısına tıklayın.
10. Sayfanın **ürün kaldırma** bölümünde, **DropDownListBox**' a eklediğiniz yeni ürünü seçin.
11. Yeni ürünü uygulamadan kaldırmak için **ürünü kaldır** düğmesine tıklayın. 

    ![Üyelik ve yönetim-ürünü kaldır](membership-and-administration/_static/image8.png)
12. Ürünün kaldırıldığını onaylamak için üst gezinti menüsünde **Ürünler** ' i seçin.
13. Mevcut yönetim modunda **Oturumu Kapat** ' a tıklayın.   
    Üst gezinti bölmesinin artık **yönetici** menü öğesini göstermediğine dikkat edin.

## <a name="summary"></a>Özet

Bu öğreticide, özel role ait olan bir özel rol ve bir Kullanıcı, Yönetim klasörü ve sayfasına kısıtlı erişim ve özel role ait olan kullanıcı için gezinti sağlanmış olarak ekledik. Bir **DropDownList** denetimini verilerle doldurmak için model bağlamayı kullandınız. **Dosya karşıya yükleme** denetimi ve doğrulama denetimlerini uyguladık. Ayrıca, bir veritabanından ürün eklemeyi ve kaldırmayı öğrendiniz. Sonraki öğreticide, ASP.NET yönlendirmeyi nasıl uygulayacağınızı öğreneceksiniz.

## <a name="additional-resources"></a>Ek Kaynaklar

[Web. config-Authorization öğesi](https://msdn.microsoft.com/library/8d82143t(v=vs.100).aspx)  
[ASP.NET Identity](../../../../identity/overview/getting-started/introduction-to-aspnet-identity.md)  
[Üyelik, OAuth ve SQL veritabanı ile bir Azure Web sitesine güvenli bir ASP.NET Web Forms uygulaması dağıtma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure Ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [Önceki](checkout-and-payment-with-paypal.md)
> [İleri](url-routing.md)
