---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: '5\. Bölüm: altını gizleme. js ile dinamik kullanıcı arabirimi oluşturma | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600004"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>5\. Bölüm: altını gizleme. js ile dinamik kullanıcı arabirimi oluşturma

, [Mike te son](https://github.com/MikeWasson)

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>Knockout.js ile Dinamik Kullanıcı Arabirimi Oluşturma

Bu bölümde, yönetici görünümüne işlevsellik eklemek için altını gizleme. js ' yi kullanacağız.

[Altını gizleme. js](http://knockoutjs.com/) , HTML denetimlerini verilere bağlamayı kolaylaştıran bir JavaScript kitaplığıdır. Altını gizleme. js Model-View-ViewModel (MVVM) modelini kullanır.

- *Model* , iş etki alanındaki verilerin sunucu tarafı gösterimidir (bizim örneğimizde, ürünlerimiz ve siparişlerde).
- *Görünüm* sunum katmanıdır (HTML).
- *View-model* , model verilerini tutan bir JavaScript nesnesidir. View-model, Kullanıcı arabiriminin kod soyutlamasıdır. HTML temsili bilgisine sahip değildir. Bunun yerine, görünümün "öğe listesi" gibi soyut özelliklerini temsil eder.

Görünüm, görünüm modeline veri ile bağlanır. Görünüm modeli güncelleştirmeleri otomatik olarak görünüme yansıtılır. Görünüm modeli Ayrıca, düğme tıklamaları gibi görünümden olayları alır ve model üzerinde bir sipariş oluşturma gibi işlemleri gerçekleştirir.

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

İlk olarak View-model tanımlayacağız. Bundan sonra, HTML işaretlemesini görünüm modeline bağlayacağız.

Aşağıdaki Razor bölümünü admin. cshtml öğesine ekleyin:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

Bu bölümü dosyada herhangi bir yere ekleyebilirsiniz. Görünüm işlendiğinde, Bölüm HTML sayfasının alt kısmında, kapatma &lt;/Body&gt; etiketinden hemen önce görünür.

Bu sayfanın tüm betiği, yorum tarafından belirtilen komut dosyası etiketinin içine alınacaktır:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

İlk olarak, bir View-model sınıfı tanımlayın:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**ko. observableArray** , bir *observable*olarak adlandırılan, altını gizleme içindeki özel bir nesne türüdür. [Altını gizleme. js belgelerinden](http://knockoutjs.com/documentation/observables.html): bir observable, abonelere değişiklikler hakkında bildirimde bulunan bir "JavaScript nesnesidir." Bir observable 'ın içeriği değiştiğinde görünüm, eşleşecek şekilde otomatik olarak güncelleştirilir.

`products` diziyi doldurmak için Web API 'sine bir AJAX isteği yapın. Görünüm paketinde API için temel URI 'yi depoladığımızda hatırlayın (öğreticinin 4. [bölümüne](using-web-api-with-entity-framework-part-4.md) bakın).

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

Ardından, Products oluşturmak, güncelleştirmek ve silmek için View-model ' e işlevler ekleyin. Bu işlevler, Web API 'sine AJAX çağrıları gönderir ve sonuçları kullanarak görünüm modelini güncelleştirir.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

Şimdi en önemli bölüm: DOM daha fazla yüklendiğinde, **ko. applyBindings** işlevini çağırın ve `ProductsViewModel`yeni bir örneğini geçirin:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

**Ko. applyBindings** yöntemi, gizlemeyi etkinleştirir ve görünüm modelini görünüme bağlar.

Artık bir görünüm modelimiz olduğuna göre, bağlamaları oluşturarız. Altını gizleme. js ' de, bunu HTML öğelerine `data-bind` öznitelikleri ekleyerek yapabilirsiniz. Örneğin, bir HTML listesini diziye bağlamak için `foreach` bağlamayı kullanın:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

`foreach` bağlama, dizi boyunca yinelenir ve dizideki her nesne için alt öğeler oluşturur. Alt öğelerdeki bağlamalar, dizi nesnelerinde özelliklere başvurabilir.

Aşağıdaki bağlamaları "Update-Products" listesine ekleyin:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

`<li>` öğesi, **foreach** bağlamasının kapsamı içinde meydana gelir. Bunun anlamı, `products` dizisindeki her ürün için öğeyi bir kez oluşturacak anlamına gelir. `<li>` öğesi içindeki tüm bağlamalar, bu ürün örneğine başvurur. Örneğin, `$data.Name` üründeki `Name` özelliğine başvurur.

Metin girişlerinin değerlerini ayarlamak için `value` bağlamayı kullanın. Düğmeler, `click` bağlamasını kullanarak model görünümündeki işlevlere bağlanır. Ürün örneği her işleve bir parametre olarak geçirilir. Daha fazla bilgi için, [altını gizleme. js belgeleri](http://knockoutjs.com/documentation/observables.html) çeşitli bağlamaların iyi açıklamalarını içerir.

Ardından, ürün Ekle formundaki **Gönder** olayı için bir bağlama ekleyin:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

Bu bağlama, yeni bir ürün oluşturmak için görünüm modelinde `create` işlevini çağırır.

Yönetici görünümü için kodun tamamı aşağıda verilmiştir:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

Uygulamayı çalıştırın, yönetici hesabıyla oturum açın ve "Yönetici" bağlantısına tıklayın. Ürünlerin listesini görmeniz ve ürün oluşturabilir, güncelleştirebilir veya silebilirsiniz.

> [!div class="step-by-step"]
> [Önceki](using-web-api-with-entity-framework-part-4.md)
> [İleri](using-web-api-with-entity-framework-part-6.md)
