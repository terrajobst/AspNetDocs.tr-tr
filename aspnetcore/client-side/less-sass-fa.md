---
title: Daha az, Sass ve Font Awesome ASP.NET Core
author: ardalis
description: ASP.NET Core uygulamalarında daha az, Sass ve Font Awesome kullanmayı öğrenin.
ms.author: tdykstra
ms.date: 10/14/2016
uid: client-side/less-sass-fa
ms.openlocfilehash: 2229c4e3b0238ff17c15e78f657b9acb10495c72
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57078336"
---
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a>Daha az, Sass ve Font Awesome ASP.NET Core

Tarafından [Steve Smith](https://ardalis.com/)

Stil ve genel deneyimi söz konusu olduğunda kullanıcılar web uygulamalarının giderek daha yüksek beklentileri var. Modern web uygulamaları, zengin Araçlar ve çerçeveler tanımlama ve kendi görünüm tutarlı bir şekilde yönetmek için sık yararlanın. Çerçeveleri ister [önyükleme](http://getbootstrap.com/) stilleri ve düzen seçeneklerini web siteleri için ortak bir dizi tanımlama yönelik uzun yol gidebilirsiniz. Ancak, çoğu Önemsiz olmayan siteler ayrıca sitenin arabirimi daha sezgisel hale gelmesine yardımcı resmi olmayan simgeler için kolay erişim sahibi olmayı yanı sıra etkili bir şekilde tanımlayabilir ve stilleri ve geçişli stil sayfası (CSS) dosyaları işaretleyebilmesine şunlardan yararlanabilirsiniz. Olduğu yer diller ve Destek Araçları [daha az](http://lesscss.org/) ve [Sass](http://sass-lang.com/), kitaplıkları gibi [Font Awesome](http://fontawesome.io/), vardır.

## <a name="css-preprocessor-languages"></a>CSS önişlemci dilleri

Diğer dillere temel alınan diliyle çalışmanın deneyimini geliştirmek için derlenmiş dillerde önişlemcilerini adlandırılır. CSS için iki popüler önişlemcilerini vardır: Daha az ve Sass.  Bu önişlemcilerini değişkenleri ve sürdürülebilirliği büyük, karmaşık stil sayfaları geliştirmeye iç içe kuralları desteği gibi CSS için özellikler ekleyin. Değişkenleri olarak basit bir şey için bile desteği olmayan bir dil olarak CSS oldukça basittir ve bu CSS dosyaları yinelenen ve bloated hale gelir. Gerçek programlama dili özelliklerini önişlemcilerini aracılığıyla ekleme azaltmak ve daha iyi kuruluş Stil kurallarının yardımcı olabilir. Visual Studio hem de daha az için yerleşik destek ve Sass yanı sıra, bu dilleriyle çalışırken geliştirme deneyimi daha da artırabilirsiniz uzantıları sağlar.

Bu CSS önişlemcilerini okunabilirlik ve sürdürülebilirliği stil bilgilerinin nasıl geliştireceğiniz hızlı örnek olarak göz önünde bulundurun:

```css
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    color: black;
    font-weight: bold;
    font-size: 14px;
    font-family: Helvetica, Arial, sans-serif;
}
```

Daha az kullanarak, bu çoğaltma, tüm ortadan kaldırmak için yazılabilir kullanarak bir *mixin* ("karışımını" izin verdiğinden, bu nedenle adlı bir sınıf veya içinde başka bir kural kümesi özelliklerini):

```less
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    .header;
    font-size: 14px;
}
```

## <a name="less"></a>daha az

Node.js kullanarak daha az CSS önişlemci çalıştırır. Daha az yüklemek için bir komut istemi'nden düğüm paketi yöneticisini (npm) kullanın (-g anlamına gelir "Genel"):

```console
npm install -g less
```

Visual Studio kullanıyorsanız, projenize bir veya daha fazla Less dosyaları ekleyerek ve ardından derleme zamanında işlenecek Gulp (veya Grunt) yapılandırma daha az başlayabilirsiniz. Ekleme bir *stilleri* projenize, klasör ve ardından yeni bir Less dosyası adlı ekleyin *main.less* bu klasöre.

![Less dosyası Ekle](less-sass-fa/_static/add-less-file.png)

Klasör yapınız eklendikten sonra aşağıdakine benzer görünmelidir:

![klasör yapısı](less-sass-fa/_static/folder-structure.png)

Şimdi bazı temel stil CSS'ye derlenen ve wwwroot klasörü Gulp tarafından dağıtılan dosyasına ekleyebilirsiniz.

Değiştirme *main.less* basit renk paleti tek bir temel renk oluşturan aşağıdaki içerik dahil etmek.

```less
@base: #663333;
@background: spin(@base, 180);
@lighter: lighten(spin(@base, 5), 10%);
@lighter2: lighten(spin(@base, 10), 20%);
@darker: darken(spin(@base, -5), 10%);
@darker2: darken(spin(@base, -10), 20%);

body {
    background-color:@background;
}
.baseColor  {color:@base}
.bgLight    {color:@lighter}
.bgLight2   {color:@lighter2}
.bgDark     {color:@darker}
.bgDark2    {color:@darker2}
```

`@base` ve diğer @-prefixed değişkenleri öğelerdir. Bunların her biri, bir rengi temsil eder. Dışında `@base`, renk işlevlerini kullanarak şey: rengini koyu ve çalıştırın. Rengini ve koyu tarayıcınızdaki beklediğiniz; yapın döndürme (etrafında renk Tekerlek) derece sayısına göre bir renk tonunu ayarlar. Bu değişkenlerin nasıl çalıştığını göstermek için herhangi bir yerde kullanmak yüzden kullanılmaz, değişkenleri yok saymak akıllı daha az işlemci. Sınıfları `.baseColor`, vb. her üretilen CSS dosyası değişkenlerinin hesaplanan değerler gösterilmektedir.

### <a name="get-started"></a>Kullanmaya başlayın

Oluşturma bir **npm yapılandırma dosyası** (*package.json*) proje klasörünüzde ve başvurmak için düzenleyin `gulp` ve `gulp-less`:

```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "3.9.1",
    "gulp-less": "3.3.0"
  }
}
```

Proje klasörünüzdeki ya da Visual Studio'da ya da bir komut isteminde bağımlılıkları yükler **Çözüm Gezgini** (**bağımlılıkları > npm > paket geri yükleme**).

```console
npm install
```

![VS paketleri geri yükle](less-sass-fa/_static/restore-packages.png)

Proje klasöründe, oluşturun bir **Gulp yapılandırma dosyası** (*gulpfile.js*) otomatik işlemleri tanımlamak için.  Bir değişken, daha az temsil etmek için dosya ve daha az çalışacak bir görev en üstüne ekleyin:

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less");

gulp.task("less", function () {
  return gulp.src('Styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('wwwroot/css'));
});
```

Açık **görev Çalıştırıcı Gezgini** (**Görünüm > diğer Windows > Görev Çalıştırıcı Gezgini**). Görevler arasında adlı yeni bir görev görmelisiniz `less`. Penceresini yenilemeniz gerekebilir.

Çalıştırma `less` görev ve burada gösterilen öğeleri için benzer bir çıktı bakın:

![daha az görev Çalıştırıcı](less-sass-fa/_static/less-task-runner.png)

*Wwwroot/css* klasörü, artık yeni bir dosya içerir *main.css*:

![oluşturulan ana css](less-sass-fa/_static/main-css-created.png)

Açık *main.css* ve aşağıdaki gibi bir şey görürsünüz:

```css
body {
    background-color: #336666;
}
.baseColor {
    color: #663333;
}
.bgLight {
    color: #884a44;
}
.bgLight2 {
    color: #aa6355;
}
.bgDark {
    color: #442225;
}
.bgDark2 {
    color: #221114;
}
```

Basit bir HTML sayfasına ekleme *wwwroot* klasörü ve başvuru *main.css* renk paletini iş başında görmek için.

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="css/main.css" rel="stylesheet" />
    <title></title>
</head>
<body>
    <div>
        <div class="baseColor">BaseColor</div>
        <div class="bgLight">Light</div>
        <div class="bgLight2">Light2</div>
        <div class="bgDark">Dark</div>
        <div class="bgDark2">Dark2</div>
    </div>
</body>
</html>
```

Gördüğünüz 180 derece üzerinde döndürme `@base` üretmek için kullanılan `@background` rengini zıt renk tekerleği içinde sonuçlandı `@base`:

![daha az test örneği](less-sass-fa/_static/less-test-screenshot.png)

Daha az Ayrıca iç içe kuralları, yanı sıra iç içe ortam sorguları destekler. Örneğin, menüler ayrıntılı CSS kurallarını sonuçlanabilir gibi iç içe Hiyerarşiler tanımlama, bunlar gibi:

```css
nav {
    height: 40px;
    width: 100%;
}
nav li {
    height: 38px;
    width: 100px;
}
nav li a:link {
    color: #000;
    text-decoration: none;
}
nav li a:visited {
    text-decoration: none;
    color: #CC3333;
}
nav li a:hover {
    text-decoration: underline;
    font-weight: bold;
}
nav li a:active {
    text-decoration: underline;
}
```

İdeal olarak tüm ilgili Stil kurallarının birlikte CSS dosyası içinde yer alır, ancak uygulamada bir şey yok kuralı ve belki de blok açıklama dışında bu kural zorlama.

Daha az kullanarak kurallar tanımlama şöyle görünür:

```less
nav {
    height: 40px;
    width: 100%;
    li {
        height: 38px;
        width: 100px;
        a {
            color: #000;
            &:link { text-decoration:none}
            &:visited { color: #CC3333; text-decoration:none}
            &:hover { text-decoration:underline; font-weight:bold}
            &:active {text-decoration:underline}
        }
    }
}
```

Bu durumda, tüm alt öğelerini unutmayın `nav` kapsamında yer alır. Artık herhangi bir üst öğe tekrarını yoktur (`nav`, `li`, `a`), ve toplam satır sayısı da bıraktı (bazıları, ancak ikinci örnekte aynı satırda bulunan değerleri yerleştirme bir sonuç). Bu kuruluş, tüm kurallar açıkça sınırlanmış bir kapsam içinde belirli bir kullanıcı Arabirimi öğesi için bu durumda görmek için dosyayı geri kalanından küme ayraçları ayarlayın çok yararlı olabilir.

`&` Söz dizimi daha az Seçici, bir özellik olan & Geçerli Seçici üst temsil eden. Bu nedenle, içinde bir {...} blok, `&` temsil eden bir `a` etiketi ve bu nedenle `&:link` eşdeğerdir `a:link`.

Medya sorgular, hızlı yanıt veren tasarımları oluşturmak için son derece yararlıdır de yoğun yineleme ve CSS karmaşıklığı katkıda bulunabilir. Tüm sınıf tanımı içinde farklı yinelenmesi gerekmez daha az sınıfları içinde iç içe ortam sorguların en üst düzey tanır; böylece `@media` öğeleri. Örneğin, hızlı yanıt veren bir menüsünü CSS şöyledir:

```css
.navigation {
    margin-top: 30%;
    width: 100%;
}
@media screen and (min-width: 40em) {
    .navigation {
        margin: 0;
    }
}
@media screen and (min-width: 62em) {
    .navigation {
        width: 960px;
        margin: 0;
    }
}
```

Bu daha az tanımlanabilir:

```less
.navigation {
    margin-top: 30%;
    width: 100%;
    @media screen and (min-width: 40em) {
        margin: 0;
    }
    @media screen and (min-width: 62em) {
        width: 960px;
        margin: 0;
    }
}
```

Başka bir özellik zaten gördük daha az önceden tanımlı değişkenleri oluşturulması stil öznitelikleri izin vererek, matematiksel işlemler desteklemesidir. Bu, temel değişkeni değiştirilebilir ve tüm bağımlı değerlerini otomatik olarak değiştirmek çok daha kolay ilgili stilleri güncelleştirme yapar.

Özellikle büyük siteler için CSS dosyaları (ve bir özellikle medya sorguları kullanılıyorsa), zaman içinde bunlarla çalışmaya zahmetli hale oldukça büyük alma eğilimindedir. Less dosyalarının ardından birlikte kullanarak çekilen ayrı ayrı tanımlanabilir `@import` yönergeleri. Daha az de bireysel CSS dosyaları da aktarmak isterseniz kullanılabilir.

*Mixin'ler* parametreleri kabul edebilir ve ne zaman belirli mixin'ler etkili tanımlamak için bildirim temelli bir yol sağlayan mixin cf biçiminde daha az destekler koşullu mantık. Mixin cf yaygın kullanım renkleri nasıl ışık göre ayarlamak için veya koyu kaynak rengi. Renk için bir parametre kabul eden bir mixin göz önünde bulundurulduğunda, mixin guard Bu rengi temel mixin değiştirmek için kullanılabilir:

```less
.box (@color) when (lightness(@color) >= 50%) {
    background-color: #000;
}
.box (@color) when (lightness(@color) < 50%) {
    background-color: #FFF;
}
.box (@color) {
    color: @color;
}

.feature {
    .box (@base);
}
```

Bizim geçerli verilen `@base` değerini `#663333`, bu daha az betik aşağıdaki CSS oluşturacak:

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

Daha az ek özellikler sağlar, ancak bu, bazı bu gücünü dil ön işleme fikir.

## <a name="sass"></a>Sass

Sass birçok aynı özellikleri, ancak biraz farklı bir sözdizimi için destek sağlayan küçük, benzer. JavaScript yerine, Ruby kullanarak oluşturulur ve böylece farklı kurulum gereksinimleri vardır. Özgün Sass dil küme ayracı veya noktalı virgüllerin kullanmadı, ancak bunun yerine boşluk ve girinti kullanarak kapsamı tanımlanır. Sürümünde Sass 3, yeni bir söz dizimi kullanıma sunulan **SCSS** ("Sassy CSS"). Girintileme düzeyi ve boşluk yok sayar ve bunun yerine, noktalı virgül ve küme ayraçlarının kullanır SCSS, CSS'ye benzerdir.

Sass yüklemek için genellikle, (Macos'ta önceden yüklenmiş) Ruby yüklemeniz ve ardından çalıştırın:

```console
gem install sass
```

Visual Studio kullanıyorsanız, daha az olduğu gibi ancak, Sass ile hemen aynı şekilde kullanmaya başlayabilirsiniz. Açık *package.json* ve "sass gulp" pakete ekleyin `devDependencies`:

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

Ardından, değişiklik *gulpfile.js* sass değişkeni ve Sass dosyalarınızı derlemek ve sonuçları wwwroot klasöre yerleştirmek için bir görev eklemek için:

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less"),
  sass = require("gulp-sass");

// other content removed

gulp.task("sass", function () {
  return gulp.src('Styles/main2.scss')
    .pipe(sass())
    .pipe(gulp.dest('wwwroot/css'));
});
```

Sass dosya eklenebilir mi artık *main2.scss* için *stilleri* projesinin kök klasörü:

![scss dosyası ekleme](less-sass-fa/_static/add-scss-file.png)

Açık *main2.scss* ve aşağıdakileri ekleyin:

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

Tüm dosyaları kaydedin. Yenilediğinizde artık **görev Çalıştırıcı Gezgini**, gördüğünüz bir `sass` görev. Çalıştırın ve konum */wwwroot/css* klasör. Artık bir *main2.css* dosyasıyla bu içerikleri:

```css
body {
    background-color: #CC0000;
}
```

Sass daha az, benzer avantajlar sağlayan yaptığı aynı olan iç içe geçirmeyi destekler. Dosyaları işlevi tarafından bölünebilir ve kullanarak dahil `@import` yönergesi:

```sass
@import 'anotherfile';
```

Sass kullanarak da mixin'ler destekler `@mixin` bunları tanımlamak için anahtar sözcüğü ve `@include` , bu örnekte olduğu gibi içerecek şekilde [sass lang.com](http://sass-lang.com):

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

Mixin'ler yanı sıra Sass ayrıca devralma kavramını başka genişletmek bir sınıf destekler. Bir mixin ancak sonuçları less CSS kodda kavramsal olarak benzer. Kullanılarak gerçekleştirilir `@extend` anahtar sözcüğü. Mixin'ler denemek için aşağıdaki ekleyin, *main2.scss* dosyası:

```sass
@mixin alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @include alert;
    border-color: green;
}

.error {
    @include alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

Çıktıyı inceleyin *main2.css* çalıştırdıktan sonra `sass` görevi **görev Çalıştırıcı Gezgini**:

```css
.success {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    border-color: green;
 }

.error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    color: red;
    border-color: red;
    font-weight: bold;
}
```

Tüm uyarı mixin ortak özelliklerini her sınıfta yinelenir dikkat edin. Geliştirme zamanında çoğaltma ortadan yardımcı olmak için iyi bir iş mixin yaptı ancak yine de CSS gerekli CSS dosyaları - olası bir performans sorununun büyük sonuçta çoğaltma'da, çok sayıda sanal makinesi.

Artık uyarı mixin ile değiştirin. bir `.alert` sınıfı ve değiştirme `@include` için `@extend` (genişletmek hatırlamak `.alert`değil `alert`):

```sass
.alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @extend .alert;
    border-color: green;
}

.error {
    @extend .alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

Sass bir kez daha çalıştırmanız ve sonuçta elde edilen CSS inceleyin:

```css
.alert, .success, .error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    border-color: green;
}

.error {
    color: red;
    border-color: red;
    font-weight: bold;
}
```

Yalnızca birden çok kez olarak gerektiği gibi özellikleri artık tanımlanır ve daha iyi CSS oluşturulur.

Sass, işlevleri ve daha az benzer koşullu mantık işlemleri de içerir. Aslında, iki dil özellikleri oldukça benzerdir.

## <a name="less-or-sass"></a>Daha az veya Sass?

Yine de daha az kullanın veya Sass genellikle daha iyi dair hiçbir fikir birliğine varılmış olan (veya hatta özgün Sass ya da daha yeni SCSS söz dizimi Sass içinde tercih). Muhtemelen en önemli için bir karardır **Bu araçlardan birini kullanın**, yalnızca elle CSS dosyalarınızı kodlama için aygıtlardır. Sonra yaptığınız karar, hem Less ve Sass, iyi bir seçenek olan.

## <a name="font-awesome"></a>Font Awesome

CSS önişlemcilerini ek olarak, başka bir harika stil modern web uygulamaları için Font Awesome kaynaktır. Yazı tipi Başar web uygulamalarınızda serbestçe kullanılabilir 500'den fazla ölçeklenebilir vektör simgeler sağlayan bir araç takımıdır. İlk önyükleme ile çalışacak şekilde tasarlanmıştır ancak bu çerçeve veya herhangi bir JavaScript kitaplıklarını bağımlılığı yoktur.

Font Awesome ile başlamanın en kolay yolu, genel içerik teslim ağı (CDN) konumuna kullanarak başvuru eklemek için verilmiştir:

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

Ayrıca, Visual Studio projenize "bağımlılıklar" ekleyerek, ekleyebileceğiniz *bower.json*:

```json
{
  "name": "ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap": "3.0.0",
    "jquery": "1.10.2",
    "jquery-validation": "1.11.1",
    "jquery-validation-unobtrusive": "3.2.2",
    "hammer.js": "2.0.4",
    "bootstrap-touch-carousel": "0.8.0",
    "Font-Awesome": "4.3.0"
  }
}
```

Bir başvuru Font Awesome sayfasında oluşturduktan sonra simgeler uygulamanıza Font Awesome sınıfları, genellikle "SK-", satır içi HTML öğeleri için ön eki uygulayarak ekleyebilirsiniz (gibi `<span>` veya `<i>`).  Örneğin, basit listeleri ve menüleri aşağıdakine benzer bir kod kullanarak simgeleri ekleyebilirsiniz:

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <link href="lib/font-awesome/css/font-awesome.css" rel="stylesheet" />
</head>
<body>
    <ul class="fa-ul">
        <li><i class="fa fa-li fa-home"></i> Home</li>
        <li><i class="fa fa-li fa-cog"></i> Settings</li>
    </ul>
</body>
</html>
```

Bu aşağıdaki tarayıcıda oluşturur - her öğenin yanındaki simgeye dikkat edin:

![Liste simgeleri](less-sass-fa/_static/list-icons-screenshot.png)

Burada kullanılabilir simgeler tam bir listesini görüntüleyebilirsiniz:

http://fontawesome.io/icons/

## <a name="summary"></a>Özet

Modern web uygulamaları, temiz, sezgisel ve kullanımı kolay cihazları çeşitli duyarlı, akıcı tasarımları giderek daha fazla isteğe bağlı. Bu hedeflere ulaşmak için gereken CSS stil sayfaları karmaşıklığı yönetme önişlemci LIKE daha az kullanarak veya Sass en iyi şekilde yapılır. Ayrıca, araç Setleri Font Awesome gibi iyi bilinen metin gezinti menüleri simgeleri hızla sağlayın ve uygulamanızı düğmeleri, geliştirme genel kullanıcı deneyimini.
