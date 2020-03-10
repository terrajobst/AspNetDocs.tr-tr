---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: JavaScript Istemcisini oluşturma | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622348"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="aca91-102">JavaScript İstemcisini Oluşturma</span><span class="sxs-lookup"><span data-stu-id="aca91-102">Create the JavaScript Client</span></span>

<span data-ttu-id="aca91-103">, [Mike te son](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="aca91-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="aca91-104">Tamamlanmış projeyi indir</span><span class="sxs-lookup"><span data-stu-id="aca91-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="aca91-105">Bu bölümde, HTML, JavaScript ve [altını gizleme. js](http://knockoutjs.com/) kitaplığı kullanarak uygulama için istemcisini oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="aca91-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="aca91-106">İstemci uygulamasını aşamalar halinde oluşturacağız:</span><span class="sxs-lookup"><span data-stu-id="aca91-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="aca91-107">Kitap listesi gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="aca91-107">Showing a list of books.</span></span>
- <span data-ttu-id="aca91-108">Bir kitap ayrıntısı gösteriliyor.</span><span class="sxs-lookup"><span data-stu-id="aca91-108">Showing a book detail.</span></span>
- <span data-ttu-id="aca91-109">Yeni kitap ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="aca91-109">Adding a new book.</span></span>

<span data-ttu-id="aca91-110">Altını gizleme kitaplığı Model-View-ViewModel (MVVM) modelini kullanır:</span><span class="sxs-lookup"><span data-stu-id="aca91-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="aca91-111">**Model** , iş etki alanındaki verilerin sunucu tarafı gösterimidir (bizim örneğimizde, kitaplarımızda ve yazarlarımız).</span><span class="sxs-lookup"><span data-stu-id="aca91-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="aca91-112">**Görünüm** sunum katmanıdır (HTML).</span><span class="sxs-lookup"><span data-stu-id="aca91-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="aca91-113">**Görünüm modeli** , modelleri tutan bir JavaScript nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="aca91-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="aca91-114">Görünüm modeli, Kullanıcı arabiriminin kod soyutlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="aca91-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="aca91-115">HTML temsili bilgisine sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="aca91-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="aca91-116">Bunun yerine, görünümün Özet özelliklerini temsil eder, örneğin kitap&quot;listesini &quot;.</span><span class="sxs-lookup"><span data-stu-id="aca91-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="aca91-117">Görünüm, görünüm modeline veri ile bağlanır.</span><span class="sxs-lookup"><span data-stu-id="aca91-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="aca91-118">Görünüm modeli güncelleştirmeleri otomatik olarak görünüme yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="aca91-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="aca91-119">Görünüm modeli, düğme tıklamaları gibi görünümden de olayları alır.</span><span class="sxs-lookup"><span data-stu-id="aca91-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="aca91-120">Bu yaklaşım, herhangi bir kodu yeniden yazmadan bağlamaları değiştirebildiğinden uygulamanızın düzen ve Kullanıcı arabirimini değiştirmeyi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="aca91-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="aca91-121">Örneğin, öğelerin bir listesini `<ul>`olarak gösterip daha sonra bir tablo olarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aca91-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="aca91-122">Altını gizleme kitaplığını ekleme</span><span class="sxs-lookup"><span data-stu-id="aca91-122">Add the Knockout Library</span></span>

<span data-ttu-id="aca91-123">Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="aca91-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="aca91-124">Ardından **Paket Yöneticisi konsolu**' nu seçin.</span><span class="sxs-lookup"><span data-stu-id="aca91-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="aca91-125">Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="aca91-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="aca91-126">Bu komut, altını gizleme dosyalarını betikler klasörüne ekler.</span><span class="sxs-lookup"><span data-stu-id="aca91-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="aca91-127">Görünüm modeli oluşturma</span><span class="sxs-lookup"><span data-stu-id="aca91-127">Create the View Model</span></span>

<span data-ttu-id="aca91-128">Scripts klasörüne App. js adlı bir JavaScript dosyası ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aca91-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="aca91-129">(Çözüm Gezgini, betikler klasörüne sağ tıklayın, **Ekle**' yi ve ardından **JavaScript dosyası**' nı seçin.) Aşağıdaki kodu yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="aca91-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="aca91-130">Altını gizleme bölümünde, `observable` sınıfı veri bağlamayı mümkün bir şekilde sunar.</span><span class="sxs-lookup"><span data-stu-id="aca91-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="aca91-131">Bir observable 'ın içeriği değiştiğinde, observable her türlü veri bağlantılı denetimi kendileri tarafından güncelleştirebilecekleri şekilde bilgilendirir.</span><span class="sxs-lookup"><span data-stu-id="aca91-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="aca91-132">(`observableArray` sınıfı, *observable*'ın dizi sürümüdür.) İle başlamak için, görünüm modelimizin iki gözlemlenenler vardır:</span><span class="sxs-lookup"><span data-stu-id="aca91-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="aca91-133">`books`, kitap listesini tutar.</span><span class="sxs-lookup"><span data-stu-id="aca91-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="aca91-134">`error` bir AJAX çağrısı başarısız olursa bir hata iletisi içerir.</span><span class="sxs-lookup"><span data-stu-id="aca91-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="aca91-135">`getAllBooks` yöntemi, kitap listesini almak için bir AJAX çağrısı yapar.</span><span class="sxs-lookup"><span data-stu-id="aca91-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="aca91-136">Sonra, sonucu `books` dizisine iter.</span><span class="sxs-lookup"><span data-stu-id="aca91-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="aca91-137">`ko.applyBindings` yöntemi, altını gizleme kitaplığının bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="aca91-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="aca91-138">Görünüm modelini bir parametre olarak alır ve veri bağlamayı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="aca91-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="aca91-139">Betik paketi ekleme</span><span class="sxs-lookup"><span data-stu-id="aca91-139">Add a Script Bundle</span></span>

<span data-ttu-id="aca91-140">Paketleme, ASP.NET 4,5 ' de birden çok dosyayı tek bir dosyada birleştirmeyi veya paketlemeyi kolaylaştıran bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="aca91-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="aca91-141">Paketleme, sunucuya yapılan istek sayısını azaltır ve bu da sayfa yükleme süresini iyileştirebilirler.</span><span class="sxs-lookup"><span data-stu-id="aca91-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="aca91-142">Start/paketleme Liconfig. cs\_dosya uygulamasını açın.</span><span class="sxs-lookup"><span data-stu-id="aca91-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="aca91-143">Aşağıdaki kodu Registerdemeti yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="aca91-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="aca91-144">[Önceki](part-5.md)
> [İleri](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="aca91-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>
