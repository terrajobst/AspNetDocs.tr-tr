---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 ' de öznitelik yönlendirme | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554987"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de öznitelik yönlendirme

, [Mike te son](https://github.com/MikeWasson)

*Yönlendirme* , Web API 'sinin bir eyleme bir URI ile eşleşmesini sağlar. Web API 2 ' de *öznitelik yönlendirme*adı verilen yeni bir yönlendirme türü desteklenir. Adından da anlaşılacağı gibi, öznitelik yönlendirme yolları tanımlamak için öznitelikleri kullanır. Öznitelik yönlendirme, Web API 'nizin URI 'Leri üzerinde daha fazla denetim sağlar. Örneğin, kaynakların hiyerarşilerini tanımlayan URI 'Leri kolayca oluşturabilirsiniz.

Kural tabanlı yönlendirme olarak adlandırılan daha önceki yönlendirmenin stili hala tam olarak desteklenmektedir. Aslında, her iki tekniği de aynı projede birleştirebilirsiniz.

Bu konu, öznitelik yönlendirmeyi nasıl etkinleştireceğinizi ve öznitelik yönlendirme için çeşitli seçenekleri açıklar. Öznitelik yönlendirme kullanan bir uçtan uca öğretici için bkz. [Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma](create-a-rest-api-with-attribute-routing.md).

## <a name="prerequisites"></a>Önkoşullar

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise Edition

Alternatif olarak, gerekli paketleri yüklemek için NuGet Paket Yöneticisi 'Ni kullanın. Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde aşağıdaki komutu girin:

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a>Neden öznitelik yönlendirme?

Web API 'sinin ilk sürümü *kural tabanlı* yönlendirme kullanıldı. Bu yönlendirme türünde, temel olarak parametreli dizeler olan bir veya daha fazla yol şablonu tanımlarsınız. Çerçeve bir istek aldığında, URI ile yol şablonunda eşleşir. (Kural tabanlı yönlendirme hakkında daha fazla bilgi için bkz. [ASP.NET Web API 'de yönlendirme](routing-in-aspnet-web-api.md).

Kural tabanlı yönlendirmenin bir avantajı, şablonların tek bir yerde tanımlanması ve yönlendirme kurallarının tüm denetleyicilerde tutarlı bir şekilde uygulanması. Ne yazık ki, kural tabanlı yönlendirme, yeniden gerçekleştirilen API 'lerde ortak olan belirli URI desenlerini desteklemeyi zorlaştırır. Örneğin, kaynaklar genellikle alt kaynaklar içerir: müşterilerin siparişi vardır, filmlerde aktörler, kitap yazarları vardır ve bu şekilde devam eder. Bu ilişkileri yansıtan URI 'Ler oluşturmak doğal bir şekilde yapılır:

`/customers/1/orders`

Bu tür URI 'nin kural tabanlı yönlendirme kullanılarak oluşturulması zordur. Yapılabilse de, çok sayıda denetleyiciniz veya kaynak türü varsa sonuçlar düzgün ölçeklenmez.

Öznitelik yönlendirme ile bu URI için bir yol tanımlamak önemsiz bir yoldur. Yalnızca denetleyici eylemine bir öznitelik eklersiniz:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

Öznitelik yönlendirmenin kolay hale getiren diğer bazı desenler aşağıda verilmiştir.

**API sürümü oluşturma**

Bu örnekte, "/api/v1/Products" farklı bir denetleyiciye "/api/v2/Products" olarak yönlendirilir.

`/api/v1/products`
`/api/v2/products`

**Aşırı yüklenmiş URI kesimleri**

Bu örnekte, "1" bir sıra numarasıdır, ancak "bekliyor" bir koleksiyonla eşlenir.

`/orders/1`
`/orders/pending`

**Birden çok parametre türü**

Bu örnekte, "1" bir sıra numarasıdır, ancak "2013/06/16" bir tarihi belirtir.

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a>Öznitelik yönlendirmeyi etkinleştirme

Öznitelik yönlendirmeyi etkinleştirmek için yapılandırma sırasında **MapHttpAttributeRoutes** çağırın. Bu genişletme yöntemi **System. Web. http. HttpConfigurationExtensions** sınıfında tanımlanmıştır.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

Öznitelik yönlendirme, [kural tabanlı](routing-in-aspnet-web-api.md) yönlendirme ile birleştirilebilir. Kural tabanlı yolları tanımlamak için **Maphttproute** yöntemini çağırın.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

Web API 'sini yapılandırma hakkında daha fazla bilgi için bkz. [ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)' yi yapılandırma.

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a>Note: Web API 1 ' den geçiş

Web API 'si 2 ' den önce, Web API proje şablonları şunun gibi kod üretti:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

Öznitelik yönlendirme etkinse, bu kod bir özel durum oluşturur. Öznitelik yönlendirmeyi kullanmak için var olan bir Web API projesini yükseltirseniz, bu yapılandırma kodunu aşağıdaki şekilde güncelleştirdiğinizden emin olun:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> Daha fazla bilgi için bkz. [ASP.net Hosting Ile Web API 'Sini yapılandırma](../advanced/configuring-aspnet-web-api.md#webhost).

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a>Rota öznitelikleri ekleme

Bir öznitelik kullanılarak tanımlanmış bir yol örneği aşağıda verilmiştir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

&quot;müşteriler/{CustomerID}/Orders&quot; dize, yolun URI şablonudur. Web API 'SI, istek URI 'sini şablonla eşleştirmeye çalışır. Bu örnekte, "Customers" ve "Orders" değişmez kesimlerdir ve "{CustomerID}" bir değişken parametresidir. Aşağıdaki URI 'Ler Bu şablonla eşleşir:

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

Bu konunun ilerleyen kısımlarında açıklanan [kısıtlamaları](#constraints)kullanarak eşleştirmeyi kısıtlayabilirsiniz.

Yol şablonundaki &quot;{CustomerID}&quot; parametresinin, yöntemindeki *CustomerID* parametresinin adıyla eşleştiğinden emin olun. Web API 'SI, denetleyici eylemini istediğinde, yol parametrelerini bağlamayı dener. Örneğin, URI `http://example.com/customers/1/orders`, Web API 'si "1" değerini eylemde *MüşteriNo* parametresine bağlamaya çalışır.

Bir URI şablonunda çeşitli parametreler bulunabilir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

Route özniteliği olmayan herhangi bir denetleyici yöntemi kural tabanlı yönlendirme kullanır. Bu şekilde, aynı projede her iki yönlendirme türünü de birleştirebilirsiniz.

## <a name="http-methods"></a>HTTP yöntemleri

Web API 'SI Ayrıca, isteğin HTTP yöntemine (GET, POST, vb.) göre eylemleri seçer. Varsayılan olarak, Web API 'SI denetleyici Yöntem adının başlangıcı ile büyük/küçük harf duyarsız bir eşleşme arar. Örneğin, `PutCustomers` adlı bir denetleyici yöntemi bir HTTP PUT isteğiyle eşleşir.

Aşağıdaki özniteliklerle yöntemi tanımlayarak bu kuralı geçersiz kılabilirsiniz:

- **[HttpDelete]**
- **HttpGet**
- **[HttpHead]**
- **[HttpOptions]**
- **[HttpPatch]**
- **HttpPost**
- **[HttpPut]**

Aşağıdaki örnekte CreateBook yöntemi HTTP POST istekleri ile eşlenir.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

Standart olmayan yöntemler dahil diğer tüm HTTP yöntemleri için, HTTP yöntemlerinin bir listesini alan **Acceptverbs** özniteliğini kullanın.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a>Rota önekleri

Genellikle, bir denetleyicideki yolların hepsi aynı ön ekiyle başlar. Örneğin:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

**[Routeprefix]** özniteliğini kullanarak tüm denetleyici için ortak bir ön ek ayarlayabilirsiniz:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

Yol önekini geçersiz kılmak için method özniteliğinde bir tilde (~) kullanın:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

Rota öneki parametreleri içerebilir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a>Yol kısıtlamaları

Yol kısıtlamaları, yol şablonundaki parametrelerin nasıl eşleştirilildiğini kısıtlamanıza olanak sağlar. Genel sözdizimi &quot;{Parameter: Constraint}&quot;. Örneğin:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

Burada, ilk yol yalnızca URI 'nin &quot;kimliği&quot; segmenti bir tamsayı ise seçilir. Aksi takdirde, ikinci yol seçilir.

Aşağıdaki tabloda desteklenen kısıtlamalar listelenmektedir.

| Kısıtlaması | Açıklama | Örnek |
| --- | --- | --- |
| Alfa | Büyük veya küçük harfli Latin alfabesi karakterleriyle eşleşir (a-z, A-Z) | {x:harfler} |
| bool | Bir Boole değeriyle eşleşir. | {x:bool} |
| datetime | Bir **Tarih saat** değeriyle eşleşir. | {x:datetime} |
| decimal | Ondalık bir değerle eşleşir. | {x:decimal} |
| çift | 64 bitlik bir kayan nokta değeriyle eşleşir. | {x:double} |
| float | 32 bitlik bir kayan nokta değeriyle eşleşir. | {x:float} |
| guid | Bir GUID değeriyle eşleşir. | {x:Guid} |
| int | 32 bitlik bir tamsayı değeriyle eşleşir. | {x:int} |
| length | Belirtilen uzunlukta veya belirtilen uzunluk aralığında olan bir dizeyle eşleşir. | {x:length (6)} {x:length (1, 20)} |
| long | 64 bitlik bir tamsayı değeriyle eşleşir. | {x:Long} |
| max | En büyük değere sahip bir tamsayıyla eşleşir. | {x:max(10)} |
| 'in | En fazla uzunluğa sahip bir dizeyle eşleşir. | {x:maxlength(10)} |
| min | En küçük değeri olan bir tamsayıyla eşleşir. | {x:min (10)} |
| minLength | En az uzunluğa sahip bir dizeyle eşleşir. | {x:minLength (10)} |
| aralık | Bir değer aralığı içindeki bir tamsayıyla eşleşir. | {x:Range (10, 50)} |
| Regex | Bir normal ifadeyle eşleşir. | {x:Regex (^ \d{3}-\d{3}-\d{4}$)} |

&quot;en az&quot;gibi bazı kısıtlamaların bağımsız değişkenleri parantez içine alır. Bir parametreye, iki nokta üst üste ile ayırarak birden çok kısıtlama uygulayabilirsiniz.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a>Özel yol kısıtlamaları

**Ihttprouteconstraint** arabirimini uygulayarak özel yol kısıtlamaları oluşturabilirsiniz. Örneğin, aşağıdaki kısıtlama bir parametreyi sıfır olmayan bir tamsayı değerine kısıtlar.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

Aşağıdaki kod kısıtlamanın nasıl kaydedileceği gösterilmektedir:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

Artık bu kısıtlamayı rotalarınızın içinde uygulayabilirsiniz:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

Ayrıca, **IInlineConstraintResolver** arabirimini uygulayarak **DefaultInlineConstraintResolver** sınıfının tamamını de değiştirebilirsiniz. Bunun yapılması, **IInlineConstraintResolver** uygulamanız özel olarak eklemedikçe yerleşik kısıtlamaların tümünün yerini alır.

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a>İsteğe bağlı URI parametreleri ve varsayılan değerler

Route parametresine bir soru işareti ekleyerek bir URI parametresini isteğe bağlı hale getirebilirsiniz. Bir rota parametresi isteğe bağlıdır, yöntem parametresi için varsayılan bir değer tanımlamanız gerekir.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

Bu örnekte, `/api/books/locale/1033` ve `/api/books/locale` aynı kaynağı döndürür.

Alternatif olarak, yol şablonu içinde aşağıdaki gibi bir varsayılan değer belirtebilirsiniz:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

Bu, önceki örnekle aynı şekilde neredeyse aynıdır, ancak varsayılan değer uygulandığında bir davranışın küçük bir farkı vardır.

- İlk örnekte ("{LCID: int?}"), varsayılan 1033 değeri doğrudan yöntem parametresine atanır, bu nedenle parametre bu tam değere sahip olur.
- İkinci örnekte ("{LCID: int = 1033}"), varsayılan "1033" değeri model bağlama işleminden geçer. Varsayılan model-cilt, "1033" değerini 1033 sayısal değerine dönüştürür. Ancak, özel bir model Bağlayıcısı takabilirsiniz, bu da farklı bir şey olabilir.

(Çoğu durumda, işlem hattınızda özel model ciltleri yoksa, iki form da eşdeğer olacaktır.)

<a id="route-names"></a>
## <a name="route-names"></a>Yol adları

Web API 'sinde, her yolun bir adı vardır. Yol adları bağlantı oluşturmak için faydalıdır, böylece bir HTTP yanıtında bir bağlantı ekleyebilirsiniz.

Yol adını belirtmek için, özniteliğinde **ad** özelliğini ayarlayın. Aşağıdaki örnek, yol adının nasıl ayarlanacağını ve ayrıca bir bağlantı oluştururken yol adının nasıl kullanılacağını gösterir.

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a>Rota sırası

Framework bir yol ile bir URI ile eşleştirmeye çalıştığında, yolları belirli bir sırada değerlendirir. Sırayı belirtmek için Route özniteliğinde **Order** özelliğini ayarlayın. Daha düşük değerler önce değerlendirilir. Varsayılan sıra değeri sıfırdır.

Toplam sıralama şöyle belirlenir:

1. Route özniteliğinin **Order** özelliğini karşılaştırın.
2. Yol şablonundaki her bir URI segmentine bakın. Her segment için aşağıdaki şekilde sıralayın:

    1. Değişmez değer kesimleri.
    2. Parametreleri kısıtlamalarla yönlendirin.
    3. Parametreleri kısıtlama olmadan yönlendirin.
    4. Kısıtlamalarla joker karakter parametresi kesimleri.
    5. Kısıtlama olmadan joker karakter parametresi kesimleri.
3. Bir bağ söz konusu olduğunda, rotalar yol şablonunun büyük/küçük harf duyarsız sıra dizesi karşılaştırması ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) tarafından sıralanır.

Aşağıda bir örnek vardır. Aşağıdaki denetleyiciyi tanımladığınızı varsayalım:

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

Bu yollar aşağıdaki gibi sıralanır.

1. Siparişler/Ayrıntılar
2. Siparişler/{id}
3. Siparişler/{customerName}
4. Siparişler/{\*Date}
5. Siparişler/bekliyor

"Details" değerinin değişmez bir kesim olduğunu ve "{id}" öncesinde göründüğünü, ancak Order özelliği 1 olduğu **için** "bekliyor" ifadesi son göründüğünü unutmayın. (Bu örnek, "details" veya "Pending" adlı bir müşteri olmadığını varsayar. Genel olarak, belirsiz yollardan kaçınmaya çalışın. Bu örnekte, `GetByCustomer` için daha iyi bir yol şablonu "Customers/{customerName}")
