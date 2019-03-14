---
ms.openlocfilehash: 3b33bb9bcab1aa7e5438c6fe3f2d7ba0833e7756
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075081"
---
--

## <a name="reporting-an-issue"></a><span data-ttu-id="26a2f-101">Bir sorun rapor etme</span><span class="sxs-lookup"><span data-stu-id="26a2f-101">Reporting an Issue</span></span>

1. <span data-ttu-id="26a2f-102">Adresleme sorun tekrarlanabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="26a2f-102">Make sure the problem you're addressing is reproducible.</span></span>
2. <span data-ttu-id="26a2f-103">Kullanım http://jsbin.com veya http://jsfiddle.net bir test sayfası sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="26a2f-103">Use http://jsbin.com or http://jsfiddle.net to provide a test page.</span></span>
3. <span data-ttu-id="26a2f-104">İçinde sorun yeniden hangi tarayıcıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="26a2f-104">Indicate what browsers the issue can be reproduced in.</span></span> <span data-ttu-id="26a2f-105">**Not: IE uyumluluk modu sorunlarını ele alınması gerekmez. Gerçek bir tarayıcıda test emin olun!**</span><span class="sxs-lookup"><span data-stu-id="26a2f-105">**Note: IE Compatibilty mode issues won't be addressed. Make sure you test in a real browser!**</span></span>
4. <span data-ttu-id="26a2f-106">Hangi eklenti sorunu tonun sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="26a2f-106">What version of the plug-in is the issue reproducible in.</span></span> <span data-ttu-id="26a2f-107">En son sürüme güncelleştirdikten sonra bu tekrarlanabilir olur.</span><span class="sxs-lookup"><span data-stu-id="26a2f-107">Is it reproducible after updating to the latest version.</span></span>

<span data-ttu-id="26a2f-108">Belge sorunlarını izlenen ayrıca [jQuery doğrulaması](https://github.com/jzaefferer/jquery-validation/issues) sorun İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="26a2f-108">Documentation issues are also tracked at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="26a2f-109">Docs geliştirmek için çekme istekleri, Hoş Geldiniz [jQuery doğrulama docs](https://github.com/jzaefferer/validation-content) depo, ancak.</span><span class="sxs-lookup"><span data-stu-id="26a2f-109">Pull Requests to improve the docs are welcome at the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository, though.</span></span>

<span data-ttu-id="26a2f-110">**E-POSTA DOĞRULAMA HAKKINDA ÖNEMLİ BİR NOT**.</span><span class="sxs-lookup"><span data-stu-id="26a2f-110">**IMPORTANT NOTE ABOUT EMAIL VALIDATION**.</span></span> <span data-ttu-id="26a2f-111">Sürüm 1.12.0 itibarıyla aynı normal ifadeyi bu eklentiyi kullanarak, [HTML5 belirtimi kullanılacak tarayıcılar için önerdiği](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span><span class="sxs-lookup"><span data-stu-id="26a2f-111">As of version 1.12.0 this plugin is using the same regular expression that the [HTML5 specification suggests for browsers to use](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address).</span></span> <span data-ttu-id="26a2f-112">Biz, onların izinden gitmekten ve aynı denetimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="26a2f-112">We will follow their lead and use the same check.</span></span> <span data-ttu-id="26a2f-113">Lütfen belirtimi yanlış olduğunu düşünüyorsanız, sorunu onlara bildirin.</span><span class="sxs-lookup"><span data-stu-id="26a2f-113">If you think the specification is wrong, please report the issue to them.</span></span> <span data-ttu-id="26a2f-114">Farklı gereksinimlere sahip değilse, göz önünde bulundurun [özel bir yöntem kullanılarak](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span><span class="sxs-lookup"><span data-stu-id="26a2f-114">If you have different requirements, consider [using a custom method](http://jqueryvalidation.org/jQuery.validator.addMethod/).</span></span>

## <a name="contributing-code"></a><span data-ttu-id="26a2f-115">Kod katkısı</span><span class="sxs-lookup"><span data-stu-id="26a2f-115">Contributing code</span></span>

<span data-ttu-id="26a2f-116">Katkıda bulunmak için teşekkürler!</span><span class="sxs-lookup"><span data-stu-id="26a2f-116">Thanks for contributing!</span></span> <span data-ttu-id="26a2f-117">Katkınızı geldiğimizi yardımcı olacak bazı yönergeler aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="26a2f-117">Here's a few guidelines to help your contribution get landed.</span></span>

1. <span data-ttu-id="26a2f-118">Adresleme sorun tekrarlanabilir olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="26a2f-118">Make sure the problem you're addressing is reproducible.</span></span> <span data-ttu-id="26a2f-119">Bir test sayfası sağlamak için jsbin.com veya jsfiddle.net kullanın.</span><span class="sxs-lookup"><span data-stu-id="26a2f-119">Use jsbin.com or jsfiddle.net to provide a test page.</span></span>
2. <span data-ttu-id="26a2f-120">İzleyin [jQuery Stil Kılavuzu](http://contribute.jquery.com/style-guides/js)</span><span class="sxs-lookup"><span data-stu-id="26a2f-120">Follow the [jQuery style guide](http://contribute.jquery.com/style-guides/js)</span></span>
3. <span data-ttu-id="26a2f-121">Ekleme veya güncelleştirme, düzeltme eki birlikte birim testleri.</span><span class="sxs-lookup"><span data-stu-id="26a2f-121">Add or update unit tests along with your patch.</span></span> <span data-ttu-id="26a2f-122">En az bir tarayıcıda (aşağıya bakın) birim testlerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="26a2f-122">Run the unit tests in at least one browser (see below).</span></span>
4. <span data-ttu-id="26a2f-123">Çalıştırma `grunt` (aşağıda linting ve diğer birkaç sorun denetlemek için bakın).</span><span class="sxs-lookup"><span data-stu-id="26a2f-123">Run `grunt` (see below) to check for linting and a few other issues.</span></span>
5. <span data-ttu-id="26a2f-124">İşleme iletisi değişikliği açıklayın ve böyle bir bilet başvuru: "Tanıtımları: Dinamik toplamlar tanıtım için sabit bir temsilci hata.</span><span class="sxs-lookup"><span data-stu-id="26a2f-124">Describe the change in your commit message and reference the ticket, like this: "Demos: Fixed delegate bug for dynamic-totals demo.</span></span> <span data-ttu-id="26a2f-125">Fixes #51".</span><span class="sxs-lookup"><span data-stu-id="26a2f-125">Fixes #51".</span></span> <span data-ttu-id="26a2f-126">Yeni bir yerelleştirme dosya ekliyorsanız aşağıdaki gibi kullanın: "Yerelleştirme: Eklenen Hırvatça (ik) yerelleştirme"</span><span class="sxs-lookup"><span data-stu-id="26a2f-126">If you're adding a new localization file, use something like this: "Localization: Added croatian (HR) localization"</span></span>

## <a name="build-setup"></a><span data-ttu-id="26a2f-127">Kurulum oluşturun</span><span class="sxs-lookup"><span data-stu-id="26a2f-127">Build setup</span></span>

1. <span data-ttu-id="26a2f-128">Yükleme [NodeJS](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="26a2f-128">Install [NodeJS](http://nodejs.org).</span></span>
2. <span data-ttu-id="26a2f-129">Grunt CLI için yükleme çalıştırarak yükleyin `npm install -g grunt-cli`.</span><span class="sxs-lookup"><span data-stu-id="26a2f-129">Install the Grunt CLI To install by running `npm install -g grunt-cli`.</span></span> <span data-ttu-id="26a2f-130">Daha fazla ayrıntı, Web sitesinde sunulan http://gruntjs.com/getting-started.</span><span class="sxs-lookup"><span data-stu-id="26a2f-130">More details are available on their website http://gruntjs.com/getting-started.</span></span>
3. <span data-ttu-id="26a2f-131">NPM bağımlılıkları çalıştırarak yükleyin `npm install`.</span><span class="sxs-lookup"><span data-stu-id="26a2f-131">Install the NPM dependencies by running `npm install`.</span></span>
4. <span data-ttu-id="26a2f-132">Derleme artık çalıştırarak çağrılabilir `grunt`.</span><span class="sxs-lookup"><span data-stu-id="26a2f-132">The build can now be called by running `grunt`.</span></span>

## <a name="creating-a-new-additional-method"></a><span data-ttu-id="26a2f-133">Yeni ek bir yöntem oluşturma</span><span class="sxs-lookup"><span data-stu-id="26a2f-133">Creating a new Additional Method</span></span>

<span data-ttu-id="26a2f-134">Olduğunuz yazdığınız varsa ek katkıda bulunmak istediğiniz özel yöntemler-methods.js:</span><span class="sxs-lookup"><span data-stu-id="26a2f-134">If you've wrote custom methods that you'd like to contribute to additional-methods.js:</span></span>

1. <span data-ttu-id="26a2f-135">Dal oluşturma</span><span class="sxs-lookup"><span data-stu-id="26a2f-135">Create a branch</span></span>
2. <span data-ttu-id="26a2f-136">Yeni bir dosya olarak yöntemi ekleme `src/additional`</span><span class="sxs-lookup"><span data-stu-id="26a2f-136">Add the method as a new file in `src/additional`</span></span>
3. <span data-ttu-id="26a2f-137">(İsteğe bağlı) Çevirileri için ekleyin `src/localization`</span><span class="sxs-lookup"><span data-stu-id="26a2f-137">(Optional) Add translations to `src/localization`</span></span>
4. <span data-ttu-id="26a2f-138">Ana dala bir çekme isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="26a2f-138">Send a pull request to the master branch.</span></span>

## <a name="unit-tests"></a><span data-ttu-id="26a2f-139">Birim testleri</span><span class="sxs-lookup"><span data-stu-id="26a2f-139">Unit Tests</span></span>

<span data-ttu-id="26a2f-140">Birim testlerini çalıştırmak için yalnızca açık `test/index.html` tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="26a2f-140">To run unit tests, just open `test/index.html` within your browser.</span></span> <span data-ttu-id="26a2f-141">Çalıştırdığınız emin `npm install` önce tüm gerekli bağımlılıkları vardır.</span><span class="sxs-lookup"><span data-stu-id="26a2f-141">Make sure you ran `npm install` before so all required dependencies are available.</span></span>
<span data-ttu-id="26a2f-142">Düzeltme geliştirmeye devam ederken bir tarayıcı ile başlayın ve diğerleri karşı yapmadan önce çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="26a2f-142">Start with one browser while developing the fix, then run against others before committing.</span></span> <span data-ttu-id="26a2f-143">Genellikle en son Chrome, Firefox, Safari ve Opera ve birkaç zellikleri.</span><span class="sxs-lookup"><span data-stu-id="26a2f-143">Usually latest Chrome, Firefox, Safari and Opera and a few IEs.</span></span>

## <a name="documentation"></a><span data-ttu-id="26a2f-144">Belgeler</span><span class="sxs-lookup"><span data-stu-id="26a2f-144">Documentation</span></span>

<span data-ttu-id="26a2f-145">Lütfen belgeleri sorunu bildirin [jQuery doğrulaması](https://github.com/jzaefferer/jquery-validation/issues) sorun İzleyicisi.</span><span class="sxs-lookup"><span data-stu-id="26a2f-145">Please report documentation issues at the [jQuery Validation](https://github.com/jzaefferer/jquery-validation/issues) issue tracker.</span></span>
<span data-ttu-id="26a2f-146">Çekme isteğiniz uygulayan veya artı olacağını Genel API değişiklikleri durumda, bir çekme isteği sağlayacağını [jQuery doğrulama docs](https://github.com/jzaefferer/validation-content) depo.</span><span class="sxs-lookup"><span data-stu-id="26a2f-146">In case your pull request implements or changes public API it would be a plus you would provide a pull request against the [jQuery Validation docs](https://github.com/jzaefferer/validation-content) repository.</span></span>

## <a name="linting"></a><span data-ttu-id="26a2f-147">Lint uygulama</span><span class="sxs-lookup"><span data-stu-id="26a2f-147">Linting</span></span>

<span data-ttu-id="26a2f-148">JSHint ve diğer Araçları'nı çalıştırmak için kullandığınız `grunt`.</span><span class="sxs-lookup"><span data-stu-id="26a2f-148">To run JSHint and other tools, use `grunt`.</span></span>
