---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: ASP.NET Identity-ASP.NET 4. x içindeki kullanıcılar için birincil anahtarı değiştirme
author: Rick-Anderson
description: Visual Studio 2013, varsayılan Web uygulaması, Kullanıcı hesapları için anahtar için bir dize değeri kullanır. ASP.NET Identity, türünü değiştirmenizi sağlar...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519147"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="59225-104">ASP.NET Identity’de Kullanıcılar için Birincil Anahtarı Değiştirme</span><span class="sxs-lookup"><span data-stu-id="59225-104">Change Primary Key for Users in ASP.NET Identity</span></span>

<span data-ttu-id="59225-105">tarafından [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="59225-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="59225-106">Visual Studio 2013, varsayılan Web uygulaması, Kullanıcı hesapları için anahtar için bir dize değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="59225-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="59225-107">ASP.NET Identity, anahtar türünü veri gereksinimlerinizi karşılayacak şekilde değiştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="59225-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="59225-108">Örneğin, anahtarın türünü bir dizeden tamsayı olarak değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="59225-109">Bu konu başlığı altında, varsayılan Web uygulamasıyla nasıl başlayacağı ve Kullanıcı hesabı anahtarı bir tamsayı olarak nasıl değiştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="59225-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="59225-110">Projenizdeki herhangi bir anahtar türünü uygulamak için aynı değişiklikleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="59225-111">Varsayılan Web uygulamasında bu değişikliklerin nasıl yapılacağını gösterir, ancak özelleştirilmiş bir uygulamaya benzer değişiklikler uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="59225-112">MVC veya Web Forms çalışırken gereken değişiklikleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="59225-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="59225-113">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="59225-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="59225-114">Güncelleştirme 2 ile Visual Studio 2013 (veya üzeri)</span><span class="sxs-lookup"><span data-stu-id="59225-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="59225-115">ASP.NET Identity 2,1 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="59225-115">ASP.NET Identity 2.1 or later</span></span>

<span data-ttu-id="59225-116">Bu öğreticideki adımları gerçekleştirmek için, ASP.NET Web uygulaması şablonundan oluşturulmuş Visual Studio 2013 güncelleştirme 2 (veya üzeri) ve bir Web uygulaması olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="59225-117">Şablon güncelleştirme 3 ' te değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="59225-117">The template changed in Update 3.</span></span> <span data-ttu-id="59225-118">Bu konuda güncelleştirme 2 ve güncelleştirme 3 ' te şablonun nasıl değiştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="59225-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="59225-119">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="59225-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="59225-120">Identity User sınıfında anahtar türünü değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="59225-121">Anahtar türünü kullanan özelleştirilmiş kimlik sınıfları ekleyin</span><span class="sxs-lookup"><span data-stu-id="59225-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="59225-122">Anahtar türünü kullanmak için bağlam sınıfını ve Kullanıcı yöneticisini değiştirme</span><span class="sxs-lookup"><span data-stu-id="59225-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="59225-123">Anahtar türünü kullanmak için başlangıç yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="59225-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="59225-124">Güncelleştirme 2 ile MVC için, AccountController 'ı anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="59225-125">Güncelleştirme 3 ile MVC için AccountController ve ManageController değerlerini anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="59225-126">Güncelleştirme 2 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="59225-127">Güncelleştirme 3 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="59225-128">Uygulamayı çalıştır</span><span class="sxs-lookup"><span data-stu-id="59225-128">Run application</span></span>](#run)
- [<span data-ttu-id="59225-129">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="59225-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="59225-130">Identity User sınıfında anahtar türünü değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="59225-131">ASP.NET Web uygulaması şablonundan oluşturulan projenizde, ApplicationUser sınıfının Kullanıcı hesapları için anahtar için bir tamsayı kullandığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="59225-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="59225-132">IdentityModels.cs içinde, ApplicationUser sınıfını TKey genel parametresi için bir **int** türüne sahip ıdentityuser öğesinden devralacak şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59225-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="59225-133">Henüz uygulamamış olduğunuz üç özelleştirilmiş sınıfın adlarını da geçitirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="59225-134">Anahtarın türünü değiştirdiniz, ancak varsayılan olarak uygulamanın geri kalanı anahtarın bir dize olduğunu varsaymaktadır.</span><span class="sxs-lookup"><span data-stu-id="59225-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="59225-135">Bir dizeyi kabul eden koddaki anahtarın türünü açıkça belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="59225-136">**ApplicationUser** sınıfında, aşağıdaki vurgulanan kodda gösterildiği gibi **Generateuserıdentityasync** yöntemini int öğesini içerecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59225-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="59225-137">Bu değişiklik, güncelleştirme 3 şablonuyla Web Forms projeler için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="59225-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="59225-138">Anahtar türünü kullanan özelleştirilmiş kimlik sınıfları ekleyin</span><span class="sxs-lookup"><span data-stu-id="59225-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="59225-139">Identityuserrole, ıdentityuserclaim, ıdentityuserlogin, ıdentityrole, UserStore, RoleStore gibi diğer kimlik sınıfları yine de bir dize anahtarı kullanacak şekilde ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="59225-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="59225-140">Bu sınıfların anahtar için bir tamsayı belirten yeni sürümlerini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59225-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="59225-141">Bu sınıflarda çok fazla uygulama kodu sağlamanız gerekmez, birincil olarak yalnızca int 'i anahtar olarak ayarlamasınız.</span><span class="sxs-lookup"><span data-stu-id="59225-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="59225-142">Aşağıdaki sınıfları IdentityModels.cs dosyanıza ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59225-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="59225-143">Anahtar türünü kullanmak için bağlam sınıfını ve Kullanıcı yöneticisini değiştirme</span><span class="sxs-lookup"><span data-stu-id="59225-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="59225-144">IdentityModels.cs içinde, **Applicationdbcontext** sınıfının tanımını, vurgulanan kodda gösterildiği gibi, yeni özelleştirilmiş sınıflarınızı ve anahtar için bir **int** kullanmak üzere değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59225-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="59225-145">ThrowIfV1Schema parametresi artık oluşturucuda geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="59225-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="59225-146">Oluşturucuyu bir ThrowIfV1Schema değeri geçirmemesi için değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59225-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="59225-147">IdentityConfig.cs 'i açın ve **Applicationusermanager** sınıfını kalıcı veriler için Yeni Kullanıcı Mağazası sınıfınızı ve anahtar için bir **int** kullanın.</span><span class="sxs-lookup"><span data-stu-id="59225-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="59225-148">Güncelleştirme 3 şablonunda, Applicationsignınmanager sınıfını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="59225-149">Anahtar türünü kullanmak için başlangıç yapılandırmasını değiştirme</span><span class="sxs-lookup"><span data-stu-id="59225-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="59225-150">Startup.Auth.cs ' de, Onvalidateıdentity kodunu aşağıda vurgulanan şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59225-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="59225-151">Getuserıdcallback tanımının dize değerini bir tamsayı olarak ayrıştırır olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="59225-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="59225-152">Projeniz **GetUserID** yönteminin genel uygulamasını tanımıyorsa, ASP.NET Identity NuGet paketini 2,1 sürümüne güncelleştirmeniz gerekebilir</span><span class="sxs-lookup"><span data-stu-id="59225-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="59225-153">ASP.NET Identity tarafından kullanılan altyapı sınıflarında çok sayıda değişiklik yaptınız.</span><span class="sxs-lookup"><span data-stu-id="59225-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="59225-154">Projeyi derlemeyi denerseniz, çok sayıda hata olduğunu fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="59225-155">Neyse ki, kalan hataların hepsi benzerdir.</span><span class="sxs-lookup"><span data-stu-id="59225-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="59225-156">Identity sınıfı anahtar için bir tamsayı bekliyor, ancak denetleyici (veya Web formu) bir dize değeri geçiriyoruyor.</span><span class="sxs-lookup"><span data-stu-id="59225-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="59225-157">Her durumda **GetUserID&lt;int&gt;** çağırarak bir dizeden ve tamsayıya dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="59225-158">Derlemeden hata listesinden çalışabilirsiniz veya aşağıdaki değişiklikleri izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="59225-159">Kalan değişiklikler oluşturmakta olduğunuz proje türüne ve Visual Studio 'da hangi güncelleştirmeyi yüklediğinize bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="59225-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="59225-160">Aşağıdaki bağlantılar aracılığıyla doğrudan ilgili bölüme gidebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="59225-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="59225-161">Güncelleştirme 2 ile MVC için, AccountController 'ı anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="59225-162">Güncelleştirme 3 ile MVC için AccountController ve ManageController değerlerini anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="59225-163">Güncelleştirme 2 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="59225-164">Güncelleştirme 3 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="59225-165">Güncelleştirme 2 ile MVC için, AccountController 'ı anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="59225-166">AccountController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="59225-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="59225-167">Aşağıdaki yöntemleri değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-167">You need to change the following methods.</span></span>

<span data-ttu-id="59225-168">**ConfirmEmail** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="59225-169">**Ilişkiyi kaldırma** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="59225-170">**Manage (ManageUserViewModel)** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="59225-171">**Linklogincallback** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="59225-172">**Removeaccountlist** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="59225-173">**HasPassword** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="59225-174">Şimdi [uygulamayı çalıştırabilir](#run) ve yeni bir kullanıcı kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="59225-175">Güncelleştirme 3 ile MVC için AccountController ve ManageController değerlerini anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="59225-176">AccountController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="59225-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="59225-177">Aşağıdaki yöntemi değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-177">You need to change the following method.</span></span>

<span data-ttu-id="59225-178">**ConfirmEmail** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="59225-179">**Sendcode** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="59225-180">ManageController.cs dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="59225-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="59225-181">Aşağıdaki yöntemleri değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-181">You need to change the following methods.</span></span>

<span data-ttu-id="59225-182">**Index** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="59225-183">**RemoveLogin** yöntemleri</span><span class="sxs-lookup"><span data-stu-id="59225-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="59225-184">**Addphonenumber** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="59225-185">**Enabletwofactorayuthentication** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="59225-186">**Disabletwofactorayuthentication** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="59225-187">**Doğrulamaları Yphonenumber** yöntemleri</span><span class="sxs-lookup"><span data-stu-id="59225-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="59225-188">**Removephonenumber** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="59225-189">**ChangePassword** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="59225-190">**SetPassword** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="59225-191">**ManageLogins** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="59225-192">**Linklogincallback** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="59225-193">**HasPassword** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="59225-194">**Hasphonenumber** yöntemi</span><span class="sxs-lookup"><span data-stu-id="59225-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="59225-195">Şimdi [uygulamayı çalıştırabilir](#run) ve yeni bir kullanıcı kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="59225-196">Güncelleştirme 2 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="59225-197">Güncelleştirme 2 ile Web Forms için aşağıdaki sayfaları değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="59225-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="59225-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="59225-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="59225-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="59225-201">Şimdi [uygulamayı çalıştırabilir](#run) ve yeni bir kullanıcı kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="59225-202">Güncelleştirme 3 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin</span><span class="sxs-lookup"><span data-stu-id="59225-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="59225-203">Güncelleştirme 3 ile Web Forms için aşağıdaki sayfaları değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="59225-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="59225-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="59225-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="59225-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="59225-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="59225-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="59225-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="59225-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="59225-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="59225-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="59225-212">Uygulamayı çalıştır</span><span class="sxs-lookup"><span data-stu-id="59225-212">Run application</span></span>

<span data-ttu-id="59225-213">Varsayılan Web uygulaması şablonunda gerekli tüm değişiklikleri tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="59225-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="59225-214">Uygulamayı çalıştırın ve yeni bir Kullanıcı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="59225-214">Run the application and register a new user.</span></span> <span data-ttu-id="59225-215">Kullanıcı kaydedildikten sonra, AspNetUsers tablosunda tamsayı olan bir kimlik sütunu olduğunu fark edeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="59225-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![Yeni birincil anahtar](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="59225-217">Daha önce farklı bir birincil anahtarla ASP.NET Identity tabloları oluşturduysanız, bazı ek değişiklikler yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="59225-218">Mümkünse, var olan veritabanını silmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="59225-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="59225-219">Web uygulamasını çalıştırdığınızda ve yeni bir kullanıcı eklediğinizde, veritabanı doğru tasarımla yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="59225-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="59225-220">Silme mümkün değilse, tabloları değiştirmek için önce kod geçişlerini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="59225-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="59225-221">Ancak, yeni tamsayı birincil anahtarı veritabanında bir SQL ıDENTITY özelliği olarak ayarlanmayacak.</span><span class="sxs-lookup"><span data-stu-id="59225-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="59225-222">Kimlik sütununu KIMLIK olarak el ile ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="59225-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="59225-223">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="59225-223">Other resources</span></span>

- [<span data-ttu-id="59225-224">ASP.NET Identity için Özel Depolama Sağlayıcılarına Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="59225-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="59225-225">Mevcut Bir Web Sitesini SQL Üyeliğinden ASP.NET Identity’ye Geçirme</span><span class="sxs-lookup"><span data-stu-id="59225-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="59225-226">Üyelik ve Kullanıcı profillerinin evrensel sağlayıcı verilerini ASP.NET Identity 'ye geçirme</span><span class="sxs-lookup"><span data-stu-id="59225-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="59225-227">Değiştirilen birincil anahtarla [örnek uygulama](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)</span><span class="sxs-lookup"><span data-stu-id="59225-227">[Sample application](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) with changed primary key</span></span>
