---
ms.openlocfilehash: 1b563a8c0674d51f893415221ca8fab574b78265
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57068505"
---
<a name="--"></a>--
================================

[![Derleme durumu](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency durumu](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)

JQuery doğrulama eklentisi, her türden özelleştirmeler uygulamanız gerçekten kolay uyacak şekilde yapma sırasında mevcut formlarınızı değiştirilebilir doğrulaması sağlar.

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[Project Yardımı](http://pledgie.com/campaigns/18159)

[![Project Yardımı](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)

Bu proje için Yardım görünüyor! [Devam eden pledgie kampanyaya bağışlamaya](http://pledgie.com/campaigns/18159) ve sözcük yayılan yardımcı olur. Eklenti kullandığınız ya da plan kullanmak için bir Bağış - göz önünde bulundurun her miktarda yardımcı olur.

Plan için harcadığınız para nasıl bulabileceğinizi [pledgie sayfa](http://pledgie.com/campaigns/18159).

## <a name="get-started"></a>Başlarken

### <a name="downloading-the-prebuilt-files"></a>Önceden oluşturulmuş dosyaları indirme

Önceden oluşturulmuş dosyaları yüklenebilir http://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>En son değişiklikleri indiriliyor

Yayımlanmamış geliştirme dosyaları tarafından alınabilir:

 1. [İndirme](https://github.com/jzaefferer/jquery-validation/archive/master.zip) veya bu deponun çatal
 2. [Derlemeyi Kur](CONTRIBUTING.md#build-setup)
 3. Çalıştırma `grunt` "dağıtım" Dizin oluşturulmuş dosyaları oluşturmak için

### <a name="including-it-on-your-page"></a>Sayfanızda dahil

JQuery ve eklenti sayfasında bulunur. Doğrulama ve çağırmak için bir form seçip `validate` yöntemi.

```html
<form>
    <input required>
</form>
<script src="jquery.js"></script>
<script src="jquery.validate.js"></script>
<script>
$("form").validate();
</script>
```

Alternatif olarak jQuery ve eklenti requirejs aracılığıyla modülünüzde içerir.

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

Bir kural ayarlama hakkında daha fazla bilgi ve özelleştirmeler [belgelere bakın](http://jqueryvalidation.org/documentation/).

## <a name="reporting-issues-and-contributing-code"></a>Sorunları bildirme ve kod katkısı

Bkz: [katkıda bulunan Kılavuzu](CONTRIBUTING.md) Ayrıntılar için.

**E-POSTA DOĞRULAMA HAKKINDA ÖNEMLİ BİR NOT**. Sürüm 1.12.0 itibarıyla aynı normal ifadeyi bu eklentiyi kullanarak, [HTML5 belirtimi kullanılacak tarayıcılar için önerdiği](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Biz, onların izinden gitmekten ve aynı denetimi kullanın. Lütfen belirtimi yanlış olduğunu düşünüyorsanız, sorunu onlara bildirin. Farklı gereksinimlere sahip değilse, göz önünde bulundurun [özel bir yöntem kullanılarak](http://jqueryvalidation.org/jQuery.validator.addMethod/).

## <a name="license"></a>Lisans
Copyright &copy; Jörn Zaefferer<br>
MIT lisansı altında lisanslanır.
