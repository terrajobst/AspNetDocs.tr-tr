---
uid: single-page-application/overview/introduction/other-libraries
title: Knockout dışında bir kitaplık biliyor musunuz? | Microsoft Docs
author: madskristensen
description: Knockout dışında bir kitaplık biliyor musunuz?
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 70ced1d53b66fbe5ced3606413594707099dda28
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/09/2019
ms.locfileid: "59406450"
---
# <a name="know-a-library-other-than-knockout"></a>Knockout dışında bir kitaplık biliyor musunuz?

tarafından [Mads Kristensen](https://github.com/madskristensen)

[Tek sayfa uygulama (SPA) şablonu](knockoutjs-template.md) tek sayfa uygulamaları yazmaya başlamak için harika bir yoludur. Şablonu kullanan [KnockoutJS](http://knockoutjs.com/) uygulama verileri için DOM öğeleri bağlamak için.

Ancak, Knockout zengin istemci uygulamaları oluşturmak için yalnızca JavaScript kitaplığı değil. Diğer kitaplıkları benzer zorlukları farklı yollar sunar. Çeşitli topluluk tarafından oluşturulan şablonlarını indirilebilir yaptık şekilde başka bir kitaplık tercih edebilirsiniz. Bu şablonlarının her biri, istemci JavaScript kitaplıklarını farklı bir karışımını kullanır.

Topluluk tarafından oluşturulan bir şablon yüklemek için bir şablonun sayfaları, aşağıda listelenen ve indir düğmesine tıklayın ziyaret edin. Şablonlar, VSIX dosyası olarak sağlanır.

## <a name="backbonejs"></a>BackboneJS

[Backbone.js SPA şablon](../templates/backbonejs-template.md). Bu şablon geliştirmeye yönelik bir başlangıç skeleton sağlar. bir [Backbone.js](http://backbonejs.org/) ASP.NET MVC uygulaması. Kullanıma hazır, kullanıcı oturum açma, kaydolma, parola sıfırlama ve kullanıcı onayı ile temel bir e-posta şablonları da dahil olmak üzere temel kullanıcı oturum açma işlevselliği sağlar.

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa) zengin bir JavaScript istemci verileri yönetmek için bir açık kaynak kitaplığı. Meltem sorgulama, önbelleğe alma, değişiklik izleme, doğrulama ve daha fazla işler. İki şablon Breeze özelliği:

- [Breeze/Knockout](../templates/breezeknockout-template.md) şablonu, bir tek sayfalı uygulama Breeze ile veri yönetimi ve KnockoutJS için veri bağlama için ne kadar kolay oluşturabileceğinizi gösteren SPA Knockout şablonu genişletir.
- [Breeze/Angular](../templates/breezeangular-template.md) şablonu da Meltem, ancak kullanarak Knockout SPA şablonla genişletir [AngularJS](http://angularjs.org) veri bağlama, bağımlılık ekleme ve ekranı Yönetim kitaplığı.

Ayrıca, [Hot Towel SPA şablon](../templates/hottowel-template.md) BreezeJS kullanır.

## <a name="emberjs"></a>EmberJS

[SPA EmberJS şablonu](../templates/emberjs-template.md). Bu şablonu kullanan [Ember](http://emberjs.com/), zengin istemci uygulamaları oluşturmak için zorlukları çeşit çözer güçlü bir MVC JavaScript kitaplığı.

Ember SPA şablon EmberJS ve Gidon şablonu kullanarak SPA Knockout şablonu yeniden bir uygulamasıdır.

## <a name="hot-towel"></a>Hot Towel

[Hot Towel SPA şablon](../templates/hottowel-template.md). Bu şablon Meltem, Knockout RequireJS ve Twitter Bootstrap dahil olmak üzere çeşitli JavaScript kitaplıkları, getirir.

Burada listelenen diğer şablonlar ile karşılaştırıldığında, Hot Towel şablonu, kendi oluşturabileceğiniz daha eksiksiz bir uygulama sağlar. Dikkat edilmesi gereken daha fazla kavram vardır, ancak bunları anladığınızda, bu şablonun yalnızca aradığınız ne olabilir. Üzerinde uygulama oluşturmanızı sağlayacak bir SPA oluşturmak istiyorsunuz, ancak Hot Towel kullanın nerede karar veremez ve saniyeler içinde bir SPA ve tüm araçlar gerekir.

## <a name="feature-table"></a>Özellik tablosu

Her SPA şablon tarafından sağlanan özellikleri şunlardır:


|                        | ASP.NET SPA | Omurga | BREEZE/Angular | Breeze/KO |  Ember   | Hot Towel |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      Yapılacaklar örneği       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     Tam şablon      |             | &#10003; |                |           |          | &#10003;  |
| Gezinti ve geçmişi |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        Kitaplıklar       |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;Omurga     |             | &#10003; |                |           |          |           |
|         Meltem         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        Durandal        |             |          |                |           |          | &#10003;  |
|         Ember          |             |          |                |           | &#10003; |           |
|        Knockout        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |

