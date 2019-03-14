---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067611"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a>[jQuery doğrulama eklentisi](https://jqueryvalidation.org/) -Form daha kolay doğrulama
================================

[![Derleme durumu](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency durumu](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)

JQuery doğrulama eklentisi, her türden özelleştirmeler uygulamanız gerçekten kolay uyacak şekilde yapma sırasında mevcut formlarınızı değiştirilebilir doğrulaması sağlar.

## <a name="getting-started"></a>Başlarken

### <a name="downloading-the-prebuilt-files"></a>Önceden oluşturulmuş dosyaları indirme

Önceden oluşturulmuş dosyaları yüklenebilir https://jqueryvalidation.org/

### <a name="downloading-the-latest-changes"></a>En son değişiklikleri indiriliyor

Yayımlanmamış geliştirme dosyaları tarafından alınabilir:

 1. [İndirme](https://github.com/jquery-validation/jquery-validation/archive/master.zip) veya bu deponun çatal
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

Bir kural ayarlama hakkında daha fazla bilgi ve özelleştirmeler [belgelere bakın](https://jqueryvalidation.org/documentation/).

## <a name="reporting-issues-and-contributing-code"></a>Sorunları bildirme ve kod katkısı

Bkz: [katkıda bulunan Kılavuzu](CONTRIBUTING.md) Ayrıntılar için.

**E-POSTA DOĞRULAMA HAKKINDA ÖNEMLİ BİR NOT**. Sürüm 1.12.0 itibarıyla aynı normal ifadeyi bu eklentiyi kullanarak, [HTML5 belirtimi kullanılacak tarayıcılar için önerdiği](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Biz, onların izinden gitmekten ve aynı denetimi kullanın. Lütfen belirtimi yanlış olduğunu düşünüyorsanız, sorunu onlara bildirin. Farklı gereksinimlere sahip değilse, göz önünde bulundurun [özel bir yöntem kullanılarak](https://jqueryvalidation.org/jQuery.validator.addMethod/).
Yerleşik doğrulama normal ifade desenleri ayarlama yapmanız durumunda, lütfen [belgeleri izleyin](https://jqueryvalidation.org/jQuery.validator.methods/).

**ÖNEMLİ NOT GEREKLİ YÖNTEMİ HAKKINDA; EYLEM**. 1.14.0 sürümden itibaren bu eklentiyi eklenen öğenin değerini kırpmayı beyaz boşlukları durdurur. Aynı sonucu elde etmek istiyorsanız, kullanabileceğiniz [ `normalizer` ](https://jqueryvalidation.org/normalizer/) doğrulama önce bir öğenin değerini dönüştürmek için kullanılabilir. Bu özellik sürümünden itibaren kullanılabilir `v1.15.0`. Diğer bir deyişle, şöyle bir şey yapabilirsiniz:
``` js
$("#myForm").validate({
    rules: {
        username: {
            required: true,
            // Using the normalizer to trim the value of the element
            // before validating it.
            //
            // The value of `this` inside the `normalizer` is the corresponding
            // DOMElement. In this example, `this` references the `username` element.
            normalizer: function(value) {
                return $.trim(value);
            }
        }
    }
});
```

## <a name="license"></a>Lisans
Copyright &copy; Jörn Zaefferer<br>
MIT lisansı altında lisanslanır.
