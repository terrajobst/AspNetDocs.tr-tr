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
# <a name="emberjs-template"></a><span data-ttu-id="c1b5c-103">EmberJS şablonu</span><span class="sxs-lookup"><span data-stu-id="c1b5c-103">EmberJS template</span></span>

<span data-ttu-id="c1b5c-104">[Xınyang Qiu](https://github.com/xqiu) tarafından</span><span class="sxs-lookup"><span data-stu-id="c1b5c-104">by [Xinyang Qiu](https://github.com/xqiu)</span></span>

> <span data-ttu-id="c1b5c-105">EmberJS MVC şablonu, Nathan Totten, Thiönce Santos ve Xınyang Qiu tarafından yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-105">The EmberJS MVC Template is written by Nathan Totten, Thiago Santos, and Xinyang Qiu.</span></span>
> 
> [<span data-ttu-id="c1b5c-106">EmberJS MVC şablonunu indirin</span><span class="sxs-lookup"><span data-stu-id="c1b5c-106">Download the EmberJS MVC Template</span></span>](https://go.microsoft.com/fwlink/?LinkId=282647)

<span data-ttu-id="c1b5c-107">EmberJS SPA şablonu, EmberJS kullanarak etkileşimli istemci tarafı Web uygulamalarını hızlıca oluşturmaya başlamanızı sağlayacak şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-107">The EmberJS SPA template is designed to get you started quickly building interactive client-side web apps using EmberJS.</span></span>

<span data-ttu-id="c1b5c-108">"Tek sayfalı uygulama" (SPA), tek bir HTML sayfası yükleyen bir Web uygulaması için genel bir terimdir ve sonra yeni sayfalar yüklemek yerine sayfayı dinamik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-108">"Single-page application" (SPA) is the general term for a web application that loads a single HTML page and then updates the page dynamically, instead of loading new pages.</span></span> <span data-ttu-id="c1b5c-109">İlk sayfa yüklendikten sonra, SPA, AJAX istekleri aracılığıyla sunucuyla iletişim kuran bir iletişim yükler.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-109">After the initial page load, the SPA talks with the server through AJAX requests.</span></span>

![](emberjs-template/_static/image1.png)

<span data-ttu-id="c1b5c-110">AJAX yeni bir şey değildir, ancak bugün büyük bir Gelişmiş SPA uygulaması oluşturmayı ve bakımını kolaylaştıran JavaScript çerçeveleri vardır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-110">AJAX is nothing new, but today there are JavaScript frameworks that make it easier to build and maintain a large sophisticated SPA application.</span></span> <span data-ttu-id="c1b5c-111">Ayrıca, HTML 5 ve CSS3 zengin Usıs oluşturmayı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-111">Also, HTML 5 and CSS3 are making it easier to create rich UIs.</span></span>

<span data-ttu-id="c1b5c-112">EmberJS SPA şablonu, AJAX isteklerindeki sayfa güncelleştirmelerini işlemek için [Ember](http://emberjs.com/) JavaScript kitaplığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-112">The EmberJS SPA Template uses the [Ember](http://emberjs.com/) JavaScript library to handle page updates from AJAX requests.</span></span> <span data-ttu-id="c1b5c-113">Ember. js sayfayı en son verilerle eşleştirmek için veri bağlamayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-113">Ember.js uses data binding to synchronize the page with the latest data.</span></span> <span data-ttu-id="c1b5c-114">Bu şekilde, JSON verilerinde izlenecek ve DOM güncelleştiren koddan herhangi birini yazmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-114">That way, you don't have to write any of the code that walks through the JSON data and updates the DOM.</span></span> <span data-ttu-id="c1b5c-115">Bunun yerine, açıklayıcı öznitelikleri HTML 'ye yerleştirerek, Ember. js ' nin verileri nasıl sunulacağı hakkında bilgi alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-115">Instead, you put declarative attributes in the HTML that tell Ember.js how to present the data.</span></span>

<span data-ttu-id="c1b5c-116">Sunucu tarafında, EmberJS şablonu, [altını gizleme Koutjs Spa şablonuyla](../introduction/knockoutjs-template.md)neredeyse aynıdır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-116">On the server side, the EmberJS template is almost identical to the [KnockoutJS SPA template](../introduction/knockoutjs-template.md).</span></span> <span data-ttu-id="c1b5c-117">ASP.NET MVC kullanarak, HTML belgelerini ve ASP.NET Web API 'sini istemciden AJAX isteklerini işleyecek şekilde işler.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-117">It uses ASP.NET MVC to serve HTML documents, and ASP.NET Web API to handle AJAX requests from the client.</span></span> <span data-ttu-id="c1b5c-118">Şablonun bu yönleri hakkında daha fazla bilgi için, [altını gizleme şablonu](../introduction/knockoutjs-template.md) belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-118">For more information about those aspects of the template, refer to the [KnockoutJS template](../introduction/knockoutjs-template.md) documentation.</span></span> <span data-ttu-id="c1b5c-119">Bu konu, altını gizleme şablonu ve EmberJS şablonu arasındaki farklara odaklanır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-119">This topic focuses on the differences between the Knockout template and the EmberJS template.</span></span>

## <a name="create-an-emberjs-spa-template-project"></a><span data-ttu-id="c1b5c-120">EmberJS SPA şablonu projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="c1b5c-120">Create an EmberJS SPA Template Project</span></span>

<span data-ttu-id="c1b5c-121">Yukarıdaki Indir düğmesine tıklayarak şablonu indirip yükleyin.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-121">Download and install the template by clicking the Download button above.</span></span> <span data-ttu-id="c1b5c-122">Visual Studio 'Yu yeniden başlatmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-122">You might need to restart Visual Studio.</span></span>

<span data-ttu-id="c1b5c-123">**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-123">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="c1b5c-124">**Görsel C#** bölümünde **Web**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-124">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="c1b5c-125">Proje şablonları listesinde **ASP.NET MVC 4 Web uygulaması**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-125">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="c1b5c-126">Projeyi adlandırın ve **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-126">Name the project and click **OK**.</span></span>

![](emberjs-template/_static/image2.png)

<span data-ttu-id="c1b5c-127">**Yeni proje** sihirbazında **Ember. js Spa projesi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-127">In the **New Project** wizard, select **Ember.js SPA Project**.</span></span>

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a><span data-ttu-id="c1b5c-128">EmberJS SPA şablonuna genel bakış</span><span class="sxs-lookup"><span data-stu-id="c1b5c-128">EmberJS SPA Template Overview</span></span>

<span data-ttu-id="c1b5c-129">EmberJS şablonu, sorunsuz, etkileşimli bir kullanıcı arabirimi oluşturmak için jQuery, Ember. js, Handleçubuklarının. js birleşimini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-129">The EmberJS template uses a combination of jQuery, Ember.js, Handlebars.js to create a smooth, interactive UI.</span></span>

<span data-ttu-id="c1b5c-130">Ember. js, istemci tarafı MVC deseninin kullanıldığı bir JavaScript kitaplığıdır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-130">Ember.js is a JavaScript library that uses a client-side MVC pattern.</span></span>

- <span data-ttu-id="c1b5c-131">Handleçubuklar şablon oluşturma dilinde yazılmış bir *şablon*, uygulama kullanıcı arabirimini açıklar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-131">A *template*, written in the Handlebars templating language, describes the application user interface.</span></span> <span data-ttu-id="c1b5c-132">Yayın modunda handleçubuklar [derleyicisi](https://github.com/Myslik/csharp-ember-handlebars) , handleçubuklar şablonunu paketleyip derlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-132">In release mode, the [Handlebars compiler](https://github.com/Myslik/csharp-ember-handlebars) is used to bundle and compile the handlebars template.</span></span>
- <span data-ttu-id="c1b5c-133">Bir *model* , sunucudan aldığı uygulama verilerini depolar (Todo listeleri ve Yapılacaklar öğeleri).</span><span class="sxs-lookup"><span data-stu-id="c1b5c-133">A *model* stores the application data that it gets from the server (ToDo lists and ToDo items).</span></span>
- <span data-ttu-id="c1b5c-134">*Denetleyici* uygulama durumunu depolar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-134">A *controller* stores application state.</span></span> <span data-ttu-id="c1b5c-135">Denetleyiciler genellikle ilişkili şablonlara model verilerini sunar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-135">Controllers often present model data to the corresponding templates.</span></span>
- <span data-ttu-id="c1b5c-136">Bir *Görünüm* uygulamadan temel olayları çevirir ve bunları denetleyiciye geçirir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-136">A *view* translates primitive events from the application and passes these to the controller.</span></span>
- <span data-ttu-id="c1b5c-137">*Yönlendirici* , uygulama durumunu yönetir, URL 'leri ve şablonları eşitlenmiş halde tutun.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-137">A *router* manages application state, keeping URLs and templates in sync.</span></span>

<span data-ttu-id="c1b5c-138">Buna ek olarak, Ember veri kitaplığı JSON nesnelerini (sunucudan bir Restıstalı API aracılığıyla elde edilen) ve istemci modellerini eşitlemeye yönelik olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-138">In addition, the Ember Data library can be used to synchronize JSON objects (obtained from the server through a RESTful API) and the client models.</span></span>

<span data-ttu-id="c1b5c-139">EmberJS SPA şablonu, betikleri sekiz katmana düzenler:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-139">The EmberJS SPA template organizes the scripts into eight layers:</span></span>

- <span data-ttu-id="c1b5c-140">WebApi\_Adapter. js, WebApi\_serileştirici. js: Ember veri kitaplığını ASP.NET Web API 'SI ile çalışacak şekilde genişletir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-140">webapi\_adapter.js, webapi\_serializer.js: Extends the Ember Data library to work with ASP.NET Web API.</span></span>
- <span data-ttu-id="c1b5c-141">Betikler/yardımcılar. js: yeni Ember Handleçubuklarının yardımcıları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-141">Scripts/helpers.js: Defines new Ember Handlebars helpers.</span></span>
- <span data-ttu-id="c1b5c-142">Betikler/App. js: uygulamayı oluşturur ve bağdaştırıcıyı ve serileştiriciyi yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-142">Scripts/app.js: Creates the app and configures the adapter and serializer.</span></span>
- <span data-ttu-id="c1b5c-143">Betikler/App/modeller/\*. js: modelleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-143">Scripts/app/models/\*.js: Defines the models.</span></span>
- <span data-ttu-id="c1b5c-144">Betikler/App/views/\*. js: görünümleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-144">Scripts/app/views/\*.js: Defines the views.</span></span>
- <span data-ttu-id="c1b5c-145">Betikler/App/Controllers/\*. js: denetleyicileri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-145">Scripts/app/controllers/\*.js: Defines the controllers.</span></span>
- <span data-ttu-id="c1b5c-146">Betikler/uygulama/rotalar, betikler/App/router. js: yolları tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-146">Scripts/app/routes, Scripts/app/router.js: Defines the routes.</span></span>
- <span data-ttu-id="c1b5c-147">Şablonlar/\*. HBS: handleçubuklarının şablonlarını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-147">Templates/\*.hbs: Defines the handlebars templates.</span></span>

<span data-ttu-id="c1b5c-148">Daha ayrıntılı bilgi için bu betiklerin bazılarına göz atalım.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-148">Let's look at some of these scripts in more detail.</span></span>

## <a name="models"></a><span data-ttu-id="c1b5c-149">Modeller</span><span class="sxs-lookup"><span data-stu-id="c1b5c-149">Models</span></span>

<span data-ttu-id="c1b5c-150">Modeller, betikler/uygulama/modeller klasöründe tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-150">The models are defined in the Scripts/app/models folder.</span></span> <span data-ttu-id="c1b5c-151">İki model dosyası vardır: TodoItem. js ve todoList. js.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-151">There are two model files: todoItem.js and todoList.js.</span></span>

<span data-ttu-id="c1b5c-152">**Todo. model. js** Yapılacaklar listeleri için istemci tarafı (tarayıcı) modellerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-152">**todo.model.js** defines the client-side (browser) models for the to-do lists.</span></span> <span data-ttu-id="c1b5c-153">İki model sınıfı vardır: TodoItem ve todoList.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-153">There are two model classes: todoItem and todoList.</span></span> <span data-ttu-id="c1b5c-154">Ember 'de, modeller DS 'nin alt sınıfları. Modelinizi.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-154">In Ember, models are subclasses of DS.Model.</span></span> <span data-ttu-id="c1b5c-155">Model, özniteliklere sahip özelliklere sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-155">A model can have properties with attributes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

<span data-ttu-id="c1b5c-156">Modeller, diğer modellerle ilişkiler tanımlayabilir:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-156">Models can define relationships to other models:</span></span>

[!code-css[Main](emberjs-template/samples/sample2.css)]

<span data-ttu-id="c1b5c-157">Modeller, diğer özelliklere bağlanan hesaplanmış özelliklere sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-157">Models can have computed properties that bind to other properties:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

<span data-ttu-id="c1b5c-158">Modeller, gözlemlenen bir özellik değiştiğinde çağrılan gözlemci işlevlerine sahip olabilir:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-158">Models can have observer functions, which are invoked when an observed property changes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a><span data-ttu-id="c1b5c-159">Görünümler</span><span class="sxs-lookup"><span data-stu-id="c1b5c-159">Views</span></span>

<span data-ttu-id="c1b5c-160">Görünümler, betikler/uygulama/görünümler klasöründe tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-160">The views are defined in the Scripts/app/views folder.</span></span> <span data-ttu-id="c1b5c-161">Bir görünüm, olayları uygulama kullanıcı arabiriminden çevirir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-161">A view translates events from the application UI.</span></span> <span data-ttu-id="c1b5c-162">Bir olay işleyicisi, denetleyici işlevlerine geri çağrı yapabilir veya yalnızca veri bağlamını doğrudan çağırabilir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-162">An event handler can call back to controller functions, or simply call the data context directly.</span></span>

<span data-ttu-id="c1b5c-163">Örneğin, aşağıdaki kod views/TodoItemEditView. js ' den.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-163">For example, the following code is from views/TodoItemEditView.js.</span></span> <span data-ttu-id="c1b5c-164">Bir girdi metin alanı için olay işlemeyi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-164">It defines the event handling for an input text field.</span></span>

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a><span data-ttu-id="c1b5c-165">Denetleyici</span><span class="sxs-lookup"><span data-stu-id="c1b5c-165">Controller</span></span>

<span data-ttu-id="c1b5c-166">Denetleyiciler betikler/uygulamalar/denetleyiciler klasöründe tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-166">The controllers are defined in the Scripts/app/controllers folder.</span></span> <span data-ttu-id="c1b5c-167">Tek bir modeli göstermek için `Ember.ObjectController`genişletin:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-167">To represent a single model, extend `Ember.ObjectController`:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

<span data-ttu-id="c1b5c-168">Denetleyici Ayrıca `Ember.ArrayController`genişleterek bir model koleksiyonunu temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-168">A controller can also represent a collection of models by extending `Ember.ArrayController`.</span></span> <span data-ttu-id="c1b5c-169">Örneğin, TodoListController `todoList` nesneleri dizisini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-169">For example, the TodoListController represents an array of `todoList` objects.</span></span> <span data-ttu-id="c1b5c-170">Denetleyici, todoList ID değerine göre sıralamayı azalan sırada yapar:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-170">The controller sorts by todoList ID, in descending order:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

<span data-ttu-id="c1b5c-171">Denetleyici, yeni bir todoList oluşturan ve onu diziye ekleyen `addTodoList`adlı bir işlevi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-171">The controller defines a function named `addTodoList`, which creates a new todoList and adds it to the array.</span></span> <span data-ttu-id="c1b5c-172">Bu işlevin nasıl çağrıldığını görmek için şablonlar klasöründe todoListTemplate. html adlı şablon dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-172">To see how this function gets called, open the template file named todoListTemplate.html, in the Templates folder.</span></span> <span data-ttu-id="c1b5c-173">Aşağıdaki şablon kodu `addTodoList` işleve bir düğme bağlar:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-173">The following template code binds a button to the `addTodoList` function:</span></span>

[!code-html[Main](emberjs-template/samples/sample8.html)]

<span data-ttu-id="c1b5c-174">Denetleyici Ayrıca bir hata mesajı tutan `error` özelliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-174">The controller also contains an `error` property, which holds an error message.</span></span> <span data-ttu-id="c1b5c-175">Hata iletisini (Ayrıca todoListTemplate. html) görüntüleyen şablon kodu aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-175">Here is the template code to display the error message (also in todoListTemplate.html):</span></span>

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a><span data-ttu-id="c1b5c-176">Yollar</span><span class="sxs-lookup"><span data-stu-id="c1b5c-176">Routes</span></span>

<span data-ttu-id="c1b5c-177">Router. js, görüntülenecek yolları ve varsayılan şablonu tanımlar, uygulama durumunu ayarlar ve yolların URL 'Lerini eşler:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-177">Router.js defines the routes and the default template to display, sets up application state, and matches URLs to routes:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

<span data-ttu-id="c1b5c-178">TodoListRoute. js, setupController işlevini geçersiz kılarak TodoListRoute için verileri yükler:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-178">TodoListRoute.js loads data for the TodoListRoute by overriding the setupController function:</span></span>

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

<span data-ttu-id="c1b5c-179">Ember, URL 'Leri, yol adlarını, denetleyicileri ve şablonları eşleştirmek için adlandırma kuralları kullanır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-179">Ember uses naming conventions to match URLs, route names, controllers, and templates.</span></span> <span data-ttu-id="c1b5c-180">Daha fazla bilgi için bkz. EmberJS belgelerindeki [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) .</span><span class="sxs-lookup"><span data-stu-id="c1b5c-180">For more information, see [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) at the EmberJS documentation.</span></span>

## <a name="templates"></a><span data-ttu-id="c1b5c-181">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="c1b5c-181">Templates</span></span>

<span data-ttu-id="c1b5c-182">Şablonlar klasörü dört şablon içerir:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-182">The Templates folder contains four templates:</span></span>

- <span data-ttu-id="c1b5c-183">Application. HBS: uygulama başlatıldığında oluşturulan varsayılan şablon.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-183">application.hbs: The default template that is rendered when the application is started.</span></span>
- <span data-ttu-id="c1b5c-184">. HBS hakkında: "/About" yolu için şablon.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-184">about.hbs: The template for the "/about" route.</span></span>
- <span data-ttu-id="c1b5c-185">index. HBS: kök "/" yolunun şablonu.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-185">index.hbs: The template for the root "/" route.</span></span>
- <span data-ttu-id="c1b5c-186">todoList. HBS: "/Todo" yolu için şablon.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-186">todoList.hbs: The template for the "/todo" route.</span></span>
- <span data-ttu-id="c1b5c-187">Gezinti çubuğunu \_. HBS: şablon, gezinti menüsünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-187">\_navbar.hbs: The template defines the navigation menu.</span></span>

<span data-ttu-id="c1b5c-188">Uygulama şablonu, ana sayfa gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-188">The application template acts like a master page.</span></span> <span data-ttu-id="c1b5c-189">Yola bağlı olarak içine diğer şablonları eklemek için bir üst bilgi, alt bilgi ve "{{priz}}" içerir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-189">It contains a header, a footer, and an "{{outlet}}" to insert other templates in depending on the route.</span></span> <span data-ttu-id="c1b5c-190">Ember 'de uygulama şablonları hakkında daha fazla bilgi için bkz. [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span><span class="sxs-lookup"><span data-stu-id="c1b5c-190">For more information about application templates in Ember, see [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).</span></span>

<span data-ttu-id="c1b5c-191">"/TodoList" şablonu iki döngü ifadesi içerir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-191">The "/todoList" template contains two loop expressions.</span></span> <span data-ttu-id="c1b5c-192">Dış döngü `{{#each controller}}`ve iç döngü `{{#each todos}}`.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-192">The outside loop is `{{#each controller}}`, and the inside loop is `{{#each todos}}`.</span></span> <span data-ttu-id="c1b5c-193">Aşağıdaki kod, yerleşik bir `Ember.Checkbox` görünümünü, özelleştirilmiş `App.TodoItemEditView`ve `deleteTodo` eylemine sahip bir bağlantıyı gösterir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-193">The following code shows a built-in `Ember.Checkbox` view, a customized `App.TodoItemEditView`, and a link with a `deleteTodo` action.</span></span>

[!code-html[Main](emberjs-template/samples/sample12.html)]

<span data-ttu-id="c1b5c-194">Controllers/HtmlHelperExtensions. cs ' de tanımlanan `HtmlHelperExtensions` sınıfı, Web. config dosyasında **hata ayıklama** **doğru** olarak ayarlandığında şablon dosyalarını önbelleğe almak ve eklemek için bir yardımcı işlevi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-194">The `HtmlHelperExtensions` class, defined in Controllers/HtmlHelperExtensions.cs, defines a helper function to cache and insert template files when **debug** is set to **true** in the Web.config file.</span></span> <span data-ttu-id="c1b5c-195">Bu işlev, views/Home/App. cshtml içinde tanımlanan ASP.NET MVC görünüm dosyasından çağrılır:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-195">This function is called from the ASP.NET MVC view file defined in Views/Home/App.cshtml:</span></span>

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

<span data-ttu-id="c1b5c-196">Bağımsız değişken olmadan çağrılan işlev, Şablonlar klasöründeki tüm şablon dosyalarını işler.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-196">Called with no arguments, the function renders all of the template files in the Templates folder.</span></span> <span data-ttu-id="c1b5c-197">Ayrıca, bir alt klasör veya belirli bir şablon dosyası da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-197">You can also specify a subfolder or a specific template file.</span></span>

<span data-ttu-id="c1b5c-198">Web. config dosyasında **hata ayıklama** **false** olduğunda, uygulama "~/paketles/Templates" paket öğesini içerir.</span><span class="sxs-lookup"><span data-stu-id="c1b5c-198">When **debug** is **false** in Web.config, the application includes the bundle item "~/bundles/templates".</span></span> <span data-ttu-id="c1b5c-199">Bu paket öğesi Handleçubuklar derleyici kitaplığı kullanılarak BundleConfig.cs 'e eklenir:</span><span class="sxs-lookup"><span data-stu-id="c1b5c-199">This bundle item is added in BundleConfig.cs, using the Handlebars compiler library:</span></span>

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]
