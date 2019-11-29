---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
title: Alışveriş sepeti | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 6898c601-6c31-432f-8388-e6843f8a17cb
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/shopping-cart
msc.type: authoredcontent
ms.openlocfilehash: 46264a0ab2244cff24761ce94b41722e61e3f426
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74614921"
---
# <a name="shopping-cart"></a>Alışveriş Sepeti

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğretici, Wingtip Toys örnek ASP.NET Web Forms uygulamasına bir alışveriş sepeti eklemek için gereken iş mantığını açıklamaktadır. Bu öğretici, önceki öğreticide "veri öğelerini ve ayrıntılarını görüntüleme" ve Wingtip oyuncak mağaza öğreticisi serisinin bir parçası olarak oluşturulur. Bu öğreticiyi tamamladığınızda, örnek uygulamanızın kullanıcıları alışveriş sepetindeki ürünleri ekleyebilir, kaldırabilir ve değiştirebilir.

## <a name="what-youll-learn"></a>Şunları öğreneceksiniz:

1. Web uygulaması için bir alışveriş sepeti oluşturma.
2. Kullanıcıların alışveriş sepetine öğe eklemesini sağlama.
3. Alışveriş sepeti ayrıntılarını göstermek için bir [GridView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview(v=vs.110).aspx#introduction) denetimi ekleme.
4. Sipariş toplamını hesaplama ve görüntüleme.
5. Alışveriş sepetindeki öğeleri kaldırma ve güncelleştirme.
6. Bir alışveriş sepeti sayacı ekleme.

## <a name="code-features-in-this-tutorial"></a>Bu öğreticideki kod özellikleri:

1. Entity Framework Code First
2. Veri Açıklamaları
3. Kesin tür belirtilmiş veri denetimleri
4. Model bağlama

## <a name="creating-a-shopping-cart"></a>Alışveriş sepeti oluşturma

Bu öğretici serisinde daha önce, bir veritabanından ürün verilerini görüntülemek için sayfa ve kod eklediniz. Bu öğreticide, kullanıcıların satın alma ile ilgilenen ürünleri yönetmek için bir alışveriş sepeti oluşturacaksınız. Kullanıcılar kayıtlı veya oturum açmış olmasalar bile alışveriş sepetine gözatabilecek ve bunlara öğe ekleyebilecektir. Alışveriş sepetini erişimini yönetmek için, Kullanıcı ilk kez alışveriş sepetine eriştiğinde bir genel benzersiz tanımlayıcı (GUID) kullanarak kullanıcılara benzersiz bir `ID` atayacaksınız. Bu `ID` ASP.NET oturum durumunu kullanarak depolayacaksınız.

> [!NOTE] 
> 
> ASP.NET oturum durumu, Kullanıcı siteden ayrıldıktan sonra sona erecektir kullanıcıya özgü bilgileri depolamak için uygun bir yerdir. Oturum durumunun kötüye kullanımı daha büyük sitelerde performans etkilerine sahip olsa da, oturum durumunun hafif kullanımı, tanıtım amacıyla iyi bir şekilde çalışacaktır. Wingtip Toys örnek projesi, oturum durumunun, siteyi barındıran Web sunucusunda işlem içinde depolandığı bir dış sağlayıcı olmadan nasıl kullanılacağını gösterir. Bir uygulamanın birden çok örneğini veya farklı sunuculardaki bir uygulamanın birden çok örneğini çalıştıran siteleri sağlayan daha büyük siteler için, **Windows Azure önbellek hizmeti**'ni kullanmayı düşünün. Bu önbellek hizmeti, Web sitesi dışında bir dağıtılmış önbelleğe alma hizmeti sağlar ve işlem içi oturum durumunu kullanma sorununu çözer. Daha fazla bilgi için bkz. [Windows Azure Web siteleri ile ASP.NET oturum durumunu kullanma](https://docs.microsoft.com/azure/redis-cache/cache-aspnet-session-state-provider).

### <a name="add-cartitem-as-a-model-class"></a>Bir model sınıfı olarak Cartıtem ekleme

Bu öğretici serisinde daha önce, *modeller* klasöründe `Category` ve `Product` sınıfları oluşturarak kategori ve ürün verilerinin şemasını tanımlamış olursunuz. Şimdi, alışveriş sepeti için şemayı tanımlamak üzere yeni bir sınıf ekleyin. Bu öğreticide daha sonra, `CartItem` tablosuna veri erişimini işlemek için bir sınıf ekleyeceksiniz. Bu sınıf, alışveriş sepetindeki öğeleri eklemek, kaldırmak ve güncelleştirmek için iş mantığı sağlar.

1. *Modeller* klasörüne sağ tıklayın ve **yeni öğe**&gt; -**Ekle** ' yi seçin. 

    ![Alışveriş sepeti-yeni öğe](shopping-cart/_static/image1.png)
2. **Yeni öğe Ekle** iletişim kutusu görüntülenir. **Kodu**seçin ve ardından **sınıf**' ı seçin. 

    ![Alışveriş sepeti-yeni öğe Ekle Iletişim kutusu](shopping-cart/_static/image2.png)
3. Bu yeni sınıfı *CartItem.cs*olarak adlandırın.
4. **Ekle**'yi tıklatın.  
   Yeni sınıf dosyası düzenleyicide görüntülenir.
5. Varsayılan kodu şu kodla değiştirin:   

    [!code-csharp[Main](shopping-cart/samples/sample1.cs)]

`CartItem` sınıfı, bir kullanıcının alışveriş sepetine eklediği her bir ürünü tanımlayan şemayı içerir. Bu sınıf, bu öğretici serisinde daha önce oluşturduğunuz diğer şema sınıflarına benzer. Kurala göre Entity Framework Code First, `CartItem` tablosunun birincil anahtarının `CartItemId` veya `ID`olacağını bekler. Ancak, kod, Data Annotation `[Key]` özniteliğini kullanarak varsayılan davranışı geçersiz kılar. ItemId özelliğinin `Key` özniteliği, `ItemID` özelliğinin birincil anahtar olduğunu belirtir.

`CartId` özelliği, satın alınacak öğeyle ilişkili kullanıcının `ID` belirtir. Kullanıcı alışveriş sepetine eriştiğinde bu kullanıcı `ID` oluşturmak için kod ekleyeceksiniz. Bu `ID`, bir ASP.NET oturum değişkeni olarak da depolanacak.

### <a name="update-the-product-context"></a>Ürün bağlamını güncelleştirme

`CartItem` sınıfı eklemenin yanı sıra, varlık sınıflarını yöneten ve veritabanına veri erişimi sağlayan veritabanı bağlamı sınıfını güncelleştirmeniz gerekir. Bunu yapmak için, yeni oluşturulan `CartItem` modeli sınıfını `ProductContext` sınıfına ekleyeceksiniz.

1. **Çözüm Gezgini**, *modeller* klasöründe *ProductContext.cs* dosyasını bulup açın.
2. Vurgulanan kodu *ProductContext.cs* dosyasına aşağıdaki şekilde ekleyin:  

    [!code-csharp[Main](shopping-cart/samples/sample2.cs?highlight=14)]

Bu öğretici serisinde daha önce bahsedildiği gibi, *ProductContext.cs* dosyasındaki kod `System.Data.Entity` ad alanını ekleyerek Entity Framework tüm çekirdek işlevlerine erişebilirsiniz. Bu işlevsellik, türü kesin belirlenmiş nesnelerle çalışarak verileri sorgulama, ekleme, güncelleştirme ve silme özelliğini içerir. `ProductContext` sınıfı, yeni eklenen `CartItem` model sınıfına erişim ekler.

### <a name="managing-the-shopping-cart-business-logic"></a>Alışveriş sepetini Iş mantığını yönetme

Sonra, `ShoppingCart` sınıfını yeni bir *mantıksal* klasörde oluşturacaksınız. `ShoppingCart` sınıfı `CartItem` tabloya veri erişimini işler. Bu sınıf, alışveriş sepetindeki öğeleri eklemek, kaldırmak ve güncelleştirmek için iş mantığını da içerir.

Ekleyeceğiniz alışveriş sepeti mantığı aşağıdaki eylemleri yönetmek için gereken işlevselliği içerir:

1. Alışveriş sepetine öğe ekleme
2. Alışveriş sepetinden öğeleri kaldırma
3. Alışveriş sepeti KIMLIĞINI alma
4. Alışveriş sepetinden öğe alma
5. Tüm alışveriş sepeti öğelerinin miktarını Toplam olarak alma
6. Alışveriş sepeti verilerini güncelleştirme

Alışveriş sepeti verilerine erişmek için bir alışveriş sepeti sayfası (*ShoppingCart. aspx*) ve alışveriş sepeti sınıfı birlikte kullanılacaktır. Alışveriş sepeti sayfası, kullanıcının alışveriş sepetine eklediği tüm öğeleri görüntüler. Alışveriş sepeti sayfasının ve sınıfının yanı sıra, alışveriş sepetine ürün eklemek için bir sayfa (*AddToCart. aspx*) oluşturacaksınız. Ayrıca, *ProductList. aspx* sayfasına ve *AddToCart. aspx* sayfasına bir bağlantı sağlayacak olan *ProductDetails. aspx* sayfasına kod ekleyeceksiniz. böylece, kullanıcının alışveriş sepetine ürün ekleyebilmesi gerekir.

Aşağıdaki diyagramda, Kullanıcı alışveriş sepetine bir ürün eklediğinde oluşan temel işlem gösterilmektedir.

![Alışveriş sepeti-alışveriş sepetine ekleme](shopping-cart/_static/image3.png)

Kullanıcı *ProductList. aspx* sayfasında veya *ProductDetails. aspx* sayfasında **sepet Ekle** bağlantısına tıkladığında, uygulama *AddToCart. aspx* sayfasına ve ardından otomatik olarak *ShoppingCart. aspx* sayfasına gider. *AddToCart. aspx* sayfası, ShoppingCart sınıfında bir yöntemi çağırarak, select ürünü alışveriş sepetine ekler. *ShoppingCart. aspx* sayfasında, alışveriş sepetine eklenmiş ürünler görüntülenir.

#### <a name="creating-the-shopping-cart-class"></a>Alışveriş sepeti sınıfı oluşturma

`ShoppingCart` sınıfı uygulamadaki ayrı bir klasöre eklenir, böylece model (modeller klasörü), sayfalar (kök klasörü) ve Logic (Logic Folder) arasında net bir ayrım olur.

1. **Çözüm Gezgini**, **wingtiptoys**projesine sağ tıklayın ve **Yeni klasör**&gt;-**Ekle** ' yi seçin. Yeni klasör *mantığını*adlandırın.
2. *Logic* klasörüne sağ tıklayın ve ardından **yeni öğe**&gt; -**Ekle** ' yi seçin.
3. *ShoppingCartActions.cs*adlı yeni bir sınıf dosyası ekleyin.
4. Varsayılan kodu şu kodla değiştirin:   

    [!code-csharp[Main](shopping-cart/samples/sample3.cs)]

`AddToCart` yöntemi, bireysel ürünlerin ürün `ID`göre alışveriş sepetine dahil edilmesini sağlar. Ürün sepete eklenir veya sepet zaten bu ürün için bir öğe içeriyorsa, miktar artırılır.

`GetCartId` yöntemi kullanıcı için sepet `ID` döndürür. Sepet `ID`, bir kullanıcının alışveriş sepetindeki öğeleri izlemek için kullanılır. Kullanıcının mevcut bir sepet `ID`yoksa, bu `ID` yeni bir sepet oluşturulur. Kullanıcı kayıtlı bir kullanıcı olarak oturum açmışsa, sepet `ID` Kullanıcı adına ayarlanır. Ancak, Kullanıcı oturum açmamışsa, sepet `ID` benzersiz bir değer (bir GUID) olarak ayarlanır. Bir GUID, oturum temelinde her bir kullanıcı için yalnızca bir sepet oluşturulmasını sağlar.

`GetCartItems` yöntemi, Kullanıcı için alışveriş sepeti öğelerinin bir listesini döndürür. Bu öğreticide daha sonra, `GetCartItems` yöntemi kullanılarak alışveriş sepetindeki sepet öğelerini görüntülemek için model bağlamanın kullanıldığını görürsünüz.

### <a name="creating-the-add-to-cart-functionality"></a>Sepetin ekleme Işlevini oluşturma

Daha önce belirtildiği gibi, kullanıcının alışveriş sepetine yeni ürünler eklemek için kullanılacak *AddToCart. aspx* adlı bir işleme sayfası oluşturacaksınız. Bu sayfa, yeni oluşturduğunuz `ShoppingCart` sınıfında `AddToCart` yöntemini çağırır. *AddToCart. aspx* sayfası bir ürün `ID` geçtiğini bekler. Bu ürün `ID`, `ShoppingCart` sınıfında `AddToCart` yöntemi çağrılırken kullanılacaktır.

> [!NOTE] 
> 
> Sayfa Kullanıcı arabirimi (*AddToCart. aspx*) değil, Bu sayfa için arka plan kodunu (*AddToCart.aspx.cs*) değiştiriyorsunuz.

#### <a name="to-create-the-add-to-cart-functionality"></a>Add-cart işlevini oluşturmak için:

1. **Çözüm Gezgini**, **wingtiptoys**projesine sağ tıklayın, **Yeni öğe**&gt; -**Ekle** ' ye tıklayın.  
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. *AddToCart. aspx*adlı uygulamaya standart yeni bir sayfa (Web formu) ekleyin. 

    ![Alışveriş sepeti-Web formu ekleme](shopping-cart/_static/image4.png)
3. **Çözüm Gezgini**, *AddToCart. aspx* sayfasına sağ tıklayıp **kodu görüntüle**' ye tıklayın. *AddToCart.aspx.cs* arka plan kod dosyası düzenleyicide açılır.
4. *AddToCart.aspx.cs* kodundaki mevcut kodu aşağıdaki kodla değiştirin:   

    [!code-csharp[Main](shopping-cart/samples/sample4.cs)]

*AddToCart. aspx* sayfası yüklendiğinde, ürün `ID` sorgu dizesinden alınır. Ardından, alışveriş sepeti sınıfının bir örneği oluşturulur ve bu öğreticide daha önce eklediğiniz `AddToCart` yöntemini çağırmak için kullanılır. *ShoppingCartActions.cs* dosyasında bulunan `AddToCart` yöntemi, seçili ürünü alışveriş sepetine ekleme veya seçili ürünün ürün miktarını artırma mantığını içerir. Ürün, alışveriş sepetine eklenmemişse, ürün veritabanının `CartItem` tablosuna eklenir. Ürün, alışveriş sepetine zaten eklendiyse ve Kullanıcı aynı ürüne ek bir öğe eklerse, `CartItem` tablosunda ürün miktarı artırılır. Son olarak, sayfa, kullanıcının sepetteki öğelerin güncelleştirilmiş bir listesini gördüğü bir sonraki adımda ekleyeceğiniz *ShoppingCart. aspx* sayfasına yeniden yönlendirilir.

Daha önce belirtildiği gibi, bir Kullanıcı `ID`, belirli bir kullanıcıyla ilişkili ürünleri belirlemek için kullanılır. Bu `ID`, Kullanıcı alışveriş sepetine her ürün eklediğinde `CartItem` tablosundaki bir satıra eklenir.

### <a name="creating-the-shopping-cart-ui"></a>Alışveriş sepeti Kullanıcı arabirimi oluşturma

*ShoppingCart. aspx* sayfası, kullanıcının kendi alışveriş sepetine eklediği ürünleri görüntüler. Ayrıca, alışveriş sepetindeki öğeleri ekleme, kaldırma ve güncelleştirme olanağı da sağlar.

1. **Çözüm Gezgini**, **wingtiptoys**' a sağ tıklayın, **Yeni öğe**&gt; -**Ekle** ' ye tıklayın.  
   **Yeni öğe Ekle** iletişim kutusu görüntülenir.
2. Ana sayfa **kullanarak Web formu**' nu seçerek ana sayfa içeren yeni bir sayfa (Web formu) ekleyin. Yeni sayfayı *ShoppingCart. aspx*olarak adlandırın.
3. Ana sayfayı yeni oluşturulan *. aspx* sayfasına eklemek için **site. Master** ' u seçin.
4. *ShoppingCart. aspx* sayfasında, varolan biçimlendirmeyi aşağıdaki biçimlendirme ile değiştirin:   

    [!code-aspx[Main](shopping-cart/samples/sample5.aspx)]

*ShoppingCart. aspx* sayfası, `CartList`adlı bir **GridView** denetimi içerir. Bu denetim, alışveriş sepeti verilerini veritabanından **GridView** denetimine bağlamak için model bağlamayı kullanır. **GridView** denetiminin `ItemType` özelliğini ayarladığınızda, `Item` veri bağlama ifadesi denetimin biçimlendirmesinde kullanılabilir ve denetim kesin bir şekilde türdedir. Bu öğretici serisinde daha önce bahsedildiği gibi, IntelliSense kullanarak `Item` nesnesinin ayrıntılarını seçebilirsiniz. Veri seçmek üzere model bağlamayı kullanmak üzere bir veri denetimi yapılandırmak için denetimin `SelectMethod` özelliğini ayarlarsınız. Yukarıdaki biçimlendirmede `SelectMethod`, bir `CartItem` nesnelerinin listesini döndüren Getshoppingcartıtems metodunu kullanacak şekilde ayarlarsınız. **GridView** veri denetimi, yöntemi sayfa yaşam döngüsünde uygun zamanda çağırır ve döndürülen verileri otomatik olarak bağlar. `GetShoppingCartItems` yöntemi yine de eklenmelidir.

#### <a name="retrieving-the-shopping-cart-items"></a>Alışveriş sepeti öğelerini alma

Ardından, alışveriş sepeti Kullanıcı arabirimini almak ve doldurmak için *ShoppingCart.aspx.cs* arka planda kod eklersiniz.

1. **Çözüm Gezgini**, *ShoppingCart. aspx* sayfasına sağ tıklayın ve sonra **kodu görüntüle**' ye tıklayın. *ShoppingCart.aspx.cs* arka plan kod dosyası düzenleyicide açılır.
2. Mevcut kodu şu kodla değiştirin:  

    [!code-csharp[Main](shopping-cart/samples/sample6.cs)]

Yukarıda belirtildiği gibi, `GridView` Data Control, `GetShoppingCartItems` yöntemini sayfa yaşam döngüsünde uygun zamanda çağırır ve döndürülen verileri otomatik olarak bağlar. `GetShoppingCartItems` yöntemi `ShoppingCartActions` nesnesinin bir örneğini oluşturur. Daha sonra kod, `GetCartItems` yöntemini çağırarak sepetteki öğeleri döndürmek için bu örneği kullanır.

### <a name="adding-products-to-the-shopping-cart"></a>Alışveriş sepetine ürün ekleme

*ProductList. aspx* veya *ProductDetails. aspx* sayfası görüntülendiğinde, Kullanıcı bir bağlantı kullanarak ürünü alışveriş sepetine ekleyebilecektir. Bağlantıyı tıkladıklarında, uygulama *AddToCart. aspx*adlı işleme sayfasına gider. *AddToCart. aspx* sayfası, bu öğreticide daha önce eklediğiniz `ShoppingCart` sınıfında `AddToCart` yöntemini çağırır.

Şimdi, *ProductList. aspx* sayfasına ve *ProductDetails. aspx* sayfasına bir **sepet Ekle** bağlantısı ekleyeceksiniz. Bu bağlantı, veritabanından alınan ürün `ID` içerecektir.

1. **Çözüm Gezgini**, *ProductList. aspx*adlı sayfayı bulup açın.
2. Tüm sayfanın aşağıdaki gibi görünmesi için, sarıya vurgulanan biçimlendirmeyi *ProductList. aspx* sayfasına ekleyin:  

    [!code-aspx[Main](shopping-cart/samples/sample7.aspx?highlight=50-54)]

### <a name="testing-the-shopping-cart"></a>Alışveriş sepetini test etme

Satın alma sepetini ürün eklemeyi öğrenmek için uygulamayı çalıştırın.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.  
 Proje veritabanını yeniden oluşturduktan sonra, tarayıcı açılır ve *varsayılan. aspx* sayfasını gösterir.
2. Kategori gezinti menüsünde **otomobiller** ' i seçin.  
 *ProductList. aspx* sayfası yalnızca "otomobiller" kategorisinde bulunan ürünlerin gösterildiği görüntülenir. 

    ![Alışveriş sepeti-otomobiller](shopping-cart/_static/image5.png)
3. Listelenen ilk ürünün yanındaki **sepet Ekle** bağlantısına tıklayın (dönüştürülebilir otomobil).   
 Alışveriş sepetinizdeki seçimi gösteren *ShoppingCart. aspx* sayfası görüntülenir. 

    ![Alışveriş sepeti-sepet](shopping-cart/_static/image6.png)
4. Kategori gezinti menüsünden **düzlemler** ' i seçerek ek ürünleri görüntüleyin.
5. Listelenen ilk ürünün yanındaki **sepet Ekle** bağlantısına tıklayın.  
 *ShoppingCart. aspx* sayfası ek öğeyle birlikte görüntülenir.
6. Tarayıcıyı kapatın.

### <a name="calculating-and-displaying-the-order-total"></a>Sipariş toplamını hesaplama ve görüntüleme

Alışveriş sepetine ürün eklemeye ek olarak, `ShoppingCart` sınıfına bir `GetTotal` yöntemi ekleyecek ve alışveriş sepeti sayfasında toplam sipariş miktarını görüntüleyecek olursunuz.

1. **Çözüm Gezgini**' de, *ShoppingCartActions.cs* dosyasını *Logic* klasöründe açın.
2. Aşağıdaki `GetTotal` yöntemini sarı olarak vurgulanmış şekilde `ShoppingCart` sınıfına ekleyin:   

    [!code-csharp[Main](shopping-cart/samples/sample8.cs?highlight=85-97)]

İlk olarak, `GetTotal` yöntemi kullanıcı için alışveriş sepetinin KIMLIĞINI alır. Daha sonra yöntemi, sepette listelenen her ürün için ürün fiyatını ürün miktarına göre çarparak sepet toplamı alır.

> [!NOTE] 
> 
> Yukarıdaki kod null yapılabilir "`int?`" türünü kullanır. Null yapılabilir türler, temel alınan bir türün tüm değerlerini ve aynı zamanda null değer olarak temsil edebilir. Daha fazla bilgi için bkz. [Nullable türler kullanma](https://msdn.microsoft.com/library/2cf62fcy(v=vs.110).aspx).

### <a name="modify-the-shopping-cart-display"></a>Alışveriş sepeti görüntüsünü değiştirme

Daha sonra, `GetTotal` yöntemini çağırmak üzere *ShoppingCart. aspx* sayfasının kodunu değiştireceksiniz ve sayfa yüklendiğinde bu toplamı *ShoppingCart. aspx* sayfasında görüntüleyebilirsiniz.

1. **Çözüm Gezgini**, *ShoppingCart. aspx* sayfasına sağ tıklayın ve **kodu görüntüle**' yi seçin.
2. *ShoppingCart.aspx.cs* dosyasında, aşağıdaki kodu sarı renkle ekleyerek `Page_Load` işleyicisini güncelleştirin:   

    [!code-csharp[Main](shopping-cart/samples/sample9.cs?highlight=16-31)]

*ShoppingCart. aspx* sayfası yüklendiğinde, alışveriş sepeti nesnesini yükler ve ardından `ShoppingCart` sınıfının `GetTotal` yöntemini çağırarak alışveriş sepeti toplamı alınır. Alışveriş sepeti boşsa, bu etkiye yönelik bir ileti görüntülenir.

### <a name="testing-the-shopping-cart-total"></a>Alışveriş sepetini toplam test etme

Yalnızca bir ürünü alışveriş sepetine nasıl ekleyekullanabileceğinizi görmek için uygulamayı şimdi çalıştırın, ancak alışveriş sepetini toplam ' u görebilirsiniz.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.  
 Tarayıcı açılır ve *default. aspx* sayfasını gösterir.
2. Kategori gezinti menüsünde **otomobiller** ' i seçin.
3. İlk ürünün yanındaki **sepet Ekle** bağlantısına tıklayın.   
 *ShoppingCart. aspx* sayfası, sipariş toplamla birlikte görüntülenir. 

    ![Alışveriş sepeti-sepet toplamı](shopping-cart/_static/image7.png)
4. Sepetin bazı ürünlerini (örneğin, bir düzlemi) ekleyin.
5. *ShoppingCart. aspx* sayfası, eklediğiniz tüm ürünlerin güncelleştirilmiş toplamı ile görüntülenir. 

    ![Alışveriş sepeti-birden çok ürün](shopping-cart/_static/image8.png)
6. Tarayıcı penceresini kapatarak çalışan uygulamayı durdurun.

### <a name="adding-update-and-checkout-buttons-to-the-shopping-cart"></a>Alışveriş sepetine güncelleştirme ve kullanıma alma düğmeleri ekleme

Kullanıcıların alışveriş sepetini değiştirmesine izin vermek için, alışveriş sepeti sayfasına bir **güncelleştirme** düğmesi ve bir **kullanıma alma** düğmesi ekleyeceksiniz. Bu öğretici serisinde daha sonra **kullanıma alma** düğmesi kullanılmaz.

1. **Çözüm Gezgini**' de, Web uygulaması projesinin kökündeki *ShoppingCart. aspx* sayfasını açın.
2. **Güncelleştirme** düğmesini ve **kullanıma al** düğmesini *ShoppingCart. aspx* sayfasına eklemek için, aşağıdaki kodda gösterildiği gibi, sarı renkle vurgulanmış biçimlendirmeyi varolan biçimlendirmeye ekleyin:   

    [!code-aspx[Main](shopping-cart/samples/sample10.aspx?highlight=36-45)]

Kullanıcı **Update** düğmesine tıkladığında `UpdateBtn_Click` olay işleyicisi çağrılır. Bu olay işleyicisi, bir sonraki adımda ekleyeceğiniz kodu çağırır.

Daha sonra, *ShoppingCart.aspx.cs* dosyasında yer alan kodu, sepet öğeleri aracılığıyla döngü yapmak ve `RemoveItem` ve `UpdateItem` yöntemlerini çağırmak için güncelleştirebilirsiniz.

1. **Çözüm Gezgini**, Web uygulaması projesinin kökündeki *ShoppingCart.aspx.cs* dosyasını açın.
2. Sarı ' de vurgulanan aşağıdaki kod bölümlerini *ShoppingCart.aspx.cs* dosyasına ekleyin:   

    [!code-csharp[Main](shopping-cart/samples/sample11.cs?highlight=9-11,33,44-89)]

Kullanıcı, *ShoppingCart. aspx* sayfasındaki **Güncelleştir** düğmesine tıkladığında updatecartıtems yöntemi çağırılır. Updatecartıtems yöntemi, alışveriş sepetindeki her öğe için güncelleştirilmiş değerleri alır. Ardından, Updatecartıtems yöntemi, alışveriş sepetinden öğe eklemek veya kaldırmak için `UpdateShoppingCartDatabase` yöntemini (sonraki adımda eklenen ve açıklanacak) çağırır. Veritabanı, alışveriş sepetindeki güncelleştirmeleri yansıtacak şekilde güncelleştirildikten sonra **, GridView için**`DataBind` yöntemi çağırarak, alışveriş sepeti sayfasında **GridView** denetimi güncellenir. Ayrıca, alışveriş sepeti sayfasındaki toplam sipariş miktarı, güncelleştirilmiş öğe listesini yansıtacak şekilde güncelleştirilir.

### <a name="updating-and-removing-shopping-cart-items"></a>Alışveriş sepeti öğelerini güncelleştirme ve kaldırma

*ShoppingCart. aspx* sayfasında, bir öğenin miktarını güncelleştirmek ve bir öğeyi kaldırmak için denetimlerin eklendiğini görebilirsiniz. Şimdi bu denetimlerin çalışmasını sağlayacak kodu ekleyin.

1. **Çözüm Gezgini**' de, *ShoppingCartActions.cs* dosyasını *Logic* klasöründe açın.
2. Sarı ' de vurgulanan aşağıdaki kodu *ShoppingCartActions.cs* sınıf dosyasına ekleyin:   

    [!code-csharp[Main](shopping-cart/samples/sample12.cs?highlight=99-213)]

*ShoppingCart.aspx.cs* sayfasındaki `UpdateCartItems` yönteminden çağrılan `UpdateShoppingCartDatabase` yöntemi, alışveriş sepetinden öğe güncelleştirme ya da kaldırma mantığını içerir. `UpdateShoppingCartDatabase` yöntemi, alışveriş sepeti listesinin içindeki tüm satırlarda yinelenir. Bir alışveriş sepeti öğesi kaldırılmak üzere işaretlenmişse veya miktar bir değerden küçükse `RemoveItem` yöntemi çağrılır. Aksi halde, `UpdateItem` yöntemi çağrıldığında, alışveriş sepeti öğesi güncelleştirmeler için denetlenir. Alışveriş sepeti öğesi kaldırıldıktan veya güncelleştirildikten sonra, veritabanı değişiklikleri kaydedilir.

`ShoppingCartUpdates` yapısı, tüm alışveriş sepeti öğelerini tutmak için kullanılır. `UpdateShoppingCartDatabase` yöntemi, herhangi bir öğenin güncelleştirilmesini veya kaldırılmasını öğrenmek için `ShoppingCartUpdates` yapısını kullanır.

Sonraki öğreticide, ürünleri satın aldıktan sonra alışveriş sepetini temizlemek için `EmptyCart` yöntemini kullanacaksınız. Ancak şimdilik, alışveriş sepetindeki öğelerin sayısını öğrenmek için *ShoppingCartActions.cs* dosyasına eklediğiniz `GetCount` yöntemini kullanacaksınız.

### <a name="adding-a-shopping-cart-counter"></a>Alışveriş sepeti sayacı ekleme

Kullanıcının alışveriş sepetindeki toplam öğe sayısını görüntülemesine izin vermek için, *site. Master* sayfasına bir sayaç ekleyeceksiniz. Bu sayaç, alışveriş sepetine bir bağlantı görevi görür.

1. **Çözüm Gezgini**, *site. Master* sayfasını açın.
2. Aşağıdaki gibi görünmesi için, kılavuz ' de gösterildiği gibi alışveriş sepeti sayacı bağlantısını, gezinti bölümüne ekleyerek biçimlendirmeyi değiştirin:  

    [!code-html[Main](shopping-cart/samples/sample13.html?highlight=6)]
3. Daha sonra, *site.Master.cs* dosyasının arka plan kodunu, sarıya vurgulanmış kodu aşağıdaki gibi ekleyerek güncelleştirin:  

    [!code-csharp[Main](shopping-cart/samples/sample14.cs?highlight=11,77-84)]

Sayfa HTML olarak işlenmeden önce `Page_PreRender` olayı tetiklenir. `Page_PreRender` işleyicisinde, alışveriş sepetinin toplam sayısı `GetCount` yöntemi çağırarak belirlenir. Döndürülen değer, *site. Master* sayfasının biçimlendirmesine dahil edilen `cartCount` aralığına eklenir. `<span>` Etiketler, iç öğelerin düzgün şekilde işlenmesini sağlar. Sitenin herhangi bir sayfası görüntülendiğinde, alışveriş sepeti toplamı görüntülenir. Kullanıcı alışveriş sepetini göstermek için satın alma sepet toplamı ' na de tıklayabilirsiniz.

## <a name="testing-the-completed-shopping-cart"></a>Tamamlanmış alışveriş sepetini test etme

Alışveriş sepetindeki öğeleri nasıl ekleyebileceğiniz, silebildiğini ve güncelleştirecağınızı görmek için uygulamayı şimdi çalıştırabilirsiniz. Alışveriş sepeti toplamı, alışveriş sepetindeki tüm öğelerin toplam maliyetini yansıtır.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.  
 Tarayıcı açılır ve *default. aspx* sayfasını gösterir.
2. Kategori gezinti menüsünde **otomobiller** ' i seçin.
3. İlk ürünün yanındaki **sepet Ekle** bağlantısına tıklayın.   
 *ShoppingCart. aspx* sayfası, sipariş toplamla birlikte görüntülenir.
4. Kategori gezinti menüsünden **düzlemler** ' i seçin.
5. İlk ürünün yanındaki **sepet Ekle** bağlantısına tıklayın.
6. Alışveriş sepetindeki ilk öğenin miktarını 3 ' e ayarlayın ve ikinci öğenin **öğesini kaldır** onay kutusunu seçin.<a id="a"></a>
7. Alışveriş sepeti sayfasını güncelleştirmek ve yeni sipariş toplamını göstermek için **Güncelleştir** düğmesine tıklayın. 

    ![Alışveriş sepeti-sepet güncelleştirmesi](shopping-cart/_static/image9.png)

## <a name="summary"></a>Özet

Bu öğreticide, Wingtip Toys Web Forms örnek uygulaması için bir alışveriş sepeti oluşturdunuz. Bu öğreticide, Entity Framework Code First, veri ek açıklamaları, türü kesin belirlenmiş veri denetimleri ve model bağlamayı kullandınız.

Alışveriş sepeti, kullanıcının satın alma için seçtiği öğelerin eklenmesini, silinmesini ve güncelleştirilmesini destekler. Alışveriş sepeti işlevinin uygulanmasının yanı sıra, bir **GridView** denetimindeki alışveriş sepeti öğelerini görüntülemeyi ve sipariş toplamını hesaplamayı öğrenmiş olursunuz.

## <a name="addition-information"></a>Ek bilgi

[ASP.NET oturum durumuna genel bakış](https://msdn.microsoft.com/library/ms178581.aspx)

> [!div class="step-by-step"]
> [Önceki](display_data_items_and_details.md)
> [İleri](checkout-and-payment-with-paypal.md)
