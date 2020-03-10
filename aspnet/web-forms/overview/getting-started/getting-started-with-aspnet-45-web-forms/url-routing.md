---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL yönlendirme | Microsoft Docs
author: Erikre
description: Bu öğretici serisi, ASP.NET 4,5 ve Microsoft Visual Studio Express 2013 ' i kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587439"
---
# <a name="url-routing"></a>URL Yönlendirme

by [Erik Reitan](https://github.com/Erikre)

[Wingtip Toys örnek projesini indirin (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) veya [indirme E-kitabı (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> Bu öğretici serisi, ASP.NET 4,5 ve Web için Microsoft Visual Studio Express 2013 kullanarak bir ASP.NET Web Forms uygulaması oluşturma hakkında temel bilgileri öğretir. [Kaynak koduna sahip C# ](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) Visual Studio 2013 bir proje, bu öğretici serisine eşlik etmek için kullanılabilir.

Bu öğreticide, Wingtip Toys örnek uygulamasını URL yönlendirmeyi destekleyecek şekilde değiştirirsiniz. Yönlendirme, Web uygulamanızın kolay, anımsanması kolay ve arama motorları tarafından daha iyi desteklenecek URL 'Leri kullanmasına olanak sağlar. Bu öğreticide, önceki öğreticide "üyelik ve yönetim" oluşturulur ve Wingtip Toys öğretici serisinin bir parçasıdır.

## <a name="what-youll-learn"></a>Öğrenecekleriniz:

- Bir ASP.NET Web Forms uygulamasının yollarını kaydetme.
- Bir Web sayfasına rotalar ekleme.
- Yolları desteklemek için bir veritabanından veri seçme.

## <a name="aspnet-routing-overview"></a>ASP.NET yönlendirmeye genel bakış

URL yönlendirme, bir uygulamayı fiziksel dosyalarla eşlenmez istek URL 'Lerini kabul edecek şekilde yapılandırmanıza olanak tanır. İstek URL 'si, bir kullanıcının Web sitenizde bir sayfa bulmak için tarayıcılarına girdiği URL 'dir. Kullanıcılara anlam açısından anlamlı olan ve arama motoru iyileştirmesi (SEO) konusunda yardımcı olabilecek URL 'Leri tanımlamak için yönlendirmeyi kullanırsınız.

Varsayılan olarak, Web Forms şablonu [ASP.net kolay URL 'leri](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)içerir. Temel yönlendirme işinin büyük bölümü, *kolay URL 'ler*kullanılarak uygulanır. Bununla birlikte, bu öğreticide özelleştirilmiş yönlendirme özellikleri ekleyeceksiniz.

URL yönlendirmeyi özelleştirmeden önce, Wingtip Toys örnek uygulaması aşağıdaki URL 'YI kullanarak bir ürüne bağlanabilir:

`https://localhost:44300/ProductDetails.aspx?productID=2`

URL yönlendirmeyi özelleştirerek, Wingtip Toys örnek uygulaması, okunması kolay bir URL kullanarak aynı ürüne bağlanır:

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>Yollar

Yol, bir işleyiciye eşlenmiş bir URL örüncidir. İşleyici, bir Web Forms uygulamasındaki. aspx dosyası gibi bir fiziksel dosya olabilir. Bir işleyici, isteği işleyen bir sınıf de olabilir. Bir yol tanımlamak için, URL şeklini, işleyiciyi ve isteğe bağlı olarak yol için bir ad belirterek yol sınıfının bir örneğini oluşturun.

`Route` nesnesini `RouteTable` sınıfının statik `Routes` özelliğine ekleyerek yolu uygulamaya eklersiniz. Rotalar özelliği, uygulama için tüm yolları depolayan bir `RouteCollection` nesnesidir.

### <a name="url-patterns"></a>URL desenleri

URL stili, değişmez değerler ve değişken yer tutucuları (URL parametreleri olarak adlandırılır) içerebilir. Sabit değerler ve yer tutucular, eğik çizgi (`/`) karakteriyle ayrılmış URL kesimlerinde bulunur.

Web uygulamanıza yönelik bir istek yapıldığında, URL kesimleri ve yer tutucuları olarak ayrıştırılır ve değişken değerleri istek işleyicisine sağlanır. Bu işlem, bir sorgu dizesindeki verilerin ayrıştırılıp istek işleyicisine geçirildiği yönteme benzerdir. Her iki durumda da, değişken bilgileri URL 'ye dahil edilir ve anahtar-değer çiftleri biçiminde işleyiciye geçirilir. Sorgu dizeleri için hem anahtarlar hem de değerler URL 'de bulunur. Yollar için anahtarlar, URL düzeninde tanımlanan yer tutucu adlarıdır ve yalnızca değerler URL 'de bulunur.

Bir URL düzeninde, yer tutucuları, küme ayraçları (`{` ve `}`) içine alarak tanımlarsınız. Bir kesimde birden fazla yer tutucu tanımlayabilirsiniz, ancak yer tutucuların bir sabit değer ile ayrılması gerekir. Örneğin, `{language}-{country}/{action}` geçerli bir yol modelidir. Ancak, yer tutucular arasında değişmez değer veya sınırlayıcı olmadığından `{language}{country}/{action}` geçerli bir model değildir. Bu nedenle, yönlendirme, ülke yer tutucusu için değerden dil yer tutucusu değerinin nerede ayrılabileceği belirlenemiyor.

### <a name="mapping-and-registering-routes"></a>Eşleme ve kayıt yolları

Wingtip Toys örnek uygulamasının sayfalarına yönlendirmeler dahil etmeden önce, uygulama başladığında yolları kaydetmeniz gerekir. Yolları kaydetmek için `Application_Start` olay işleyicisini değiştirirsiniz.

1. Visual Studio 'nun **Çözüm Gezgini**, *Global.asax.cs* dosyasını bulun ve açın.
2. Sarıya vurgulanan kodu *Global.asax.cs* dosyasına aşağıdaki şekilde ekleyin:   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

Wingtip Toys örnek uygulaması başladığında `Application_Start` olay işleyicisini çağırır. Bu olay işleyicisinin sonunda `RegisterCustomRoutes` yöntemi çağrılır. `RegisterCustomRoutes` yöntemi, `RouteCollection` nesnesinin `MapPageRoute` yöntemini çağırarak her bir yolu ekler. Yollar rota adı, yol URL 'SI ve fiziksel URL kullanılarak tanımlanır.

İlk parametre ("`ProductsByCategoryRoute`") yol adıdır. Gerektiğinde rotayı çağırmak için kullanılır. İkinci parametre ("`Category/{categoryName}`"), koda göre dinamik olabilecek kolay değiştirme URL 'sini tanımlar. Verileri temel alarak oluşturulan bağlantılarla bir veri denetimi doldururken bu yolu kullanırsınız. Yol aşağıdaki şekilde gösterilmiştir:

[!code-csharp[Main](url-routing/samples/sample2.cs)]

Yolun ikinci parametresi, küme ayraçları (`{ }`) tarafından belirtilen dinamik bir değer içerir. Bu durumda `categoryName`, doğru yönlendirme yolunu belirlemede kullanılacak bir değişkendir.

> [!NOTE] 
> 
> **Optional**
> 
> `RegisterCustomRoutes` yöntemini ayrı bir sınıfa taşıyarak kodunuzun yönetimini daha kolay bulabilirsiniz. *Logic* klasöründe, ayrı bir `RouteActions` sınıfı oluşturun. Yukarıdaki `RegisterCustomRoutes` yöntemini *Global.asax.cs* dosyasından yeni `RoutesActions` sınıfına taşıyın. *Global.asax.cs* dosyasından `RegisterCustomRoutes` yönteminin nasıl çağrılacağını gösteren bir örnek olarak `RoleActions` sınıfını ve `createAdmin` yöntemini kullanın.

Ayrıca, `Application_Start` olay işleyicisinin başındaki `RouteConfig` nesnesini kullanarak `RegisterRoutes` yöntemi çağrısını fark etmiş olabilirsiniz. Bu çağrı varsayılan yönlendirmeyi uygulamak için yapılır. Uygulamayı Visual Studio 'nun Web Forms şablonu kullanarak oluşturduğunuzda varsayılan kod olarak eklenmiştir.

## <a name="retrieving-and-using-route-data"></a>Rota verilerini alma ve kullanma

Yukarıda belirtildiği gibi, rotalar tanımlanabilir. *Global.asax.cs* dosyasındaki `Application_Start` olay işleyicisine eklediğiniz kod, tanımlanabilir yolları yükler.

### <a name="setting-routes"></a>Yolları ayarlama

Yollar ek kod eklemenizi gerektirir. Bu öğreticide, bir veri denetimindeki verileri kullanarak yollar oluştururken kullanılan `RouteValueDictionary` nesnesini almak için model bağlamayı kullanacaksınız. `RouteValueDictionary` nesnesi, belirli bir ürün kategorisine ait ürün adlarının bir listesini içerir. Her ürün için veri ve rota temelinde bir bağlantı oluşturulur.

#### <a name="enable-routes-for-categories-and-products"></a>Kategoriler ve ürünler için yolları etkinleştirme

Ardından, her bir ürün kategorisi bağlantısına dahil edilecek doğru yolu belirleyebilmek için `ProductsByCategoryRoute` kullanmak üzere uygulamayı güncelleştireceksiniz. Ayrıca, *ProductList. aspx* sayfasını her ürün için yönlendirilmiş bir bağlantı içerecek şekilde güncelleştireceksiniz. Bağlantılar değişiklikten önceki gibi görüntülenir, ancak bağlantılar artık URL yönlendirme kullanır.

1. **Çözüm Gezgini**, zaten açık değilse, *site. Master* sayfasını açın.
2. "`categoryList`" adlı **ListView** denetimini, sarı renkle vurgulanan değişikliklerle güncelleştirin, bu nedenle biçimlendirme aşağıdaki gibi görünür:   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. **Çözüm Gezgini**, *ProductList. aspx* sayfasını açın.
4. *ProductList. aspx* sayfasının `ItemTemplate` öğesini sarı olarak vurgulanan güncelleştirmeler ile güncelleştirin, bu nedenle biçimlendirme aşağıdaki gibi görünür:   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. *ProductList.aspx.cs* 'in arka plan kodunu açın ve sarı renkle vurgulanmış şekilde aşağıdaki ad alanını ekleyin:  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. Arka plan kodunun `GetProducts` yöntemini (*ProductList.aspx.cs*) aşağıdaki kodla değiştirin:   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>Ürün ayrıntıları için kod Ekle

Şimdi, rota verilerini kullanmak için *ProductDetails. aspx* sayfası için arka plan kodu (*ProductDetails.aspx.cs*) güncelleştirin. Yeni `GetProduct` yönteminin, kullanıcının daha eski, yönlendirilemeyen, yönlendirilmemiş URL 'YI kullanan bir bağlantı işareti olduğu durum için bir sorgu dizesi değeri de kabul ettiğini unutmayın.

1. Arka plan kodunun `GetProduct` yöntemini (*ProductDetails.aspx.cs*) aşağıdaki kodla değiştirin:   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Güncelleştirilmiş yolları görmek için uygulamayı şimdi çalıştırabilirsiniz.

1. Wingtip Toys örnek uygulamasını çalıştırmak için **F5** tuşuna basın.  
 Tarayıcı açılır ve *default. aspx* sayfasını gösterir.
2. Sayfanın üst kısmındaki **Ürünler** bağlantısına tıklayın.  
 Tüm ürünler *ProductList. aspx* sayfasında görüntülenir. Tarayıcı için aşağıdaki URL (bağlantı noktası numaranızı kullanarak) görüntülenir:  
    `https://localhost:44300/ProductList`
3. Sonra, sayfanın üst kısmındaki **araba** kategorisi bağlantısına tıklayın.  
 *ProductList. aspx* sayfasında yalnızca otomobiller görüntülenir. Tarayıcı için aşağıdaki URL (bağlantı noktası numaranızı kullanarak) görüntülenir:  
    `https://localhost:44300/Category/Cars`
4. Ürün ayrıntılarını göstermek için sayfada listelenen ilk arabasının adını ("**dönüştürülebilir otomobil**") içeren bağlantıya tıklayın.  
 Tarayıcı için aşağıdaki URL (bağlantı noktası numaranızı kullanarak) görüntülenir:  
    `https://localhost:44300/Product/Convertible%20Car`
5. Ardından, aşağıdaki yönlendirilmeyen URL 'YI (bağlantı noktası numaranızı kullanarak) tarayıcıya girin:  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 Kod yine de bir sorgu dizesi içeren bir URL 'YI tanırken, kullanıcının bir bağlantısı yer işareti olduğu durumdur.

## <a name="summary"></a>Özet

Bu öğreticide Kategoriler ve ürünler için yollar eklediniz. Yolların model bağlama kullanan veri denetimleriyle nasıl tümleştirileceğini öğrendiniz. Sonraki öğreticide genel hata işleme uygulayacaksınız.

## <a name="additional-resources"></a>Ek Kaynaklar

[ASP.NET kolay URL 'Ler](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[Üyelik, OAuth ve SQL veritabanı ile güvenli bir ASP.NET Web Forms uygulamasını dağıtın Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure Ücretsiz deneme](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [Önceki](membership-and-administration.md)
> [İleri](aspnet-error-handling.md)
