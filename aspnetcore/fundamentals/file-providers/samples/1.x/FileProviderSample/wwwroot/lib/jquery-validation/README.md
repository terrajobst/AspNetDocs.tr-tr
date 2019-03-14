---
ms.openlocfilehash: 24c36493284988aa45b15c78e2577c0ef96aba56
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067611"
---
<a name="jquery-validation-pluginhttpsjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="8a165-101">[jQuery doğrulama eklentisi](https://jqueryvalidation.org/) -Form daha kolay doğrulama</span><span class="sxs-lookup"><span data-stu-id="8a165-101">[jQuery Validation Plugin](https://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="8a165-102">[![Derleme durumu](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency durumu](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="8a165-102">[![Build Status](https://secure.travis-ci.org/jquery-validation/jquery-validation.svg)](https://travis-ci.org/jquery-validation/jquery-validation)
[![devDependency Status](https://david-dm.org/jquery-validation/jquery-validation/dev-status.svg?theme=shields.io)](https://david-dm.org/jquery-validation/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="8a165-103">JQuery doğrulama eklentisi, her türden özelleştirmeler uygulamanız gerçekten kolay uyacak şekilde yapma sırasında mevcut formlarınızı değiştirilebilir doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a165-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8a165-104">Başlarken</span><span class="sxs-lookup"><span data-stu-id="8a165-104">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="8a165-105">Önceden oluşturulmuş dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="8a165-105">Downloading the prebuilt files</span></span>

<span data-ttu-id="8a165-106">Önceden oluşturulmuş dosyaları yüklenebilir https://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="8a165-106">Prebuilt files can be downloaded from https://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="8a165-107">En son değişiklikleri indiriliyor</span><span class="sxs-lookup"><span data-stu-id="8a165-107">Downloading the latest changes</span></span>

<span data-ttu-id="8a165-108">Yayımlanmamış geliştirme dosyaları tarafından alınabilir:</span><span class="sxs-lookup"><span data-stu-id="8a165-108">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="8a165-109">[İndirme](https://github.com/jquery-validation/jquery-validation/archive/master.zip) veya bu deponun çatal</span><span class="sxs-lookup"><span data-stu-id="8a165-109">[Downloading](https://github.com/jquery-validation/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="8a165-110">Derlemeyi Kur</span><span class="sxs-lookup"><span data-stu-id="8a165-110">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="8a165-111">Çalıştırma `grunt` "dağıtım" Dizin oluşturulmuş dosyaları oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="8a165-111">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="8a165-112">Sayfanızda dahil</span><span class="sxs-lookup"><span data-stu-id="8a165-112">Including it on your page</span></span>

<span data-ttu-id="8a165-113">JQuery ve eklenti sayfasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="8a165-113">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="8a165-114">Doğrulama ve çağırmak için bir form seçip `validate` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8a165-114">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="8a165-115">Alternatif olarak jQuery ve eklenti requirejs aracılığıyla modülünüzde içerir.</span><span class="sxs-lookup"><span data-stu-id="8a165-115">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="8a165-116">Bir kural ayarlama hakkında daha fazla bilgi ve özelleştirmeler [belgelere bakın](https://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="8a165-116">For more information on how to setup a rules and customizations, [check the documentation](https://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="8a165-117">Sorunları bildirme ve kod katkısı</span><span class="sxs-lookup"><span data-stu-id="8a165-117">Reporting issues and contributing code</span></span>

<span data-ttu-id="8a165-118">Bkz: [katkıda bulunan Kılavuzu](CONTRIBUTING.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="8a165-118">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="8a165-119">**E-POSTA DOĞRULAMA HAKKINDA ÖNEMLİ BİR NOT**.</span><span class="sxs-lookup"><span data-stu-id="8a165-119">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="8a165-120">Sürüm 1.12.0 itibarıyla aynı normal ifadeyi bu eklentiyi kullanarak, [HTML5 belirtimi kullanılacak tarayıcılar için önerdiği](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="8a165-120">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="8a165-121">Biz, onların izinden gitmekten ve aynı denetimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="8a165-121">We will follow their lead and use the same check.</span></span> <span data-ttu-id="8a165-122">Lütfen belirtimi yanlış olduğunu düşünüyorsanız, sorunu onlara bildirin.</span><span class="sxs-lookup"><span data-stu-id="8a165-122">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="8a165-123">Farklı gereksinimlere sahip değilse, göz önünde bulundurun [özel bir yöntem kullanılarak](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="8a165-123">If you have different requirements, consider [using a custom method](https://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>
<span data-ttu-id="8a165-124">Yerleşik doğrulama normal ifade desenleri ayarlama yapmanız durumunda, lütfen [belgeleri izleyin](https://jqueryvalidation.org/jQuery.validator.methods/).</span><span class="sxs-lookup"><span data-stu-id="8a165-124">In case you need to adjust the built-in validation regular expression patterns, please [follow the documentation](https://jqueryvalidation.org/jQuery.validator.methods/).</span></span>

<span data-ttu-id="8a165-125">**ÖNEMLİ NOT GEREKLİ YÖNTEMİ HAKKINDA; EYLEM**.</span><span class="sxs-lookup"><span data-stu-id="8a165-125">**IMPORTANT NOTE ABOUT REQUIRED METHOD**.</span></span> <span data-ttu-id="8a165-126">1.14.0 sürümden itibaren bu eklentiyi eklenen öğenin değerini kırpmayı beyaz boşlukları durdurur.</span><span class="sxs-lookup"><span data-stu-id="8a165-126">As of version 1.14.0 this plugin stops trimming white spaces from the value of the attached element.</span></span> <span data-ttu-id="8a165-127">Aynı sonucu elde etmek istiyorsanız, kullanabileceğiniz [ `normalizer` ](https://jqueryvalidation.org/normalizer/) doğrulama önce bir öğenin değerini dönüştürmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8a165-127">If you want to achieve the same result, you can use the [`normalizer`](https://jqueryvalidation.org/normalizer/) that can be used to transform the value of an element before validation.</span></span> <span data-ttu-id="8a165-128">Bu özellik sürümünden itibaren kullanılabilir `v1.15.0`.</span><span class="sxs-lookup"><span data-stu-id="8a165-128">This feature was available since `v1.15.0`.</span></span> <span data-ttu-id="8a165-129">Diğer bir deyişle, şöyle bir şey yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8a165-129">In other words, you can do something like this:</span></span>
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

## <a name="license"></a><span data-ttu-id="8a165-130">Lisans</span><span class="sxs-lookup"><span data-stu-id="8a165-130">License</span></span>
<span data-ttu-id="8a165-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="8a165-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="8a165-132">MIT lisansı altında lisanslanır.</span><span class="sxs-lookup"><span data-stu-id="8a165-132">Licensed under the MIT license.</span></span>
