---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: ASP.NET Web API 1-ASP.NET 4. x içinde CRUD Işlemlerini etkinleştirme
author: MikeWasson
description: Öğreticide, ASP.NET 4. x için ASP.NET Web API 'sini kullanarak bir HTTP hizmetindeki CRUD işlemlerini destekleme işlemi gösterilmektedir.
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556205"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a>ASP.NET Web API 1 ' de CRUD Işlemlerini etkinleştirme

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> Bu öğreticide, ASP.NET 4. x için ASP.NET Web API 'sini kullanarak bir HTTP hizmetindeki CRUD işlemlerini destekleme işlemi gösterilmektedir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Visual Studio 2012
> - Web API 1 (Ayrıca Web API 2 ile birlikte çalışarak)

CRUD, dört temel veritabanı işlemi olan &quot;oluşturma, okuma, güncelleştirme ve&quot; silme işlemlerini temsil eder. Birçok HTTP hizmeti Ayrıca REST veya REST API 'Ler aracılığıyla CRUD işlemlerini modelleyebilir.

Bu öğreticide, ürünlerin listesini yönetmek için çok basit bir Web API 'SI oluşturacaksınız. Her ürün bir ad, Fiyat ve kategori (&quot;Toys&quot; veya &quot;donanım&quot;), ayrıca bir ürün KIMLIĞI içerir.

Ürünler API 'SI aşağıdaki yöntemleri ortaya çıkarır.

| Eylem | HTTP yöntemi | Göreli URI'si |
| --- | --- | --- |
| Tüm ürünlerin bir listesini alın | GET | /api/Products |
| KIMLIĞE göre ürün al | GET | /api/Products/*ID* |
| Kategoriye göre bir ürün al | GET | /api/Products? kategori =*Kategori* |
| Yeni ürün oluştur | POST | /api/Products |
| Bir ürünü güncelleştirme | PUT | /api/Products/*ID* |
| Bir ürünü silme | DELETE | /api/Products/*ID* |

URI 'lerden bazılarının, yoldaki ürün KIMLIĞINI içerdiğine dikkat edin. Örneğin, KIMLIĞI 28 olan ürünü almak için, istemci `http://hostname/api/products/28`için bir GET isteği gönderir.

### <a name="resources"></a>Kaynaklar

Products API 'SI iki kaynak türü için URI tanımlar:

| Kaynak | URI |
| --- | --- |
| Tüm ürünlerin listesi. | /api/Products |
| Tek bir ürün. | /api/Products/*ID* |

### <a name="methods"></a>Yöntemler

Dört ana HTTP yöntemi (GET, PUT, POST ve DELETE) şu şekilde CRUD işlemlerine eşlenebilir:

- GET, kaynağın belirtilen URI 'de temsilini alır. GET 'in sunucu üzerinde hiçbir yan etkisi olmamalıdır.
- Güncelleştirme bir kaynağı belirtilen bir URI 'ye YERLEŞTIRIN. Ayrıca, sunucu istemcilerin yeni URI 'Ler belirlemesine izin veriyorsa belirtilen bir URI 'de yeni bir kaynak oluşturmak için de kullanabilirsiniz. Bu öğretici için, API PUT aracılığıyla oluşturmayı desteklemez.
- GÖNDERI yeni bir kaynak oluşturur. Sunucu, yeni nesnenin URI 'sini atar ve bu URI 'yi yanıt iletisinin bir parçası olarak döndürür.
- DELETE, belirtilen URI 'de bir kaynağı siler.

Note: PUT yöntemi tüm ürün varlığının yerini alır. Diğer bir deyişle, istemcinin güncelleştirilmiş ürünün tüm gösterimini gönderebilmesi beklenir. Kısmi güncelleştirmeleri desteklemek istiyorsanız, düzeltme eki yöntemi tercih edilir. Bu öğretici, düzeltme eki uygulamaz.

## <a name="create-a-new-web-api-project"></a>Yeni bir Web API projesi oluştur

Visual Studio 'Yu çalıştırarak başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin. Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi &quot;ProductStore&quot; olarak adlandırın ve **Tamam**' a tıklayın.

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

**Yeni ASP.NET MVC 4 proje** Iletişim kutusunda **Web API 'si** ' ni seçin ve **Tamam**' ı tıklatın.

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a>Model Ekleme

*Model* , uygulamanızdaki verileri temsil eden bir nesnedir. ASP.NET Web API 'sinde, kesin türü belirtilmiş CLR nesnelerini modeller olarak kullanabilirsiniz ve istemci için otomatik olarak XML veya JSON olarak serileştirilir.

ProductStore API 'SI için verilerimiz ürünlerden oluşur. bu nedenle `Product`adlı yeni bir sınıf oluşturacağız.

Çözüm Gezgini zaten görünmüyorsa, **Görünüm** menüsüne tıklayın ve **Çözüm Gezgini**öğesini seçin. Çözüm Gezgini **modeller** klasörüne sağ tıklayın. Bağlam menüsünden **Ekle**' yi ve ardından **sınıf**' ı seçin. Sınıfı ürün&quot;&quot;adlandırın.

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

Aşağıdaki özellikleri `Product` sınıfına ekleyin.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a>Depo ekleme

Ürünlerin bir koleksiyonunu depoladık. Koleksiyonu hizmet uygulamamızda ayırmak iyi bir fikirdir. Bu şekilde, hizmet sınıfını yeniden yazmadan yedekleme deposunu değiştirebiliriz. Bu tür tasarıma *Depo* deseninin adı verilir. Depo için genel bir arabirim tanımlayarak başlayın.

Çözüm Gezgini **modeller** klasörüne sağ tıklayın. **Ekle**' yi ve ardından **Yeni öğe**' yi seçin.

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve C# düğümü genişletin. Altında C# **kod**' ı seçin. Kod şablonları listesinde **arabirim**' i seçin. &quot;ıproductrepository&quot;arabirimini adlandırın.

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

Aşağıdaki uygulamayı ekleyin:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

Şimdi, &quot;ProductRepository adlı modeller klasörüne başka bir sınıf ekleyin. Bu sınıf&quot;, `IProductRepository` arabirimini uygular. Aşağıdaki uygulamayı ekleyin:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

Depo, listeyi yerel bellekte tutar. Bu bir öğretici için Tamam, ancak gerçek bir uygulamada, verileri harici olarak veya bulut depolama alanında depoladığınızda. Depo deseninin daha sonra uygulanması daha kolay hale gelir.

## <a name="adding-a-web-api-controller"></a>Web API denetleyicisi ekleme

ASP.NET MVC ile çalıştıysanız, denetleyicilerle zaten bilgi sahibisiniz. ASP.NET Web API 'sinde, *Denetleyici* ISTEMCIDEN gelen http isteklerini işleyen bir sınıftır. Yeni proje Sihirbazı, projeyi oluştururken sizin için iki denetleyici oluşturdu. Bunları görmek için Çözüm Gezgini içindeki Denetleyiciler klasörünü genişletin.

- HomeController geleneksel bir ASP.NET MVC denetleyicisidir. Site için HTML sayfalarının sunulmasından sorumludur ve doğrudan Web API 'imizle ilgili değildir.
- ValuesController örnek bir WebAPI Controller.

Çözüm Gezgini ' de dosyaya sağ tıklayıp Sil ' i seçerek ValuesController 'ı silin **.** Şimdi yeni bir denetleyiciyi şu şekilde ekleyin:

**Çözüm Gezgini**, denetleyiciler klasörüne sağ tıklayın. **Ekle** ' yi ve ardından **Denetleyici**' yi seçin.

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

**Denetleyici ekleme** Sihirbazı ' nda, denetleyiciyi &quot;productscontroller&quot;olarak adlandırın. **Şablon** açılan LISTESINDE **boş API denetleyicisi**' ni seçin. Daha sonra **Ekle**'ye tıklayın.

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> Denetleyicilerinizi denetleyiciler adlı bir klasöre koymak gerekli değildir. Klasör adı önemli değildir; kaynak dosyalarınızı düzenlemek için kullanışlı bir yoldur.

**Denetleyici ekleme** Sihirbazı, denetleyiciler klasöründe ProductsController.cs adlı bir dosya oluşturur. Bu dosya henüz açık değilse, açmak için dosyaya çift tıklayın. Aşağıdaki **using** ifadesini ekleyin:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

**Iproductrepository** örneğini tutan bir alan ekleyin.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> Denetleyiciyi, denetleyicinin belirli bir `IProductRepository`uygulamasına bağladığından, denetleyicinin `new ProductRepository()` çağrılması en iyi tasarım değildir. Daha iyi bir yaklaşım için bkz. [Web API bağımlılığı çözümleyici 'Yi kullanma](../advanced/dependency-injection.md).

## <a name="getting-a-resource"></a>Kaynak alma

ProductStore API 'SI, birkaç &quot;okuma&quot; eylemini HTTP GET yöntemleri olarak kullanıma sunacaktır. Her eylem, `ProductsController` sınıfındaki bir yönteme karşılık gelir.

| Eylem | HTTP yöntemi | Göreli URI'si |
| --- | --- | --- |
| Tüm ürünlerin bir listesini alın | GET | /api/Products |
| KIMLIĞE göre ürün al | GET | /api/Products/*ID* |
| Kategoriye göre bir ürün al | GET | /api/Products? kategori =*Kategori* |

Tüm ürünlerin listesini almak için, bu yöntemi `ProductsController` sınıfına ekleyin:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

Yöntem adı &quot;Get&quot;ile başlar, bu sayede istekleri almak üzere eşlenir. Ayrıca, yönteminin parametresi olmadığından, yol içinde *&quot;kimliği&quot;* segment IÇERMEYEN bir URI ile eşlenir.

KIMLIĞE göre bir ürün almak için, bu yöntemi `ProductsController` sınıfına ekleyin:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

Bu yöntem adı ayrıca &quot;al&quot;başlar, ancak yönteminde *ID*adlı bir parametre bulunur. Bu parametre, URI yolunun &quot;ID&quot; kesimine eşlenir. ASP.NET Web API çerçevesi, KIMLIĞI parametresinin doğru veri türüne (**int**) otomatik olarak dönüştürür.

GetProduct metodu, *kimlik* geçerli değilse **httpresponseexception** türünde bir özel durum oluşturur. Bu özel durum Framework tarafından 404 (bulunamadı) hatası olarak çevrilecek.

Son olarak, kategoriye göre ürün bulmak için bir yöntem ekleyin:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

İstek URI 'sinin bir sorgu dizesi varsa, Web API 'SI, denetleyici yöntemindeki parametrelerle sorgu parametrelerini eşleştirmeye çalışır. Bu nedenle, "API/Products? Category =*category*" BIÇIMINDEKI bir URI bu yöntemle eşlenir.

## <a name="creating-a-resource"></a>Kaynak oluşturma

Sonra, yeni bir ürün oluşturmak için `ProductsController` sınıfına bir yöntem ekleyeceğiz. Yöntemin basit bir uygulamasıdır:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

Bu yöntemle ilgili iki şeyi göz önünde bulundurmanız gerekenler:

- Yöntem adı &quot;Post...&quot;ile başlar. Yeni bir ürün oluşturmak için istemci bir HTTP POST isteği gönderir.
- Yöntemi ürün türünde bir parametre alır. Web API 'sinde, karmaşık türlere sahip parametrelerin, istek gövdesinden serisi kaldırılır. Bu nedenle, istemcinin, XML veya JSON biçiminde bir ürün nesnesinin seri hale getirilmiş gösterimini göndermesini bekledik.

Bu uygulama çalışır, ancak tam olarak tamamlanmaz. İdeal olarak, HTTP yanıtının aşağıdakileri içermesini istiyoruz:

- **Yanıt kodu:** Varsayılan olarak, Web API çerçevesi yanıt durum kodunu 200 (Tamam) olarak ayarlar. Ancak, HTTP/1.1 protokolüne göre, bir POST isteği bir kaynak oluşturulmasına neden olduğunda, sunucu 201 (oluşturuldu) durumuyla yanıt vermesi gerekir.
- **Konum:** Sunucu bir kaynak oluşturduğunda, yanıtın konum üst bilgisinde yeni kaynağın URI 'sini içermesi gerekir.

ASP.NET Web API 'SI, HTTP yanıt iletisini işlemeyi kolaylaştırır. Geliştirilmiş uygulama aşağıda verilmiştir:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

Yöntemin dönüş türünün artık **HttpResponseMessage**olduğuna dikkat edin. Bir ürün yerine bir **HttpResponseMessage** döndürerek, durum kodu ve konum üstbilgisi dahil olmak üzere http yanıt iletisinin ayrıntılarını denetleyebiliriz.

**Createres,** yöntemi bir **HttpResponseMessage** oluşturur ve Product nesnesinin serileştirilmiş bir gösterimini yanıt iletisi olan gövdeye otomatik olarak yazar.

> [!NOTE]
> Bu örnek `Product`doğrulamaz. Model doğrulama hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de model doğrulaması](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).

## <a name="updating-a-resource"></a>Kaynak güncelleştiriliyor

Bir ürünü PUT ile güncelleştirmek basittir:

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

Yöntem adı &quot;put...&quot;ile başlar, bu nedenle Web API 'SI istekleri koymak için onunla eşleşir. Yöntemi iki parametre alır, ürün KIMLIĞI ve güncelleştirilmiş ürün. *ID* parametresi URI yolundan alınır ve *ürün* parametresi, istek gövdesinden seri durumdan çıkarılacak. Varsayılan olarak, ASP.NET Web API çerçevesi, istek gövdesinden yol ve karmaşık türlerden basit parametre türlerini alır.

## <a name="deleting-a-resource"></a>Kaynak silme

Bir kaynağı silmek için bir "Sil..." tanımlayın yöntemidir.

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

SILME isteği başarılı olursa, durumu açıklayan bir varlık gövdesiyle 200 (Tamam) durumunu döndürebilir; durum 202 (kabul edildi) silme hala bekliyor; veya varlık gövdesi olmayan bir durum 204 (Içerik yok). Bu durumda `DeleteProduct` yöntemi `void` bir dönüş türüne sahiptir, bu nedenle ASP.NET Web API bunu otomatik olarak 204 (Içerik yok) durum koduna dönüştürür.
