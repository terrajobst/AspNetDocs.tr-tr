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
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a><span data-ttu-id="e9c41-103">Daha az, Sass ve Font Awesome ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="e9c41-103">Less, Sass, and Font Awesome in ASP.NET Core</span></span>

<span data-ttu-id="e9c41-104">Tarafından [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="e9c41-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="e9c41-105">Stil ve genel deneyimi söz konusu olduğunda kullanıcılar web uygulamalarının giderek daha yüksek beklentileri var.</span><span class="sxs-lookup"><span data-stu-id="e9c41-105">Users of web applications have increasingly high expectations when it comes to style and overall experience.</span></span> <span data-ttu-id="e9c41-106">Modern web uygulamaları, zengin Araçlar ve çerçeveler tanımlama ve kendi görünüm tutarlı bir şekilde yönetmek için sık yararlanın.</span><span class="sxs-lookup"><span data-stu-id="e9c41-106">Modern web applications frequently leverage rich tools and frameworks for defining and managing their look and feel in a consistent manner.</span></span> <span data-ttu-id="e9c41-107">Çerçeveleri ister [önyükleme](http://getbootstrap.com/) stilleri ve düzen seçeneklerini web siteleri için ortak bir dizi tanımlama yönelik uzun yol gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9c41-107">Frameworks like [Bootstrap](http://getbootstrap.com/) can go a long way toward defining a common set of styles and layout options for web sites.</span></span> <span data-ttu-id="e9c41-108">Ancak, çoğu Önemsiz olmayan siteler ayrıca sitenin arabirimi daha sezgisel hale gelmesine yardımcı resmi olmayan simgeler için kolay erişim sahibi olmayı yanı sıra etkili bir şekilde tanımlayabilir ve stilleri ve geçişli stil sayfası (CSS) dosyaları işaretleyebilmesine şunlardan yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9c41-108">However, most non-trivial sites also benefit from being able to effectively define and maintain styles and cascading style sheet (CSS) files, as well as having easy access to non-image icons that help make the site's interface more intuitive.</span></span> <span data-ttu-id="e9c41-109">Olduğu yer diller ve Destek Araçları [daha az](http://lesscss.org/) ve [Sass](http://sass-lang.com/), kitaplıkları gibi [Font Awesome](http://fontawesome.io/), vardır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-109">That's where languages and tools that support [Less](http://lesscss.org/) and [Sass](http://sass-lang.com/), and libraries like [Font Awesome](http://fontawesome.io/), come in.</span></span>

## <a name="css-preprocessor-languages"></a><span data-ttu-id="e9c41-110">CSS önişlemci dilleri</span><span class="sxs-lookup"><span data-stu-id="e9c41-110">CSS preprocessor languages</span></span>

<span data-ttu-id="e9c41-111">Diğer dillere temel alınan diliyle çalışmanın deneyimini geliştirmek için derlenmiş dillerde önişlemcilerini adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-111">Languages that are compiled into other languages, in order to improve the experience of working with the underlying language, are referred to as preprocessors.</span></span> <span data-ttu-id="e9c41-112">CSS için iki popüler önişlemcilerini vardır: Daha az ve Sass.</span><span class="sxs-lookup"><span data-stu-id="e9c41-112">There are two popular preprocessors for CSS: Less and Sass.</span></span>  <span data-ttu-id="e9c41-113">Bu önişlemcilerini değişkenleri ve sürdürülebilirliği büyük, karmaşık stil sayfaları geliştirmeye iç içe kuralları desteği gibi CSS için özellikler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e9c41-113">These preprocessors add features to CSS, such as support for variables and nested rules, which improve the maintainability of large, complex stylesheets.</span></span> <span data-ttu-id="e9c41-114">Değişkenleri olarak basit bir şey için bile desteği olmayan bir dil olarak CSS oldukça basittir ve bu CSS dosyaları yinelenen ve bloated hale gelir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-114">CSS as a language is very basic, lacking support even for something as simple as variables, and this tends to make CSS files repetitive and bloated.</span></span> <span data-ttu-id="e9c41-115">Gerçek programlama dili özelliklerini önişlemcilerini aracılığıyla ekleme azaltmak ve daha iyi kuruluş Stil kurallarının yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-115">Adding real programming language features via preprocessors can help reduce duplication and provide better organization of styling rules.</span></span> <span data-ttu-id="e9c41-116">Visual Studio hem de daha az için yerleşik destek ve Sass yanı sıra, bu dilleriyle çalışırken geliştirme deneyimi daha da artırabilirsiniz uzantıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e9c41-116">Visual Studio provides built-in support for both Less and Sass, as well as extensions that can further improve the development experience when working with these languages.</span></span>

<span data-ttu-id="e9c41-117">Bu CSS önişlemcilerini okunabilirlik ve sürdürülebilirliği stil bilgilerinin nasıl geliştireceğiniz hızlı örnek olarak göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="e9c41-117">As a quick example of how preprocessors can improve readability and maintainability of style information, consider this CSS:</span></span>

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

<span data-ttu-id="e9c41-118">Daha az kullanarak, bu çoğaltma, tüm ortadan kaldırmak için yazılabilir kullanarak bir *mixin* ("karışımını" izin verdiğinden, bu nedenle adlı bir sınıf veya içinde başka bir kural kümesi özelliklerini):</span><span class="sxs-lookup"><span data-stu-id="e9c41-118">Using Less, this can be rewritten to eliminate all of the duplication, using a *mixin* (so named because it allows you to "mix in" properties from one class or rule-set into another):</span></span>

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

## <a name="less"></a><span data-ttu-id="e9c41-119">daha az</span><span class="sxs-lookup"><span data-stu-id="e9c41-119">Less</span></span>

<span data-ttu-id="e9c41-120">Node.js kullanarak daha az CSS önişlemci çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-120">The Less CSS preprocessor runs using Node.js.</span></span> <span data-ttu-id="e9c41-121">Daha az yüklemek için bir komut istemi'nden düğüm paketi yöneticisini (npm) kullanın (-g anlamına gelir "Genel"):</span><span class="sxs-lookup"><span data-stu-id="e9c41-121">To install Less, use Node Package Manager (npm) from a command prompt (-g means "global"):</span></span>

```console
npm install -g less
```

<span data-ttu-id="e9c41-122">Visual Studio kullanıyorsanız, projenize bir veya daha fazla Less dosyaları ekleyerek ve ardından derleme zamanında işlenecek Gulp (veya Grunt) yapılandırma daha az başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9c41-122">If you're using Visual Studio, you can get started with Less by adding one or more Less files to your project, and then configuring Gulp (or Grunt) to process them at compile-time.</span></span> <span data-ttu-id="e9c41-123">Ekleme bir *stilleri* projenize, klasör ve ardından yeni bir Less dosyası adlı ekleyin *main.less* bu klasöre.</span><span class="sxs-lookup"><span data-stu-id="e9c41-123">Add a *Styles* folder to your project, and then add a new Less file named *main.less* to this folder.</span></span>

![Less dosyası Ekle](less-sass-fa/_static/add-less-file.png)

<span data-ttu-id="e9c41-125">Klasör yapınız eklendikten sonra aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e9c41-125">Once added, your folder structure should look something like this:</span></span>

![klasör yapısı](less-sass-fa/_static/folder-structure.png)

<span data-ttu-id="e9c41-127">Şimdi bazı temel stil CSS'ye derlenen ve wwwroot klasörü Gulp tarafından dağıtılan dosyasına ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9c41-127">Now you can add some basic styling to the file, which will be compiled into CSS and deployed to the wwwroot folder by Gulp.</span></span>

<span data-ttu-id="e9c41-128">Değiştirme *main.less* basit renk paleti tek bir temel renk oluşturan aşağıdaki içerik dahil etmek.</span><span class="sxs-lookup"><span data-stu-id="e9c41-128">Modify *main.less* to include the following content, which creates a simple color palette from a single base color.</span></span>

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

<span data-ttu-id="e9c41-129">`@base` ve diğer @-prefixed değişkenleri öğelerdir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-129">`@base` and the other @-prefixed items are variables.</span></span> <span data-ttu-id="e9c41-130">Bunların her biri, bir rengi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e9c41-130">Each of them represents a color.</span></span> <span data-ttu-id="e9c41-131">Dışında `@base`, renk işlevlerini kullanarak şey: rengini koyu ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e9c41-131">Except for `@base`, they're set using color functions: lighten, darken, and spin.</span></span> <span data-ttu-id="e9c41-132">Rengini ve koyu tarayıcınızdaki beklediğiniz; yapın döndürme (etrafında renk Tekerlek) derece sayısına göre bir renk tonunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e9c41-132">Lighten and darken do pretty much what you would expect; spin adjusts the hue of a color by a number of degrees (around the color wheel).</span></span> <span data-ttu-id="e9c41-133">Bu değişkenlerin nasıl çalıştığını göstermek için herhangi bir yerde kullanmak yüzden kullanılmaz, değişkenleri yok saymak akıllı daha az işlemci.</span><span class="sxs-lookup"><span data-stu-id="e9c41-133">The Less processor is smart enough to ignore variables that aren't used, so to demonstrate how these variables work, we need to use them somewhere.</span></span> <span data-ttu-id="e9c41-134">Sınıfları `.baseColor`, vb. her üretilen CSS dosyası değişkenlerinin hesaplanan değerler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-134">The classes `.baseColor`, etc. will demonstrate the calculated values of each of the variables in the CSS file that's produced.</span></span>

### <a name="get-started"></a><span data-ttu-id="e9c41-135">Kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="e9c41-135">Get started</span></span>

<span data-ttu-id="e9c41-136">Oluşturma bir **npm yapılandırma dosyası** (*package.json*) proje klasörünüzde ve başvurmak için düzenleyin `gulp` ve `gulp-less`:</span><span class="sxs-lookup"><span data-stu-id="e9c41-136">Create an **npm Configuration File** (*package.json*) in your project folder and edit it to reference `gulp` and `gulp-less`:</span></span>

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

<span data-ttu-id="e9c41-137">Proje klasörünüzdeki ya da Visual Studio'da ya da bir komut isteminde bağımlılıkları yükler **Çözüm Gezgini** (**bağımlılıkları > npm > paket geri yükleme**).</span><span class="sxs-lookup"><span data-stu-id="e9c41-137">Install the dependencies either at a command prompt in your project folder, or in Visual Studio **Solution Explorer** (**Dependencies > npm > Restore packages**).</span></span>

```console
npm install
```

![VS paketleri geri yükle](less-sass-fa/_static/restore-packages.png)

<span data-ttu-id="e9c41-139">Proje klasöründe, oluşturun bir **Gulp yapılandırma dosyası** (*gulpfile.js*) otomatik işlemleri tanımlamak için.</span><span class="sxs-lookup"><span data-stu-id="e9c41-139">In the project folder, create a **Gulp Configuration File** (*gulpfile.js*) to define the automated process.</span></span>  <span data-ttu-id="e9c41-140">Bir değişken, daha az temsil etmek için dosya ve daha az çalışacak bir görev en üstüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e9c41-140">Add a variable at the top of the file to represent Less, and a task to run Less:</span></span>

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

<span data-ttu-id="e9c41-141">Açık **görev Çalıştırıcı Gezgini** (**Görünüm > diğer Windows > Görev Çalıştırıcı Gezgini**).</span><span class="sxs-lookup"><span data-stu-id="e9c41-141">Open the **Task Runner Explorer** (**View > Other Windows > Task Runner Explorer**).</span></span> <span data-ttu-id="e9c41-142">Görevler arasında adlı yeni bir görev görmelisiniz `less`.</span><span class="sxs-lookup"><span data-stu-id="e9c41-142">Among the tasks, you should see a new task named `less`.</span></span> <span data-ttu-id="e9c41-143">Penceresini yenilemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-143">You might have to refresh the window.</span></span>

<span data-ttu-id="e9c41-144">Çalıştırma `less` görev ve burada gösterilen öğeleri için benzer bir çıktı bakın:</span><span class="sxs-lookup"><span data-stu-id="e9c41-144">Run the `less` task, and you see output similar to what is shown here:</span></span>

![daha az görev Çalıştırıcı](less-sass-fa/_static/less-task-runner.png)

<span data-ttu-id="e9c41-146">*Wwwroot/css* klasörü, artık yeni bir dosya içerir *main.css*:</span><span class="sxs-lookup"><span data-stu-id="e9c41-146">The *wwwroot/css* folder now contains a new file, *main.css*:</span></span>

![oluşturulan ana css](less-sass-fa/_static/main-css-created.png)

<span data-ttu-id="e9c41-148">Açık *main.css* ve aşağıdaki gibi bir şey görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="e9c41-148">Open *main.css* and you see something like the following:</span></span>

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

<span data-ttu-id="e9c41-149">Basit bir HTML sayfasına ekleme *wwwroot* klasörü ve başvuru *main.css* renk paletini iş başında görmek için.</span><span class="sxs-lookup"><span data-stu-id="e9c41-149">Add a simple HTML page to the *wwwroot* folder, and reference *main.css* to see the color palette in action.</span></span>

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

<span data-ttu-id="e9c41-150">Gördüğünüz 180 derece üzerinde döndürme `@base` üretmek için kullanılan `@background` rengini zıt renk tekerleği içinde sonuçlandı `@base`:</span><span class="sxs-lookup"><span data-stu-id="e9c41-150">You can see that the 180 degree spin on `@base` used to produce `@background` resulted in the color wheel opposing color of `@base`:</span></span>

![daha az test örneği](less-sass-fa/_static/less-test-screenshot.png)

<span data-ttu-id="e9c41-152">Daha az Ayrıca iç içe kuralları, yanı sıra iç içe ortam sorguları destekler.</span><span class="sxs-lookup"><span data-stu-id="e9c41-152">Less also provides support for nested rules, as well as nested media queries.</span></span> <span data-ttu-id="e9c41-153">Örneğin, menüler ayrıntılı CSS kurallarını sonuçlanabilir gibi iç içe Hiyerarşiler tanımlama, bunlar gibi:</span><span class="sxs-lookup"><span data-stu-id="e9c41-153">For example, defining nested hierarchies like menus can result in verbose CSS rules like these:</span></span>

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

<span data-ttu-id="e9c41-154">İdeal olarak tüm ilgili Stil kurallarının birlikte CSS dosyası içinde yer alır, ancak uygulamada bir şey yok kuralı ve belki de blok açıklama dışında bu kural zorlama.</span><span class="sxs-lookup"><span data-stu-id="e9c41-154">Ideally all of the related style rules will be placed together within the CSS file, but in practice there's nothing enforcing this rule except convention and perhaps block comments.</span></span>

<span data-ttu-id="e9c41-155">Daha az kullanarak kurallar tanımlama şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="e9c41-155">Defining these same rules using Less looks like this:</span></span>

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

<span data-ttu-id="e9c41-156">Bu durumda, tüm alt öğelerini unutmayın `nav` kapsamında yer alır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-156">Note that in this case, all of the subordinate elements of `nav` are contained within its scope.</span></span> <span data-ttu-id="e9c41-157">Artık herhangi bir üst öğe tekrarını yoktur (`nav`, `li`, `a`), ve toplam satır sayısı da bıraktı (bazıları, ancak ikinci örnekte aynı satırda bulunan değerleri yerleştirme bir sonuç).</span><span class="sxs-lookup"><span data-stu-id="e9c41-157">There's no longer any repetition of parent elements (`nav`, `li`, `a`), and the total line count has dropped as well (though some of that's a result of putting values on the same lines in the second example).</span></span> <span data-ttu-id="e9c41-158">Bu kuruluş, tüm kurallar açıkça sınırlanmış bir kapsam içinde belirli bir kullanıcı Arabirimi öğesi için bu durumda görmek için dosyayı geri kalanından küme ayraçları ayarlayın çok yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-158">It can be very helpful, organizationally, to see all of the rules for a given UI element within an explicitly bounded scope, in this case set off from the rest of the file by curly braces.</span></span>

<span data-ttu-id="e9c41-159">`&` Söz dizimi daha az Seçici, bir özellik olan & Geçerli Seçici üst temsil eden.</span><span class="sxs-lookup"><span data-stu-id="e9c41-159">The `&` syntax is a Less selector feature, with & representing the current selector parent.</span></span> <span data-ttu-id="e9c41-160">Bu nedenle, içinde bir {...}</span><span class="sxs-lookup"><span data-stu-id="e9c41-160">So, within the a {...}</span></span> <span data-ttu-id="e9c41-161">blok, `&` temsil eden bir `a` etiketi ve bu nedenle `&:link` eşdeğerdir `a:link`.</span><span class="sxs-lookup"><span data-stu-id="e9c41-161">block, `&` represents an `a` tag, and thus `&:link` is equivalent to `a:link`.</span></span>

<span data-ttu-id="e9c41-162">Medya sorgular, hızlı yanıt veren tasarımları oluşturmak için son derece yararlıdır de yoğun yineleme ve CSS karmaşıklığı katkıda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-162">Media queries, extremely useful in creating responsive designs, can also contribute heavily to repetition and complexity in CSS.</span></span> <span data-ttu-id="e9c41-163">Tüm sınıf tanımı içinde farklı yinelenmesi gerekmez daha az sınıfları içinde iç içe ortam sorguların en üst düzey tanır; böylece `@media` öğeleri.</span><span class="sxs-lookup"><span data-stu-id="e9c41-163">Less allows media queries to be nested within classes, so that the entire class definition doesn't need to be repeated within different top-level `@media` elements.</span></span> <span data-ttu-id="e9c41-164">Örneğin, hızlı yanıt veren bir menüsünü CSS şöyledir:</span><span class="sxs-lookup"><span data-stu-id="e9c41-164">For example, here is CSS for a responsive menu:</span></span>

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

<span data-ttu-id="e9c41-165">Bu daha az tanımlanabilir:</span><span class="sxs-lookup"><span data-stu-id="e9c41-165">This can be better defined in Less as:</span></span>

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

<span data-ttu-id="e9c41-166">Başka bir özellik zaten gördük daha az önceden tanımlı değişkenleri oluşturulması stil öznitelikleri izin vererek, matematiksel işlemler desteklemesidir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-166">Another feature of Less that we have already seen is its support for mathematical operations, allowing style attributes to be constructed from pre-defined variables.</span></span> <span data-ttu-id="e9c41-167">Bu, temel değişkeni değiştirilebilir ve tüm bağımlı değerlerini otomatik olarak değiştirmek çok daha kolay ilgili stilleri güncelleştirme yapar.</span><span class="sxs-lookup"><span data-stu-id="e9c41-167">This makes updating related styles much easier, since the base variable can be modified and all dependent values change automatically.</span></span>

<span data-ttu-id="e9c41-168">Özellikle büyük siteler için CSS dosyaları (ve bir özellikle medya sorguları kullanılıyorsa), zaman içinde bunlarla çalışmaya zahmetli hale oldukça büyük alma eğilimindedir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-168">CSS files, especially for large sites (and especially if media queries are being used), tend to get quite large over time, making working with them unwieldy.</span></span> <span data-ttu-id="e9c41-169">Less dosyalarının ardından birlikte kullanarak çekilen ayrı ayrı tanımlanabilir `@import` yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="e9c41-169">Less files can be defined separately, then pulled together using `@import` directives.</span></span> <span data-ttu-id="e9c41-170">Daha az de bireysel CSS dosyaları da aktarmak isterseniz kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-170">Less can also be used to import individual CSS files, as well, if desired.</span></span>

<span data-ttu-id="e9c41-171">*Mixin'ler* parametreleri kabul edebilir ve ne zaman belirli mixin'ler etkili tanımlamak için bildirim temelli bir yol sağlayan mixin cf biçiminde daha az destekler koşullu mantık.</span><span class="sxs-lookup"><span data-stu-id="e9c41-171">*Mixins* can accept parameters, and Less supports conditional logic in the form of mixin guards, which provide a declarative way to define when certain mixins take effect.</span></span> <span data-ttu-id="e9c41-172">Mixin cf yaygın kullanım renkleri nasıl ışık göre ayarlamak için veya koyu kaynak rengi.</span><span class="sxs-lookup"><span data-stu-id="e9c41-172">A common use for mixin guards is to adjust colors based on how light or dark the source color is.</span></span> <span data-ttu-id="e9c41-173">Renk için bir parametre kabul eden bir mixin göz önünde bulundurulduğunda, mixin guard Bu rengi temel mixin değiştirmek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="e9c41-173">Given a mixin that accepts a parameter for color, a mixin guard can be used to modify the mixin based on that color:</span></span>

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

<span data-ttu-id="e9c41-174">Bizim geçerli verilen `@base` değerini `#663333`, bu daha az betik aşağıdaki CSS oluşturacak:</span><span class="sxs-lookup"><span data-stu-id="e9c41-174">Given our current `@base` value of `#663333`, this Less script will produce the following CSS:</span></span>

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

<span data-ttu-id="e9c41-175">Daha az ek özellikler sağlar, ancak bu, bazı bu gücünü dil ön işleme fikir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-175">Less provides a number of additional features, but this should give you some idea of the power of this preprocessing language.</span></span>

## <a name="sass"></a><span data-ttu-id="e9c41-176">Sass</span><span class="sxs-lookup"><span data-stu-id="e9c41-176">Sass</span></span>

<span data-ttu-id="e9c41-177">Sass birçok aynı özellikleri, ancak biraz farklı bir sözdizimi için destek sağlayan küçük, benzer.</span><span class="sxs-lookup"><span data-stu-id="e9c41-177">Sass is similar to Less, providing support for many of the same features, but with slightly different syntax.</span></span> <span data-ttu-id="e9c41-178">JavaScript yerine, Ruby kullanarak oluşturulur ve böylece farklı kurulum gereksinimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-178">It's built using Ruby, rather than JavaScript, and so has different setup requirements.</span></span> <span data-ttu-id="e9c41-179">Özgün Sass dil küme ayracı veya noktalı virgüllerin kullanmadı, ancak bunun yerine boşluk ve girinti kullanarak kapsamı tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-179">The original Sass language didn't use curly braces or semicolons, but instead defined scope using white space and indentation.</span></span> <span data-ttu-id="e9c41-180">Sürümünde Sass 3, yeni bir söz dizimi kullanıma sunulan **SCSS** ("Sassy CSS").</span><span class="sxs-lookup"><span data-stu-id="e9c41-180">In version 3 of Sass, a new syntax was introduced, **SCSS** ("Sassy CSS").</span></span> <span data-ttu-id="e9c41-181">Girintileme düzeyi ve boşluk yok sayar ve bunun yerine, noktalı virgül ve küme ayraçlarının kullanır SCSS, CSS'ye benzerdir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-181">SCSS is similar to CSS in that it ignores indentation levels and whitespace, and instead uses semicolons and curly braces.</span></span>

<span data-ttu-id="e9c41-182">Sass yüklemek için genellikle, (Macos'ta önceden yüklenmiş) Ruby yüklemeniz ve ardından çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e9c41-182">To install Sass, typically you would first install Ruby (pre-installed on macOS), and then run:</span></span>

```console
gem install sass
```

<span data-ttu-id="e9c41-183">Visual Studio kullanıyorsanız, daha az olduğu gibi ancak, Sass ile hemen aynı şekilde kullanmaya başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e9c41-183">However, if you're running Visual Studio, you can get started with Sass in much the same way as you would with Less.</span></span> <span data-ttu-id="e9c41-184">Açık *package.json* ve "sass gulp" pakete ekleyin `devDependencies`:</span><span class="sxs-lookup"><span data-stu-id="e9c41-184">Open *package.json* and add the "gulp-sass" package to `devDependencies`:</span></span>

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

<span data-ttu-id="e9c41-185">Ardından, değişiklik *gulpfile.js* sass değişkeni ve Sass dosyalarınızı derlemek ve sonuçları wwwroot klasöre yerleştirmek için bir görev eklemek için:</span><span class="sxs-lookup"><span data-stu-id="e9c41-185">Next, modify *gulpfile.js* to add a sass variable and a task to compile your Sass files and place the results in the wwwroot folder:</span></span>

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

<span data-ttu-id="e9c41-186">Sass dosya eklenebilir mi artık *main2.scss* için *stilleri* projesinin kök klasörü:</span><span class="sxs-lookup"><span data-stu-id="e9c41-186">Now you can add the Sass file *main2.scss* to the *Styles* folder in the root of the project:</span></span>

![scss dosyası ekleme](less-sass-fa/_static/add-scss-file.png)

<span data-ttu-id="e9c41-188">Açık *main2.scss* ve aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e9c41-188">Open *main2.scss* and add the following:</span></span>

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

<span data-ttu-id="e9c41-189">Tüm dosyaları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e9c41-189">Save all of your files.</span></span> <span data-ttu-id="e9c41-190">Yenilediğinizde artık **görev Çalıştırıcı Gezgini**, gördüğünüz bir `sass` görev.</span><span class="sxs-lookup"><span data-stu-id="e9c41-190">Now when you refresh **Task Runner Explorer**, you see a `sass` task.</span></span> <span data-ttu-id="e9c41-191">Çalıştırın ve konum */wwwroot/css* klasör.</span><span class="sxs-lookup"><span data-stu-id="e9c41-191">Run it, and look in the */wwwroot/css* folder.</span></span> <span data-ttu-id="e9c41-192">Artık bir *main2.css* dosyasıyla bu içerikleri:</span><span class="sxs-lookup"><span data-stu-id="e9c41-192">There's now a *main2.css* file, with these contents:</span></span>

```css
body {
    background-color: #CC0000;
}
```

<span data-ttu-id="e9c41-193">Sass daha az, benzer avantajlar sağlayan yaptığı aynı olan iç içe geçirmeyi destekler.</span><span class="sxs-lookup"><span data-stu-id="e9c41-193">Sass supports nesting in much the same was that Less does, providing similar benefits.</span></span> <span data-ttu-id="e9c41-194">Dosyaları işlevi tarafından bölünebilir ve kullanarak dahil `@import` yönergesi:</span><span class="sxs-lookup"><span data-stu-id="e9c41-194">Files can be split up by function and included using the `@import` directive:</span></span>

```sass
@import 'anotherfile';
```

<span data-ttu-id="e9c41-195">Sass kullanarak da mixin'ler destekler `@mixin` bunları tanımlamak için anahtar sözcüğü ve `@include` , bu örnekte olduğu gibi içerecek şekilde [sass lang.com](http://sass-lang.com):</span><span class="sxs-lookup"><span data-stu-id="e9c41-195">Sass supports mixins as well, using the `@mixin` keyword to define them and `@include` to include them, as in this example from [sass-lang.com](http://sass-lang.com):</span></span>

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

<span data-ttu-id="e9c41-196">Mixin'ler yanı sıra Sass ayrıca devralma kavramını başka genişletmek bir sınıf destekler.</span><span class="sxs-lookup"><span data-stu-id="e9c41-196">In addition to mixins, Sass also supports the concept of inheritance, allowing one class to extend another.</span></span> <span data-ttu-id="e9c41-197">Bir mixin ancak sonuçları less CSS kodda kavramsal olarak benzer.</span><span class="sxs-lookup"><span data-stu-id="e9c41-197">It's conceptually similar to a mixin, but results in less CSS code.</span></span> <span data-ttu-id="e9c41-198">Kullanılarak gerçekleştirilir `@extend` anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="e9c41-198">It's accomplished using the `@extend` keyword.</span></span> <span data-ttu-id="e9c41-199">Mixin'ler denemek için aşağıdaki ekleyin, *main2.scss* dosyası:</span><span class="sxs-lookup"><span data-stu-id="e9c41-199">To try out mixins, add the following to your *main2.scss* file:</span></span>

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

<span data-ttu-id="e9c41-200">Çıktıyı inceleyin *main2.css* çalıştırdıktan sonra `sass` görevi **görev Çalıştırıcı Gezgini**:</span><span class="sxs-lookup"><span data-stu-id="e9c41-200">Examine the output in *main2.css* after running the `sass` task in **Task Runner Explorer**:</span></span>

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

<span data-ttu-id="e9c41-201">Tüm uyarı mixin ortak özelliklerini her sınıfta yinelenir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="e9c41-201">Notice that all of the common properties of the alert mixin are repeated in each class.</span></span> <span data-ttu-id="e9c41-202">Geliştirme zamanında çoğaltma ortadan yardımcı olmak için iyi bir iş mixin yaptı ancak yine de CSS gerekli CSS dosyaları - olası bir performans sorununun büyük sonuçta çoğaltma'da, çok sayıda sanal makinesi.</span><span class="sxs-lookup"><span data-stu-id="e9c41-202">The mixin did a good job of helping eliminate duplication at development time, but it's still creating CSS with a lot of duplication in it, resulting in larger than necessary CSS files - a potential performance issue.</span></span>

<span data-ttu-id="e9c41-203">Artık uyarı mixin ile değiştirin. bir `.alert` sınıfı ve değiştirme `@include` için `@extend` (genişletmek hatırlamak `.alert`değil `alert`):</span><span class="sxs-lookup"><span data-stu-id="e9c41-203">Now replace the alert mixin with a `.alert` class, and change `@include` to `@extend` (remembering to extend `.alert`, not `alert`):</span></span>

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

<span data-ttu-id="e9c41-204">Sass bir kez daha çalıştırmanız ve sonuçta elde edilen CSS inceleyin:</span><span class="sxs-lookup"><span data-stu-id="e9c41-204">Run Sass once more, and examine the resulting CSS:</span></span>

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

<span data-ttu-id="e9c41-205">Yalnızca birden çok kez olarak gerektiği gibi özellikleri artık tanımlanır ve daha iyi CSS oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e9c41-205">Now the properties are defined only as many times as needed, and better CSS is generated.</span></span>

<span data-ttu-id="e9c41-206">Sass, işlevleri ve daha az benzer koşullu mantık işlemleri de içerir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-206">Sass also includes functions and conditional logic operations, similar to Less.</span></span> <span data-ttu-id="e9c41-207">Aslında, iki dil özellikleri oldukça benzerdir.</span><span class="sxs-lookup"><span data-stu-id="e9c41-207">In fact, the two languages' capabilities are very similar.</span></span>

## <a name="less-or-sass"></a><span data-ttu-id="e9c41-208">Daha az veya Sass?</span><span class="sxs-lookup"><span data-stu-id="e9c41-208">Less or Sass?</span></span>

<span data-ttu-id="e9c41-209">Yine de daha az kullanın veya Sass genellikle daha iyi dair hiçbir fikir birliğine varılmış olan (veya hatta özgün Sass ya da daha yeni SCSS söz dizimi Sass içinde tercih).</span><span class="sxs-lookup"><span data-stu-id="e9c41-209">There's still no consensus as to whether it's generally better to use Less or Sass (or even whether to prefer the original Sass or the newer SCSS syntax within Sass).</span></span> <span data-ttu-id="e9c41-210">Muhtemelen en önemli için bir karardır **Bu araçlardan birini kullanın**, yalnızca elle CSS dosyalarınızı kodlama için aygıtlardır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-210">Probably the most important decision is to **use one of these tools**, as opposed to just hand-coding your CSS files.</span></span> <span data-ttu-id="e9c41-211">Sonra yaptığınız karar, hem Less ve Sass, iyi bir seçenek olan.</span><span class="sxs-lookup"><span data-stu-id="e9c41-211">Once you've made that decision, both Less and Sass are good choices.</span></span>

## <a name="font-awesome"></a><span data-ttu-id="e9c41-212">Font Awesome</span><span class="sxs-lookup"><span data-stu-id="e9c41-212">Font Awesome</span></span>

<span data-ttu-id="e9c41-213">CSS önişlemcilerini ek olarak, başka bir harika stil modern web uygulamaları için Font Awesome kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-213">In addition to CSS preprocessors, another great resource for styling modern web applications is Font Awesome.</span></span> <span data-ttu-id="e9c41-214">Yazı tipi Başar web uygulamalarınızda serbestçe kullanılabilir 500'den fazla ölçeklenebilir vektör simgeler sağlayan bir araç takımıdır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-214">Font Awesome is a toolkit that provides over 500 scalable vector icons that can be freely used in your web applications.</span></span> <span data-ttu-id="e9c41-215">İlk önyükleme ile çalışacak şekilde tasarlanmıştır ancak bu çerçeve veya herhangi bir JavaScript kitaplıklarını bağımlılığı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e9c41-215">It was originally designed to work with Bootstrap, but it has no dependency on that framework or on any JavaScript libraries.</span></span>

<span data-ttu-id="e9c41-216">Font Awesome ile başlamanın en kolay yolu, genel içerik teslim ağı (CDN) konumuna kullanarak başvuru eklemek için verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e9c41-216">The easiest way to get started with Font Awesome is to add a reference to it, using its public content delivery network (CDN) location:</span></span>

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

<span data-ttu-id="e9c41-217">Ayrıca, Visual Studio projenize "bağımlılıklar" ekleyerek, ekleyebileceğiniz *bower.json*:</span><span class="sxs-lookup"><span data-stu-id="e9c41-217">You can also add it to your Visual Studio project by adding it to the "dependencies" in *bower.json*:</span></span>

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

<span data-ttu-id="e9c41-218">Bir başvuru Font Awesome sayfasında oluşturduktan sonra simgeler uygulamanıza Font Awesome sınıfları, genellikle "SK-", satır içi HTML öğeleri için ön eki uygulayarak ekleyebilirsiniz (gibi `<span>` veya `<i>`).</span><span class="sxs-lookup"><span data-stu-id="e9c41-218">Once you have a reference to Font Awesome on a page, you can add icons to your application by applying Font Awesome classes, typically prefixed with "fa-", to your inline HTML elements (such as `<span>` or `<i>`).</span></span>  <span data-ttu-id="e9c41-219">Örneğin, basit listeleri ve menüleri aşağıdakine benzer bir kod kullanarak simgeleri ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e9c41-219">For example, you can add icons to simple lists and menus using code like this:</span></span>

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

<span data-ttu-id="e9c41-220">Bu aşağıdaki tarayıcıda oluşturur - her öğenin yanındaki simgeye dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="e9c41-220">This produces the following in the browser - note the icon beside each item:</span></span>

![Liste simgeleri](less-sass-fa/_static/list-icons-screenshot.png)

<span data-ttu-id="e9c41-222">Burada kullanılabilir simgeler tam bir listesini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e9c41-222">You can view a complete list of the available icons here:</span></span>

http://fontawesome.io/icons/

## <a name="summary"></a><span data-ttu-id="e9c41-223">Özet</span><span class="sxs-lookup"><span data-stu-id="e9c41-223">Summary</span></span>

<span data-ttu-id="e9c41-224">Modern web uygulamaları, temiz, sezgisel ve kullanımı kolay cihazları çeşitli duyarlı, akıcı tasarımları giderek daha fazla isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="e9c41-224">Modern web applications increasingly demand responsive, fluid designs that are clean, intuitive, and easy to use from a variety of devices.</span></span> <span data-ttu-id="e9c41-225">Bu hedeflere ulaşmak için gereken CSS stil sayfaları karmaşıklığı yönetme önişlemci LIKE daha az kullanarak veya Sass en iyi şekilde yapılır.</span><span class="sxs-lookup"><span data-stu-id="e9c41-225">Managing the complexity of the CSS stylesheets required to achieve these goals is best done using a preprocessor like Less or Sass.</span></span> <span data-ttu-id="e9c41-226">Ayrıca, araç Setleri Font Awesome gibi iyi bilinen metin gezinti menüleri simgeleri hızla sağlayın ve uygulamanızı düğmeleri, geliştirme genel kullanıcı deneyimini.</span><span class="sxs-lookup"><span data-stu-id="e9c41-226">In addition, toolkits like Font Awesome quickly provide well-known icons to textual navigation menus and buttons, improving the overall user experience of your application.</span></span>
