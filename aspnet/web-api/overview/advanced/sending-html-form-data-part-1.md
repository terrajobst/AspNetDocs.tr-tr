---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: "ASP.NET Web API 'sinde HTML form verileri gönderme: form-urlencoded Data-ASP.NET 4. x"
author: MikeWasson
description: Bu makalede, form-urlencoded verilerinin ASP.NET 4. x ile bir Web API denetleyicisine nasıl nakledileceği gösterilmektedir
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557605"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a>ASP.NET Web API 'sinde HTML form verileri gönderme: form-urlencoded Data

, [Mike te son](https://github.com/MikeWasson)

## <a name="part-1-form-urlencoded-data"></a>1\. kısım: form-urlencoded verileri

Bu makalede, form-urlencoded verilerinin bir Web API denetleyicisine nasıl nakledileceği gösterilmektedir.

- [HTML formlarına genel bakış](#overview_of_html_forms)
- [Karmaşık türler gönderiliyor](#sending_complex_types)
- [AJAX aracılığıyla form verileri gönderme](#sending_form_data_via_ajax)
- [Basit türler gönderiliyor](#sending_simple_types)

> [!NOTE]
> [Tamamlanmış projeyi indirin](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a>HTML formlarına genel bakış

HTML formları, verileri sunucuya göndermek için GET veya POST kullanır. **Form** öğesinin **Method** özniteliği http yöntemini verir:

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

Varsayılan yöntem Al ' dır. Form GET kullanıyorsa, form verileri URI 'de bir sorgu dizesi olarak kodlanır. Form POST kullanıyorsa, form verileri istek gövdesine yerleştirilir. Postalanan veriler için, **Enctype** özniteliği istek gövdesinin biçimini belirtir:

| Enctype | Açıklama |
| --- | --- |
| Application/x-www-form-urlencoded | Form verileri, bir URI sorgu dizesine benzer şekilde ad/değer çiftleri olarak kodlanır. Bu, POST için varsayılan biçimdir. |
| multipart/form-Data | Form verileri çok parçalı bir MIME iletisi olarak kodlanır. Sunucuya bir dosya yüklüyorsanız bu biçimi kullanın. |

Bu makalenin 1. bölümü, x-www-form-urlencoded biçimine bakar. [Bölüm 2](sending-html-form-data-part-2.md) çok parçalı MIME tanımlar.

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a>Karmaşık türler gönderiliyor

Genellikle, çeşitli form denetimlerinden alınan değerlerden oluşan karmaşık bir tür gönderilir. Bir durum güncelleştirmesini temsil eden aşağıdaki modeli göz önünde bulundurun:

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

GÖNDERI aracılığıyla `Update` nesnesini kabul eden bir Web API denetleyicisi aşağıda verilmiştir.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> Bu denetleyici [eylem tabanlı yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name)kullanır, bu nedenle yol şablonu &quot;API/{Controller}/{Action}/{id}&quot;. İstemci, verileri/api/Updates/Complex&quot;&quot;nakleder.

Şimdi, kullanıcıların bir durum güncelleştirmesi göndermesi için bir HTML formu yazalım.

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

Form üzerindeki **Action** özniteliğinin Controller eylemizin URI 'si olduğunu unutmayın. Aşağıda, bazı değerlerin girildiği form verilmiştir:

![](sending-html-form-data-part-1/_static/image1.png)

Kullanıcı Gönder ' e tıkladığında tarayıcı aşağıdakine benzer bir HTTP isteği gönderir:

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

İstek gövdesinin, ad/değer çiftleri olarak biçimlendirilen form verilerini içerdiğine dikkat edin. Web API 'SI, ad/değer çiftlerini otomatik olarak `Update` sınıfının bir örneğine dönüştürür.

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a>AJAX aracılığıyla form verileri gönderme

Kullanıcı bir form gönderdiğinde, tarayıcı geçerli sayfadan uzağa gider ve yanıt iletisinin gövdesini işler. Yanıt bir HTML sayfası olduğunda bu tamam. Ancak, bir Web API 'SI ile yanıt gövdesi genellikle boştur veya JSON gibi yapılandırılmış verileri içerir. Bu durumda, bir AJAX isteği kullanarak form verilerinin gönderilmesi daha anlamlı hale gelir, böylece sayfa yanıtı işleyebilir.

Aşağıdaki kod, form verilerinin jQuery kullanılarak nasıl nakledileceğini gösterir.

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

JQuery **Gönder** işlevi form eyleminin yerine yeni bir işlev koyar. Bu, Gönder düğmesinin varsayılan davranışını geçersiz kılar. Serileştirme işlevi, form verilerini ad/değer çiftlerine seri **hale** getirir. Form verilerini sunucuya göndermek için `$.post()`çağırın.

İstek tamamlandığında, `.success()` veya `.error()` işleyicisi kullanıcıya uygun bir ileti gösterir.

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a>Basit türler gönderiliyor

Önceki bölümlerde, bir model sınıfının örneğine bir Web API 'SI seri durumdan çıkarılan karmaşık bir tür gönderdik. Ayrıca, bir dize gibi basit türler de gönderebilirsiniz.

> [!NOTE]
> Basit bir tür göndermeden önce, bunun yerine değeri karmaşık bir türde kaydırmayı düşünün. Bu, sunucu tarafında model doğrulamanın avantajlarından yararlanmanızı sağlar ve gerekirse modelinizi genişletmeyi kolaylaştırır.

Basit bir tür göndermek için temel adımlar aynıdır, ancak iki hafif farklılık vardır. İlk olarak, denetleyicide, parametre adını **Frombody** özniteliğiyle tasarlamanız gerekir.

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

Web API 'SI varsayılan olarak istek URI 'sinden basit türler almaya çalışır. **Frombody** özniteliği, Web API 'sinin istek gövdesinden değeri okumasını söyler.

> [!NOTE]
> Web API 'SI, yanıt gövdesini en çok bir kez okur. bu nedenle, bir eylemin yalnızca bir parametresi istek gövdesinden gelebilir. İstek gövdesinden birden çok değer almanız gerekiyorsa, karmaşık bir tür tanımlayın.

İkinci olarak, istemcinin değeri aşağıdaki biçimle gönderebilmesi gerekir:

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

Özel olarak, basit bir tür için ad/değer çiftinin ad kısmı boş olmalıdır. Tüm tarayıcılar bunu HTML formları için desteklemez, ancak bu biçimi komut dosyasında aşağıdaki gibi oluşturursunuz:

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

Örnek bir form aşağıda verilmiştir:

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

Form değerini göndermek için komut dosyası aşağıda verilmiştir. Önceki betikten tek fark, **Post** işlevine geçirilen bağımsız değişkendir.

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

Basit türden bir diziyi göndermek için aynı yaklaşımı kullanabilirsiniz:

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a>Ek Kaynaklar

[Bölüm 2: dosya yükleme ve çok parçalı MIME](sending-html-form-data-part-2.md)
