---
uid: single-page-application/overview/templates/emberjs-template
title: EmberJS şablonu | Microsoft Docs
author: xqiu
description: EmberJS şablonu
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578507"
---
# <a name="emberjs-template"></a>EmberJS şablonu

[Xınyang Qiu](https://github.com/xqiu) tarafından

> EmberJS MVC şablonu, Nathan Totten, Thiönce Santos ve Xınyang Qiu tarafından yazılmıştır.
> 
> [EmberJS MVC şablonunu indirin](https://go.microsoft.com/fwlink/?LinkId=282647)

EmberJS SPA şablonu, EmberJS kullanarak etkileşimli istemci tarafı Web uygulamalarını hızlıca oluşturmaya başlamanızı sağlayacak şekilde tasarlanmıştır.

"Tek sayfalı uygulama" (SPA), tek bir HTML sayfası yükleyen bir Web uygulaması için genel bir terimdir ve sonra yeni sayfalar yüklemek yerine sayfayı dinamik olarak güncelleştirir. İlk sayfa yüklendikten sonra, SPA, AJAX istekleri aracılığıyla sunucuyla iletişim kuran bir iletişim yükler.

![](emberjs-template/_static/image1.png)

AJAX yeni bir şey değildir, ancak bugün büyük bir Gelişmiş SPA uygulaması oluşturmayı ve bakımını kolaylaştıran JavaScript çerçeveleri vardır. Ayrıca, HTML 5 ve CSS3 zengin Usıs oluşturmayı kolaylaştırır.

EmberJS SPA şablonu, AJAX isteklerindeki sayfa güncelleştirmelerini işlemek için [Ember](http://emberjs.com/) JavaScript kitaplığını kullanır. Ember. js sayfayı en son verilerle eşleştirmek için veri bağlamayı kullanır. Bu şekilde, JSON verilerinde izlenecek ve DOM güncelleştiren koddan herhangi birini yazmanız gerekmez. Bunun yerine, açıklayıcı öznitelikleri HTML 'ye yerleştirerek, Ember. js ' nin verileri nasıl sunulacağı hakkında bilgi alabilirsiniz.

Sunucu tarafında, EmberJS şablonu, [altını gizleme Koutjs Spa şablonuyla](../introduction/knockoutjs-template.md)neredeyse aynıdır. ASP.NET MVC kullanarak, HTML belgelerini ve ASP.NET Web API 'sini istemciden AJAX isteklerini işleyecek şekilde işler. Şablonun bu yönleri hakkında daha fazla bilgi için, [altını gizleme şablonu](../introduction/knockoutjs-template.md) belgelerine bakın. Bu konu, altını gizleme şablonu ve EmberJS şablonu arasındaki farklara odaklanır.

## <a name="create-an-emberjs-spa-template-project"></a>EmberJS SPA şablonu projesi oluşturma

Yukarıdaki Indir düğmesine tıklayarak şablonu indirip yükleyin. Visual Studio 'Yu yeniden başlatmanız gerekebilir.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** bölümünde **Web**' i seçin. Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin. Projeyi adlandırın ve **Tamam**' a tıklayın.

![](emberjs-template/_static/image2.png)

**Yeni proje** sihirbazında **Ember. js Spa projesi**' ni seçin.

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>EmberJS SPA şablonuna genel bakış

EmberJS şablonu, sorunsuz, etkileşimli bir kullanıcı arabirimi oluşturmak için jQuery, Ember. js, Handleçubuklarının. js birleşimini kullanır.

Ember. js, istemci tarafı MVC deseninin kullanıldığı bir JavaScript kitaplığıdır.

- Handleçubuklar şablon oluşturma dilinde yazılmış bir *şablon*, uygulama kullanıcı arabirimini açıklar. Yayın modunda handleçubuklar [derleyicisi](https://github.com/Myslik/csharp-ember-handlebars) , handleçubuklar şablonunu paketleyip derlemek için kullanılır.
- Bir *model* , sunucudan aldığı uygulama verilerini depolar (Todo listeleri ve Yapılacaklar öğeleri).
- *Denetleyici* uygulama durumunu depolar. Denetleyiciler genellikle ilişkili şablonlara model verilerini sunar.
- Bir *Görünüm* uygulamadan temel olayları çevirir ve bunları denetleyiciye geçirir.
- *Yönlendirici* , uygulama durumunu yönetir, URL 'leri ve şablonları eşitlenmiş halde tutun.

Buna ek olarak, Ember veri kitaplığı JSON nesnelerini (sunucudan bir Restıstalı API aracılığıyla elde edilen) ve istemci modellerini eşitlemeye yönelik olarak kullanılabilir.

EmberJS SPA şablonu, betikleri sekiz katmana düzenler:

- WebApi\_Adapter. js, WebApi\_serileştirici. js: Ember veri kitaplığını ASP.NET Web API 'SI ile çalışacak şekilde genişletir.
- Betikler/yardımcılar. js: yeni Ember Handleçubuklarının yardımcıları tanımlar.
- Betikler/App. js: uygulamayı oluşturur ve bağdaştırıcıyı ve serileştiriciyi yapılandırır.
- Betikler/App/modeller/\*. js: modelleri tanımlar.
- Betikler/App/views/\*. js: görünümleri tanımlar.
- Betikler/App/Controllers/\*. js: denetleyicileri tanımlar.
- Betikler/uygulama/rotalar, betikler/App/router. js: yolları tanımlar.
- Şablonlar/\*. HBS: handleçubuklarının şablonlarını tanımlar.

Daha ayrıntılı bilgi için bu betiklerin bazılarına göz atalım.

## <a name="models"></a>Modeller

Modeller, betikler/uygulama/modeller klasöründe tanımlanmıştır. İki model dosyası vardır: TodoItem. js ve todoList. js.

**Todo. model. js** Yapılacaklar listeleri için istemci tarafı (tarayıcı) modellerini tanımlar. İki model sınıfı vardır: TodoItem ve todoList. Ember 'de, modeller DS 'nin alt sınıfları. Modelinizi. Model, özniteliklere sahip özelliklere sahip olabilir:

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

Modeller, diğer modellerle ilişkiler tanımlayabilir:

[!code-css[Main](emberjs-template/samples/sample2.css)]

Modeller, diğer özelliklere bağlanan hesaplanmış özelliklere sahip olabilir:

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

Modeller, gözlemlenen bir özellik değiştiğinde çağrılan gözlemci işlevlerine sahip olabilir:

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>Görünümler

Görünümler, betikler/uygulama/görünümler klasöründe tanımlanmıştır. Bir görünüm, olayları uygulama kullanıcı arabiriminden çevirir. Bir olay işleyicisi, denetleyici işlevlerine geri çağrı yapabilir veya yalnızca veri bağlamını doğrudan çağırabilir.

Örneğin, aşağıdaki kod views/TodoItemEditView. js ' den. Bir girdi metin alanı için olay işlemeyi tanımlar.

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>Denetleyici

Denetleyiciler betikler/uygulamalar/denetleyiciler klasöründe tanımlanmıştır. Tek bir modeli göstermek için `Ember.ObjectController`genişletin:

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

Denetleyici Ayrıca `Ember.ArrayController`genişleterek bir model koleksiyonunu temsil edebilir. Örneğin, TodoListController `todoList` nesneleri dizisini temsil eder. Denetleyici, todoList ID değerine göre sıralamayı azalan sırada yapar:

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

Denetleyici, yeni bir todoList oluşturan ve onu diziye ekleyen `addTodoList`adlı bir işlevi tanımlar. Bu işlevin nasıl çağrıldığını görmek için şablonlar klasöründe todoListTemplate. html adlı şablon dosyasını açın. Aşağıdaki şablon kodu `addTodoList` işleve bir düğme bağlar:

[!code-html[Main](emberjs-template/samples/sample8.html)]

Denetleyici Ayrıca bir hata mesajı tutan `error` özelliğini içerir. Hata iletisini (Ayrıca todoListTemplate. html) görüntüleyen şablon kodu aşağıda verilmiştir:

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>Yollar

Router. js, görüntülenecek yolları ve varsayılan şablonu tanımlar, uygulama durumunu ayarlar ve yolların URL 'Lerini eşler:

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute. js, setupController işlevini geçersiz kılarak TodoListRoute için verileri yükler:

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

Ember, URL 'Leri, yol adlarını, denetleyicileri ve şablonları eşleştirmek için adlandırma kuralları kullanır. Daha fazla bilgi için bkz. EmberJS belgelerindeki [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) .

## <a name="templates"></a>Şablonlar

Şablonlar klasörü dört şablon içerir:

- Application. HBS: uygulama başlatıldığında oluşturulan varsayılan şablon.
- . HBS hakkında: "/About" yolu için şablon.
- index. HBS: kök "/" yolunun şablonu.
- todoList. HBS: "/Todo" yolu için şablon.
- Gezinti çubuğunu \_. HBS: şablon, gezinti menüsünü tanımlar.

Uygulama şablonu, ana sayfa gibi davranır. Yola bağlı olarak içine diğer şablonları eklemek için bir üst bilgi, alt bilgi ve "{{priz}}" içerir. Ember 'de uygulama şablonları hakkında daha fazla bilgi için bkz. [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).

"/TodoList" şablonu iki döngü ifadesi içerir. Dış döngü `{{#each controller}}`ve iç döngü `{{#each todos}}`. Aşağıdaki kod, yerleşik bir `Ember.Checkbox` görünümünü, özelleştirilmiş `App.TodoItemEditView`ve `deleteTodo` eylemine sahip bir bağlantıyı gösterir.

[!code-html[Main](emberjs-template/samples/sample12.html)]

Controllers/HtmlHelperExtensions. cs ' de tanımlanan `HtmlHelperExtensions` sınıfı, Web. config dosyasında **hata ayıklama** **doğru** olarak ayarlandığında şablon dosyalarını önbelleğe almak ve eklemek için bir yardımcı işlevi tanımlar. Bu işlev, views/Home/App. cshtml içinde tanımlanan ASP.NET MVC görünüm dosyasından çağrılır:

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

Bağımsız değişken olmadan çağrılan işlev, Şablonlar klasöründeki tüm şablon dosyalarını işler. Ayrıca, bir alt klasör veya belirli bir şablon dosyası da belirtebilirsiniz.

Web. config dosyasında **hata ayıklama** **false** olduğunda, uygulama "~/paketles/Templates" paket öğesini içerir. Bu paket öğesi Handleçubuklar derleyici kitaplığı kullanılarak BundleConfig.cs 'e eklenir:

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
