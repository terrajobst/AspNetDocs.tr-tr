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
ms.openlocfilehash: 64a4ad1fb411f7291a5cba634afdf4d2fdb16d55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578549"
---
# <a name="know-a-library-other-than-knockout"></a>Knockout dışında bir kitaplık biliyor musunuz?

[Mads Kristensen](https://github.com/madskristensen) tarafından

[Tek sayfalı uygulama (Spa) şablonu](knockoutjs-template.md) , tek sayfalı uygulamalar yazmaya başlamak için harika bir yoldur. Şablon, uygulama verilerini DOM öğelerine bağlamak için [altını gizleme Koutjs](http://knockoutjs.com/) kullanır.

Ancak altını gizleme, zengin istemci uygulamaları oluşturmak için tek JavaScript kitaplığı değildir. Diğer Kitaplıklar benzer zorlukları farklı yollarla çözecektir. Bir kitaplığı başka bir şekilde tercih edebilirsiniz. bu nedenle, birçok topluluk tarafından oluşturulan şablonu indirilebilir hale sunuyoruz. Bu şablonların her biri, istemci JavaScript kitaplıklarının farklı bir karışımını kullanır.

Topluluk tarafından oluşturulan bir şablon yüklemek için, aşağıda listelenen şablon sayfalarından birini ziyaret edin ve Indir düğmesine tıklayın. Şablonlar VSıX dosyaları olarak sağlanır.

## <a name="backbonejs"></a>BackboneJS

[Omurga. js Spa şablonu](../templates/backbonejs-template.md). Bu şablon, ASP.NET MVC 'de bir [omurga. js](http://backbonejs.org/) uygulaması geliştirmek için bir başlangıç iskelet sağlar. Bu, temel e-posta şablonlarıyla Kullanıcı kaydolma, oturum açma, parola sıfırlama ve kullanıcı onayı dahil olmak üzere temel Kullanıcı oturum açma işlevlerini sağlar.

## <a name="breezejs"></a>BreezeJS

[Breezejs](http://www.breezejs.com/?utm_source=ms-spa) , bir JavaScript istemcisinde zengin verilerin yönetilmesi için açık kaynak bir kitaplıktır. Breeze, sorgulama, önbelleğe alma, değişiklik izleme, doğrulama ve daha fazlasını gerçekleştirir. İki şablon özelliği Breeze:

- [Breeze/altını gizleme](../templates/breezeknockout-template.md) şablonu, veri yönetimi Için Breeze ve veri bağlama için altını gizleme ile tek sayfalı bir uygulama oluşturmanın ne kadar kolay olduğunu gösteren ALTıNı gizleme Spa şablonunu genişletir.
- [Breeze/angular](../templates/breezeangular-template.md) şablonu Ayrıca Breeze Ile ALTıNı gizleme Spa şablonunu genişletir, ancak veri bağlama, bağımlılık ekleme ve ekran yönetimi için [AngularJS](http://angularjs.org) kitaplığını kullanmaktır.

Buna ek olarak, [sık ERIŞIMLI Spa](../templates/hottowel-template.md) , BreezeJS ' yi kullanır.

## <a name="emberjs"></a>EmberJS

[Emberjs Spa şablonu](../templates/emberjs-template.md). Bu şablon, zengin istemci uygulamaları oluşturmak için çok sayıda zorluk çözen güçlü bir MVC JavaScript kitaplığı olan [Ember](http://emberjs.com/)'yi kullanır.

Ember SPA şablonu, EmberJS ve Handleçubuklarının şablon oluşturma kullanılarak altını gizleme SPA şablonunun yeniden uygulanmasıdır.

## <a name="hot-towel"></a>Etkin simgesi

[Sık ERIŞIMLI Spa şablonu](../templates/hottowel-template.md). Bu şablon, Breeze, altını gizleme, RequireJS ve Twitter önyüklemesi dahil olmak üzere birkaç JavaScript kitaplığı sunar.

Burada listelenen diğer şablonlar ile karşılaştırıldığında, sık erişimli şablon, kendi kendinize oluşturabileceğiniz daha kapsamlı bir uygulama sağlar. Bilinmesi gereken daha fazla kavram vardır, ancak bunları anladığınızda, bu şablon yalnızca sizin aradığınıza ait olabilir. Bir SPA oluşturmak ve nereden başlayacağınıza karar vermek istiyorsanız, sık e-başnu kullanın ve saniyeler içinde, üzerinde oluşturmanız gereken bir SPA ve tüm araçlara sahip olacaksınız.

## <a name="feature-table"></a>Özellik tablosu

Her SPA şablonu tarafından sunulan özellikler şunlardır:

|                        | ASP.NET SPA | Yönlendiricide | Breeze/angular | Breeze/KO |  Ember   | Etkin simgesi |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      ToDo örneği       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     Çıplak şablon      |             | &#10003; |                |           |          | &#10003;  |
| Gezinti ve geçmiş |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        Kitaplıklar       |             |          |                |           |          |           |
|        Angular         |             |          |    &#10003;    |           |          |           |
|    &#8195;Yönlendiricide     |             | &#10003; |                |           |          |           |
|         Breeze         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        Durandal        |             |          |                |           |          | &#10003;  |
|         Ember          |             |          |                |           | &#10003; |           |
|        Renkleri        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |
