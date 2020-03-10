---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: Hizmet katmanı ile doğrulama (VB) | Microsoft Docs
author: StephenWalther
description: Doğrulama mantığınızı denetleyici eylemlerinizin dışında ve ayrı bir hizmet katmanında nasıl taşıyacağınızı öğrenin. Bu öğreticide, Stephen Walther nasıl yapılacağını açıklar...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 704657ffe6f50eaf3eb0d91d0d334567003ab7f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542828"
---
# <a name="validating-with-a-service-layer-vb"></a><span data-ttu-id="45b54-104">Hizmet Katmanı ile Doğrulama (VB)</span><span class="sxs-lookup"><span data-stu-id="45b54-104">Validating with a Service Layer (VB)</span></span>

<span data-ttu-id="45b54-105">ile [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="45b54-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="45b54-106">Doğrulama mantığınızı denetleyici eylemlerinizin dışında ve ayrı bir hizmet katmanında nasıl taşıyacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="45b54-106">Learn how to move your validation logic out of your controller actions and into a separate service layer.</span></span> <span data-ttu-id="45b54-107">Bu öğreticide, Stephen Walther, hizmet katmanınızı denetleyici katmanınızdan yalıtarak sorunları nasıl keskin bir şekilde koruyabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="45b54-107">In this tutorial, Stephen Walther explains how you can maintain a sharp separation of concerns by isolating your service layer from your controller layer.</span></span>

<span data-ttu-id="45b54-108">Bu öğreticinin amacı, bir ASP.NET MVC uygulamasında doğrulama gerçekleştirme yöntemini açıklıyor.</span><span class="sxs-lookup"><span data-stu-id="45b54-108">The goal of this tutorial is to describe one method of performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="45b54-109">Bu öğreticide, doğrulama mantığınızı denetleyicilerden ve ayrı bir hizmet katmanına taşımayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="45b54-109">In this tutorial, you learn how to move your validation logic out of your controllers and into a separate service layer.</span></span>

## <a name="separating-concerns"></a><span data-ttu-id="45b54-110">Kaygıları ayırma</span><span class="sxs-lookup"><span data-stu-id="45b54-110">Separating Concerns</span></span>

<span data-ttu-id="45b54-111">Bir ASP.NET MVC uygulaması oluşturduğunuzda, veritabanı mantığınızı denetleyici eylemlerinizin içine yerleştirmemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="45b54-111">When you build an ASP.NET MVC application, you should not place your database logic inside your controller actions.</span></span> <span data-ttu-id="45b54-112">Veritabanınızı ve denetleyici mantığınızı karıştırmak, uygulamanızın zaman içinde bakımını daha zor hale getirir.</span><span class="sxs-lookup"><span data-stu-id="45b54-112">Mixing your database and controller logic makes your application more difficult to maintain over time.</span></span> <span data-ttu-id="45b54-113">Öneri, tüm veritabanı mantığınızı ayrı bir depo katmanında yerleştirmesidir.</span><span class="sxs-lookup"><span data-stu-id="45b54-113">The recommendation is that you place all of your database logic in a separate repository layer.</span></span>

<span data-ttu-id="45b54-114">Örneğin, Listeleme 1, ProductRepository adlı basit bir depo içerir.</span><span class="sxs-lookup"><span data-stu-id="45b54-114">For example, Listing 1 contains a simple repository named the ProductRepository.</span></span> <span data-ttu-id="45b54-115">Ürün deposu, uygulamanın tüm veri erişim kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="45b54-115">The product repository contains all of the data access code for the application.</span></span> <span data-ttu-id="45b54-116">Liste ayrıca, ürün deposunun uyguladığı ıproductrepository arabirimini de içerir.</span><span class="sxs-lookup"><span data-stu-id="45b54-116">The listing also includes the IProductRepository interface that the product repository implements.</span></span>

<span data-ttu-id="45b54-117">**Listeleme 1-Models\productdepotory.exe**</span><span class="sxs-lookup"><span data-stu-id="45b54-117">**Listing 1 - Models\ProductRepository.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

<span data-ttu-id="45b54-118">Listeleme 2 ' deki denetleyici, dizin () ve Create () eylemleri içinde depo katmanını kullanır.</span><span class="sxs-lookup"><span data-stu-id="45b54-118">The controller in Listing 2 uses the repository layer in both its Index() and Create() actions.</span></span> <span data-ttu-id="45b54-119">Bu denetleyicinin herhangi bir veritabanı mantığı içermediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="45b54-119">Notice that this controller does not contain any database logic.</span></span> <span data-ttu-id="45b54-120">Bir depo katmanı oluşturmak, kaygılara yönelik temiz ayrımı korumanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="45b54-120">Creating a repository layer enables you to maintain a clean separation of concerns.</span></span> <span data-ttu-id="45b54-121">Denetleyiciler, uygulama akış denetim mantığından sorumludur ve veri erişim mantığıyla depo sorumludur.</span><span class="sxs-lookup"><span data-stu-id="45b54-121">Controllers are responsible for application flow control logic and the repository is responsible for data access logic.</span></span>

<span data-ttu-id="45b54-122">**Listeleme 2-Controllers\productcontroller.exe**</span><span class="sxs-lookup"><span data-stu-id="45b54-122">**Listing 2 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a><span data-ttu-id="45b54-123">Hizmet katmanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="45b54-123">Creating a Service Layer</span></span>

<span data-ttu-id="45b54-124">Bu nedenle, uygulama akış denetim mantığı bir denetleyiciye aittir ve veri erişim mantığı bir depoya aittir.</span><span class="sxs-lookup"><span data-stu-id="45b54-124">So, application flow control logic belongs in a controller and data access logic belongs in a repository.</span></span> <span data-ttu-id="45b54-125">Bu durumda, doğrulama mantığınızı nereye yerleştirmeniz gerekir?</span><span class="sxs-lookup"><span data-stu-id="45b54-125">In that case, where do you put your validation logic?</span></span> <span data-ttu-id="45b54-126">Bir seçenek, doğrulama mantığınızı bir *hizmet katmanına*yerleştirmadır.</span><span class="sxs-lookup"><span data-stu-id="45b54-126">One option is to place your validation logic in a *service layer*.</span></span>

<span data-ttu-id="45b54-127">Bir hizmet katmanı, bir ASP.NET MVC uygulamasındaki bir denetleyici ve depo katmanı arasındaki iletişimi destekleyen ek bir katmandır.</span><span class="sxs-lookup"><span data-stu-id="45b54-127">A service layer is an additional layer in an ASP.NET MVC application that mediates communication between a controller and repository layer.</span></span> <span data-ttu-id="45b54-128">Hizmet katmanı iş mantığını içerir.</span><span class="sxs-lookup"><span data-stu-id="45b54-128">The service layer contains business logic.</span></span> <span data-ttu-id="45b54-129">Özellikle, doğrulama mantığını içerir.</span><span class="sxs-lookup"><span data-stu-id="45b54-129">In particular, it contains validation logic.</span></span>

<span data-ttu-id="45b54-130">Örneğin, kod 3 ' teki ürün hizmeti katmanının bir CreateProduct () yöntemi vardır.</span><span class="sxs-lookup"><span data-stu-id="45b54-130">For example, the product service layer in Listing 3 has a CreateProduct() method.</span></span> <span data-ttu-id="45b54-131">CreateProduct () yöntemi, ürünü ürün deposuna geçirmeden önce yeni bir ürünü doğrulamak için ValidateProduct () yöntemini çağırır.</span><span class="sxs-lookup"><span data-stu-id="45b54-131">The CreateProduct() method calls the ValidateProduct() method to validate a new product before passing the product to the product repository.</span></span>

<span data-ttu-id="45b54-132">**Listeleme 3-Models\productservice.exe**</span><span class="sxs-lookup"><span data-stu-id="45b54-132">**Listing 3 - Models\ProductService.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

<span data-ttu-id="45b54-133">Ürün denetleyicisi, kod 4 ' te depo katmanı yerine hizmet katmanını kullanmak üzere güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="45b54-133">The Product controller has been updated in Listing 4 to use the service layer instead of the repository layer.</span></span> <span data-ttu-id="45b54-134">Denetleyici katmanı hizmet katmanıyla oynanır.</span><span class="sxs-lookup"><span data-stu-id="45b54-134">The controller layer talks to the service layer.</span></span> <span data-ttu-id="45b54-135">Hizmet katmanı, depo katmanıyla konuşur.</span><span class="sxs-lookup"><span data-stu-id="45b54-135">The service layer talks to the repository layer.</span></span> <span data-ttu-id="45b54-136">Her katmanın ayrı bir sorumluluğu vardır.</span><span class="sxs-lookup"><span data-stu-id="45b54-136">Each layer has a separate responsibility.</span></span>

<span data-ttu-id="45b54-137">**Listeleme 4-Controllers\productcontroller.exe**</span><span class="sxs-lookup"><span data-stu-id="45b54-137">**Listing 4 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

<span data-ttu-id="45b54-138">Ürün hizmeti 'nin ürün denetleyicisi oluşturucusunda oluşturulmuş olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="45b54-138">Notice that the product service is created in the product controller constructor.</span></span> <span data-ttu-id="45b54-139">Ürün hizmeti oluşturulduğunda, model durum sözlüğü hizmete geçirilir.</span><span class="sxs-lookup"><span data-stu-id="45b54-139">When the product service is created, the model state dictionary is passed to the service.</span></span> <span data-ttu-id="45b54-140">Ürün hizmeti, doğrulama hata iletilerini denetleyiciye geri geçirmek için model durumunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="45b54-140">The product service uses model state to pass validation error messages back to the controller.</span></span>

## <a name="decoupling-the-service-layer"></a><span data-ttu-id="45b54-141">Hizmet katmanını bağlama</span><span class="sxs-lookup"><span data-stu-id="45b54-141">Decoupling the Service Layer</span></span>

<span data-ttu-id="45b54-142">Denetleyiciyi ve hizmet katmanlarını tek bir şekilde yalıtamadı.</span><span class="sxs-lookup"><span data-stu-id="45b54-142">We have failed to isolate the controller and service layers in one respect.</span></span> <span data-ttu-id="45b54-143">Denetleyici ve hizmet katmanları, model durumu üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="45b54-143">The controller and service layers communicate through model state.</span></span> <span data-ttu-id="45b54-144">Diğer bir deyişle, hizmet katmanının, ASP.NET MVC çerçevesinin belirli bir özelliğine bağımlılığı vardır.</span><span class="sxs-lookup"><span data-stu-id="45b54-144">In other words, the service layer has a dependency on a particular feature of the ASP.NET MVC framework.</span></span>

<span data-ttu-id="45b54-145">Hizmet katmanını denetleyici katmanımız kadar mümkün olduğunca yalıtmak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="45b54-145">We want to isolate the service layer from our controller layer as much as possible.</span></span> <span data-ttu-id="45b54-146">Teorik olarak, hizmet katmanını yalnızca bir ASP.NET MVC uygulaması değil, herhangi bir uygulama türüyle kullanabilmelidir.</span><span class="sxs-lookup"><span data-stu-id="45b54-146">In theory, we should be able to use the service layer with any type of application and not only an ASP.NET MVC application.</span></span> <span data-ttu-id="45b54-147">Örneğin, gelecekte uygulamamız için bir WPF ön ucu oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b54-147">For example, in the future, we might want to build a WPF front-end for our application.</span></span> <span data-ttu-id="45b54-148">ASP.NET MVC modeli durumundaki bağımlılığı hizmet katmanımızdan kaldırmanın bir yolunu bulduk.</span><span class="sxs-lookup"><span data-stu-id="45b54-148">We should find a way to remove the dependency on ASP.NET MVC model state from our service layer.</span></span>

<span data-ttu-id="45b54-149">5\. listede, hizmet katmanı artık model durumunu kullanmamasını sağlayacak şekilde güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="45b54-149">In Listing 5, the service layer has been updated so that it no longer uses model state.</span></span> <span data-ttu-id="45b54-150">Bunun yerine, ıvalidationdictionary arabirimini uygulayan herhangi bir sınıfı kullanır.</span><span class="sxs-lookup"><span data-stu-id="45b54-150">Instead, it uses any class that implements the IValidationDictionary interface.</span></span>

<span data-ttu-id="45b54-151">**Listeleme 5-Models\productservice,vb (ayrılmış)**</span><span class="sxs-lookup"><span data-stu-id="45b54-151">**Listing 5 - Models\ProductService.vb (decoupled)**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

<span data-ttu-id="45b54-152">Ivalidationdictionary arabirimi, liste 6 ' da tanımlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="45b54-152">The IValidationDictionary interface is defined in Listing 6.</span></span> <span data-ttu-id="45b54-153">Bu basit arabirim tek bir yönteme ve tek bir özelliğe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="45b54-153">This simple interface has a single method and a single property.</span></span>

<span data-ttu-id="45b54-154">**Listeleme 6-Models\IValidationDictionary.cs**</span><span class="sxs-lookup"><span data-stu-id="45b54-154">**Listing 6 - Models\IValidationDictionary.cs**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

<span data-ttu-id="45b54-155">ModelStateWrapper sınıfı adlı Listeleme 7 ' deki sınıf ıvalidationdictionary arabirimini uygular.</span><span class="sxs-lookup"><span data-stu-id="45b54-155">The class in Listing 7, named the ModelStateWrapper class, implements the IValidationDictionary interface.</span></span> <span data-ttu-id="45b54-156">Bir model durum sözlüğünü oluşturucuya geçirerek ModelStateWrapper sınıfının örneğini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b54-156">You can instantiate the ModelStateWrapper class by passing a model state dictionary to the constructor.</span></span>

<span data-ttu-id="45b54-157">**Listeleme 7-Models\ModelStateWrapper.vb**</span><span class="sxs-lookup"><span data-stu-id="45b54-157">**Listing 7 - Models\ModelStateWrapper.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

<span data-ttu-id="45b54-158">Son olarak, liste 8 ' deki güncelleştirilmiş denetleyici, Oluşturucu içinde hizmet katmanını oluştururken ModelStateWrapper kullanır.</span><span class="sxs-lookup"><span data-stu-id="45b54-158">Finally, the updated controller in Listing 8 uses the ModelStateWrapper when creating the service layer in its constructor.</span></span>

<span data-ttu-id="45b54-159">**8-Controllers\productcontroller.exe listeleme**</span><span class="sxs-lookup"><span data-stu-id="45b54-159">**Listing 8 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

<span data-ttu-id="45b54-160">Ivalidationdictionary arabirimini ve ModelStateWrapper sınıfını kullanmak, hizmet katmanımızı denetleyici katmanımızdan tamamen yalıtmamızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="45b54-160">Using the IValidationDictionary interface and the ModelStateWrapper class enables us to completely isolate our service layer from our controller layer.</span></span> <span data-ttu-id="45b54-161">Hizmet katmanı artık model durumuna bağlı değil.</span><span class="sxs-lookup"><span data-stu-id="45b54-161">The service layer is no longer dependent on model state.</span></span> <span data-ttu-id="45b54-162">Ivalidationdictionary arabirimini uygulayan herhangi bir sınıfı hizmet katmanına geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b54-162">You can pass any class that implements the IValidationDictionary interface to the service layer.</span></span> <span data-ttu-id="45b54-163">Örneğin, bir WPF uygulaması, bir basit koleksiyon sınıfıyla ıvalidationdictionary arabirimini uygulayabilir.</span><span class="sxs-lookup"><span data-stu-id="45b54-163">For example, a WPF application might implement the IValidationDictionary interface with a simple collection class.</span></span>

## <a name="summary"></a><span data-ttu-id="45b54-164">Özet</span><span class="sxs-lookup"><span data-stu-id="45b54-164">Summary</span></span>

<span data-ttu-id="45b54-165">Bu öğreticinin amacı, bir ASP.NET MVC uygulamasında doğrulama gerçekleştirmeye yönelik bir yaklaşımı tartışmaktır.</span><span class="sxs-lookup"><span data-stu-id="45b54-165">The goal of this tutorial was to discuss one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="45b54-166">Bu öğreticide, tüm doğrulama mantığınızı denetleyicilerden ve ayrı bir hizmet katmanına nasıl taşıyabileceğinizi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="45b54-166">In this tutorial, you learned how to move all of your validation logic out of your controllers and into a separate service layer.</span></span> <span data-ttu-id="45b54-167">Ayrıca, bir Modelstatesarmalayıcı sınıfı oluşturarak hizmet katmanınızı denetleyici katmanınızdan yalıtmak için de öğrenirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45b54-167">You also learned how to isolate your service layer from your controller layer by creating a ModelStateWrapper class.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="45b54-168">[Önceki](validating-with-the-idataerrorinfo-interface-vb.md)
> [İleri](validation-with-the-data-annotation-validators-vb.md)</span><span class="sxs-lookup"><span data-stu-id="45b54-168">[Previous](validating-with-the-idataerrorinfo-interface-vb.md)
[Next](validation-with-the-data-annotation-validators-vb.md)</span></span>
