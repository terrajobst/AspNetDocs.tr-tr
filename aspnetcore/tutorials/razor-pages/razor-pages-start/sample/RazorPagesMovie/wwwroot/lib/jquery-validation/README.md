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

<span data-ttu-id="5b0fd-101">[![Derleme durumu](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency durumu](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span><span class="sxs-lookup"><span data-stu-id="5b0fd-101">[![Build Status](https://secure.travis-ci.org/jzaefferer/jquery-validation.png)](http://travis-ci.org/jzaefferer/jquery-validation)
[![devDependency Status](https://david-dm.org/jzaefferer/jquery-validation/dev-status.png?theme=shields.io)](https://david-dm.org/jzaefferer/jquery-validation#info=devDependencies)</span></span>

<span data-ttu-id="5b0fd-102">JQuery doğrulama eklentisi, her türden özelleştirmeler uygulamanız gerçekten kolay uyacak şekilde yapma sırasında mevcut formlarınızı değiştirilebilir doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-102">The jQuery Validation Plugin provides drop-in validation for your existing forms, while making all kinds of customizations to fit your application really easy.</span></span>

## <a name="help-the-projecthttppledgiecomcampaigns18159"></a>[<span data-ttu-id="5b0fd-103">Project Yardımı</span><span class="sxs-lookup"><span data-stu-id="5b0fd-103">Help the project</span></span>](http://pledgie.com/campaigns/18159)

<span data-ttu-id="5b0fd-104">[![Project Yardımı](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span><span class="sxs-lookup"><span data-stu-id="5b0fd-104">[![Help the project](http://www.pledgie.com/campaigns/18159.png?skin_name=chrome)](http://pledgie.com/campaigns/18159)</span></span>

<span data-ttu-id="5b0fd-105">Bu proje için Yardım görünüyor!</span><span class="sxs-lookup"><span data-stu-id="5b0fd-105">This project is looking for help!</span></span> <span data-ttu-id="5b0fd-106">[Devam eden pledgie kampanyaya bağışlamaya](http://pledgie.com/campaigns/18159) ve sözcük yayılan yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-106">[You can donate to the ongoing pledgie campaign](http://pledgie.com/campaigns/18159) and help spread the word.</span></span> <span data-ttu-id="5b0fd-107">Eklenti kullandığınız ya da plan kullanmak için bir Bağış - göz önünde bulundurun her miktarda yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-107">If you've used the plugin, or plan to use, consider a donation - any amount will help.</span></span>

<span data-ttu-id="5b0fd-108">Plan için harcadığınız para nasıl bulabileceğinizi [pledgie sayfa](http://pledgie.com/campaigns/18159).</span><span class="sxs-lookup"><span data-stu-id="5b0fd-108">You can find the plan for how to spend the money on the [pledgie page](http://pledgie.com/campaigns/18159).</span></span>

## <a name="get-started"></a><span data-ttu-id="5b0fd-109">Başlarken</span><span class="sxs-lookup"><span data-stu-id="5b0fd-109">Get Started</span></span>

### <a name="downloading-the-prebuilt-files"></a><span data-ttu-id="5b0fd-110">Önceden oluşturulmuş dosyaları indirme</span><span class="sxs-lookup"><span data-stu-id="5b0fd-110">Downloading the prebuilt files</span></span>

<span data-ttu-id="5b0fd-111">Önceden oluşturulmuş dosyaları yüklenebilir http://jqueryvalidation.org/</span><span class="sxs-lookup"><span data-stu-id="5b0fd-111">Prebuilt files can be downloaded from http://jqueryvalidation.org/</span></span>

### <a name="downloading-the-latest-changes"></a><span data-ttu-id="5b0fd-112">En son değişiklikleri indiriliyor</span><span class="sxs-lookup"><span data-stu-id="5b0fd-112">Downloading the latest changes</span></span>

<span data-ttu-id="5b0fd-113">Yayımlanmamış geliştirme dosyaları tarafından alınabilir:</span><span class="sxs-lookup"><span data-stu-id="5b0fd-113">The unreleased development files can be obtained by:</span></span>

 1. <span data-ttu-id="5b0fd-114">[İndirme](https://github.com/jzaefferer/jquery-validation/archive/master.zip) veya bu deponun çatal</span><span class="sxs-lookup"><span data-stu-id="5b0fd-114">[Downloading](https://github.com/jzaefferer/jquery-validation/archive/master.zip) or Forking this repository</span></span>
 2. [<span data-ttu-id="5b0fd-115">Derlemeyi Kur</span><span class="sxs-lookup"><span data-stu-id="5b0fd-115">Setup the build</span></span>](CONTRIBUTING.md#build-setup)
 3. <span data-ttu-id="5b0fd-116">Çalıştırma `grunt` "dağıtım" Dizin oluşturulmuş dosyaları oluşturmak için</span><span class="sxs-lookup"><span data-stu-id="5b0fd-116">Run `grunt` to create the built files in the "dist" directory</span></span>

### <a name="including-it-on-your-page"></a><span data-ttu-id="5b0fd-117">Sayfanızda dahil</span><span class="sxs-lookup"><span data-stu-id="5b0fd-117">Including it on your page</span></span>

<span data-ttu-id="5b0fd-118">JQuery ve eklenti sayfasında bulunur.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-118">Include jQuery and the plugin on a page.</span></span> <span data-ttu-id="5b0fd-119">Doğrulama ve çağırmak için bir form seçip `validate` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-119">Then select a form to validate and call the `validate` method.</span></span>

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

<span data-ttu-id="5b0fd-120">Alternatif olarak jQuery ve eklenti requirejs aracılığıyla modülünüzde içerir.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-120">Alternatively include jQuery and the plugin via requirejs in your module.</span></span>

```js
define(["jquery", "jquery.validate"], function( $ ) {
    $("form").validate();
});
```

<span data-ttu-id="5b0fd-121">Bir kural ayarlama hakkında daha fazla bilgi ve özelleştirmeler [belgelere bakın](http://jqueryvalidation.org/documentation/).</span><span class="sxs-lookup"><span data-stu-id="5b0fd-121">For more information on how to setup a rules and customizations, [check the documentation](http://jqueryvalidation.org/documentation/).</span></span>

## <a name="reporting-issues-and-contributing-code"></a><span data-ttu-id="5b0fd-122">Sorunları bildirme ve kod katkısı</span><span class="sxs-lookup"><span data-stu-id="5b0fd-122">Reporting issues and contributing code</span></span>

<span data-ttu-id="5b0fd-123">Bkz: [katkıda bulunan Kılavuzu](CONTRIBUTING.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-123">See the [Contributing Guidelines](CONTRIBUTING.md) for details.</span></span>

<span data-ttu-id="5b0fd-124">**E-POSTA DOĞRULAMA HAKKINDA ÖNEMLİ BİR NOT**.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-124">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="5b0fd-125">Sürüm 1.12.0 itibarıyla aynı normal ifadeyi bu eklentiyi kullanarak, [HTML5 belirtimi kullanılacak tarayıcılar için önerdiği](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="5b0fd-125">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="5b0fd-126">Biz, onların izinden gitmekten ve aynı denetimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-126">We will follow their lead and use the same check.</span></span> <span data-ttu-id="5b0fd-127">Lütfen belirtimi yanlış olduğunu düşünüyorsanız, sorunu onlara bildirin.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-127">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="5b0fd-128">Farklı gereksinimlere sahip değilse, göz önünde bulundurun [özel bir yöntem kullanılarak](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="5b0fd-128">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="license"></a><span data-ttu-id="5b0fd-129">Lisans</span><span class="sxs-lookup"><span data-stu-id="5b0fd-129">License</span></span>
<span data-ttu-id="5b0fd-130">Copyright &copy; Jörn Zaefferer</span><span class="sxs-lookup"><span data-stu-id="5b0fd-130">Copyright &copy; Jörn Zaefferer</span></span><br>
<span data-ttu-id="5b0fd-131">MIT lisansı altında lisanslanır.</span><span class="sxs-lookup"><span data-stu-id="5b0fd-131">Licensed under the MIT license.</span></span>
