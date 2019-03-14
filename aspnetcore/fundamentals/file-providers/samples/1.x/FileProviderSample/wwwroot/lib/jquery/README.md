---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067098"
---
# <a name="jquery"></a><span data-ttu-id="6b6e2-101">jQuery</span><span class="sxs-lookup"><span data-stu-id="6b6e2-101">jQuery</span></span>

> <span data-ttu-id="6b6e2-102">jQuery hızlı, küçük ve zengin bir JavaScript Kitaplığı ' dir.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-102">jQuery is a fast, small, and feature-rich JavaScript library.</span></span>

<span data-ttu-id="6b6e2-103">Nasıl başlayacağınızı ve jQuery kullanma hakkında daha fazla bilgi için lütfen bkz [jQuery'nın belgeleri](http://api.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="6b6e2-103">For information on how to get started and how to use jQuery, please see [jQuery's documentation](http://api.jquery.com/).</span></span>
<span data-ttu-id="6b6e2-104">Kaynak dosyaları ve sorunları için lütfen [jQuery depo](https://github.com/jquery/jquery).</span><span class="sxs-lookup"><span data-stu-id="6b6e2-104">For source files and issues, please visit the [jQuery repo](https://github.com/jquery/jquery).</span></span>

<span data-ttu-id="6b6e2-105">Yükseltme, lütfen bkz [3.3.1 için blog gönderisini](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span><span class="sxs-lookup"><span data-stu-id="6b6e2-105">If upgrading, please see the [blog post for 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span></span> <span data-ttu-id="6b6e2-106">Bu, önceki sürümü ve daha okunabilir bir changelog belirgin farklılıkları içerir.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-106">This includes notable differences from the previous version and a more readable changelog.</span></span>

## <a name="including-jquery"></a><span data-ttu-id="6b6e2-107">JQuery dahil olmak üzere</span><span class="sxs-lookup"><span data-stu-id="6b6e2-107">Including jQuery</span></span>

<span data-ttu-id="6b6e2-108">JQuery dahil etmek için en yaygın yollarından bazıları aşağıdadır.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-108">Below are some of the most common ways to include jQuery.</span></span>

### <a name="browser"></a><span data-ttu-id="6b6e2-109">Tarayıcı</span><span class="sxs-lookup"><span data-stu-id="6b6e2-109">Browser</span></span>

#### <a name="script-tag"></a><span data-ttu-id="6b6e2-110">Komut dosyası etiketi</span><span class="sxs-lookup"><span data-stu-id="6b6e2-110">Script tag</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a><span data-ttu-id="6b6e2-111">Babel</span><span class="sxs-lookup"><span data-stu-id="6b6e2-111">Babel</span></span>

<span data-ttu-id="6b6e2-112">[Babel](http://babeljs.io/) bir sonraki nesil JavaScript derleyicisi.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-112">[Babel](http://babeljs.io/) is a next generation JavaScript compiler.</span></span> <span data-ttu-id="6b6e2-113">Tarayıcılar henüz bu özellik yerel olarak desteklemiyor olsa da, özellikleri artık, ES6/ES2015 modülleri kullanma olanağı biridir.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-113">One of the features is the ability to use ES6/ES2015 modules now, even though browsers do not yet support this feature natively.</span></span>

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a><span data-ttu-id="6b6e2-114">Browserify Web</span><span class="sxs-lookup"><span data-stu-id="6b6e2-114">Browserify/Webpack</span></span>

<span data-ttu-id="6b6e2-115">Kullanmak için birkaç yol vardır [Browserify](http://browserify.org/) ve [Web](https://webpack.github.io/).</span><span class="sxs-lookup"><span data-stu-id="6b6e2-115">There are several ways to use [Browserify](http://browserify.org/) and [Webpack](https://webpack.github.io/).</span></span> <span data-ttu-id="6b6e2-116">Bu araçları kullanarak daha fazla bilgi için lütfen için karşılık gelen projenin belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-116">For more information on using these tools, please refer to the corresponding project's documention.</span></span> <span data-ttu-id="6b6e2-117">Betikte, jQuery dahil olmak üzere genellikle şu şekilde görünür...</span><span class="sxs-lookup"><span data-stu-id="6b6e2-117">In the script, including jQuery will usually look like this...</span></span>

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a><span data-ttu-id="6b6e2-118">AMD (uyumsuz modül tanımı)</span><span class="sxs-lookup"><span data-stu-id="6b6e2-118">AMD (Asynchronous Module Definition)</span></span>

<span data-ttu-id="6b6e2-119">AMD tarayıcı için yerleşik bir modül biçimidir.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-119">AMD is a module format built for the browser.</span></span> <span data-ttu-id="6b6e2-120">Daha fazla bilgi için öneririz [require.js belgeleri](http://requirejs.org/docs/whyamd.html).</span><span class="sxs-lookup"><span data-stu-id="6b6e2-120">For more information, we recommend [require.js' documentation](http://requirejs.org/docs/whyamd.html).</span></span>

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a><span data-ttu-id="6b6e2-121">Düğüm</span><span class="sxs-lookup"><span data-stu-id="6b6e2-121">Node</span></span>

<span data-ttu-id="6b6e2-122">JQuery de içerecek şekilde [düğüm](nodejs.org), önce npm ile yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-122">To include jQuery in [Node](nodejs.org), first install with npm.</span></span>

```sh
npm install jquery
```

<span data-ttu-id="6b6e2-123">Bir pencere bir belgesiyle düğümünde iş jQuery için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-123">For jQuery to work in Node, a window with a document is required.</span></span> <span data-ttu-id="6b6e2-124">Böyle bir pencere düğümünde yerel olarak mevcut olduğundan, bir araçları tarafından gibi örnek [jsdom](https://github.com/tmpvar/jsdom).</span><span class="sxs-lookup"><span data-stu-id="6b6e2-124">Since no such window exists natively in Node, one can be mocked by tools such as [jsdom](https://github.com/tmpvar/jsdom).</span></span> <span data-ttu-id="6b6e2-125">Sınama amacıyla yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="6b6e2-125">This can be useful for testing purposes.</span></span>

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
