---
uid: web-api/overview/formats-and-model-binding/media-formatters
title: ASP.NET Web API 2-ASP.NET 4. x içindeki medya biçimleri
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sinde ek medya biçimlerinin nasıl destekleyeceği gösterilmektedir.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: 4c56f64a-086a-44ce-99c2-4c69604cd7fd
msc.legacyurl: /web-api/overview/formats-and-model-binding/media-formatters
msc.type: authoredcontent
ms.openlocfilehash: da0c566dad302054d7d0a6435e4c6df178c64772
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557255"
---
# <a name="media-formatters-in-aspnet-web-api-2"></a>ASP.NET Web API 2 ' de medya biçimleri

, [Mike te son](https://github.com/MikeWasson)

Bu öğreticide, ASP.NET Web API 'sinde ek medya biçimlerinin nasıl destekleyeceği gösterilmektedir.

## <a name="internet-media-types"></a>Internet medya türleri

MIME türü olarak da bilinen bir medya türü, bir veri parçasının biçimini tanımlar. HTTP 'de medya türleri ileti gövdesinin biçimini tanımlarlar. Medya türü iki dizeden oluşur, bir türü ve alt türü. Örneğin:

- metin/html
- resim/png
- uygulama/json

Bir HTTP iletisi bir varlık gövdesi içerdiğinde, Content-Type üstbilgisi ileti gövdesinin biçimini belirtir. Bu, alıcıya ileti gövdesinin içeriğini ayrıştırmayı söyler.

Örneğin, bir HTTP yanıtı bir PNG görüntüsü içeriyorsa, yanıt aşağıdaki üst bilgilere sahip olabilir.

[!code-console[Main](media-formatters/samples/sample1.cmd)]

İstemci bir istek iletisi gönderdiğinde, bir Accept üst bilgisi içerebilir. Accept üst bilgisi sunucuya, istemcinin sunucudan istediği medya türlerini bildirir. Örneğin:

[!code-console[Main](media-formatters/samples/sample2.cmd)]

Bu üst bilgi, sunucuya istemcinin HTML, XHTML veya XML istediğini söyler.

Medya türü, Web API 'sinin HTTP ileti gövdesini serileştirerek ve serileştirmesi gerektiğini belirler. Web API 'si, XML, JSON, BSON ve form-urlencoded verileri için yerleşik desteğe sahiptir ve *medya biçimlendirici*yazarak ek medya türlerini destekleyebilirsiniz.

Bir medya biçimlendirici oluşturmak için, bu sınıflardan birini türet:

- [MediaTypeFormatter](https://msdn.microsoft.com/library/system.net.http.formatting.mediatypeformatter.aspx). Bu sınıf zaman uyumsuz okuma ve yazma yöntemlerini kullanır.
- [Bufferedmediatypeformatter](https://msdn.microsoft.com/library/system.net.http.formatting.bufferedmediatypeformatter.aspx). Bu sınıf, **MediaTypeFormatter** 'dan türetilir ancak zaman uyumlu okuma/yazma yöntemlerini kullanır.

**Bufferedmediatypeformatter** 'dan türetme, zaman uyumsuz kod olmadığı için daha basittir, ancak aynı zamanda çağıran iş parçacığının g/ç sırasında engelleyebileceği anlamına gelir.

## <a name="example-creating-a-csv-media-formatter"></a>Örnek: CSV medya biçimlendiricisi oluşturma

Aşağıdaki örnek, bir ürün nesnesini bir virgülle ayrılmış değerler (CSV) biçimine seri hale getirebilen bir medya türü biçimlendirici gösterir. Bu örnek, [CRUD Işlemlerini destekleyen bir Web API 'Si oluşturma](../older-versions/creating-a-web-api-that-supports-crud-operations.md)öğreticisinde tanımlanan ürün türünü kullanır. Ürün nesnesinin tanımı aşağıda verilmiştir:

[!code-csharp[Main](media-formatters/samples/sample3.cs)]

Bir CSV biçimlendirici uygulamak için, **Bufferedmediatypeformatter**'dan türeyen bir sınıf tanımlayın:

[!code-csharp[Main](media-formatters/samples/sample4.cs)]

Oluşturucuda, biçimlendiricinin desteklediği medya türlerini ekleyin. Bu örnekte, biçimlendirici tek bir medya türünü destekler &quot;metin/CSV&quot;:

[!code-csharp[Main](media-formatters/samples/sample5.cs)]

Biçimlendiricinin seri hale getirebileceği türleri belirtmek için **CanWriteType** yöntemini geçersiz kılın:

[!code-csharp[Main](media-formatters/samples/sample6.cs)]

Bu örnekte, biçimlendirici tek `Product` nesnelerinin yanı sıra `Product` nesne koleksiyonlarını seri hale getirebilirsiniz.

Benzer şekilde, biçimlendirici 'in seri durumdan çıkarabileceği türleri göstermek için **CanReadType** yöntemini geçersiz kılın. Bu örnekte, biçimlendirici serisini kaldırma ' yı desteklemez, bu nedenle metot yalnızca **false**değerini döndürür.

[!code-csharp[Main](media-formatters/samples/sample7.cs)]

Son olarak, **WriteToStream** yöntemini geçersiz kılın. Bu yöntem bir akışa yazarak bir türü seri hale getirir. Biçimlendirici seri durumdan çıkarmayı destekliyorsa **ReadFromStream** yöntemini de geçersiz kılın.

[!code-csharp[Main](media-formatters/samples/sample8.cs)]

## <a name="adding-a-media-formatter-to-the-web-api-pipeline"></a>Web API ardışık düzenine medya biçimlendirici ekleme

Web API ardışık düzenine bir medya türü biçimlendirici eklemek için **HttpConfiguration** nesnesindeki **Formatters** özelliğini kullanın.

[!code-csharp[Main](media-formatters/samples/sample9.cs)]

## <a name="character-encodings"></a>Karakter kodlamaları

İsteğe bağlı olarak, bir medya biçimlendiricisi UTF-8 veya ISO 8859-1 gibi birden çok karakter kodlamasını destekleyebilir.

Oluşturucuda, **Supportedencotypes** koleksiyonuna bir veya daha fazla [System. Text. Encoding](https://msdn.microsoft.com/library/system.text.encoding.aspx) türü ekleyin. Önce varsayılan kodlamayı yerleştirin.

[!code-csharp[Main](media-formatters/samples/sample10.cs?highlight=6-7)]

**WriteToStream** ve **ReadFromStream** yöntemlerinde, tercih edilen karakter kodlamasını seçmek için [MediaTypeFormatter. selectkarakterencoding](https://msdn.microsoft.com/library/hh969054.aspx) ' i çağırın. Bu yöntem, istek üst bilgilerini desteklenen Kodlamalar listesiyle eşleştirir. Akıştan okurken veya yazarken döndürülen **kodlamayı** kullanın:

[!code-csharp[Main](media-formatters/samples/sample11.cs?highlight=3,5)]
