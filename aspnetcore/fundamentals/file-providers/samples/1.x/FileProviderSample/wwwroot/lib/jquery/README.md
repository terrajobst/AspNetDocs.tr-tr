---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067098"
---
# <a name="jquery"></a>jQuery

> jQuery hızlı, küçük ve zengin bir JavaScript Kitaplığı ' dir.

Nasıl başlayacağınızı ve jQuery kullanma hakkında daha fazla bilgi için lütfen bkz [jQuery'nın belgeleri](http://api.jquery.com/).
Kaynak dosyaları ve sorunları için lütfen [jQuery depo](https://github.com/jquery/jquery).

Yükseltme, lütfen bkz [3.3.1 için blog gönderisini](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/). Bu, önceki sürümü ve daha okunabilir bir changelog belirgin farklılıkları içerir.

## <a name="including-jquery"></a>JQuery dahil olmak üzere

JQuery dahil etmek için en yaygın yollarından bazıları aşağıdadır.

### <a name="browser"></a>Tarayıcı

#### <a name="script-tag"></a>Komut dosyası etiketi

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a>Babel

[Babel](http://babeljs.io/) bir sonraki nesil JavaScript derleyicisi. Tarayıcılar henüz bu özellik yerel olarak desteklemiyor olsa da, özellikleri artık, ES6/ES2015 modülleri kullanma olanağı biridir.

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a>Browserify Web

Kullanmak için birkaç yol vardır [Browserify](http://browserify.org/) ve [Web](https://webpack.github.io/). Bu araçları kullanarak daha fazla bilgi için lütfen için karşılık gelen projenin belgelerine bakın. Betikte, jQuery dahil olmak üzere genellikle şu şekilde görünür...

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a>AMD (uyumsuz modül tanımı)

AMD tarayıcı için yerleşik bir modül biçimidir. Daha fazla bilgi için öneririz [require.js belgeleri](http://requirejs.org/docs/whyamd.html).

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a>Düğüm

JQuery de içerecek şekilde [düğüm](nodejs.org), önce npm ile yükleyin.

```sh
npm install jquery
```

Bir pencere bir belgesiyle düğümünde iş jQuery için gereklidir. Böyle bir pencere düğümünde yerel olarak mevcut olduğundan, bir araçları tarafından gibi örnek [jsdom](https://github.com/tmpvar/jsdom). Sınama amacıyla yararlı olabilir.

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```
