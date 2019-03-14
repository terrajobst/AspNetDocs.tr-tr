---
ms.openlocfilehash: 3b33bb9bcab1aa7e5438c6fe3f2d7ba0833e7756
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076908"
---
--

## <a name="reporting-an-issue"></a>Bir sorun rapor etme

1. Adresleme sorun tekrarlanabilir olduğundan emin olun.
2. Kullanım http://jsbin.com veya http://jsfiddle.net bir test sayfası sağlamak için.
3. İçinde sorun yeniden hangi tarayıcıları gösterir. **Not: IE uyumluluk modu sorunlarını ele alınması gerekmez. Gerçek bir tarayıcıda test emin olun!**
4. Hangi eklenti sorunu tonun sürümüdür. En son sürüme güncelleştirdikten sonra bu tekrarlanabilir olur.

Belge sorunlarını izlenen ayrıca [jQuery doğrulaması](https://github.com/jzaefferer/jquery-validation/issues) sorun İzleyicisi.
Docs geliştirmek için çekme istekleri, Hoş Geldiniz [jQuery doğrulama docs](https://github.com/jzaefferer/validation-content) depo, ancak.

**E-POSTA DOĞRULAMA HAKKINDA ÖNEMLİ BİR NOT**. Sürüm 1.12.0 itibarıyla aynı normal ifadeyi bu eklentiyi kullanarak, [HTML5 belirtimi kullanılacak tarayıcılar için önerdiği](https://html.spec.whatwg.org/multipage/forms.html#valid-e-mail-address). Biz, onların izinden gitmekten ve aynı denetimi kullanın. Lütfen belirtimi yanlış olduğunu düşünüyorsanız, sorunu onlara bildirin. Farklı gereksinimlere sahip değilse, göz önünde bulundurun [özel bir yöntem kullanılarak](http://jqueryvalidation.org/jQuery.validator.addMethod/).

## <a name="contributing-code"></a>Kod katkısı

Katkıda bulunmak için teşekkürler! Katkınızı geldiğimizi yardımcı olacak bazı yönergeler aşağıda verilmiştir.

1. Adresleme sorun tekrarlanabilir olduğundan emin olun. Bir test sayfası sağlamak için jsbin.com veya jsfiddle.net kullanın.
2. İzleyin [jQuery Stil Kılavuzu](http://contribute.jquery.com/style-guides/js)
3. Ekleme veya güncelleştirme, düzeltme eki birlikte birim testleri. En az bir tarayıcıda (aşağıya bakın) birim testlerini çalıştırın.
4. Çalıştırma `grunt` (aşağıda linting ve diğer birkaç sorun denetlemek için bakın).
5. İşleme iletisi değişikliği açıklayın ve böyle bir bilet başvuru: "Tanıtımları: Dinamik toplamlar tanıtım için sabit bir temsilci hata. Fixes #51". Yeni bir yerelleştirme dosya ekliyorsanız aşağıdaki gibi kullanın: "Yerelleştirme: Eklenen Hırvatça (ik) yerelleştirme"

## <a name="build-setup"></a>Kurulum oluşturun

1. Yükleme [NodeJS](http://nodejs.org).
2. Grunt CLI için yükleme çalıştırarak yükleyin `npm install -g grunt-cli`. Daha fazla ayrıntı, Web sitesinde sunulan http://gruntjs.com/getting-started.
3. NPM bağımlılıkları çalıştırarak yükleyin `npm install`.
4. Derleme artık çalıştırarak çağrılabilir `grunt`.

## <a name="creating-a-new-additional-method"></a>Yeni ek bir yöntem oluşturma

Olduğunuz yazdığınız varsa ek katkıda bulunmak istediğiniz özel yöntemler-methods.js:

1. Dal oluşturma
2. Yeni bir dosya olarak yöntemi ekleme `src/additional`
3. (İsteğe bağlı) Çevirileri için ekleyin `src/localization`
4. Ana dala bir çekme isteği gönderin.

## <a name="unit-tests"></a>Birim testleri

Birim testlerini çalıştırmak için yalnızca açık `test/index.html` tarayıcınızda. Çalıştırdığınız emin `npm install` önce tüm gerekli bağımlılıkları vardır.
Düzeltme geliştirmeye devam ederken bir tarayıcı ile başlayın ve diğerleri karşı yapmadan önce çalıştırın. Genellikle en son Chrome, Firefox, Safari ve Opera ve birkaç zellikleri.

## <a name="documentation"></a>Belgeler

Lütfen belgeleri sorunu bildirin [jQuery doğrulaması](https://github.com/jzaefferer/jquery-validation/issues) sorun İzleyicisi.
Çekme isteğiniz uygulayan veya artı olacağını Genel API değişiklikleri durumda, bir çekme isteği sağlayacağını [jQuery doğrulama docs](https://github.com/jzaefferer/validation-content) depo.

## <a name="linting"></a>Lint uygulama

JSHint ve diğer Araçları'nı çalıştırmak için kullandığınız `grunt`.
