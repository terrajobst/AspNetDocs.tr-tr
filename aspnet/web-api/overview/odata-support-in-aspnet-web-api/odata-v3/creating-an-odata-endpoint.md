---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
title: Web API 2 ile OData v3 uç noktası oluşturma | Microsoft Docs
author: MikeWasson
description: Açık Veri Protokolü (OData) Web için bir veri erişim protokolüdür. OData, verileri yapılandırmak, verileri sorgulamak ve verileri işlemek için Tekdüzen bir yol sağlar...
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 262843d6-43a2-4f1c-82d9-0b90ae6df0cf
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/creating-an-odata-endpoint
msc.type: authoredcontent
ms.openlocfilehash: e68a454398f109dfd089be9c9a44d3fe662acc2f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600427"
---
# <a name="creating-an-odata-v3-endpoint-with-web-api-2"></a>Web API 2 ile OData v3 uç noktası oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> [Açık Veri Protokolü](http://www.odata.org/) (OData) Web için bir veri erişim protokolüdür. OData, verileri yapılandırmak, verileri sorgulamak ve veri kümesini CRUD işlemleri (oluşturma, okuma, güncelleştirme ve silme) aracılığıyla işlemek için Tekdüzen bir yol sağlar. OData hem AtomPub (XML) hem de JSON biçimlerini destekler. OData Ayrıca veriler hakkında meta verileri açığa çıkarmak için bir yol tanımlar. İstemciler, veri kümesine ilişkin tür bilgilerini ve ilişkilerini saptamak için meta verileri kullanabilir.
>
> ASP.NET Web API 'SI, bir veri kümesi için OData uç noktası oluşturmayı kolaylaştırır. Endpoint 'in hangi OData işlemlerini desteklediğini tam olarak denetleyebilirsiniz. OData dışı uç noktaları ile birlikte birden çok OData uç noktası barındırabilirsiniz. Veri modeliniz, arka uç iş mantığı ve veri katmanınız üzerinde tam denetim sahibi olursunuz.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - OData sürüm 3
> - Entity Framework 6
> - [Fiddler Web hata ayıklama proxy (Isteğe bağlı)](http://www.fiddler2.com)
>
> Web API OData desteği [ASP.NET and Web Tools 2012,2 güncelleştirmesine](https://go.microsoft.com/fwlink/?LinkId=282650)eklenmiştir. Ancak, bu öğretici Visual Studio 2013 eklenen yapı iskelesi kullanır.

Bu öğreticide, istemcilerin sorgulayabilirler basit bir OData uç noktası oluşturacaksınız. Uç nokta için de bir C# istemci oluşturacaksınız. Bu Öğreticiyi tamamladıktan sonra, bir sonraki öğretici kümesinde varlık ilişkileri, Eylemler ve $expand/$select dahil daha fazla işlevsellik ekleme gösterilmektedir.

- [Visual Studio projesi oluşturma](#create-project)
- [Varlık modeli ekleme](#add-model)
- [OData denetleyicisi ekleme](#add-controller)
- [EDM ve rota Ekle](#edm)
- [Veritabanını çekirdek olarak (Isteğe bağlı)](#seed-db)
- [OData uç noktasını keşfetme](#explore)
- [OData serileştirme biçimleri](#formats)

<a id="create-project"></a>
## <a name="create-the-visual-studio-project"></a>Visual Studio projesi oluşturma

Bu öğreticide, temel CRUD işlemlerini destekleyen bir OData uç noktası oluşturacaksınız. Uç nokta tek bir kaynak ve ürünlerin bir listesini ortaya çıkarır. Daha sonraki öğreticiler daha fazla özellik ekleyecek.

Visual Studio 'Yu başlatın ve başlangıç sayfasından **Yeni proje** ' yi seçin. Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve görsel C# düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. **ASP.NET Web uygulaması** şablonunu seçin.

![](creating-an-odata-endpoint/_static/image1.png)

**Yeni ASP.NET projesi** Iletişim kutusunda **boş** şablonu seçin. &quot;altında...&quot;klasör ve çekirdek başvuruları ekleyin, **Web API 'sini**kontrol edin. **Tamam**'a tıklayın.

![](creating-an-odata-endpoint/_static/image2.png)

<a id="add-model"></a>
## <a name="add-an-entity-model"></a>Varlık modeli ekleme

*Model* , uygulamanızdaki verileri temsil eden bir nesnedir. Bu öğreticide, bir ürünü temsil eden bir modele ihtiyacımız var. Model, OData varlık türüne karşılık gelir.

Çözüm Gezgini modeller klasörüne sağ tıklayın. Bağlam menüsünden **Ekle** ' yi ve ardından **sınıf**' ı seçin.

![](creating-an-odata-endpoint/_static/image3.png)

Yeni öğe **Ekle** iletişim kutusunda, &quot;ürün&quot;adını adlandırın.

![](creating-an-odata-endpoint/_static/image4.png)

> [!NOTE]
> Kurala göre model sınıfları modeller klasörüne yerleştirilir. Bu kuralı kendi projelerinizde izlemeniz gerekmez, ancak bu öğreticide bunu kullanacağız.

Product.cs dosyasında aşağıdaki sınıf tanımını ekleyin:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample1.cs)]

ID özelliği varlık anahtarı olacak. İstemciler, ürünleri KIMLIĞE göre sorgulayabilir. Bu alan, arka uç veritabanında da birincil anahtar olmalıdır.

Projeyi şimdi oluşturun. Bir sonraki adımda, ürün türünü bulmak için yansıma kullanan bazı Visual Studio yapı iskelesi kullanacağız.

<a id="add-controller"></a>
## <a name="add-an-odata-controller"></a>OData denetleyicisi ekleme

*Denetleyici* , http isteklerini işleyen bir sınıftır. OData hizmetinde her bir varlık kümesi için ayrı bir denetleyici tanımlarsınız. Bu öğreticide, tek bir denetleyici oluşturacağız.

Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın. **Ekle** ' yi ve ardından **Denetleyici**' yi seçin.

![](creating-an-odata-endpoint/_static/image5.png)

**İskele Ekle** iletişim kutusunda, Entity Framework&quot;kullanarak eylemleri olan &quot;Web API 2 OData denetleyicisi ' ni seçin.

![](creating-an-odata-endpoint/_static/image6.png)

**Denetleyici Ekle** iletişim kutusunda "ProductsController" adlı denetleyiciyi adlandırın. Zaman uyumsuz denetleyici eylemlerini kullan&quot; onay kutusunu &quot;seçin. **Model** açılan listesinde ürün sınıfını seçin.

![](creating-an-odata-endpoint/_static/image7.png)

**Yeni veri bağlamı...** düğmesine tıklayın. Veri bağlamı türü için varsayılan adı bırakın ve **Ekle**' ye tıklayın.

![](creating-an-odata-endpoint/_static/image8.png)

Denetleyiciyi eklemek için denetleyici Ekle iletişim kutusunda Ekle ' ye tıklayın.

![](creating-an-odata-endpoint/_static/image9.png)

Note:...&quot;türü alınırken bir hata olduğunu &quot;belirten bir hata iletisi alırsanız, ürün sınıfını ekledikten sonra Visual Studio projesini derlediğinizden emin olun. Scafkatlama, sınıfını bulmak için yansıma kullanır.

![](creating-an-odata-endpoint/_static/image10.png)

Scafkatlama, projeye iki kod dosyası ekler:

- Products.cs OData uç noktasını uygulayan Web API denetleyicisini tanımlar.
- ProductServiceContext.cs, Entity Framework kullanarak temel veritabanını sorgulamak için yöntemler sağlar.

![](creating-an-odata-endpoint/_static/image11.png)

<a id="edm"></a>
## <a name="add-the-edm-and-route"></a>EDM ve rota Ekle

Çözüm Gezgini ' de, uygulama\_Başlat klasörünü genişletin ve WebApiConfig.cs adlı dosyayı açın. Bu sınıf, Web API 'SI için yapılandırma kodunu içerir. Bu kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample2.cs)]

Bu kod iki şeyi yapar:

- OData uç noktası için bir Varlık Veri Modeli (EDM) oluşturur.
- Uç nokta için bir yol ekler.

EDM, verilerin soyut bir modelidir. EDM, meta veri belgesini oluşturmak ve hizmet için URI 'Leri tanımlamak için kullanılır. **ODataConventionModelBuilder** , EDM varsayılan adlandırma kuralları kümesini kullanarak bir EDM oluşturur. Bu yaklaşım için en az kod gereklidir. EDM üzerinde daha fazla denetim istiyorsanız, özellik, anahtar ve gezinti özelliklerini açıkça ekleyerek EDM oluşturmak için **ODataModelBuilder** sınıfını kullanabilirsiniz.

**EntitySet** YÖNTEMI, EDM öğesine bir varlık kümesi ekler:

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample3.cs)]

"Products" dizesi varlık kümesinin adını tanımlar. Denetleyicinin adı, varlık kümesinin adı ile aynı olmalıdır. Bu öğreticide, varlık kümesi "Ürünler" olarak adlandırılmıştır ve denetleyicinin adı `ProductsController`. "ProductSet" varlık kümesini adlandırdıysanız, denetleyiciyi `ProductSetController`olarak adlandırmış olursunuz. Bir uç noktanın birden çok varlık kümesine sahip olabileceğini unutmayın. Her varlık kümesi için **EntitySet&lt;t&gt;** çağırın ve ardından karşılık gelen bir denetleyici tanımlayın.

**MapODataRoute** yöntemi OData uç noktası için bir yol ekler.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample4.cs)]

İlk parametre yol için kolay bir addır. Hizmetinizin istemcileri bu adı görmez. İkinci parametre uç noktanın URI önekidir. Bu kod verildiğinde, Products varlık kümesi URI 'SI http://<em>hostname</em>/OData/Products. olur. Uygulamanız birden fazla OData uç noktasına sahip olabilir. Her uç nokta için, <strong>MapODataRoute</strong> çağırın ve benzersiz bir yol adı ve BENZERSIZ bir URI öneki sağlayın.

<a id="seed-db"></a>
## <a name="seed-the-database-optional"></a>Veritabanını çekirdek olarak (Isteğe bağlı)

Bu adımda, veritabanını bazı test verileriyle temel almak için Entity Framework kullanacaksınız. Bu adım isteğe bağlıdır, ancak OData uç noktanızı hemen test etmenizi sağlar.

**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-console[Main](creating-an-odata-endpoint/samples/sample5.cmd)]

Bu, geçişler adlı bir klasör ve Configuration.cs adlı bir kod dosyası ekler.

![](creating-an-odata-endpoint/_static/image12.png)

Bu dosyayı açın ve `Configuration.Seed` yöntemine aşağıdaki kodu ekleyin.

[!code-csharp[Main](creating-an-odata-endpoint/samples/sample6.cs)]

Paket Yöneticisi konsolu penceresinde aşağıdaki komutları girin:

[!code-console[Main](creating-an-odata-endpoint/samples/sample7.cmd)]

Bu komutlar veritabanını oluşturan kodu oluşturur ve ardından bu kodu yürütür.

<a id="explore"></a>
## <a name="exploring-the-odata-endpoint"></a>OData uç noktasını keşfetme

Bu bölümde, uç noktalara istek göndermek ve yanıt iletilerini incelemek için [Fiddler Web hata ayıklama proxy](http://www.fiddler2.com) 'sini kullanacağız. Bu, bir OData uç noktasının yeteneklerini anlamanıza yardımcı olur.

Visual Studio 'da hata ayıklamayı başlatmak için F5 tuşuna basın. Varsayılan olarak, Visual Studio tarayıcınızı `http://localhost:*port*`için açar, burada *bağlantı noktası* proje ayarlarında yapılandırılan bağlantı noktası numarasıdır.

Proje ayarlarındaki bağlantı noktası numarasını değiştirebilirsiniz. Çözüm Gezgini, projeye sağ tıklayın ve **Özellikler**' i seçin. Özellikler penceresinde **Web**' i seçin. **Proje URL 'si**altında bağlantı noktası numarasını girin.

### <a name="service-document"></a>Hizmet belgesi

*Hizmet belgesi* , OData uç noktası için varlık kümelerinin bir listesini içerir. Hizmet belgesini almak için, hizmetin kök URI 'sine bir GET isteği gönderin.

Fiddler 'ı kullanarak, **Oluşturucu** SEKMESINE aşağıdaki URI 'yi girin: `http://localhost:port/odata/`, *bağlantı* noktası numarası.

![](creating-an-odata-endpoint/_static/image13.png)

**Yürüt** düğmesine tıklayın. Fiddler uygulamanıza bir HTTP GET isteği gönderir. Yanıtı Web oturumları listesinde görmeniz gerekir. Her şey çalışıyorsa, durum kodu 200 olacaktır.

![](creating-an-odata-endpoint/_static/image14.png)

Inspector sekmesinde yanıt iletisinin ayrıntılarını görmek için Web oturumları listesinde yanıta çift tıklayın.

![](creating-an-odata-endpoint/_static/image15.png)

Ham HTTP yanıt iletisi aşağıdakine benzer görünmelidir:

[!code-console[Main](creating-an-odata-endpoint/samples/sample8.cmd)]

Varsayılan olarak, Web API 'SI, AtomPub biçimindeki hizmet belgesini döndürür. JSON istemek için, HTTP isteğine aşağıdaki üstbilgiyi ekleyin:

`Accept: application/json`

![](creating-an-odata-endpoint/_static/image16.png)

HTTP yanıtı şu anda bir JSON yükü içeriyor:

[!code-console[Main](creating-an-odata-endpoint/samples/sample9.cmd)]

### <a name="service-metadata-document"></a>Hizmet meta verileri belgesi

*Hizmet meta verileri belgesi* , kavramsal şema tanım DILI (csdl) adı VERILEN bir xml dili kullanılarak hizmetin veri modelini açıklar. Meta veri belgesi, hizmette verilerin yapısını gösterir ve istemci kodu oluşturmak için kullanılabilir.

Meta veri belgesini almak için `http://localhost:port/odata/$metadata`için bir GET isteği gönderin. Bu öğreticide gösterilen uç nokta için meta veriler aşağıda verilmiştir.

[!code-console[Main](creating-an-odata-endpoint/samples/sample10.cmd)]

### <a name="entity-set"></a>Varlık kümesi

Products varlık kümesini almak için `http://localhost:port/odata/Products`için bir GET isteği gönderin.

[!code-console[Main](creating-an-odata-endpoint/samples/sample11.cmd)]

### <a name="entity"></a>Varlık

Tek bir ürün almak için, `http://localhost:port/odata/Products(1)`için bir GET isteği gönderin, burada "1" ürün KIMLIĞIDIR.

[!code-console[Main](creating-an-odata-endpoint/samples/sample12.cmd)]

<a id="formats"></a>
## <a name="odata-serialization-formats"></a>OData serileştirme biçimleri

OData birkaç serileştirme biçimini destekler:

- Atom pub (XML)
- JSON "Light" (OData v3 'de kullanıma sunuldu)
- JSON "verbose" (OData v2)

Varsayılan olarak, Web API 'SI AtomPubJSON "Light" biçimini kullanır.

AtomPub biçimini almak için Accept üst bilgisini "Application/atom + xml" olarak ayarlayın. Örnek bir yanıt gövdesi aşağıda verilmiştir:

[!code-console[Main](creating-an-odata-endpoint/samples/sample13.cmd)]

Atom biçiminin belirgin bir dezavantajına bakabilirsiniz: Bu, JSON ışığının daha ayrıntılıdır. Ancak, AtomPub 'yi anlayan bir istemciniz varsa, istemci bu biçimi JSON üzerinden tercih edebilir.

Aynı varlığın JSON hafif sürümü aşağıda verilmiştir:

[!code-console[Main](creating-an-odata-endpoint/samples/sample14.cmd)]

JSON light biçimi, OData protokolünün 3. sürümünde sunulmuştur. Geriye dönük uyumluluk için, bir istemci eski "ayrıntılı" JSON biçimini talep edebilir. Ayrıntılı JSON istemek için Accept üst bilgisini `application/json;odata=verbose`olarak ayarlayın. Verbose sürümü aşağıda verilmiştir:

[!code-console[Main](creating-an-odata-endpoint/samples/sample15.cmd)]

Bu biçim yanıt gövdesinde daha fazla meta veri getirir. Bu, bir oturumun tamamına çok fazla yük eklenebilir. Ayrıca, nesneyi "d" adlı bir özellikte sarmalayarak bir yöneltme düzeyi ekler.

## <a name="next-steps"></a>Sonraki Adımlar

- [Varlık Ilişkileri ekleme](working-with-entity-relations.md)
- [OData eylemleri ekleme](odata-actions.md)
- [Bir .NET Istemcisinden OData hizmetini çağırma](calling-an-odata-service-from-a-net-client.md)
