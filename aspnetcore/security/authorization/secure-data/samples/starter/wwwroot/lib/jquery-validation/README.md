---
ms.openlocfilehash: 83a958fe6a8d61becf9f9062e8ad0ff69108b435
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069117"
---
<a name="jquery-validation-pluginhttpjqueryvalidationorg---form-validation-made-easy"></a><span data-ttu-id="f47a9-101">[jQuery doğrulama eklentisi](http://jqueryvalidation.org/) -Form daha kolay doğrulama</span><span class="sxs-lookup"><span data-stu-id="f47a9-101">[jQuery Validation Plugin](http://jqueryvalidation.org/) - Form validation made easy</span></span>
================================

<span data-ttu-id="f47a9-102">[![Derleme durumu](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency durumu](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="f47a9-102">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="f47a9-103">JQuery doğrulama eklentisi, her türden özelleştirmeler uygulamanız gerçekten kolay uyacak şekilde yapma sırasında mevcut formlarınızı değiştirilebilir doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="f47a9-103">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="f47a9-104">Project Yardımı</span><span class="sxs-lookup"><span data-stu-id="f47a9-104">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="f47a9-105">[![Project Yardımı](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="f47a9-105">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="f47a9-106">Bu proje için Yardım görünüyor!</span><span class="sxs-lookup"><span data-stu-id="f47a9-106">This project is looking for help!</span></span> <span data-ttu-id="f47a9-107">[Devam eden pledgie kampanyaya bağışlamaya](http://pledgie.com/campaigns/18159) ve sözcük yayılan yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f47a9-107">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="f47a9-108">Eklenti kullandığınız ya da plan kullanmak için bir Bağış - göz önünde bulundurun her miktarda yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f47a9-108">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="f47a9-109">Plan için harcadığınız para nasıl bulabileceğinizi [pledgie sayfa](http://pledgie.com/campaigns/18159).</span><span class="sxs-lookup"><span data-stu-id="f47a9-109">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="getting-started"></a><span data-ttu-id="f47a9-110">Başlarken</span><span class="sxs-lookup"><span data-stu-id="f47a9-110">Getting Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="f47a9-111">Önceden oluşturulmuş dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="f47a9-111">Downloading the prebuilt files</span></span>

<span data-ttu-id="f47a9-112">Önceden oluşturulmuş dosyaları yüklenebilir http://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="f47a9-112">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="f47a9-113">En son değişiklikleri indiriliyor</span><span class="sxs-lookup"><span data-stu-id="f47a9-113">Downloading the latest changes</span></span>

<span data-ttu-id="f47a9-114">Yayımlanmamış geliştirme dosyaları tarafından alınabilir:</span><span class="sxs-lookup"><span data-stu-id="f47a9-114">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="f47a9-115">[İndirme](https://github.com/jzaefferer/jquery-validation/archive/master.zip) veya bu deponun çatal</span><span class="sxs-lookup"><span data-stu-id="f47a9-115">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="f47a9-116">Derlemeyi Kur</span><span class="sxs-lookup"><span data-stu-id="f47a9-116">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="f47a9-117">Çalıştırma `grunt` "dağıtım" Dizin oluşturulmuş dosyaları oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="f47a9-117">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="f47a9-118">Sayfanızda dahil</span><span class="sxs-lookup"><span data-stu-id="f47a9-118">Including it on your page</span></span>

<span data-ttu-id="f47a9-119">JQuery ve eklenti sayfasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="f47a9-119">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="f47a9-120">Doğrulama ve çağırmak için bir form seçip `validate` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f47a9-120">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="f47a9-121">Alternatif olarak jQuery ve eklenti requirejs aracılığıyla modülünüzde içerir.</span><span class="sxs-lookup"><span data-stu-id="f47a9-121">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="f47a9-122">Bir kural ayarlama hakkında daha fazla bilgi ve özelleştirmeler [belgelere bakın](http://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="f47a9-122">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="f47a9-123">Sorunları bildirme ve kod katkısı</span><span class="sxs-lookup"><span data-stu-id="f47a9-123">Reporting issues and contributing code</span></span>

<span data-ttu-id="f47a9-124">Bkz: [katkıda bulunan Kılavuzu](CONTRIBUTING.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="f47a9-124">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="f47a9-125">**E-POSTA DOĞRULAMA HAKKINDA ÖNEMLİ BİR NOT**.</span><span class="sxs-lookup"><span data-stu-id="f47a9-125">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="f47a9-126">Sürüm 1.12.0 itibarıyla aynı normal ifadeyi bu eklentiyi kullanarak, [HTML5 belirtimi kullanılacak tarayıcılar için önerdiği](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="f47a9-126">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="f47a9-127">Biz, onların izinden gitmekten ve aynı denetimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="f47a9-127">We will follow their lead and use the same check.</span></span> <span data-ttu-id="f47a9-128">Lütfen belirtimi yanlış olduğunu düşünüyorsanız, sorunu onlara bildirin.</span><span class="sxs-lookup"><span data-stu-id="f47a9-128">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="f47a9-129">Farklı gereksinimlere sahip değilse, göz önünde bulundurun [özel bir yöntem kullanılarak](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="f47a9-129">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="f47a9-130">Lisans</span><span class="sxs-lookup"><span data-stu-id="f47a9-130">License</span></span>
<span data-ttu-id="f47a9-131">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="f47a9-131">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="f47a9-132">MIT lisansı altında lisanslanır.</span><span class="sxs-lookup"><span data-stu-id="f47a9-132">Licensed under the MIT license.</span></span>
