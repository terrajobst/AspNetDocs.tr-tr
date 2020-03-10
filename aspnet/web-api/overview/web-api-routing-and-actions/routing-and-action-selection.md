---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API 'de yönlendirme ve eylem seçimi | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554889"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a>ASP.NET Web API 'sinde yönlendirme ve eylem seçimi

, [Mike te son](https://github.com/MikeWasson)

Bu makalede, ASP.NET Web API 'sinin bir denetleyicideki belirli bir eyleme HTTP isteğini nasıl yönlendirdiğini açıklanmaktadır.

> [!NOTE]
> Yönlendirmeye yönelik üst düzey bir genel bakış için bkz. [ASP.NET Web API 'de yönlendirme](routing-in-aspnet-web-api.md).

Bu makale, yönlendirme sürecinin ayrıntılarına bakar. Bir Web API projesi oluşturur ve bazı isteklerin istediğiniz şekilde yönlendirilmeyeceğini görürseniz, bu makalede yardımcı olacak.

Yönlendirme üç ana aşamaya sahiptir:

1. URI ile bir yol şablonuna eşleme.
2. Denetleyici seçiliyor.
3. Bir eylem seçme.

İşlemin bazı parçalarını kendi özel davranışlarınız ile değiştirebilirsiniz. Bu makalede, varsayılan davranışı açıklıyorum. Sonda, davranışı özelleştirebileceğiniz yerleri de göz önünde koydum.

## <a name="route-templates"></a>Rota şablonları

Bir yol şablonu bir URI yoluna benzer, ancak küme ayraçları ile gösterilen yer tutucu değerlerine sahip olabilir:

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

Bir yol oluşturduğunuzda, yer tutucuların bazıları veya tümü için varsayılan değer sağlayabilirsiniz:

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

Ayrıca, bir URI segmentinin bir yer tutucu ile nasıl eşleşeceğini kısıtlayan kısıtlamalar da sağlayabilirsiniz:

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

Çerçeve, URI yolundaki kesimleri şablonla eşleştirmeye çalışır. Şablondaki değişmez değerler tam olarak eşleşmelidir. Bir yer tutucu, kısıtlama belirtmediğiniz müddetçe herhangi bir değerle eşleşir. Çerçeve, URI 'nin ana bilgisayar adı veya sorgu parametreleri gibi diğer bölümleriyle eşleşmez. Framework, yol tablosundaki URI ile eşleşen ilk yolu seçer.

İki özel yer tutucu vardır: "{Controller}" ve "{Action}".

- "{Controller}" denetleyicinin adını sağlar.
- "{Action}", eylemin adını sağlar. Web API 'de, her zamanki kural "{Action}" öğesini atlayamaz.

### <a name="defaults"></a>Varsayılanları

Varsayılan değer sağlarsanız, yol, bu kesimleri eksik olan bir URI ile eşleştirecektir. Örneğin:

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

URI 'Ler `http://localhost/api/products/all` ve `http://localhost/api/products` önceki rotayla eşleşir. İkinci URI 'de, eksik `{category}` kesimine `all`varsayılan değer atanır.

### <a name="route-dictionary"></a>Yol sözlüğü

Çerçeve bir URI için eşleşme bulursa, her yer tutucunun değerini içeren bir sözlük oluşturur. Anahtarlar, küme ayraçları dahil değil yer tutucu adlarıdır. Değerler URI yolundan veya varsayılandan alınır. Sözlük **ıhttproutedata** nesnesinde depolanır.

Bu rota eşleştirme aşamasında, özel "{Controller}" ve "{Action}" yer tutucuları, diğer yer tutucuları gibi değerlendirilir. Yalnızca diğer değerlerle sözlükte depolanırlar.

Varsayılan, RouteParameter özel değerine sahip olabilir **. Isteğe bağlı**. Bir yer tutucu bu değere atanmışsa, değer yol sözlüğüne eklenmez. Örneğin:

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

"API/Products" URI yolu için yol sözlüğü şunları içerir:

- Denetleyici: "Ürünler"
- Kategori: "tümü"

Bununla birlikte, "API/Products/Toys/123" için yol sözlüğü şunları içerir:

- Denetleyici: "Ürünler"
- Kategori: "Toys"
- Kimlik: "123"

Varsayılanlar, yol şablonunda hiçbir yerde görünmeyen bir değer içerebilir. Yol eşleşiyorsa, bu değer sözlükte depolanır. Örneğin:

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

URI yolu "api/root/8" ise, sözlük iki değer içerir:

- Denetleyici: "müşteriler"
- Kimlik: "8"

## <a name="selecting-a-controller"></a>Denetleyici seçme

Denetleyici seçimi **IHttpControllerSelector. SelectController** yöntemi tarafından işlenir. Bu yöntem bir **HttpRequestMessage** örneği alır ve bir **httpcontrollerdescriptor**döndürür. Varsayılan uygulama **DefaultHttpControllerSelector** sınıfı tarafından sağlanır. Bu sınıf, basit bir algoritma kullanır:

1. "Denetleyici" anahtarı için yol sözlüğüne bakın.
2. Bu anahtar için değeri alın ve denetleyicinin tür adını almak için "Controller" dizesini ekleyin.
3. Bu tür adıyla bir Web API denetleyicisi arayın.

Örneğin, yol sözlüğü anahtar-değer çifti "denetleyici" = "Ürünler" içeriyorsa, denetleyici türü "ProductsController" olur. Eşleşen bir tür veya birden fazla eşleşme yoksa, çerçeve istemciye bir hata döndürür.

3\. adım için, **DefaultHttpControllerSelector** Web API denetleyici türlerinin listesini almak Için **ıhttpcontrollertyperesolver** arabirimini kullanır. **Ihttpcontrollertyperesolver** 'in varsayılan uygulaması, (a) **ıhttpcontroller**uygulayan tüm genel sınıfları döndürür, (b) soyut değildir ve (c) "Controller" ile biten bir ada sahiptir.

## <a name="action-selection"></a>Eylem seçimi

Denetleyiciyi seçtikten sonra Framework, **ıhttpactionselector. SelectAction** yöntemini çağırarak eylemi seçer. Bu yöntem bir **HttpControllerContext** alır ve bir **HttpActionDescriptor**döndürür.

Varsayılan uygulama **ApiControllerActionSelector** sınıfı tarafından sağlanır. Bir eylem seçmek için, aşağıdakilere bakar:

- İsteğin HTTP yöntemi.
- Varsa, yol şablonunda "{Action}" yer tutucusu.
- Denetleyicideki eylemlerin parametreleri.

Seçim algoritmasına bakmadan önce, denetleyici eylemleriyle ilgili bazı şeyleri anladık.

**Denetleyicideki hangi Yöntemler "eylemler" olarak değerlendirilir?** Bir eylem seçerken, çerçeve yalnızca denetleyicideki ortak örnek yöntemlerine bakar. Ayrıca, ["özel ad"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) yöntemlerini (oluşturucular, olaylar, operatör aşırı yüklemeleri vs.) ve **Apicontroller** sınıfından devralınan yöntemleri dışlar.

**HTTP yöntemleri.** Framework yalnızca isteğin HTTP yöntemiyle eşleşen eylemleri seçer, şöyle belirlenir:

1. HTTP yöntemini bir özniteliğiyle belirtebilirsiniz: **Acceptverbs**, **httpdelete**, **HttpGet**, **httphead**, **HttpOptions**, **httppatch**, **HttpPost**veya **httpput**.
2. Aksi halde, denetleyici yönteminin adı "Get", "Post", "put", "Delete", "Head", "Options" veya "Patch" ile başlıyorsa ve bu HTTP yöntemini desteklediği kurala göre yapılır.
3. Yukarıdakilerden hiçbiri, yöntemi GÖNDERIYI destekler.

**Parametre bağlamaları.** Bir parametre bağlama, Web API 'sinin bir parametre için bir değer oluşturmasıdır. Parametre bağlama için varsayılan kural aşağıda verilmiştir:

- Basit türler URI 'den alınır.
- Karmaşık türler, istek gövdesinden alınır.

Basit türler [.NET Framework ilkel türler](https://msdn.microsoft.com/library/system.type.isprimitive), ayrıca **DateTime**, **Decimal**, Guid, **dize**ve **TimeSpan** **değerleri**içerir. Her eylem için, en fazla bir parametre istek gövdesini okuyabilir.

> [!NOTE]
> Varsayılan bağlama kurallarını geçersiz kılmak mümkündür. Bkz. bir [çocuk altındaki WebAPI parametre bağlama](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).

Bu arka plan ile eylem seçim algoritması aşağıda verilmiştir.

1. Denetleyicide HTTP istek yöntemiyle eşleşen tüm eylemlerin bir listesini oluşturun.
2. Yol sözlüğünde bir "Action" girişi varsa, adı bu değerle eşleşmeyen eylemleri kaldırın.
3. Aşağıdaki gibi eylem parametrelerini URI ile eşleştirmeye çalışın: 

    1. Her eylem için, bağlamanın URI 'den parametreyi aldığı basit türde parametrelerin bir listesini alın. İsteğe bağlı parametreleri dışlayın.
    2. Bu listeden, yol sözlüğünde veya URI sorgu dizesinde her bir parametre adı için bir eşleşme bulmayı deneyin. Eşleşmeler büyük/küçük harfe duyarlıdır ve parametre sırasına bağlı değildir.
    3. Listedeki her parametrenin URI 'de eşleşen bir eylem seçin.
    4. Bu ölçütlere uyan birden fazla eylem varsa, en fazla parametre eşleştirmelerle birini seçin.
4. **[Nonactıon]** özniteliğiyle eylemleri yoksayın.

Adım #3, büyük olasılıkla en karmaşıktır. Temel düşünce, bir parametrenin değerini URI 'den, istek gövdesinden veya özel bir bağlamadan alabilir. URI 'den gelen parametreler için, URI 'nin gerçekten bu parametre için bir değer (yol sözlüğü aracılığıyla) ya da sorgu dizesinde bir değer içerdiğinden emin olmak istiyoruz.

Örneğin, aşağıdaki eylemi göz önünde bulundurun:

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

*ID* parametresi URI 'ye bağlanır. Bu nedenle, bu eylem yalnızca yol sözlüğünde veya sorgu dizesinde "ID" değeri içeren bir URI ile eşleşemez.

İsteğe bağlı parametreler, isteğe bağlı oldukları için bir özel durumdur. İsteğe bağlı bir parametre için bağlama URI 'den değeri alamazsanız Tamam olur.

Karmaşık türler, farklı bir nedenden dolayı özel durumdur. Karmaşık bir tür yalnızca özel bir bağlama aracılığıyla URI 'ye bağlanabilir. Ancak bu durumda, parametrenin belirli bir URI 'ye bağlanıp bağlanamayacağını önceden bilemezsiniz. Bunu öğrenmek için bağlamayı çağırması gerekir. Seçim algoritmasının hedefi, herhangi bir bağlama çağırmadan önce statik açıklamadan bir eylem seçmektir. Bu nedenle, karmaşık türler eşleşen algoritmadan dışlanır.

Eylem seçildikten sonra tüm parametre bağlamaları çağrılır.

Özet:

- Eylemin, isteğin HTTP yöntemiyle eşleşmesi gerekir.
- Varsa, yol sözlüğünde eylem adı "Action" girdisiyle eşleşmelidir.
- İşlemin her parametresi için parametre URI 'den alınsaydı, parametre adının yol sözlüğünde ya da URI sorgu dizesinde bulunması gerekir. (Karmaşık türler içeren isteğe bağlı parametreler ve parametreler dışarıda bırakılır.)
- En fazla parametre sayısını eşleştirmeye çalışın. En iyi eşleşme parametresi olmayan bir yöntem olabilir.

## <a name="extended-example"></a>Genişletilmiş örnek

Yolların

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

Denetleyici:

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

HTTP isteği:

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a>Rota eşleştirme

URI, "DefaultApi" adlı yol ile eşleşiyor. Yol sözlüğü aşağıdaki girişleri içerir:

- Denetleyici: "Ürünler"
- Kimlik: "1"

Yol sözlüğü sorgu dizesi parametreleri, "sürüm" ve "Ayrıntılar" içeremez, ancak bunlar eylem seçimi sırasında göz önünde bulundurulacaktır.

### <a name="controller-selection"></a>Denetleyici seçimi

Yol sözlüğündeki "denetleyici" girdisinden, denetleyici türü `ProductsController`.

### <a name="action-selection"></a>Eylem seçimi

HTTP isteği bir GET isteği. GET 'i destekleyen denetleyici eylemleri `GetAll`, `GetById`ve `FindProductsByName`. Yol sözlüğü "eylem" için bir giriş içermiyor, bu nedenle eylem adıyla eşleşmesi gerekmez.

Ardından, eylemler için parametre adlarını eşleştirmeye çalışırız ve yalnızca GET eylemlerine bakmaya çalışıyoruz.

| Eylem | Eşleştirilecek parametreler |
| --- | --- |
| `GetAll` | yok |
| `GetById` | numarasını |
| `FindProductsByName` | ada |

İsteğe bağlı bir parametre olduğu için `GetById` *Sürüm* parametresinin değerlendirilmediğine dikkat edin.

`GetAll` yöntemi, önemli ölçüde eşleşir. Yol sözlüğü "ID" içerdiğinden `GetById` yöntemi de eşleşir. `FindProductsByName` yöntemi eşleşmiyor.

`GetById` yöntemi, bir parametresiyle eşleştiğinden, `GetAll`için hiçbir parametre olmadığından WINS. Yöntemi aşağıdaki parametre değerleriyle çağrılır:

- *kimlik* = 1
- *Sürüm* = 1,5

*Sürüm* seçim algoritmasında kullanılmasa da, PARAMETRENIN değeri URI sorgu dizesinden geliyor olduğuna dikkat edin.

## <a name="extension-points"></a>Uzantı noktaları

Web API 'SI, yönlendirme sürecinin bazı bölümleri için uzantı noktaları sağlar.

| Arabirim | Açıklama |
| --- | --- |
| **IHttpControllerSelector** | Denetleyiciyi seçer. |
| **Ihttpcontrollertyperesolver** | Denetleyici türleri listesini alır. **DefaultHttpControllerSelector** bu listeden denetleyici türünü seçer. |
| **Ibirleştiricliesresolver** | Proje derlemelerinin listesini alır. **Ihttpcontrollertyperesolver** arabirimi, denetleyici türlerini bulmak için bu listeyi kullanır. |
| **Ihttpcontrolleretkinleştirici** | Yeni denetleyici örnekleri oluşturur. |
| **Ihttpactionselector** | Eylemi seçer. |
| **Ihttpactionınvoker** | Eylemi çağırır. |

Bu arabirimlerin herhangi birine yönelik uygulamanızı sağlamak için **HttpConfiguration** nesnesindeki **Hizmetler** koleksiyonunu kullanın:

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
