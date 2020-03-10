---
uid: web-api/overview/formats-and-model-binding/json-and-xml-serialization
title: ASP.NET Web API-ASP.NET 4. x içinde JSON ve XML serileştirme
author: MikeWasson
description: ASP.NET 4. x için ASP.NET Web API 'sindeki JSON ve XML formatlarını açıklar.
ms.author: riande
ms.date: 05/30/2012
ms.custom: seoapril2019
ms.assetid: 1cd7525d-de5e-4ab6-94f0-51480d3255d1
msc.legacyurl: /web-api/overview/formats-and-model-binding/json-and-xml-serialization
msc.type: authoredcontent
ms.openlocfilehash: 00fa07f00eabf7e6c883c5e9ceaf9a38a8f49605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557472"
---
# <a name="json-and-xml-serialization-in-aspnet-web-api"></a>ASP.NET Web API 'sinde JSON ve XML serileştirme

, [Mike te son](https://github.com/MikeWasson)

Bu makalede ASP.NET Web API 'sindeki JSON ve XML formatlayıcıları açıklanmaktadır.

ASP.NET Web API 'sinde, bir *medya türü biçimlendiricisi* şunları yapabilir:

- Bir HTTP ileti gövdesinden CLR nesnelerini okuma
- CLR nesnelerini bir HTTP ileti gövdesine yazma

Web API 'si hem JSON hem de XML için medya türü biçimleri sağlar. Framework, varsayılan olarak bu biçimleri ardışık düzene ekler. İstemciler, HTTP isteğinin Accept üst bilgisinde JSON veya XML isteğinde bulunabilir.

## <a name="contents"></a>İçindekiler

- [JSON medya türü biçimlendirici](#json_media_type_formatter)

    - [Salt okunurdur özellikleri](#json_readonly)
    - [Tarihle](#json_dates)
    - [Girintileme](#json_indenting)
    - [Kamel büyük harfleri](#json_camelcasing)
    - [Anonim ve zayıf türsüz nesneler](#json_anon)
- [XML medya türü biçimlendirici](#xml_media_type_formatter)

    - [Salt okunurdur özellikleri](#xml_readonly)
    - [Tarihle](#xml_dates)
    - [Girintileme](#xml_indenting)
    - [Tür başına XML serileştiricileri ayarlanıyor](#xml_pertype)
- [JSON veya XML biçimlendirici kaldırılıyor](#removing_the_json_or_xml_formatter)
- [Döngüsel nesne başvurularını işleme](#handling_circular_object_references)
- [Test nesnesi serileştirme](#testing_object_serialization)

<a id="json_media_type_formatter"></a>
## <a name="json-media-type-formatter"></a>JSON medya türü biçimlendirici

JSON biçimlendirmesi, **Jsonmediatypeformatter** sınıfı tarafından sağlanır. Varsayılan olarak, **Jsonmediatypeformatter** serileştirme gerçekleştirmek için [JSON.net](https://github.com/JamesNK/Newtonsoft.Json) kitaplığını kullanır. Json.NET, üçüncü taraf bir açık kaynak projem.

İsterseniz, Json.NET yerine **DataContractJsonSerializer** kullanmak Için **Jsonmediatypeformatter** sınıfını yapılandırabilirsiniz. Bunu yapmak için **Usedatacontractjsonserializer** özelliğini **true**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample1.cs)]

### <a name="json-serialization"></a>JSON Seri Hale Getirme

Bu bölümde, varsayılan [JSON.net](https://github.com/JamesNK/Newtonsoft.Json) serileştirici kullanılarak JSON biçimlendirici 'nin bazı belirli davranışları açıklanmaktadır. Bu, Json.NET kitaplığı hakkında kapsamlı bir belge olması anlamına gelir; daha fazla bilgi için [JSON.net belgelerine](http://james.newtonking.com/projects/json/help/)bakın.

#### <a name="what-gets-serialized"></a>Ne seri hale getirilebilir?

Varsayılan olarak, tüm ortak özellikler ve alanlar serileştirilmiş JSON 'a dahil edilir. Bir özellik veya alanı atlamak için, bunu **Jsonıgnore** özniteliğiyle süsle.

[!code-csharp[Main](json-and-xml-serialization/samples/sample2.cs)]

&quot;kabul&quot; yaklaşımını tercih ediyorsanız, sınıfı **DataContract** özniteliğiyle süsler. Bu öznitelik mevcutsa, **DataMember**öğesine sahip olmadıkları müddetçe Üyeler göz ardı edilir. Özel üyeleri seri hale getirmek için **DataMember** de kullanabilirsiniz.

[!code-csharp[Main](json-and-xml-serialization/samples/sample3.cs)]

<a id="json_readonly"></a>
### <a name="read-only-properties"></a>Salt okunurdur özellikleri

Salt okuma özellikleri varsayılan olarak serileştirilir.

<a id="json_dates"></a>
### <a name="dates"></a>Tarihler

Varsayılan olarak, Json.NET tarihleri [ıso 8601](http://www.w3.org/TR/NOTE-datetime) biçiminde yazar. UTC (Eşgüdümlü Evrensel Saat) tarihleri "Z" sonekiyle yazılır. Yerel saat içindeki tarihler, saat dilimi konumunu içerir. Örneğin:

[!code-console[Main](json-and-xml-serialization/samples/sample4.cmd)]

Varsayılan olarak, Json.NET saat dilimini korur. DateTimeZoneHandling özelliğini ayarlayarak bunu geçersiz kılabilirsiniz:

[!code-csharp[Main](json-and-xml-serialization/samples/sample5.cs)]

ISO 8601 yerine [MICROSOFT JSON tarih biçimini](https://msdn.microsoft.com/library/bb299886.aspx#intro_to_json_sidebarb) (`"\/Date(ticks)\/"`) kullanmayı tercih ediyorsanız, serileştirici ayarlarındaki **DateFormatHandling** özelliğini ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample6.cs)]

<a id="json_indenting"></a>
### <a name="indenting"></a>Girintileme

Girintili JSON yazmak için **biçimlendirme** ayarını **biçimlendirme. girintili**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample7.cs)]

<a id="json_camelcasing"></a>
### <a name="camel-casing"></a>Kamel büyük harfleri

Veri modelinizi değiştirmeden JSON özellik adlarını kamel büyük küçük harfe yazmak için, seri hale getirici üzerinde **Camelcasepropertynamescontractresolver** ' ı ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample8.cs)]

<a id="json_anon"></a>
### <a name="anonymous-and-weakly-typed-objects"></a>Anonim ve zayıf türsüz nesneler

Bir eylem yöntemi, anonim bir nesne döndürebilir ve bunu JSON 'a seri hale getirebilirsiniz. Örneğin:

[!code-csharp[Main](json-and-xml-serialization/samples/sample9.cs)]

Yanıt iletisi gövdesinde şu JSON yer alacak:

[!code-json[Main](json-and-xml-serialization/samples/sample10.json)]

Web API 'niz istemcilerden gevşek olarak yapılandırılmış JSON nesneleri alırsa, istek gövdesinin serisini bir **Newtonsoft. JSON. LINQ. JObject** türüne taşıyabilirsiniz.

[!code-csharp[Main](json-and-xml-serialization/samples/sample11.cs)]

Ancak, türü kesin belirlenmiş veri nesneleri kullanmak genellikle daha iyidir. Daha sonra verileri kendiniz ayrıştırmanıza gerek kalmaz ve model doğrulamasının avantajlarını elde edersiniz.

XML serileştiricisi anonim türleri veya **JObject** örneklerini desteklemez. JSON verileriniz için bu özellikleri kullanırsanız, bu makalenin ilerleyen kısımlarında açıklandığı gibi, XML biçimlendirici ' i ardışık düzen öğesinden kaldırmanız gerekir.

<a id="xml_media_type_formatter"></a>
## <a name="xml-media-type-formatter"></a>XML medya türü biçimlendirici

XML biçimlendirmesi **Xmlmediatypeformatter** sınıfı tarafından sağlanır. Varsayılan olarak, **Xmlmediatypeformatter** serileştirme işlemini gerçekleştirmek için **DataContractSerializer** sınıfını kullanır.

Tercih ederseniz, **Xmlmediatypeformatter** 'ı **DataContractSerializer**yerine **XmlSerializer** 'ı kullanacak şekilde yapılandırabilirsiniz. Bunu yapmak için **useXmlSerializer** özelliğini **true**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample12.cs)]

**XmlSerializer** sınıfı, **DataContractSerializer**'dan daha dar bir tür kümesini destekler, ancak sonuçta elde edilen XML üzerinde daha fazla denetim sağlar. Mevcut bir XML şemasıyla eşleşmesi gerekiyorsa **XmlSerializer** kullanmayı düşünün.

### <a name="xml-serialization"></a>XML seri hale getirme

Bu bölümde, varsayılan **DataContractSerializer**kullanılarak XML biçimlendirici 'nin bazı belirli davranışları açıklanmaktadır.

Varsayılan olarak, DataContractSerializer aşağıdaki gibi davranır:

- Tüm genel okuma/yazma özellikleri ve alanları serileştirilir. Bir özellik veya alanı atlamak için, **ıgnoredatamember** özniteliğiyle süslenmiş.
- Özel ve korunan Üyeler serileştirilmez.
- Salt okuma özellikleri serileştirilmez. (Ancak, salt okunurdur bir koleksiyon özelliğinin içeriği serileştirilir.)
- Sınıf ve üye adları, sınıf bildiriminde göründükleri gibi XML 'e tam olarak yazılır.
- Varsayılan bir XML ad alanı kullanılır.

Serileştirme üzerinde daha fazla denetime ihtiyacınız varsa, bir sınıfı **DataContract** özniteliğiyle süslemek için kullanabilirsiniz. Bu öznitelik mevcut olduğunda, sınıf aşağıdaki şekilde serileştirilir:

- &quot;&quot; yaklaşımı: Özellikler ve alanlar varsayılan olarak serileştirilmez. Bir özellik veya alanı seri hale getirmek için, bunu **DataMember** özniteliğiyle süsle.
- Özel veya korumalı bir üyeyi seri hale getirmek için, bunu **DataMember** özniteliğiyle süsle.
- Salt okuma özellikleri serileştirilmez.
- Sınıf adının XML 'de nasıl göründüğünü değiştirmek için, **DataContract** özniteliğinde *Name* parametresini ayarlayın.
- Bir üye adının XML 'de nasıl göründüğünü değiştirmek için, **DataMember** özniteliğinde *Name* parametresini ayarlayın.
- XML ad alanını değiştirmek için, **DataContract** sınıfında *ad alanı* parametresini ayarlayın.

<a id="xml_readonly"></a>
### <a name="read-only-properties"></a>Salt okunurdur özellikleri

Salt okuma özellikleri serileştirilmez. Salt okunurdur bir özelliğin bir yedekleme özel alanı varsa, özel alanı **DataMember** özniteliğiyle işaretleyebilirsiniz. Bu yaklaşım, sınıfında **DataContract** özniteliğini gerektirir.

[!code-csharp[Main](json-and-xml-serialization/samples/sample13.cs)]

<a id="xml_dates"></a>
### <a name="dates"></a>Tarihler

Tarihler ISO 8601 biçiminde yazılır. Örneğin, &quot;2012-05-23T20:21:37.9116538 Z&quot;.

<a id="xml_indenting"></a>
### <a name="indenting"></a>Girintileme

Girintili XML yazmak için **Girintile** özelliğini **true**olarak ayarlayın:

[!code-csharp[Main](json-and-xml-serialization/samples/sample14.cs)]

<a id="xml_pertype"></a>
## <a name="setting-per-type-xml-serializers"></a>Tür başına XML serileştiricileri ayarlanıyor

Farklı CLR türleri için farklı XML serileştiricileri ayarlayabilirsiniz. Örneğin, geriye doğru uyumluluk için **XmlSerializer** gerektiren belirli bir veri nesneniz olabilir. Bu nesne için **XmlSerializer** 'ı kullanabilir ve diğer türler için **DataContractSerializer** kullanmaya devam edebilirsiniz.

Belirli bir tür için bir XML serileştirici ayarlamak için **setserializer**çağırın.

[!code-csharp[Main](json-and-xml-serialization/samples/sample15.cs)]

Bir **XmlSerializer** veya **XmlObjectSerializer**öğesinden türetilen herhangi bir nesne belirtebilirsiniz.

<a id="removing_the_json_or_xml_formatter"></a>
## <a name="removing-the-json-or-xml-formatter"></a>JSON veya XML biçimlendirici kaldırılıyor

JSON biçimlendirici veya XML biçimlendirici, bunları kullanmak istemiyorsanız Formatters listesinden kaldırabilirsiniz. Bunu yapmak için başlıca nedenler şunlardır:

- Web API yanıtlarınızı belirli bir medya türüyle sınırlamak için. Örneğin, yalnızca JSON yanıtlarını desteklemeye karar verebilir ve XML biçimlendirici ' ı kaldırabilirsiniz.
- Varsayılan biçimlendiricisi özel bir biçimlendirici ile değiştirmek için. Örneğin, JSON biçimlendirici bir JSON biçimlendiricisi kendi özel uygulamanıza göre değiştirebilirsiniz.

Aşağıdaki kod, varsayılan formatlamalara nasıl kaldırılacağını gösterir. Bunu, Global. asax dosyasında tanımlanan **uygulamanızdan\_start** yönteminden çağırın.

[!code-csharp[Main](json-and-xml-serialization/samples/sample16.cs)]

<a id="handling_circular_object_references"></a>
## <a name="handling-circular-object-references"></a>Döngüsel nesne başvurularını işleme

Varsayılan olarak, JSON ve XML formatlayıcıları tüm nesneleri değer olarak yazar. İki özellik aynı nesneye başvurursanız veya aynı nesne bir koleksiyonda iki kez görünürse, biçimlendirici nesneyi iki kez serileştirilir. Bu, nesne grafikleriniz döngüler içeriyorsa, bu bir sorundur çünkü seri hale getirici grafikte bir döngü algıladığında bir özel durum oluşturur.

Aşağıdaki nesne modellerini ve denetleyiciyi göz önünde bulundurun.

[!code-csharp[Main](json-and-xml-serialization/samples/sample17.cs)]

Bu eylemi çağırmak, biçimlendirici bir durum kodu 500 (Iç sunucu hatası) yanıtına çeviren bir özel durum oluşturulmasına neden olur.

JSON 'daki nesne başvurularını korumak için aşağıdaki kodu Global. asax dosyasındaki **Application\_start** yöntemine ekleyin:

[!code-csharp[Main](json-and-xml-serialization/samples/sample18.cs)]

Artık denetleyici eylemi şuna benzer bir JSON döndürür:

[!code-json[Main](json-and-xml-serialization/samples/sample19.json)]

Seri hale getiricinin her iki nesneye bir &quot;$id&quot; özelliği eklediğine dikkat edin. Ayrıca, Employee. Department özelliğinin bir döngü oluşturduğunu algılar, bu yüzden değeri bir nesne başvurusuyla değiştirir: {&quot;$ref&quot;:&quot;1&quot;}.

> [!NOTE]
> Nesne başvuruları JSON 'da standart değildir. Bu özelliği kullanmadan önce, istemcilerinizin sonuçları ayrıştırabilecek olup olmayacağını göz önünde bulundurun. Yalnızca grafikten döngüleri kaldırmak daha iyi olabilir. Örneğin, çalışana kadar olan bağlantı bu örnekte gerçekten gerekli değildir.

XML 'deki nesne başvurularını korumak için iki seçeneğiniz vardır. Daha basit seçenek, model sınıfınıza `[DataContract(IsReference=true)]` eklemektir. *IsReference* parametresi nesne başvurularını mümkün bir şekilde sunar. **DataContract** serileştirme kabul eder, bu nedenle ayrıca özelliklere **DataMember** öznitelikleri eklemeniz gerekir:

[!code-csharp[Main](json-and-xml-serialization/samples/sample20.cs)]

Artık biçimlendirici şuna benzer bir XML oluşturacak:

[!code-xml[Main](json-and-xml-serialization/samples/sample21.xml)]

Model sınıfınıza ait özniteliklerin önüne geçmek istiyorsanız, başka bir seçenek vardır: yeni türe özgü bir **DataContractSerializer** örneği oluşturun ve bu tür Için *preserveObjectReferences* öğesini **true** olarak ayarlayın. Sonra bu örneği, XML medya türü biçimlendirici üzerinde tür başına seri hale getirici olarak ayarlayın. Aşağıdaki kod bunun nasıl yapılacağını göstermektedir:

[!code-csharp[Main](json-and-xml-serialization/samples/sample22.cs?highlight=3)]

<a id="testing_object_serialization"></a>
## <a name="testing-object-serialization"></a>Test nesnesi serileştirme

Web API 'nizi tasarlarken, veri nesnelerinizin nasıl seri hale getirileceğinin test olması yararlı olur. Bunu, denetleyici oluşturmadan veya bir denetleyici eylemi çağırmadan yapabilirsiniz.

[!code-csharp[Main](json-and-xml-serialization/samples/sample23.cs)]
