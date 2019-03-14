---
ms.openlocfilehash: f60f934934ae9e16bbd1174959d99aecdbb5833d
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070923"
---
--

<span data-ttu-id="6ee28-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower sürüm](https://img.shields.io/bower/v/bootstrap.svg)
[![npm sürüm](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![yapı durumu](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap) 
 [ ![devDependency durumu](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium Test durumu](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span><span class="sxs-lookup"><span data-stu-id="6ee28-101">[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower version](https://img.shields.io/bower/v/bootstrap.svg)
[![npm version](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![Build Status](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap)
[![devDependency Status](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium Test Status](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)</span></span>

<span data-ttu-id="6ee28-102">Önyükleme, şık, kullanımı kolay ve güçlü bir ön uç altyapısıdır tarafından oluşturulan daha hızlı ve kolay web geliştirme için [işareti Otto](https://twitter.com/mdo) ve [Jacob Thornton](https://twitter.com/fat)ve destekleyen [takımÇekirdek](https://github.com/orgs/twbs/people) büyük destek ve topluluk katılımı ile.</span><span class="sxs-lookup"><span data-stu-id="6ee28-102">Bootstrap is a sleek, intuitive, and powerful front-end framework for faster and easier web development, created by [Mark Otto](https://twitter.com/mdo) and [Jacob Thornton](https://twitter.com/fat), and maintained by the [core team](https://github.com/orgs/twbs/people) with the massive support and involvement of the community.</span></span>

<span data-ttu-id="6ee28-103">Başlamak için kullanıma <http://getbootstrap.com>!</span><span class="sxs-lookup"><span data-stu-id="6ee28-103">To get started, check out <http://getbootstrap.com>!</span></span>


## <a name="table-of-contents"></a><span data-ttu-id="6ee28-104">İçindekiler tablosu</span><span class="sxs-lookup"><span data-stu-id="6ee28-104">Table of contents</span></span>

* [<span data-ttu-id="6ee28-105">Hızlı Başlangıç</span><span class="sxs-lookup"><span data-stu-id="6ee28-105">Quick start</span></span>](#quick-start)
* [<span data-ttu-id="6ee28-106">Hatalar ve özellik istekleri</span><span class="sxs-lookup"><span data-stu-id="6ee28-106">Bugs and feature requests</span></span>](#bugs-and-feature-requests)
* [<span data-ttu-id="6ee28-107">Belgeler</span><span class="sxs-lookup"><span data-stu-id="6ee28-107">Documentation</span></span>](#documentation)
* [<span data-ttu-id="6ee28-108">Katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="6ee28-108">Contributing</span></span>](#contributing)
* [<span data-ttu-id="6ee28-109">Topluluk</span><span class="sxs-lookup"><span data-stu-id="6ee28-109">Community</span></span>](#community)
* [<span data-ttu-id="6ee28-110">Sürüm Oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ee28-110">Versioning</span></span>](#versioning)
* [<span data-ttu-id="6ee28-111">Oluşturucuları</span><span class="sxs-lookup"><span data-stu-id="6ee28-111">Creators</span></span>](#creators)
* [<span data-ttu-id="6ee28-112">Telif hakkı ve lisans</span><span class="sxs-lookup"><span data-stu-id="6ee28-112">Copyright and license</span></span>](#copyright-and-license)


## <a name="quick-start"></a><span data-ttu-id="6ee28-113">Hızlı Başlangıç</span><span class="sxs-lookup"><span data-stu-id="6ee28-113">Quick start</span></span>

<span data-ttu-id="6ee28-114">Birkaç hızlı başlangıç seçenekleri kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="6ee28-114">Several quick start options are available:</span></span>

* <span data-ttu-id="6ee28-115">[En son sürümü indirmek](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).</span><span class="sxs-lookup"><span data-stu-id="6ee28-115">[Download the latest release](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).</span></span>
* <span data-ttu-id="6ee28-116">Depoyu kopyalama: `git clone https://github.com/twbs/bootstrap.git`.</span><span class="sxs-lookup"><span data-stu-id="6ee28-116">Clone the repo: `git clone https://github.com/twbs/bootstrap.git`.</span></span>
* <span data-ttu-id="6ee28-117">İle yükleme [Bower](http://bower.io): `bower install bootstrap`.</span><span class="sxs-lookup"><span data-stu-id="6ee28-117">Install with [Bower](http://bower.io): `bower install bootstrap`.</span></span>
* <span data-ttu-id="6ee28-118">İle yükleme [npm](https://www.npmjs.com): `npm install bootstrap@3`.</span><span class="sxs-lookup"><span data-stu-id="6ee28-118">Install with [npm](https://www.npmjs.com): `npm install bootstrap@3`.</span></span>
* <span data-ttu-id="6ee28-119">İle yükleme [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`.</span><span class="sxs-lookup"><span data-stu-id="6ee28-119">Install with [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`.</span></span>
* <span data-ttu-id="6ee28-120">İle yükleme [Oluşturucusu](https://getcomposer.org): `composer require twbs/bootstrap`.</span><span class="sxs-lookup"><span data-stu-id="6ee28-120">Install with [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.</span></span>

<span data-ttu-id="6ee28-121">Okuma [Başlarken sayfası](http://getbootstrap.com/getting-started/) framework içeriği, şablonları ve örnekler ve daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="6ee28-121">Read the [Getting started page](http://getbootstrap.com/getting-started/) for information on the framework contents, templates and examples, and more.</span></span>

### <a name="whats-included"></a><span data-ttu-id="6ee28-122">Neleri kapsar</span><span class="sxs-lookup"><span data-stu-id="6ee28-122">What's included</span></span>

<span data-ttu-id="6ee28-123">İndirme içinde aşağıdaki dizinlerin bulabilirsiniz ve mantıksal olarak genel varlıklar gruplandırma ve hem dosyaları, derlenmiş ve çeşitlemeleri küçültülmüş.</span><span class="sxs-lookup"><span data-stu-id="6ee28-123">Within the download you'll find the following directories and files, logically grouping common assets and providing both compiled and minified variations.</span></span> <span data-ttu-id="6ee28-124">Şöyle görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="6ee28-124">You'll see something like this:</span></span>

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

<span data-ttu-id="6ee28-125">Derlenmiş CSS ve JS sağlıyoruz (`bootstrap.*`) derlenmiş işlemlerini ve küçültülmüş CSS ve JS (`bootstrap.min.*`).</span><span class="sxs-lookup"><span data-stu-id="6ee28-125">We provide compiled CSS and JS (`bootstrap.*`), as well as compiled and minified CSS and JS (`bootstrap.min.*`).</span></span> <span data-ttu-id="6ee28-126">CSS [kaynak eşlemeleri](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) bazı tarayıcılar geliştirici araçları ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ee28-126">CSS [source maps](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) are available for use with certain browsers' developer tools.</span></span> <span data-ttu-id="6ee28-127">İsteğe bağlı bir önyükleme temasının olduğu gibi Glyphicons yazı dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="6ee28-127">Fonts from Glyphicons are included, as is the optional Bootstrap theme.</span></span>


## <a name="bugs-and-feature-requests"></a><span data-ttu-id="6ee28-128">Hatalar ve özellik istekleri</span><span class="sxs-lookup"><span data-stu-id="6ee28-128">Bugs and feature requests</span></span>

<span data-ttu-id="6ee28-129">Bir hata veya bir özellik isteği var mı?</span><span class="sxs-lookup"><span data-stu-id="6ee28-129">Have a bug or a feature request?</span></span> <span data-ttu-id="6ee28-130">Lütfen ilk önce okuma [sorun yönergeleri](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) ve var olan ve kapalı sorunları arayın.</span><span class="sxs-lookup"><span data-stu-id="6ee28-130">Please first read the [issue guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) and search for existing and closed issues.</span></span> <span data-ttu-id="6ee28-131">Sorun veya fikir henüz ele değil [Lütfen yeni bir sorun açın](https://github.com/twbs/bootstrap/issues/new).</span><span class="sxs-lookup"><span data-stu-id="6ee28-131">If your problem or idea isn't addressed yet, [please open a new issue](https://github.com/twbs/bootstrap/issues/new).</span></span>

<span data-ttu-id="6ee28-132">Unutmayın **gerekir özellik istekleri hedef [önyükleme v4](https://github.com/twbs/bootstrap/tree/v4-dev),** önyükleme v3 şimdi bakım modunda olan ve yeni özellikleri devre dışı kapalı.</span><span class="sxs-lookup"><span data-stu-id="6ee28-132">Note that **feature requests must target [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev),** because Bootstrap v3 is now in maintenance mode and is closed off to new features.</span></span> <span data-ttu-id="6ee28-133">Bu, böylelikle çalışmalarımızın önyükleme v4 odaklanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ee28-133">This is so that we can focus our efforts on Bootstrap v4.</span></span>


## <a name="documentation"></a><span data-ttu-id="6ee28-134">Belgeler</span><span class="sxs-lookup"><span data-stu-id="6ee28-134">Documentation</span></span>

<span data-ttu-id="6ee28-135">Bu deponun kök dizininde bulunan önyükleme'nın belgeleri ile oluşturulmuş [Jekyll](http://jekyllrb.com) ve genel olarak GitHub sayfalarında barındırılan <http://getbootstrap.com>.</span><span class="sxs-lookup"><span data-stu-id="6ee28-135">Bootstrap's documentation, included in this repo in the root directory, is built with [Jekyll](http://jekyllrb.com) and publicly hosted on GitHub Pages at <http://getbootstrap.com>.</span></span> <span data-ttu-id="6ee28-136">Docs da yerel olarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="6ee28-136">The docs may also be run locally.</span></span>

### <a name="running-documentation-locally"></a><span data-ttu-id="6ee28-137">Yerel olarak çalışan belgeleri</span><span class="sxs-lookup"><span data-stu-id="6ee28-137">Running documentation locally</span></span>

1. <span data-ttu-id="6ee28-138">Gerekirse, [Jekyll yükleme](http://jekyllrb.com/docs/installation) ve diğer Ruby bağımlılıklarla `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="6ee28-138">If necessary, [install Jekyll](http://jekyllrb.com/docs/installation) and other Ruby dependencies with `bundle install`.</span></span>
   <span data-ttu-id="6ee28-139">**Windows kullanıcıları için Not:** Okuma [resmi olmayan bu kılavuzda](http://jekyll-windows.juthilo.com/) sorunsuz çalışmaya Jekyll alınamıyor.</span><span class="sxs-lookup"><span data-stu-id="6ee28-139">**Note for Windows users:** Read [this unofficial guide](http://jekyll-windows.juthilo.com/) to get Jekyll up and running without problems.</span></span>
2. <span data-ttu-id="6ee28-140">Kök `/bootstrap` çalışması dizini `bundle exec jekyll serve` komut satırında.</span><span class="sxs-lookup"><span data-stu-id="6ee28-140">From the root `/bootstrap` directory, run `bundle exec jekyll serve` in the command line.</span></span>
4. <span data-ttu-id="6ee28-141">Açık `http://localhost:9001` tarayıcı ve voilà.</span><span class="sxs-lookup"><span data-stu-id="6ee28-141">Open `http://localhost:9001` in your browser, and voilà.</span></span>

<span data-ttu-id="6ee28-142">Okuyarak Jekyll kullanma hakkında daha fazla bilgi edinin, [belgeleri](http://jekyllrb.com/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="6ee28-142">Learn more about using Jekyll by reading its [documentation](http://jekyllrb.com/docs/home/).</span></span>

### <a name="documentation-for-previous-releases"></a><span data-ttu-id="6ee28-143">Önceki sürümlerine yönelik belgeler</span><span class="sxs-lookup"><span data-stu-id="6ee28-143">Documentation for previous releases</span></span>

<span data-ttu-id="6ee28-144">V2.3.2 belgelerine yapıldı, şimdilik kullanılabilir <http://getbootstrap.com/2.3.2/> while önyükleme 3 istemeyenler geçiş.</span><span class="sxs-lookup"><span data-stu-id="6ee28-144">Documentation for v2.3.2 has been made available for the time being at <http://getbootstrap.com/2.3.2/> while folks transition to Bootstrap 3.</span></span>

<span data-ttu-id="6ee28-145">[Önceki sürümlerde](https://github.com/twbs/bootstrap/releases) ve kullanıcıların belgeleri de indirilebilir.</span><span class="sxs-lookup"><span data-stu-id="6ee28-145">[Previous releases](https://github.com/twbs/bootstrap/releases) and their documentation are also available for download.</span></span>


## <a name="contributing"></a><span data-ttu-id="6ee28-146">Katkıda bulunan</span><span class="sxs-lookup"><span data-stu-id="6ee28-146">Contributing</span></span>

<span data-ttu-id="6ee28-147">Lütfen okumak bizim [katkıda bulunan Kılavuzu](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md).</span><span class="sxs-lookup"><span data-stu-id="6ee28-147">Please read through our [contributing guidelines](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md).</span></span> <span data-ttu-id="6ee28-148">Kodlama standartları ve geliştirme ile ilgili notlar sorunları, açmak için yönergeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="6ee28-148">Included are directions for opening issues, coding standards, and notes on development.</span></span>

<span data-ttu-id="6ee28-149">Çekme isteğiniz JavaScript düzeltme ekleri veya özellikler içeriyorsa, ayrıca, içermelidir [ilgili birim testlerini](https://github.com/twbs/bootstrap/tree/master/js/tests).</span><span class="sxs-lookup"><span data-stu-id="6ee28-149">Moreover, if your pull request contains JavaScript patches or features, you must include [relevant unit tests](https://github.com/twbs/bootstrap/tree/master/js/tests).</span></span> <span data-ttu-id="6ee28-150">Tüm HTML ve CSS uyması gereken [kod Kılavuzu](https://github.com/mdo/code-guide), tarafından tutulan [işareti Otto](https://github.com/mdo).</span><span class="sxs-lookup"><span data-stu-id="6ee28-150">All HTML and CSS should conform to the [Code Guide](https://github.com/mdo/code-guide), maintained by [Mark Otto](https://github.com/mdo).</span></span>

<span data-ttu-id="6ee28-151">**Önyükleme v3 şimdi kapatmak için yeni özellikler kapalı.**</span><span class="sxs-lookup"><span data-stu-id="6ee28-151">**Bootstrap v3 is now closed off to new features.**</span></span> <span data-ttu-id="6ee28-152">Biz yürüttüğümüz çalışmalar üzerinde odaklanabilmeniz için bakım moduna geçti [önyükleme v4](https://github.com/twbs/bootstrap/tree/v4-dev), framework'ün gelecek.</span><span class="sxs-lookup"><span data-stu-id="6ee28-152">It has gone into maintenance mode so that we can focus our efforts on [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev), the future of the framework.</span></span> <span data-ttu-id="6ee28-153">Yeni özellikler eklemek (yerine hataları düzeltmek) çekme istekleri hedef [önyükleme v4 ( `v4-dev` git dalı)](https://github.com/twbs/bootstrap/tree/v4-dev) yerine.</span><span class="sxs-lookup"><span data-stu-id="6ee28-153">Pull requests which add new features (rather than fix bugs) should target [Bootstrap v4 (the `v4-dev` git branch)](https://github.com/twbs/bootstrap/tree/v4-dev) instead.</span></span>

<span data-ttu-id="6ee28-154">Düzenleyici tercihleri kullanılabilir [Düzenleyicisi yapılandırma](https://github.com/twbs/bootstrap/blob/master/.editorconfig) kolay kullanmak yaygın olarak kullanılan metin düzenleyiciler.</span><span class="sxs-lookup"><span data-stu-id="6ee28-154">Editor preferences are available in the [editor config](https://github.com/twbs/bootstrap/blob/master/.editorconfig) for easy use in common text editors.</span></span> <span data-ttu-id="6ee28-155">Daha fazla bilgi edinin ve eklentileri, indirme <http://editorconfig.org>.</span><span class="sxs-lookup"><span data-stu-id="6ee28-155">Read more and download plugins at <http://editorconfig.org>.</span></span>


## <a name="community"></a><span data-ttu-id="6ee28-156">Topluluk</span><span class="sxs-lookup"><span data-stu-id="6ee28-156">Community</span></span>

<span data-ttu-id="6ee28-157">Önyükleme'nın geliştirme ve proje maintainers ve topluluk üyelerine ile Sohbet güncelleştirmeleri alın.</span><span class="sxs-lookup"><span data-stu-id="6ee28-157">Get updates on Bootstrap's development and chat with the project maintainers and community members.</span></span>

* <span data-ttu-id="6ee28-158">İzleyin [ @getbootstrap Twitter'da](https://twitter.com/getbootstrap).</span><span class="sxs-lookup"><span data-stu-id="6ee28-158">Follow [@getbootstrap on Twitter](https://twitter.com/getbootstrap).</span></span>
* <span data-ttu-id="6ee28-159">Okuma ve abone [önyükleme resmi blogu](http://blog.getbootstrap.com).</span><span class="sxs-lookup"><span data-stu-id="6ee28-159">Read and subscribe to [The Official Bootstrap Blog](http://blog.getbootstrap.com).</span></span>
* <span data-ttu-id="6ee28-160">Birleştirme [resmi Slack odası](https://bootstrap-slack.herokuapp.com).</span><span class="sxs-lookup"><span data-stu-id="6ee28-160">Join [the official Slack room](https://bootstrap-slack.herokuapp.com).</span></span>
* <span data-ttu-id="6ee28-161">IRC bildirimindeki üyesi ile sohbet edin.</span><span class="sxs-lookup"><span data-stu-id="6ee28-161">Chat with fellow Bootstrappers in IRC.</span></span> <span data-ttu-id="6ee28-162">Üzerinde `irc.freenode.net` sunucusu, `##bootstrap` kanal.</span><span class="sxs-lookup"><span data-stu-id="6ee28-162">On the `irc.freenode.net` server, in the `##bootstrap` channel.</span></span>
* <span data-ttu-id="6ee28-163">Stack Overflow'da Yardım uygulama bulunabilir (etiketli [ `twitter-bootstrap-3` ](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).</span><span class="sxs-lookup"><span data-stu-id="6ee28-163">Implementation help may be found at Stack Overflow (tagged [`twitter-bootstrap-3`](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).</span></span>
* <span data-ttu-id="6ee28-164">Geliştiriciler, anahtar sözcüğünü kullanması gereken `bootstrap` değiştirin veya önyükleme işlevselliğini aracılığıyla dağıtırken ekleyebileceğiniz paketleri [npm](https://www.npmjs.com/browse/keyword/bootstrap) veya en fazla bulunabilirlik için benzer teslim mekanizması.</span><span class="sxs-lookup"><span data-stu-id="6ee28-164">Developers should use the keyword `bootstrap` on packages which modify or add to the functionality of Bootstrap when distributing through [npm](https://www.npmjs.com/browse/keyword/bootstrap) or similar delivery mechanisms for maximum discoverability.</span></span>


## <a name="versioning"></a><span data-ttu-id="6ee28-165">Sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ee28-165">Versioning</span></span>

<span data-ttu-id="6ee28-166">Bizim sürüm döngüsü ve geriye dönük uyumluluk sağlamak da saydamlık için önyükleme altında korunur [Semantic Versioning yönergeleri](http://semver.org/).</span><span class="sxs-lookup"><span data-stu-id="6ee28-166">For transparency into our release cycle and in striving to maintain backward compatibility, Bootstrap is maintained under [the Semantic Versioning guidelines](http://semver.org/).</span></span> <span data-ttu-id="6ee28-167">Biz bazen hissetmek ancak biz, mümkün olduğunda bu kurallarına uyması.</span><span class="sxs-lookup"><span data-stu-id="6ee28-167">Sometimes we screw up, but we'll adhere to those rules whenever possible.</span></span>

<span data-ttu-id="6ee28-168">Bkz: [GitHub Projemizin yayınlar bölümünü](https://github.com/twbs/bootstrap/releases) changelogs için her önyükleme sürümü için.</span><span class="sxs-lookup"><span data-stu-id="6ee28-168">See [the Releases section of our GitHub project](https://github.com/twbs/bootstrap/releases) for changelogs for each release version of Bootstrap.</span></span> <span data-ttu-id="6ee28-169">Duyuru postalar üzerinde sürüm [resmi önyükleme blogu](http://blog.getbootstrap.com) her sürümünde yapılan en önemli değişikliklerin özetini içerir.</span><span class="sxs-lookup"><span data-stu-id="6ee28-169">Release announcement posts on [the official Bootstrap blog](http://blog.getbootstrap.com) contain summaries of the most noteworthy changes made in each release.</span></span>


## <a name="creators"></a><span data-ttu-id="6ee28-170">Oluşturucuları</span><span class="sxs-lookup"><span data-stu-id="6ee28-170">Creators</span></span>

<span data-ttu-id="6ee28-171">**İşareti Otto**</span><span class="sxs-lookup"><span data-stu-id="6ee28-171">**Mark Otto**</span></span>

* <https://twitter.com/mdo>
* <https://github.com/mdo>

<span data-ttu-id="6ee28-172">**Jacob Thornton**</span><span class="sxs-lookup"><span data-stu-id="6ee28-172">**Jacob Thornton**</span></span>

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a><span data-ttu-id="6ee28-173">Telif hakkı ve lisans</span><span class="sxs-lookup"><span data-stu-id="6ee28-173">Copyright and license</span></span>

<span data-ttu-id="6ee28-174">Kodu ve belgeler 2011-2016 Twitter, Inc. Telif Hakkı Kod yayımlanan altında [MIT lisansı](https://github.com/twbs/bootstrap/blob/master/LICENSE).</span><span class="sxs-lookup"><span data-stu-id="6ee28-174">Code and documentation copyright 2011-2016 Twitter, Inc. Code released under [the MIT license](https://github.com/twbs/bootstrap/blob/master/LICENSE).</span></span> <span data-ttu-id="6ee28-175">Docs yayımlanan altında [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).</span><span class="sxs-lookup"><span data-stu-id="6ee28-175">Docs released under [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).</span></span>
