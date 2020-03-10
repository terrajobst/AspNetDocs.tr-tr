---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: ASP.NET Web API 2 (C#) Ile çalışmaya başlama-ASP.NET 4. x
author: MikeWasson
description: Kod ile öğretici. Ürünlerin bir listesini döndüren bir Web API 'SI oluşturmak için ASP.NET Web API 'sini kullanın.
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556800"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a>ASP.NET Web API 2 (C#) Ile çalışmaya başlama

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

Bu öğreticide, ürünlerin listesini döndüren bir Web API 'SI oluşturmak için ASP.NET Web API kullanacaksınız.

HTTP yalnızca Web sayfalarına hizmet vermek için değildir. HTTP Ayrıca hizmet ve verileri kullanıma sunan API 'Leri oluşturmaya yönelik güçlü bir platformdur. HTTP basit, esnek ve ubititous. Düşünebildiğiniz neredeyse her platformda bir HTTP kitaplığı vardır. bu nedenle, HTTP Hizmetleri tarayıcılar, mobil cihazlar ve geleneksel masaüstü uygulamaları gibi çok sayıda istemciye ulaşabilir.

ASP.NET Web API 'SI, .NET Framework en üstünde Web API 'Leri oluşturmaya yönelik bir çerçevedir. 

## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri

- [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- Web API 2

Bu öğreticinin daha yeni bir sürümü için [ASP.NET Core ve Windows Için Visual Studio ile Web API 'Si oluşturma](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) makalesine bakın.

## <a name="create-a-web-api-project"></a>Web API projesi oluşturma

Bu öğreticide, ürünlerin listesini döndüren bir Web API 'SI oluşturmak için ASP.NET Web API kullanacaksınız. Ön uç Web sayfası, sonuçları göstermek için jQuery kullanır.

![](tutorial-your-first-web-api/_static/image1.png)

Visual Studio 'Yu başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin. Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET Web uygulaması**' nı seçin. Projeyi "ProductsApp" olarak adlandırın ve **Tamam**' a tıklayın.

![](tutorial-your-first-web-api/_static/image2.png)

**Yeni ASP.NET projesi** Iletişim kutusunda **boş** şablonu seçin. &quot;için klasör ve temel başvurular eklemek &quot;altında, **Web API 'sini**kontrol edin. **Tamam**’a tıklayın.

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> Ayrıca, &quot;Web API&quot; şablonunu kullanarak bir Web API projesi oluşturabilirsiniz. Web API şablonu, API yardım sayfalarını sağlamak için ASP.NET MVC kullanır. Bu öğretici için boş şablon kullanıyorum çünkü Web API 'sini MVC olmadan göstermek istiyorum. Genel olarak, Web API 'sini kullanmak için ASP.NET MVC 'yi bilmeniz gerekmez.

## <a name="adding-a-model"></a>Model Ekleme

*Model* , uygulamanızdaki verileri temsil eden bir nesnedir. ASP.NET Web API 'SI, modelinizi JSON, XML veya başka bir biçime otomatik olarak seri hale getirilebilir ve ardından seri hale getirilmiş verileri HTTP yanıt iletisinin gövdesine yazabilir. Bir istemci serileştirme biçimini okuyabilirler, nesne seri durumdan çıkarabilirler. Çoğu istemci, XML veya JSON 'yi ayrıştırabilirler. Ayrıca, istemci, HTTP istek iletisinde Accept üst bilgisini ayarlayarak hangi biçimin istediğini belirtebilir.

Bir ürünü temsil eden basit bir model oluşturarak başlayalım.

Çözüm Gezgini zaten görünmüyorsa, **Görünüm** menüsüne tıklayın ve **Çözüm Gezgini**öğesini seçin. Çözüm Gezgini modeller klasörüne sağ tıklayın. Bağlam menüsünden **Ekle** ' yi ve ardından **sınıf**' ı seçin.

![](tutorial-your-first-web-api/_static/image4.png)

Sınıfı ürün&quot;&quot;adlandırın. Aşağıdaki özellikleri `Product` sınıfına ekleyin.

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a>Denetleyici Ekleme

Web API 'sinde, *DENETLEYICI* http isteklerini işleyen bir nesnedir. Ürünlerin bir listesini ya da ID tarafından belirtilen tek bir ürünü döndüren bir denetleyici ekleyeceğiz.

> [!NOTE]
> ASP.NET MVC kullandıysanız, denetleyicilerle zaten bilgi sahibisiniz. Web API denetleyicileri MVC denetleyicilerine benzerdir, ancak **Controller** sınıfı yerine **Apicontroller** sınıfını devralınır.

**Çözüm Gezgini**, denetleyiciler klasörüne sağ tıklayın. **Ekle** ' yi ve ardından **Denetleyici**' yi seçin.

![](tutorial-your-first-web-api/_static/image5.png)

**Yapı Iskelesi Ekle** Iletişim kutusunda **Web API denetleyicisi-boş**seçeneğini belirleyin. **Ekle**'yi tıklatın.

![](tutorial-your-first-web-api/_static/image6.png)

**Denetleyici Ekle** iletişim kutusunda, denetleyiciyi &quot;productscontroller&quot;olarak adlandırın. **Ekle**'yi tıklatın.

![](tutorial-your-first-web-api/_static/image7.png)

Yapı iskelesi, denetleyiciler klasöründe ProductsController.cs adlı bir dosya oluşturur.

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> Denetleyicilerinizi denetleyiciler adlı bir klasöre koymanız gerekmez. Klasör adı, kaynak dosyalarınızı düzenlemenin yalnızca uygun bir yoludur.

Bu dosya henüz açık değilse, açmak için dosyaya çift tıklayın. Bu dosyadaki kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

Bu örneği basit tutmak için, ürünler Controller sınıfının içindeki sabit bir dizide depolanır. Kuşkusuz, gerçek bir uygulamada bir veritabanını sorgulayıp başka bir dış veri kaynağı kullanacaksınız.

Denetleyici, ürünleri döndüren iki yöntemi tanımlar:

- `GetAllProducts` yöntemi, tüm ürün listesini **ıenumerable&lt;ürün&gt;** türü olarak döndürür.
- `GetProduct` yöntemi, KIMLIĞINE göre tek bir ürün arar.

İşte bu kadar! Çalışan bir Web API 'SI var. Denetleyicideki her yöntem bir veya daha fazla URI 'ye karşılık gelir:

| Controller yöntemi | URI |
| --- | --- |
| GetAllProducts | /api/Products |
| GetProduct | /api/Products/*ID* |

`GetProduct` yöntemi için URI 'deki *kimlik* bir yer tutucudur. Örneğin, KIMLIĞI 5 olan ürünü almak için URI `api/products/5`.

Web API 'sinin denetleyici yöntemlerine HTTP isteklerini nasıl yönlendirdiğini hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).

## <a name="calling-the-web-api-with-javascript-and-jquery"></a>JavaScript ve jQuery ile Web API 'sini çağırma

Bu bölümde, Web API 'sini çağırmak için AJAX kullanan bir HTML sayfası ekleyeceğiz. AJAX çağrılarını yapmak ve ayrıca sayfayı sonuçlarla güncelleştirmek için jQuery kullanacağız.

Çözüm Gezgini, projeye sağ tıklayın ve **Ekle**' yi ve ardından **Yeni öğe**' yi seçin.

![](tutorial-your-first-web-api/_static/image9.png)

**Yeni öğe Ekle** iletişim kutusunda, **görsel C#** altında **Web** düğümünü seçin ve ardından **HTML sayfası** öğesini seçin. Sayfayı index. html&quot;&quot;olarak adlandırın.

![](tutorial-your-first-web-api/_static/image10.png)

Bu dosyadaki her şeyi aşağıdakiler ile değiştirin:

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

JQuery almak için birkaç yolu vardır. Bu örnekte, [Microsoft Ajax CDN](../../../ajax/cdn/overview.md)'yi kullandım. Ayrıca, [http://jquery.com/](http://jquery.com/)adresinden indirebilirsiniz ve ASP.net "Web API" proje şablonu jQuery de içerir.

### <a name="getting-a-list-of-products"></a>Ürünlerin bir listesini alma

Ürünlerin bir listesini almak için &quot;/api/Products&quot;bir HTTP GET isteği gönderin.

JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) IşLEVI bir AJAX isteği gönderir. Yanıt için JSON nesneleri dizisi içerir. `done` işlevi, istek başarılı olursa çağrılan bir geri çağırma işlemini belirtir. Geri aramada, DOM 'ı ürün bilgileriyle güncelleştiririz.

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a>KIMLIĞE göre ürün alma

Bir ürünü KIMLIĞE göre almak için, &quot;/api/Products/*ıd*&quot;IÇIN BIR http get isteği gönderin; burada *kimlik* ürün kimliğidir.

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

AJAX isteğini göndermek için hala `getJSON` çağrısı yaptık, ancak bu kez KIMLIĞI istek URI 'sine yerleştirtik. Bu istekten gelen yanıt, tek bir ürünün JSON gösterimidir.

## <a name="running-the-application"></a>Uygulamayı Çalıştırma

Uygulamada hata ayıklamaya başlamak için F5'e basın. Web sayfası aşağıdaki gibi görünmelidir:

![](tutorial-your-first-web-api/_static/image11.png)

KIMLIĞE göre bir ürün almak için KIMLIĞI girin ve ara ' ya tıklayın:

![](tutorial-your-first-web-api/_static/image12.png)

Geçersiz bir KIMLIK girerseniz, sunucu bir HTTP hatası döndürür:

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a>HTTP Isteğini ve yanıtını görüntülemek için F12 kullanma

Bir HTTP hizmetiyle çalışırken, HTTP isteği ve istek iletilerini görmek çok faydalı olabilir. Bunu, Internet Explorer 9 ' da F12 geliştirici araçlarını kullanarak yapabilirsiniz. Internet Explorer 9 ' da, araçları açmak için **F12** tuşuna basın. Ağ sekmesine tıklayın ve **Yakalamayı Başlat**' **a** basın. Şimdi Web sayfasına geri dönün ve **F5** 'e basarak Web sayfasını yeniden yükleyin. Internet Explorer, tarayıcı ile Web sunucusu arasındaki HTTP trafiğini yakalar. Özet görünümü bir sayfanın tüm ağ trafiğini gösterir:

![](tutorial-your-first-web-api/_static/image14.png)

Göreli URI "API/Products/" girdisini bulun. Bu girişi seçin ve **ayrıntılı görünüme git ' e**tıklayın. Ayrıntı görünümünde, istek ve yanıt üst bilgilerini ve gövdeleri görüntülemek için sekmeler vardır. Örneğin, **istek üstbilgileri** sekmesine tıklarsanız, istemcinin Accept üst bilgisinde &quot;Application/JSON&quot; isteğinde bulunduğunu görebilirsiniz.

![](tutorial-your-first-web-api/_static/image15.png)

Yanıt gövdesi sekmesine tıklarsanız, ürün listesinin JSON olarak serileştirilme şeklini görebilirsiniz. Diğer Tarayıcıların benzer işlevleri vardır. Bir Web hata ayıklama proxy 'si olan diğer faydalı bir araç, [Fiddler](http://www.fiddler2.com/fiddler2/)'dir. Fiddler 'ı kullanarak HTTP trafiğinizi görüntüleyebilir ve ayrıca, istekteki HTTP üstbilgileri üzerinde tam denetim elde etmenizi sağlayan HTTP istekleri oluşturabilirsiniz.

## <a name="see-this-app-running-on-azure"></a>Bkz. Azure 'da çalışan bu uygulama

Canlı bir Web uygulaması olarak çalışan tamamlanmış siteyi görmek istiyor musunuz? Aşağıdaki düğmeye tıklayarak uygulamanın tüm sürümünü Azure hesabınıza dağıtabilirsiniz.

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

Bu çözümü Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir. Henüz bir hesabınız yoksa, aşağıdaki seçeneklere sahip olursunuz:

- [Ücretsiz bir Azure hesabı açarak](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler edinin ve hatta kullanıldıktan sonra bile hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.
- [MSDN abonesi avantajlarınızı etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.

## <a name="next-steps"></a>Sonraki Adımlar

- GÖNDERME, YERLEŞTIRME ve SILME eylemlerini ve veritabanına yazma işlemlerini destekleyen bir HTTP hizmetinin daha kapsamlı bir örneği için bkz. [Entity Framework 6 Ile Web API 2 kullanma](../data/using-web-api-with-entity-framework/part-1.md).
- HTTP hizmetinin üstünde akıcı ve hızlı yanıt veren Web uygulamaları oluşturma hakkında daha fazla bilgi için bkz. [ASP.net Single Page Application](../../../single-page-application/index.md).
- Azure App Service için bir Visual Studio Web projesi dağıtma hakkında daha fazla bilgi için, bkz. [Azure App Service Web uygulaması oluşturma](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).
