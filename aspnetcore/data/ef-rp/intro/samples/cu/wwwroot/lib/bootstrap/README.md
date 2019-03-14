---
ms.openlocfilehash: 3be420696add54094f24424285a905e7e7963bad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069366"
---
# <a name="bootstraphttpgetbootstrapcom"></a>[Önyükleme](http://getbootstrap.com)

[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower sürüm](https://img.shields.io/bower/v/bootstrap.svg)
[![npm sürüm](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![yapı durumu](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap) 
 [ ![devDependency durumu](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![Selenium Test durumu](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)

Önyükleme, şık, kullanımı kolay ve güçlü bir ön uç altyapısıdır tarafından oluşturulan daha hızlı ve kolay web geliştirme için [işareti Otto](https://twitter.com/mdo) ve [Jacob Thornton](https://twitter.com/fat)ve destekleyen [takımÇekirdek](https://github.com/orgs/twbs/people) büyük destek ve topluluk katılımı ile.

Başlamak için kullanıma <http://getbootstrap.com>!


## <a name="table-of-contents"></a>İçindekiler tablosu

* [Hızlı Başlangıç](#quick-start)
* [Hatalar ve özellik istekleri](#bugs-and-feature-requests)
* [Belgeler](#documentation)
* [Katkıda bulunan](#contributing)
* [Topluluk](#community)
* [Sürüm Oluşturma](#versioning)
* [Oluşturucuları](#creators)
* [Telif hakkı ve lisans](#copyright-and-license)


## <a name="quick-start"></a>Hızlı Başlangıç

Birkaç hızlı başlangıç seçenekleri kullanılabilir:

* [En son sürümü indirmek](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).
* Depoyu kopyalama: `git clone https://github.com/twbs/bootstrap.git`.
* İle yükleme [Bower](http://bower.io): `bower install bootstrap`.
* İle yükleme [npm](https://www.npmjs.com): `npm install bootstrap@3`.
* İle yükleme [Meteor](https://www.meteor.com): `meteor add twbs:bootstrap`.
* İle yükleme [Oluşturucusu](https://getcomposer.org): `composer require twbs/bootstrap`.

Okuma [Başlarken sayfası](http://getbootstrap.com/getting-started/) framework içeriği, şablonları ve örnekler ve daha fazla bilgi için.

### <a name="whats-included"></a>Neleri kapsar

İndirme içinde aşağıdaki dizinlerin bulabilirsiniz ve mantıksal olarak genel varlıklar gruplandırma ve hem dosyaları, derlenmiş ve çeşitlemeleri küçültülmüş. Şöyle görürsünüz:

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

Derlenmiş CSS ve JS sağlıyoruz (`bootstrap.*`) derlenmiş işlemlerini ve küçültülmüş CSS ve JS (`bootstrap.min.*`). CSS [kaynak eşlemeleri](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) bazı tarayıcılar geliştirici araçları ile kullanılabilir. İsteğe bağlı bir önyükleme temasının olduğu gibi Glyphicons yazı dahil edilir.


## <a name="bugs-and-feature-requests"></a>Hatalar ve özellik istekleri

Bir hata veya bir özellik isteği var mı? Lütfen ilk önce okuma [sorun yönergeleri](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) ve var olan ve kapalı sorunları arayın. Sorun veya fikir henüz ele alınmamışsa [Lütfen yeni bir sorun açın](https://github.com/twbs/bootstrap/issues/new).

Unutmayın **gerekir özellik istekleri hedef [önyükleme v4](https://github.com/twbs/bootstrap/tree/v4-dev),** önyükleme v3 şimdi bakım modunda olan ve yeni özellikleri devre dışı kapalı. Bu, böylelikle çalışmalarımızın önyükleme v4 odaklanabilirsiniz.


## <a name="documentation"></a>Belgeler

Bu deponun kök dizininde bulunan önyükleme'nın belgeleri ile oluşturulmuş [Jekyll](http://jekyllrb.com) ve genel olarak GitHub sayfalarında barındırılan <http://getbootstrap.com>. Docs da yerel olarak çalıştırılabilir.

### <a name="running-documentation-locally"></a>Yerel olarak çalışan belgeleri

1. Gerekirse, [Jekyll yükleme](http://jekyllrb.com/docs/installation) ve diğer Ruby bağımlılıklarla `bundle install`.
   **Windows kullanıcıları için Not:** Okuma [resmi olmayan bu kılavuzda](http://jekyll-windows.juthilo.com/) sorunsuz çalışmaya Jekyll alınamıyor.
2. Kök `/bootstrap` çalışması dizini `bundle exec jekyll serve` komut satırında.
4. Açık `http://localhost:9001` tarayıcı ve voilà.

Okuyarak Jekyll kullanma hakkında daha fazla bilgi edinin, [belgeleri](http://jekyllrb.com/docs/home/).

### <a name="documentation-for-previous-releases"></a>Önceki sürümlerine yönelik belgeler

V2.3.2 belgelerine yapıldı, şimdilik kullanılabilir <http://getbootstrap.com/2.3.2/> while önyükleme 3 istemeyenler geçiş.

[Önceki sürümlerde](https://github.com/twbs/bootstrap/releases) ve kullanıcıların belgeleri de indirilebilir.


## <a name="contributing"></a>Katkıda bulunan

Lütfen okumak bizim [katkıda bulunan Kılavuzu](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md). Kodlama standartları ve geliştirme ile ilgili notlar sorunları, açmak için yönergeleri içerir.

Çekme isteğiniz JavaScript düzeltme ekleri veya özellikler içeriyorsa, ayrıca, içermelidir [ilgili birim testlerini](https://github.com/twbs/bootstrap/tree/master/js/tests). Tüm HTML ve CSS uyması gereken [kod Kılavuzu](https://github.com/mdo/code-guide), tarafından tutulan [işareti Otto](https://github.com/mdo).

**Önyükleme v3 şimdi kapatmak için yeni özellikler kapalı.** Biz yürüttüğümüz çalışmalar üzerinde odaklanabilmeniz için bakım moduna geçti [önyükleme v4](https://github.com/twbs/bootstrap/tree/v4-dev), framework'ün gelecek. Yeni özellikler eklemek (yerine hataları düzeltmek) çekme istekleri hedef [önyükleme v4 ( `v4-dev` git dalı)](https://github.com/twbs/bootstrap/tree/v4-dev) yerine.

Düzenleyici tercihleri kullanılabilir [Düzenleyicisi yapılandırma](https://github.com/twbs/bootstrap/blob/master/.editorconfig) kolay kullanmak yaygın olarak kullanılan metin düzenleyiciler. Daha fazla bilgi edinin ve eklentileri, indirme <http://editorconfig.org>.


## <a name="community"></a>Topluluk

Önyükleme'nın geliştirme ve proje maintainers ve topluluk üyelerine ile Sohbet güncelleştirmeleri alın.

* İzleyin [ @getbootstrap Twitter'da](https://twitter.com/getbootstrap).
* Okuma ve abone [önyükleme resmi blogu](http://blog.getbootstrap.com).
* Birleştirme [resmi Slack odası](https://bootstrap-slack.herokuapp.com).
* IRC bildirimindeki üyesi ile sohbet edin. Üzerinde `irc.freenode.net` sunucusu, `##bootstrap` kanal.
* Stack Overflow'da Yardım uygulama bulunabilir (etiketli [ `twitter-bootstrap-3` ](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).
* Geliştiriciler, anahtar sözcüğünü kullanması gereken `bootstrap` değiştirin veya önyükleme işlevselliğini aracılığıyla dağıtırken ekleyebileceğiniz paketleri [npm](https://www.npmjs.com/browse/keyword/bootstrap) veya en fazla bulunabilirlik için benzer teslim mekanizması.


## <a name="versioning"></a>Sürüm oluşturma

Bizim sürüm döngüsü ve geriye dönük uyumluluk sağlamak da saydamlık için önyükleme altında korunur [Semantic Versioning yönergeleri](http://semver.org/). Biz bazen hissetmek ancak biz, mümkün olduğunda bu kurallarına uyması.

Bkz: [GitHub Projemizin yayınlar bölümünü](https://github.com/twbs/bootstrap/releases) changelogs için her önyükleme sürümü için. Duyuru postalar üzerinde sürüm [resmi önyükleme blogu](http://blog.getbootstrap.com) her sürümünde yapılan en önemli değişikliklerin özetini içerir.


## <a name="creators"></a>Oluşturucuları

**İşareti Otto**

* <https://twitter.com/mdo>
* <https://github.com/mdo>

**Jacob Thornton**

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a>Telif hakkı ve lisans

Kodu ve belgeler 2011-2016 Twitter, Inc. Telif Hakkı Kod yayımlanan altında [MIT lisansı](https://github.com/twbs/bootstrap/blob/master/LICENSE). Docs yayımlanan altında [Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).
