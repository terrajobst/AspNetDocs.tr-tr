---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: ASP.NET Web API-ASP.NET 4. x içinde model doğrulaması
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sinde model doğrulamasına genel bakış.
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557241"
---
# <a name="model-validation-in-aspnet-web-api"></a>ASP.NET Web API 'de model doğrulaması

, [Mike te son](https://github.com/MikeWasson)

Bu makalede, modellerinize not ekleme, veri doğrulama için ek açıklamaları kullanma ve Web API 'nizin doğrulama hatalarını işleme işlemlerinin nasıl yapılacağı gösterilir. Bir istemci Web API 'nize veri gönderdiğinde, genellikle herhangi bir işlem yapmadan önce verileri doğrulamak istersiniz. 

## <a name="data-annotations"></a>Veri Açıklamaları

ASP.NET Web API 'sinde, modelinizdeki özelliklerin doğrulama kurallarını ayarlamak için [System. ComponentModel. Dataaçıklamalarda](/dotnet/api/system.componentmodel.dataannotations) ad alanındaki öznitelikleri kullanabilirsiniz. Aşağıdaki modeli göz önünde bulundurun:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

ASP.NET MVC 'de model doğrulaması kullandıysanız, bu tanıdık gelmelidir. **Gerekli** öznitelik `Name` özelliğinin null olmaması gerektiğini belirtir. **Range** özniteliği `Weight` sıfır ile 999 arasında olması gerektiğini belirtir.

Bir istemcinin aşağıdaki JSON gösterimiyle bir POST isteği gönderdiğini varsayalım:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

İstemcinin gerekli olarak işaretlenen `Name` özelliğini içermediğini görebilirsiniz. Web API 'si, JSON 'ı bir `Product` örneğine dönüştürdüğünde, doğrulama özniteliklerine karşı `Product` doğrular. Denetleyici eyleinizde, modelin geçerli olup olmadığını kontrol edebilirsiniz:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

Model doğrulama, istemci verilerinin güvenli olduğunu garanti etmez. Uygulamanın diğer katmanlarında ek doğrulama gerekebilir. (Örneğin, veri katmanı yabancı anahtar kısıtlamalarını uygulayabilir.) [Web API 'sini Entity Framework kullanma](../data/using-web-api-with-entity-framework/part-1.md) öğreticisinde bu sorunlardan bazıları incelenmektedir.

**"In-Posting"** : altında, istemci bazı özellikleri bıraktığında gerçekleşir. Örneğin, istemcinin aşağıdakileri göndereceğini varsayalım:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

Burada istemci, `Price` veya `Weight`için değerler belirtmedi. JSON biçimlendiricisi eksik özelliklere sıfır varsayılan değeri atar.

![](model-validation-in-aspnet-web-api/_static/image1.png)

Sıfır değeri bu özellikler için geçerli bir değer olduğundan model durumu geçerli. Bunun bir sorun olup olmadığı, senaryonuza bağlıdır. Örneğin, bir güncelleştirme işleminde, "sıfır" ve "ayarlanmadı" arasında ayrım yapmak isteyebilirsiniz. İstemcileri bir değer ayarlamaya zorlamak için özelliği null yapılabilir yapın ve **gerekli** özniteliği ayarlayın:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"Aşırı gönderme"** : bir istemci, beklediğinizden *daha fazla* veri gönderebilir. Örneğin:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

Burada JSON, `Product` modelinde mevcut olmayan bir Özellik ("Color") içerir. Bu durumda, JSON biçimlendiricisi yalnızca bu değeri yoksayar. (XML biçimlendiricisi aynı şekilde yapılır.) Daha fazla bilgi için, modelinizde salt okunurdur. Örneğin:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

Kullanıcıların `IsAdmin` özelliğini güncelleştirmesini ve kendilerini yöneticilere yükseltmenizi istemezsiniz! En güvenli strateji, istemcinin gönderilmesine izin verilen şekilde tam olarak eşleşen bir model sınıfı kullanmaktır:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Atacan Solson 'un blog gönderisine "[giriş doğrulaması ve ASP.NET MVC 'de model doğrulama](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)",-Posting ve over-Posting konusunda iyi bir tartışmaya sahiptir. Post, ASP.NET MVC 2 ile ilgili olsa da, sorunlar hala Web API 'SI ile ilgilidir.

## <a name="handling-validation-errors"></a>Doğrulama hatalarını işleme

Doğrulama başarısız olduğunda Web API 'SI istemciye otomatik olarak bir hata döndürmez. Bu, model durumunu denetlemek ve uygun şekilde yanıt vermek için denetleyici eylemine sahiptir.

Ayrıca, denetleyici eylemi çağrılmadan önce model durumunu denetlemek için bir eylem filtresi de oluşturabilirsiniz. Aşağıdaki kodda bir örnek gösterilir:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

Model doğrulaması başarısız olursa, bu filtre doğrulama hatalarını içeren bir HTTP yanıtı döndürür. Bu durumda, denetleyici eylemi çağrılmaz.

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

Bu filtreyi tüm Web API denetleyicilerine uygulamak için, yapılandırma sırasında **HttpConfiguration. Filters** koleksiyonuna filtrenin bir örneğini ekleyin:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

Farklı bir seçenek, filtreyi ayrı denetleyicilerde veya denetleyici eylemlerinde bir öznitelik olarak ayarlamanıza olanak sağlar:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]
