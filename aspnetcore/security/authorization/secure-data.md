---
title: Kullanıcı verilerinin yetkilendirme tarafından korunduğu ile bir ASP.NET Core uygulaması oluşturma
author: rick-anderson
description: Kullanıcı verilerinin yetkilendirme tarafından korunduğu ile Razor sayfaları uygulaması oluşturmayı öğrenin. HTTPS, kimlik doğrulama, güvenlik, ASP.NET Core kimliği içerir.
ms.author: riande
ms.date: 12/18/2018
ms.custom: seodec18
uid: security/authorization/secure-data
ms.openlocfilehash: bdba706c1ef24ebe35129cb8bb2d9949196245a1
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075789"
---
# <a name="create-an-aspnet-core-app-with-user-data-protected-by-authorization"></a><span data-ttu-id="59733-104">Kullanıcı verilerinin yetkilendirme tarafından korunduğu ile bir ASP.NET Core uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="59733-104">Create an ASP.NET Core app with user data protected by authorization</span></span>

<span data-ttu-id="59733-105">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT) ve [ALi Audette](https://twitter.com/joeaudette)</span><span class="sxs-lookup"><span data-stu-id="59733-105">By [Rick Anderson](https://twitter.com/RickAndMSFT) and [Joe Audette](https://twitter.com/joeaudette)</span></span>

::: moniker range="<= aspnetcore-1.1"

<span data-ttu-id="59733-106">Bkz: [bu PDF](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_1-16-18.pdf) ASP.NET Core MVC sürümü için.</span><span class="sxs-lookup"><span data-stu-id="59733-106">See [this PDF](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_1-16-18.pdf) for the ASP.NET Core MVC version.</span></span> <span data-ttu-id="59733-107">Bu öğreticide ASP.NET Core 1.1 sürümü [bu](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) klasör.</span><span class="sxs-lookup"><span data-stu-id="59733-107">The ASP.NET Core 1.1 version of this tutorial is in [this](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data) folder.</span></span> <span data-ttu-id="59733-108">ASP.NET Core örnek konusu 1.1 [örnekleri](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2).</span><span class="sxs-lookup"><span data-stu-id="59733-108">The 1.1 ASP.NET Core sample is in the [samples](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2).</span></span>

::: moniker-end

::: moniker range="= aspnetcore-2.0"

<span data-ttu-id="59733-109">Bkz: [bu pdf](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_July16_18.pdf)</span><span class="sxs-lookup"><span data-stu-id="59733-109">See [this pdf](https://webpifeed.blob.core.windows.net/webpifeed/Partners/asp.net_repo_pdf_July16_18.pdf)</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

<span data-ttu-id="59733-110">Bu öğretici, kullanıcı verilerinin yetkilendirme tarafından korunduğu ile ASP.NET Core web uygulaması oluşturma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="59733-110">This tutorial shows how to create an ASP.NET Core web app with user data protected by authorization.</span></span> <span data-ttu-id="59733-111">Kimlik doğrulaması (kayıtlı) kullanıcılar kişiler listesi görüntüler oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="59733-111">It displays a list of contacts that authenticated (registered) users have created.</span></span> <span data-ttu-id="59733-112">Üç güvenlik grubu vardır:</span><span class="sxs-lookup"><span data-stu-id="59733-112">There are three security groups:</span></span>

* <span data-ttu-id="59733-113">**Kayıtlı kullanıcıların** onaylanan tüm verileri görüntüleyebilir ve kullanıcıların kendi verilerini düzenleme/silebilir.</span><span class="sxs-lookup"><span data-stu-id="59733-113">**Registered users** can view all the approved data and can edit/delete their own data.</span></span>
* <span data-ttu-id="59733-114">**Yöneticileri** onaylayabilecek veya reddedebilecek kişi verilerini.</span><span class="sxs-lookup"><span data-stu-id="59733-114">**Managers** can approve or reject contact data.</span></span> <span data-ttu-id="59733-115">Yalnızca onaylanan kişilere, kullanıcılar tarafından görülebilir.</span><span class="sxs-lookup"><span data-stu-id="59733-115">Only approved contacts are visible to users.</span></span>
* <span data-ttu-id="59733-116">**Yöneticiler** Onayla/Reddet ve herhangi bir veri düzenleme/silme kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59733-116">**Administrators** can approve/reject and edit/delete any data.</span></span>

<span data-ttu-id="59733-117">Aşağıdaki görüntüde, kullanıcı Rick (`rick@example.com`) açmıştır.</span><span class="sxs-lookup"><span data-stu-id="59733-117">In the following image, user Rick (`rick@example.com`) is signed in.</span></span> <span data-ttu-id="59733-118">Rick yalnızca onaylanan kişiler görüntüleyebilir ve **Düzenle**/**Sil**/**Yeni Oluştur** kendi kişiler için bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="59733-118">Rick can only view approved contacts and **Edit**/**Delete**/**Create New** links for his contacts.</span></span> <span data-ttu-id="59733-119">Yalnızca en son kaydını görüntüler Rick tarafından oluşturulan **Düzenle** ve **Sil** bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="59733-119">Only the last record, created by Rick, displays **Edit** and **Delete** links.</span></span> <span data-ttu-id="59733-120">Bir yöneticinin "Onaylandı" durum olana kadar diğer kullanıcılar en son kaydını görmez.</span><span class="sxs-lookup"><span data-stu-id="59733-120">Other users won't see the last record until a manager or administrator changes the status to "Approved".</span></span>

![Oturum Rick gösteren ekran görüntüsü](secure-data/_static/rick.png)

<span data-ttu-id="59733-122">Aşağıdaki görüntüde, `manager@contoso.com` ve yöneticileri rolünde imzalanır:</span><span class="sxs-lookup"><span data-stu-id="59733-122">In the following image, `manager@contoso.com` is signed in and in the managers role:</span></span>

![Gösteren ekran görüntüsü manager@contoso.com oturum açıldı](secure-data/_static/manager1.png)

<span data-ttu-id="59733-124">Aşağıdaki resimde, bir kişi ayrıntıları görünümünü yöneticileri gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="59733-124">The following image shows the managers details view of a contact:</span></span>

![Bir kişinin yöneticisinin görüntüle](secure-data/_static/manager.png)

<span data-ttu-id="59733-126">**Onayla** ve **Reddet** düğmeleri yalnızca Yöneticiler ve Yöneticiler için görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="59733-126">The **Approve** and **Reject** buttons are only displayed for managers and administrators.</span></span>

<span data-ttu-id="59733-127">Aşağıdaki görüntüde, `admin@contoso.com` ve yöneticiler rolünde imzalanır:</span><span class="sxs-lookup"><span data-stu-id="59733-127">In the following image, `admin@contoso.com` is signed in and in the administrators role:</span></span>

![Gösteren ekran görüntüsü admin@contoso.com oturum açıldı](secure-data/_static/admin.png)

<span data-ttu-id="59733-129">Yöneticisinin tüm ayrıcalıklara sahip değil.</span><span class="sxs-lookup"><span data-stu-id="59733-129">The administrator has all privileges.</span></span> <span data-ttu-id="59733-130">Okuma/düzenleme/silme herhangi iletişime geçebiliriz ve kişiler birinin durumunu değiştirin.</span><span class="sxs-lookup"><span data-stu-id="59733-130">She can read/edit/delete any contact and change the status of contacts.</span></span>

<span data-ttu-id="59733-131">Uygulama tarafından oluşturulan [yapı iskelesi](xref:tutorials/first-mvc-app/adding-model#scaffold-the-movie-model) aşağıdaki `Contact` modeli:</span><span class="sxs-lookup"><span data-stu-id="59733-131">The app was created by [scaffolding](xref:tutorials/first-mvc-app/adding-model#scaffold-the-movie-model) the following `Contact` model:</span></span>

[!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet1)]

<span data-ttu-id="59733-132">Örnek aşağıdaki yetkilendirme işleyicilerini içerir:</span><span class="sxs-lookup"><span data-stu-id="59733-132">The sample contains the following authorization handlers:</span></span>

* <span data-ttu-id="59733-133">`ContactIsOwnerAuthorizationHandler`: Bir kullanıcı yalnızca kendi verilerini düzenleyebilir sağlar.</span><span class="sxs-lookup"><span data-stu-id="59733-133">`ContactIsOwnerAuthorizationHandler`: Ensures that a user can only edit their data.</span></span>
* <span data-ttu-id="59733-134">`ContactManagerAuthorizationHandler`: Yöneticileri onaylayabilir veya kişiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="59733-134">`ContactManagerAuthorizationHandler`: Allows managers to approve or reject contacts.</span></span>
* <span data-ttu-id="59733-135">`ContactAdministratorsAuthorizationHandler`: Yöneticilerin onaylama veya reddetme kişiler ve kişiler düzenleme/silme olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="59733-135">`ContactAdministratorsAuthorizationHandler`: Allows administrators to approve or reject contacts and to edit/delete contacts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59733-136">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="59733-136">Prerequisites</span></span>

<span data-ttu-id="59733-137">Bu öğreticide gelişmiştir.</span><span class="sxs-lookup"><span data-stu-id="59733-137">This tutorial is advanced.</span></span> <span data-ttu-id="59733-138">Sahibi olmalısınız:</span><span class="sxs-lookup"><span data-stu-id="59733-138">You should be familiar with:</span></span>

* [<span data-ttu-id="59733-139">ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="59733-139">ASP.NET Core</span></span>](xref:tutorials/first-mvc-app/start-mvc)
* [<span data-ttu-id="59733-140">Kimlik Doğrulaması</span><span class="sxs-lookup"><span data-stu-id="59733-140">Authentication</span></span>](xref:security/authentication/identity)
* [<span data-ttu-id="59733-141">Hesap Onaylama ve Parola Kurtarma</span><span class="sxs-lookup"><span data-stu-id="59733-141">Account Confirmation and Password Recovery</span></span>](xref:security/authentication/accconfirm)
* [<span data-ttu-id="59733-142">Yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="59733-142">Authorization</span></span>](xref:security/authorization/introduction)
* [<span data-ttu-id="59733-143">Entity Framework Core</span><span class="sxs-lookup"><span data-stu-id="59733-143">Entity Framework Core</span></span>](xref:data/ef-mvc/intro)

::: moniker-end

::: moniker range="= aspnetcore-2.1"

<span data-ttu-id="59733-144">ASP.NET Core 2.1 içinde `User.IsInRole` kullanırken başarısız `AddDefaultIdentity`.</span><span class="sxs-lookup"><span data-stu-id="59733-144">In ASP.NET Core 2.1, `User.IsInRole` fails when using `AddDefaultIdentity`.</span></span> <span data-ttu-id="59733-145">Bu öğreticide `AddDefaultIdentity` ve bu nedenle ASP.NET Core 2.2 veya sonraki bir sürümü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="59733-145">This tutorial uses `AddDefaultIdentity` and therefore requires ASP.NET Core 2.2 or later.</span></span> <span data-ttu-id="59733-146">Bkz: [bu GitHub sorunu](https://github.com/aspnet/Identity/issues/1813#issuecomment-394543909) geçici için.</span><span class="sxs-lookup"><span data-stu-id="59733-146">See [this GitHub issue](https://github.com/aspnet/Identity/issues/1813#issuecomment-394543909) for a work-around.</span></span>

::: moniker-end

::: moniker range=">= aspnetcore-2.1"

## <a name="the-starter-and-completed-app"></a><span data-ttu-id="59733-147">Tamamlanmış uygulama ve başlangıç</span><span class="sxs-lookup"><span data-stu-id="59733-147">The starter and completed app</span></span>

<span data-ttu-id="59733-148">[İndirme](xref:index#how-to-download-a-sample) [tamamlandı](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) uygulama.</span><span class="sxs-lookup"><span data-stu-id="59733-148">[Download](xref:index#how-to-download-a-sample) the [completed](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/final2) app.</span></span> <span data-ttu-id="59733-149">[Test](#test-the-completed-app) tamamlanan uygulama güvenlik özellikleri ile ilgili bilgi sahibi olursunuz.</span><span class="sxs-lookup"><span data-stu-id="59733-149">[Test](#test-the-completed-app) the completed app so you become familiar with its security features.</span></span>

### <a name="the-starter-app"></a><span data-ttu-id="59733-150">Başlangıç uygulaması</span><span class="sxs-lookup"><span data-stu-id="59733-150">The starter app</span></span>

<span data-ttu-id="59733-151">[İndirme](xref:index#how-to-download-a-sample) [başlangıç](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) uygulama.</span><span class="sxs-lookup"><span data-stu-id="59733-151">[Download](xref:index#how-to-download-a-sample) the [starter](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2) app.</span></span>

<span data-ttu-id="59733-152">Uygulamayı çalıştırın, dokunun **ContactManager** bağlamak ve oluşturmak, düzenlemek ve bir kişi Sil doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="59733-152">Run the app, tap the **ContactManager** link, and verify you can create, edit, and delete a contact.</span></span>

## <a name="secure-user-data"></a><span data-ttu-id="59733-153">Kullanıcı verilerinin güvenliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="59733-153">Secure user data</span></span>

<span data-ttu-id="59733-154">Aşağıdaki bölümlerde, güvenli kullanıcı veri uygulaması oluşturmak için ana tüm adımları tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="59733-154">The following sections have all the major steps to create the secure user data app.</span></span> <span data-ttu-id="59733-155">Tamamlanan projeye başvuran daha yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="59733-155">You may find it helpful to refer to the completed project.</span></span>

### <a name="tie-the-contact-data-to-the-user"></a><span data-ttu-id="59733-156">Kullanıcı kişi verilerini bağlayın</span><span class="sxs-lookup"><span data-stu-id="59733-156">Tie the contact data to the user</span></span>

<span data-ttu-id="59733-157">ASP.NET kullanmak [kimlik](xref:security/authentication/identity) kullanıcılar emin olmak için kullanıcı kimliği verilerine, ancak diğer kullanıcıların verileri düzenleyebilir.</span><span class="sxs-lookup"><span data-stu-id="59733-157">Use the ASP.NET [Identity](xref:security/authentication/identity) user ID to ensure users can edit their data, but not other users data.</span></span> <span data-ttu-id="59733-158">Ekleme `OwnerID` ve `ContactStatus` için `Contact` modeli:</span><span class="sxs-lookup"><span data-stu-id="59733-158">Add `OwnerID` and `ContactStatus` to the `Contact` model:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Models/Contact.cs?name=snippet1&highlight=5-6,16-999)]

<span data-ttu-id="59733-159">`OwnerID` kullanıcının kimliği olan `AspNetUser` tablosundaki [kimlik](xref:security/authentication/identity) veritabanı.</span><span class="sxs-lookup"><span data-stu-id="59733-159">`OwnerID` is the user's ID from the `AspNetUser` table in the [Identity](xref:security/authentication/identity) database.</span></span> <span data-ttu-id="59733-160">`Status` Alanı, bir kişi genel kullanıcılar tarafından görüntülenebilir olup olmadığını belirler.</span><span class="sxs-lookup"><span data-stu-id="59733-160">The `Status` field determines if a contact is viewable by general users.</span></span>

<span data-ttu-id="59733-161">Yeni geçiş oluştur ve veritabanını güncelleştir:</span><span class="sxs-lookup"><span data-stu-id="59733-161">Create a new migration and update the database:</span></span>

```console
dotnet ef migrations add userID_Status
dotnet ef database update
```

### <a name="add-role-services-to-identity"></a><span data-ttu-id="59733-162">Kimlik için rol hizmetleri Ekle</span><span class="sxs-lookup"><span data-stu-id="59733-162">Add Role services to Identity</span></span>

<span data-ttu-id="59733-163">Append [ndeki](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) rol hizmetlerini eklemek için:</span><span class="sxs-lookup"><span data-stu-id="59733-163">Append [AddRoles](/dotnet/api/microsoft.aspnetcore.identity.identitybuilder.addroles#Microsoft_AspNetCore_Identity_IdentityBuilder_AddRoles__1) to add Role services:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet2&highlight=12)]

### <a name="require-authenticated-users"></a><span data-ttu-id="59733-164">Kimliği doğrulanmış kullanıcılar gerektirir</span><span class="sxs-lookup"><span data-stu-id="59733-164">Require authenticated users</span></span>

<span data-ttu-id="59733-165">Kullanıcıların kimliklerinin doğrulanmasını istemek için varsayılan kimlik doğrulama ilkesi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="59733-165">Set the default authentication policy to require users to be authenticated:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet&highlight=17-99)] 

 <span data-ttu-id="59733-166">Kimlik doğrulaması ile Razor sayfası, denetleyici veya eylem yöntemi düzeyinde dışında iyileştirilmiş `[AllowAnonymous]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="59733-166">You can opt out of authentication at the Razor Page, controller, or action method level with the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="59733-167">Kullanıcıların kimliklerinin doğrulanmasını istemek için varsayılan kimlik doğrulama İlkesi ayarı, yeni eklenen Razor sayfaları ve denetleyicileri korur.</span><span class="sxs-lookup"><span data-stu-id="59733-167">Setting the default authentication policy to require users to be authenticated protects newly added Razor Pages and controllers.</span></span> <span data-ttu-id="59733-168">Kimlik doğrulaması varsayılan olarak gerekli olan bağlı olan, yeni denetleyicileri ve dahil etmek için Razor sayfaları hakkında daha fazla güvenli `[Authorize]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="59733-168">Having authentication required by default is more secure than relying on new controllers and Razor Pages to include the `[Authorize]` attribute.</span></span>

<span data-ttu-id="59733-169">Ekleme [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) dizine hakkında ve kişi sayfaları böylece bunlar kaydetmeden önce anonim kullanıcılar siteyle ilgili bilgileri elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59733-169">Add [AllowAnonymous](/dotnet/api/microsoft.aspnetcore.authorization.allowanonymousattribute) to the Index, About, and Contact pages so anonymous users can get information about the site before they register.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Index.cshtml.cs?highlight=1,6)]

### <a name="configure-the-test-account"></a><span data-ttu-id="59733-170">Test hesabı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="59733-170">Configure the test account</span></span>

<span data-ttu-id="59733-171">`SeedData` Sınıfı iki hesap oluşturur: Yönetici ve.</span><span class="sxs-lookup"><span data-stu-id="59733-171">The `SeedData` class creates two accounts: administrator and manager.</span></span> <span data-ttu-id="59733-172">Kullanım [gizli dizi Yöneticisi aracını](xref:security/app-secrets) bu hesaplar için bir parola ayarlamak için.</span><span class="sxs-lookup"><span data-stu-id="59733-172">Use the [Secret Manager tool](xref:security/app-secrets) to set a password for these accounts.</span></span> <span data-ttu-id="59733-173">Proje dizininden parolayı ayarlayın (dizinini içeren *Program.cs*):</span><span class="sxs-lookup"><span data-stu-id="59733-173">Set the password from the project directory (the directory containing *Program.cs*):</span></span>

```console
dotnet user-secrets set SeedUserPW <PW>
```

<span data-ttu-id="59733-174">Güçlü bir parola belirtilmediği takdirde, bir özel durum `SeedData.Initialize` çağrılır.</span><span class="sxs-lookup"><span data-stu-id="59733-174">If a strong password is not specified, an exception is thrown when `SeedData.Initialize` is called.</span></span>

<span data-ttu-id="59733-175">Güncelleştirme `Main` test parola kullanmak üzere:</span><span class="sxs-lookup"><span data-stu-id="59733-175">Update `Main` to use the test password:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Program.cs?name=snippet)]

### <a name="create-the-test-accounts-and-update-the-contacts"></a><span data-ttu-id="59733-176">Test hesapları oluşturabilir ve kişilerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="59733-176">Create the test accounts and update the contacts</span></span>

<span data-ttu-id="59733-177">Güncelleştirme `Initialize` yönteminde `SeedData` test hesapları oluşturma sınıfı:</span><span class="sxs-lookup"><span data-stu-id="59733-177">Update the `Initialize` method in the `SeedData` class to create the test accounts:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet_Initialize)]

<span data-ttu-id="59733-178">Yönetici kullanıcı Kimliğini ekleyin ve `ContactStatus` kişilere.</span><span class="sxs-lookup"><span data-stu-id="59733-178">Add the administrator user ID and `ContactStatus` to the contacts.</span></span> <span data-ttu-id="59733-179">"Gönderildi" ve "Reddedildi" bir kişilerden biri olun.</span><span class="sxs-lookup"><span data-stu-id="59733-179">Make one of the contacts "Submitted" and one "Rejected".</span></span> <span data-ttu-id="59733-180">Kullanıcı kimliği ve durumu tüm kişileri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59733-180">Add the user ID and status to all the contacts.</span></span> <span data-ttu-id="59733-181">Tek bir kişi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="59733-181">Only one contact is shown:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Data/SeedData.cs?name=snippet1&highlight=17,18)]

## <a name="create-owner-manager-and-administrator-authorization-handlers"></a><span data-ttu-id="59733-182">Sahip, yönetici ve yönetici yetkilendirme işleyicileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="59733-182">Create owner, manager, and administrator authorization handlers</span></span>

<span data-ttu-id="59733-183">Oluşturma bir `ContactIsOwnerAuthorizationHandler` sınıfını *yetkilendirme* klasör.</span><span class="sxs-lookup"><span data-stu-id="59733-183">Create a `ContactIsOwnerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="59733-184">`ContactIsOwnerAuthorizationHandler` Bir kaynakta çalışan kullanıcı kaynağın sahibi doğrular.</span><span class="sxs-lookup"><span data-stu-id="59733-184">The `ContactIsOwnerAuthorizationHandler` verifies that the user acting on a resource owns the resource.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactIsOwnerAuthorizationHandler.cs)]

<span data-ttu-id="59733-185">`ContactIsOwnerAuthorizationHandler` Çağrıları [bağlamı. Başarılı](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) kişi sahibi kimliği doğrulanmış geçerli kullanıcı ise.</span><span class="sxs-lookup"><span data-stu-id="59733-185">The `ContactIsOwnerAuthorizationHandler` calls [context.Succeed](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.succeed#Microsoft_AspNetCore_Authorization_AuthorizationHandlerContext_Succeed_Microsoft_AspNetCore_Authorization_IAuthorizationRequirement_) if the current authenticated user is the contact owner.</span></span> <span data-ttu-id="59733-186">Yetkilendirme işleyicileri genellikle:</span><span class="sxs-lookup"><span data-stu-id="59733-186">Authorization handlers generally:</span></span>

* <span data-ttu-id="59733-187">Dönüş `context.Succeed` gereksinimleri karşılanmadığı zaman.</span><span class="sxs-lookup"><span data-stu-id="59733-187">Return `context.Succeed` when the requirements are met.</span></span>
* <span data-ttu-id="59733-188">Dönüş `Task.CompletedTask` zaman olmayan gereksinimleri karşılanıyor.</span><span class="sxs-lookup"><span data-stu-id="59733-188">Return `Task.CompletedTask` when requirements aren't met.</span></span> <span data-ttu-id="59733-189">`Task.CompletedTask` ne success veya FAILURE olur&mdash;çalıştırmak, diğer yetkilendirme işleyicileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="59733-189">`Task.CompletedTask` is neither success or failure&mdash;it allows other authorization handlers to run.</span></span>

<span data-ttu-id="59733-190">Açıkça başarısız gerekiyorsa, iade [bağlamı. Başarısız](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail).</span><span class="sxs-lookup"><span data-stu-id="59733-190">If you need to explicitly fail, return [context.Fail](/dotnet/api/microsoft.aspnetcore.authorization.authorizationhandlercontext.fail).</span></span>

<span data-ttu-id="59733-191">Düzenleme/silme/oluşturma iletişim sahiplere kendi verilerini verir.</span><span class="sxs-lookup"><span data-stu-id="59733-191">The app allows contact owners to edit/delete/create their own data.</span></span> <span data-ttu-id="59733-192">`ContactIsOwnerAuthorizationHandler` gereksinim parametrede aktarılan işlemi denetleyin. gerekmez.</span><span class="sxs-lookup"><span data-stu-id="59733-192">`ContactIsOwnerAuthorizationHandler` doesn't need to check the operation passed in the requirement parameter.</span></span>

### <a name="create-a-manager-authorization-handler"></a><span data-ttu-id="59733-193">Bir yönetici yetkilendirme işleyici oluşturun</span><span class="sxs-lookup"><span data-stu-id="59733-193">Create a manager authorization handler</span></span>

<span data-ttu-id="59733-194">Oluşturma bir `ContactManagerAuthorizationHandler` sınıfını *yetkilendirme* klasör.</span><span class="sxs-lookup"><span data-stu-id="59733-194">Create a `ContactManagerAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="59733-195">`ContactManagerAuthorizationHandler` Kaynak üzerinde çalışan kullanıcı, bir yönetici yer almadığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="59733-195">The `ContactManagerAuthorizationHandler` verifies the user acting on the resource is a manager.</span></span> <span data-ttu-id="59733-196">Yalnızca Yöneticiler onaylayabileceğiniz veya reddedebileceğiniz içerik değişiklikleri (yeni veya değiştirilmiş).</span><span class="sxs-lookup"><span data-stu-id="59733-196">Only managers can approve or reject content changes (new or changed).</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactManagerAuthorizationHandler.cs)]

### <a name="create-an-administrator-authorization-handler"></a><span data-ttu-id="59733-197">Bir yönetici yetkilendirme işleyicisi oluşturun</span><span class="sxs-lookup"><span data-stu-id="59733-197">Create an administrator authorization handler</span></span>

<span data-ttu-id="59733-198">Oluşturma bir `ContactAdministratorsAuthorizationHandler` sınıfını *yetkilendirme* klasör.</span><span class="sxs-lookup"><span data-stu-id="59733-198">Create a `ContactAdministratorsAuthorizationHandler` class in the *Authorization* folder.</span></span> <span data-ttu-id="59733-199">`ContactAdministratorsAuthorizationHandler` Kaynak üzerinde çalışan kullanıcı, yönetici yer almadığını doğrular.</span><span class="sxs-lookup"><span data-stu-id="59733-199">The `ContactAdministratorsAuthorizationHandler` verifies the user acting on the resource is an administrator.</span></span> <span data-ttu-id="59733-200">Yönetici, tüm işlemleri yapabilir.</span><span class="sxs-lookup"><span data-stu-id="59733-200">Administrator can do all operations.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactAdministratorsAuthorizationHandler.cs)]

## <a name="register-the-authorization-handlers"></a><span data-ttu-id="59733-201">Yetkilendirme işleyicilerini kaydedin</span><span class="sxs-lookup"><span data-stu-id="59733-201">Register the authorization handlers</span></span>

<span data-ttu-id="59733-202">Entity Framework Core kullanan hizmetler için kaydedilmelidir [bağımlılık ekleme](xref:fundamentals/dependency-injection) kullanarak [AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions).</span><span class="sxs-lookup"><span data-stu-id="59733-202">Services using Entity Framework Core must be registered for [dependency injection](xref:fundamentals/dependency-injection) using [AddScoped](/dotnet/api/microsoft.extensions.dependencyinjection.servicecollectionserviceextensions).</span></span> <span data-ttu-id="59733-203">`ContactIsOwnerAuthorizationHandler` ASP.NET Core kullanan [kimlik](xref:security/authentication/identity), Entity Framework Core üzerinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="59733-203">The `ContactIsOwnerAuthorizationHandler` uses ASP.NET Core [Identity](xref:security/authentication/identity), which is built on Entity Framework Core.</span></span> <span data-ttu-id="59733-204">Kullanılabilir bulunmaları işleyicilerini hizmet koleksiyonuyla kaydedin `ContactsController` aracılığıyla [bağımlılık ekleme](xref:fundamentals/dependency-injection).</span><span class="sxs-lookup"><span data-stu-id="59733-204">Register the handlers with the service collection so they're available to the `ContactsController` through [dependency injection](xref:fundamentals/dependency-injection).</span></span> <span data-ttu-id="59733-205">Sonuna aşağıdaki kodu ekleyin `ConfigureServices`:</span><span class="sxs-lookup"><span data-stu-id="59733-205">Add the following code to the end of `ConfigureServices`:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Startup.cs?name=snippet_defaultPolicy&highlight=27-99)]

<span data-ttu-id="59733-206">`ContactAdministratorsAuthorizationHandler` ve `ContactManagerAuthorizationHandler` teklileri eklenir.</span><span class="sxs-lookup"><span data-stu-id="59733-206">`ContactAdministratorsAuthorizationHandler` and `ContactManagerAuthorizationHandler` are added as singletons.</span></span> <span data-ttu-id="59733-207">Oldukları teklileri çünkü bunlar EF kullanmayın ve gereken tüm bilgiler `Context` parametresinin `HandleRequirementAsync` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="59733-207">They're singletons because they don't use EF and all the information needed is in the `Context` parameter of the `HandleRequirementAsync` method.</span></span>

## <a name="support-authorization"></a><span data-ttu-id="59733-208">Destek yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="59733-208">Support authorization</span></span>

<span data-ttu-id="59733-209">Bu bölümde, Razor sayfaları güncelleştirmeniz ve bir işlem gereksinimleri sınıfı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59733-209">In this section, you update the Razor Pages and add an operations requirements class.</span></span>

### <a name="review-the-contact-operations-requirements-class"></a><span data-ttu-id="59733-210">Gözden geçirme kişi işlem gereksinimleri sınıfı</span><span class="sxs-lookup"><span data-stu-id="59733-210">Review the contact operations requirements class</span></span>

<span data-ttu-id="59733-211">Gözden geçirme `ContactOperations` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="59733-211">Review the `ContactOperations` class.</span></span> <span data-ttu-id="59733-212">Bu sınıf gereksinimleri içeren uygulama destekler:</span><span class="sxs-lookup"><span data-stu-id="59733-212">This class contains the requirements the app supports:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Authorization/ContactOperations.cs)]

### <a name="create-a-base-class-for-the-contacts-razor-pages"></a><span data-ttu-id="59733-213">Kişiler Razor sayfaları için bir temel sınıf oluşturma</span><span class="sxs-lookup"><span data-stu-id="59733-213">Create a base class for the Contacts Razor Pages</span></span>

<span data-ttu-id="59733-214">Razor sayfaları kişiler kullanılan hizmetler içeren temel bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="59733-214">Create a base class that contains the services used in the contacts Razor Pages.</span></span> <span data-ttu-id="59733-215">Temel sınıf başlatma kodunu tek bir yerde getirir:</span><span class="sxs-lookup"><span data-stu-id="59733-215">The base class puts the initialization code in one location:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/DI_BasePageModel.cs)]

<span data-ttu-id="59733-216">Yukarıdaki kod:</span><span class="sxs-lookup"><span data-stu-id="59733-216">The preceding code:</span></span>

* <span data-ttu-id="59733-217">Ekler `IAuthorizationService` yetkilendirme işleyicilere erişmek için hizmet.</span><span class="sxs-lookup"><span data-stu-id="59733-217">Adds the `IAuthorizationService` service to access to the authorization handlers.</span></span>
* <span data-ttu-id="59733-218">Kimlik ekler `UserManager` hizmeti.</span><span class="sxs-lookup"><span data-stu-id="59733-218">Adds the Identity `UserManager` service.</span></span>
* <span data-ttu-id="59733-219">Ekleme `ApplicationDbContext`.</span><span class="sxs-lookup"><span data-stu-id="59733-219">Add the `ApplicationDbContext`.</span></span>

### <a name="update-the-createmodel"></a><span data-ttu-id="59733-220">Güncelleştirme CreateModel</span><span class="sxs-lookup"><span data-stu-id="59733-220">Update the CreateModel</span></span>

<span data-ttu-id="59733-221">Kullanılacak Oluştur sayfası model Oluşturucu güncelleştirme `DI_BasePageModel` temel sınıfı:</span><span class="sxs-lookup"><span data-stu-id="59733-221">Update the create page model constructor to use the `DI_BasePageModel` base class:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippetCtor)]

<span data-ttu-id="59733-222">Güncelleştirme `CreateModel.OnPostAsync` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="59733-222">Update the `CreateModel.OnPostAsync` method to:</span></span>

* <span data-ttu-id="59733-223">Kullanıcı Kimliğinize ekleme `Contact` modeli.</span><span class="sxs-lookup"><span data-stu-id="59733-223">Add the user ID to the `Contact` model.</span></span>
* <span data-ttu-id="59733-224">Kullanıcının Kişiler oluşturma iznine sahip doğrulamak için yetkilendirme işleyici çağırın.</span><span class="sxs-lookup"><span data-stu-id="59733-224">Call the authorization handler to verify the user has permission to create contacts.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Create.cshtml.cs?name=snippet_Create)]

### <a name="update-the-indexmodel"></a><span data-ttu-id="59733-225">Güncelleştirme IndexModel</span><span class="sxs-lookup"><span data-stu-id="59733-225">Update the IndexModel</span></span>

<span data-ttu-id="59733-226">Güncelleştirme `OnGetAsync` yalnızca onaylanan kişilere genel kullanıcılara gösterilecek şekilde yöntemi:</span><span class="sxs-lookup"><span data-stu-id="59733-226">Update the `OnGetAsync` method so only approved contacts are shown to general users:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml.cs?name=snippet)]

### <a name="update-the-editmodel"></a><span data-ttu-id="59733-227">Güncelleştirme EditModel</span><span class="sxs-lookup"><span data-stu-id="59733-227">Update the EditModel</span></span>

<span data-ttu-id="59733-228">Kullanıcının sahip olduğu kişi doğrulamak için bir yetkilendirme işleyicisi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59733-228">Add an authorization handler to verify the user owns the contact.</span></span> <span data-ttu-id="59733-229">Kaynak Yetkilendirme Doğrulanmakta olan çünkü `[Authorize]` özniteliği yeterli değil.</span><span class="sxs-lookup"><span data-stu-id="59733-229">Because resource authorization is being validated, the `[Authorize]` attribute is not enough.</span></span> <span data-ttu-id="59733-230">Öznitelikleri değerlendirildiğinde uygulama kaynağa erişimi yok.</span><span class="sxs-lookup"><span data-stu-id="59733-230">The app doesn't have access to the resource when attributes are evaluated.</span></span> <span data-ttu-id="59733-231">Kaynak tabanlı yetkilendirme kesinlik temelli olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="59733-231">Resource-based authorization must be imperative.</span></span> <span data-ttu-id="59733-232">Uygulama sayfası modele yükleniyor ya da işleyicisinin içerisinde yükleme kaynağına erişimi olduğunda denetimleri gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="59733-232">Checks must be performed once the app has access to the resource, either by loading it in the page model or by loading it within the handler itself.</span></span> <span data-ttu-id="59733-233">Sık sık geçirerek kaynak anahtarı kaynağa erişir.</span><span class="sxs-lookup"><span data-stu-id="59733-233">You frequently access the resource by passing in the resource key.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Edit.cshtml.cs?name=snippet)]

### <a name="update-the-deletemodel"></a><span data-ttu-id="59733-234">Güncelleştirme DeleteModel</span><span class="sxs-lookup"><span data-stu-id="59733-234">Update the DeleteModel</span></span>

<span data-ttu-id="59733-235">Delete sayfa modeli, kişi hakkında kullanıcıyı silme izni doğrulamak için yetkilendirme işleyicisi kullanacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="59733-235">Update the delete page model to use the authorization handler to verify the user has delete permission on the contact.</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Delete.cshtml.cs?name=snippet)]

## <a name="inject-the-authorization-service-into-the-views"></a><span data-ttu-id="59733-236">Kimlik doğrulama servisi görünümlere ekleme</span><span class="sxs-lookup"><span data-stu-id="59733-236">Inject the authorization service into the views</span></span>

<span data-ttu-id="59733-237">Şu anda kullanıcı Arabirimi gösterir düzenleyin ve kişiler kullanıcı değiştiremez bağlantılarını silin.</span><span class="sxs-lookup"><span data-stu-id="59733-237">Currently, the UI shows edit and delete links for contacts the user can't modify.</span></span>

<span data-ttu-id="59733-238">Yetkilendirme hizmetinde ekleme *Views/_ViewImports.cshtml* tüm görünümlere kullanılabilir olacak şekilde dosya:</span><span class="sxs-lookup"><span data-stu-id="59733-238">Inject the authorization service in the *Views/_ViewImports.cshtml* file so it's available to all views:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/_ViewImports.cshtml?highlight=6-99)]

<span data-ttu-id="59733-239">Birkaç önceki biçimlendirme ekler `using` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="59733-239">The preceding markup adds several `using` statements.</span></span>

<span data-ttu-id="59733-240">Güncelleştirme **Düzenle** ve **Sil** bağlantılar *Pages/Contacts/Index.cshtml* bunlar yalnızca uygun izinlere sahip kullanıcılar tarafından işlenen için:</span><span class="sxs-lookup"><span data-stu-id="59733-240">Update the **Edit** and **Delete** links in *Pages/Contacts/Index.cshtml* so they're only rendered for users with the appropriate permissions:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Index.cshtml?highlight=34-36,62-999)]

> [!WARNING]
> <span data-ttu-id="59733-241">Bağlantıları veri değiştirme iznine sahip olmayan kullanıcılardan gizleyerek uygulama güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="59733-241">Hiding links from users that don't have permission to change data doesn't secure the app.</span></span> <span data-ttu-id="59733-242">Bağlantıları gizleme uygulamayı daha kullanıcı dostu yalnızca geçerli bağlantıları görüntüleyerek yapar.</span><span class="sxs-lookup"><span data-stu-id="59733-242">Hiding links makes the app more user-friendly by displaying only valid links.</span></span> <span data-ttu-id="59733-243">Kullanıcıları düzenleme çağırmak ve silme işlemleri ait olmayan veriler üzerinde oluşturulan URL'leri hack.</span><span class="sxs-lookup"><span data-stu-id="59733-243">Users can hack the generated URLs to invoke edit and delete operations on data they don't own.</span></span> <span data-ttu-id="59733-244">Razor sayfası veya denetleyici verileri korumak için erişim denetimleri zorlamalıdır.</span><span class="sxs-lookup"><span data-stu-id="59733-244">The Razor Page or controller must enforce access checks to secure the data.</span></span>

### <a name="update-details"></a><span data-ttu-id="59733-245">Güncelleştirme ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="59733-245">Update Details</span></span>

<span data-ttu-id="59733-246">Ayrıntılar görünümü yöneticileri onaylayabilir veya reddedebilir kişiler güncelleştirin:</span><span class="sxs-lookup"><span data-stu-id="59733-246">Update the details view so managers can approve or reject contacts:</span></span>

[!code-cshtml[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml?name=snippet)]

<span data-ttu-id="59733-247">Güncelleştirme ayrıntıları sayfa modeli:</span><span class="sxs-lookup"><span data-stu-id="59733-247">Update the details page model:</span></span>

[!code-csharp[](secure-data/samples/final2.1/Pages/Contacts/Details.cshtml.cs?name=snippet)]

## <a name="add-or-remove-a-user-to-a-role"></a><span data-ttu-id="59733-248">Ekleme veya bir rolü için bir kullanıcıyı kaldırma</span><span class="sxs-lookup"><span data-stu-id="59733-248">Add or remove a user to a role</span></span>

<span data-ttu-id="59733-249">Bkz: [bu sorunu](https://github.com/aspnet/Docs/issues/8502) hakkında bilgi için:</span><span class="sxs-lookup"><span data-stu-id="59733-249">See [this issue](https://github.com/aspnet/Docs/issues/8502) for information on:</span></span>

* <span data-ttu-id="59733-250">Bir kullanıcıdan ayrıcalıklarının kaldırılması.</span><span class="sxs-lookup"><span data-stu-id="59733-250">Removing privileges from a user.</span></span> <span data-ttu-id="59733-251">Örneğin, bir kullanıcı bir sohbet uygulaması ses kapatma.</span><span class="sxs-lookup"><span data-stu-id="59733-251">For example muting a user in a chat app.</span></span>
* <span data-ttu-id="59733-252">Bir kullanıcı ayrıcalıkları ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="59733-252">Adding privileges to a user.</span></span>

## <a name="test-the-completed-app"></a><span data-ttu-id="59733-253">Tamamlanmış uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="59733-253">Test the completed app</span></span>

<span data-ttu-id="59733-254">Kapsanan kullanıcı hesapları için bir parola belirlemediyseniz kullanın [gizli dizi Yöneticisi aracını](xref:security/app-secrets#secret-manager) parola ayarlamak için:</span><span class="sxs-lookup"><span data-stu-id="59733-254">If you haven't already set a password for seeded user accounts, use the [Secret Manager tool](xref:security/app-secrets#secret-manager) to set a password:</span></span>

* <span data-ttu-id="59733-255">Güçlü bir parola seçin: Sekiz kullanın veya daha fazla karakter ve en az bir büyük harf karakter, sayı ve simge.</span><span class="sxs-lookup"><span data-stu-id="59733-255">Choose a strong password: Use eight or more characters and at least one upper-case character, number, and symbol.</span></span> <span data-ttu-id="59733-256">Örneğin, `Passw0rd!` güçlü parola gereksinimlerini karşılıyor.</span><span class="sxs-lookup"><span data-stu-id="59733-256">For example, `Passw0rd!` meets the strong password requirements.</span></span>
* <span data-ttu-id="59733-257">Aşağıdaki komutu yürütün proje klasöründen burada `<PW>` parola:</span><span class="sxs-lookup"><span data-stu-id="59733-257">Execute the following command from the project's folder, where `<PW>` is the password:</span></span>

  ```console
  dotnet user-secrets set SeedUserPW <PW>
  ```

<span data-ttu-id="59733-258">Uygulamanın, kişiler varsa:</span><span class="sxs-lookup"><span data-stu-id="59733-258">If the app has contacts:</span></span>

* <span data-ttu-id="59733-259">Tüm kayıtları silin `Contact` tablo.</span><span class="sxs-lookup"><span data-stu-id="59733-259">Delete all of the records in the `Contact` table.</span></span>
* <span data-ttu-id="59733-260">Veritabanının çekirdeğini oluşturma için uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="59733-260">Restart the app to seed the database.</span></span>

<span data-ttu-id="59733-261">Tamamlanmış uygulamayı test etmek için kolay bir yolu, üç farklı tarayıcılar (veya ıncognito/InPrivate oturumları) başlatılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="59733-261">An easy way to test the completed app is to launch three different browsers (or incognito/InPrivate sessions).</span></span> <span data-ttu-id="59733-262">Yeni bir kullanıcı bir tarayıcıda kaydedin (örneğin, `test@example.com`).</span><span class="sxs-lookup"><span data-stu-id="59733-262">In one browser, register a new user (for example, `test@example.com`).</span></span> <span data-ttu-id="59733-263">Her bir tarayıcıya farklı bir kullanıcı ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="59733-263">Sign in to each browser with a different user.</span></span> <span data-ttu-id="59733-264">Aşağıdaki işlemleri doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="59733-264">Verify the following operations:</span></span>

* <span data-ttu-id="59733-265">Kayıtlı kullanıcılar tüm onaylanmış kişi verilerini görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="59733-265">Registered users can view all of the approved contact data.</span></span>
* <span data-ttu-id="59733-266">Kayıtlı kullanıcıların kendi verilerini düzenleme/silebilir.</span><span class="sxs-lookup"><span data-stu-id="59733-266">Registered users can edit/delete their own data.</span></span>
* <span data-ttu-id="59733-267">Yöneticileri Onayla/kişi verilerini reddet.</span><span class="sxs-lookup"><span data-stu-id="59733-267">Managers can approve/reject contact data.</span></span> <span data-ttu-id="59733-268">`Details` Görüntülemek gösterir **Onayla** ve **Reddet** düğmeleri.</span><span class="sxs-lookup"><span data-stu-id="59733-268">The `Details` view shows **Approve** and **Reject** buttons.</span></span>
* <span data-ttu-id="59733-269">Yöneticiler Onayla/Reddet ve tüm verileri düzenleme/silme.</span><span class="sxs-lookup"><span data-stu-id="59733-269">Administrators can approve/reject and edit/delete all data.</span></span>

| <span data-ttu-id="59733-270">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="59733-270">User</span></span>                | <span data-ttu-id="59733-271">Uygulama tarafından sağlanmış</span><span class="sxs-lookup"><span data-stu-id="59733-271">Seeded by the app</span></span> | <span data-ttu-id="59733-272">Seçenekler</span><span class="sxs-lookup"><span data-stu-id="59733-272">Options</span></span>                                  |
| ------------------- | :---------------: | ---------------------------------------- |
| test@example.com    | <span data-ttu-id="59733-273">Hayır</span><span class="sxs-lookup"><span data-stu-id="59733-273">No</span></span>                | <span data-ttu-id="59733-274">Kendi veri düzenleme veya silme.</span><span class="sxs-lookup"><span data-stu-id="59733-274">Edit/delete the own data.</span></span>                |
| manager@contoso.com | <span data-ttu-id="59733-275">Evet</span><span class="sxs-lookup"><span data-stu-id="59733-275">Yes</span></span>               | <span data-ttu-id="59733-276">Onayla/Reddet ve kendi veri düzenleme/silme.</span><span class="sxs-lookup"><span data-stu-id="59733-276">Approve/reject and edit/delete own data.</span></span> |
| admin@contoso.com   | <span data-ttu-id="59733-277">Evet</span><span class="sxs-lookup"><span data-stu-id="59733-277">Yes</span></span>               | <span data-ttu-id="59733-278">Onayla/Reddet ve tüm verileri düzenleme/silme.</span><span class="sxs-lookup"><span data-stu-id="59733-278">Approve/reject and edit/delete all data.</span></span> |

<span data-ttu-id="59733-279">Bir kişi, yöneticinin tarayıcıda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="59733-279">Create a contact in the administrator's browser.</span></span> <span data-ttu-id="59733-280">Silme için URL'yi kopyalayın ve yönetici kişiden düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="59733-280">Copy the URL for delete and edit from the administrator contact.</span></span> <span data-ttu-id="59733-281">Bu bağlantıları test kullanıcı bu işlemleri gerçekleştiremezsiniz doğrulamak için test kullanıcının tarayıcısına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="59733-281">Paste these links into the test user's browser to verify the test user can't perform these operations.</span></span>

## <a name="create-the-starter-app"></a><span data-ttu-id="59733-282">Başlangıç uygulaması oluşturun</span><span class="sxs-lookup"><span data-stu-id="59733-282">Create the starter app</span></span>

* <span data-ttu-id="59733-283">"ContactManager" adlı bir Razor sayfaları uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="59733-283">Create a Razor Pages app named "ContactManager"</span></span>
  * <span data-ttu-id="59733-284">Uygulamayı oluşturma **bireysel kullanıcı hesapları**.</span><span class="sxs-lookup"><span data-stu-id="59733-284">Create the app with **Individual User Accounts**.</span></span>
  * <span data-ttu-id="59733-285">Örnekte kullanılan ad alanı ad alanı eşleşecek şekilde "ContactManager" adlandırın.</span><span class="sxs-lookup"><span data-stu-id="59733-285">Name it "ContactManager" so the namespace matches the namespace used in the sample.</span></span>
  * <span data-ttu-id="59733-286">`-uld` LocalDB yerine SQLite belirtir</span><span class="sxs-lookup"><span data-stu-id="59733-286">`-uld` specifies LocalDB instead of SQLite</span></span>

  ```console
  dotnet new webapp -o ContactManager -au Individual -uld
  ```

* <span data-ttu-id="59733-287">Ekleme *Models/Contact.cs*:</span><span class="sxs-lookup"><span data-stu-id="59733-287">Add *Models/Contact.cs*:</span></span>

  [!code-csharp[](secure-data/samples/starter2.1/Models/Contact.cs?name=snippet1)]

* <span data-ttu-id="59733-288">İskele `Contact` modeli.</span><span class="sxs-lookup"><span data-stu-id="59733-288">Scaffold the `Contact` model.</span></span>
* <span data-ttu-id="59733-289">İlk geçiş oluşturun ve veritabanını güncelleştir:</span><span class="sxs-lookup"><span data-stu-id="59733-289">Create initial migration and update the database:</span></span>

  ```console
  dotnet aspnet-codegenerator razorpage -m Contact -udl -dc ApplicationDbContext -outDir Pages\Contacts --referenceScriptLibraries
  dotnet ef database drop -f
  dotnet ef migrations add initial
  dotnet ef database update
  ```

* <span data-ttu-id="59733-290">Güncelleştirme **ContactManager** içinde yer işareti *Pages/_Layout.cshtml* dosyası:</span><span class="sxs-lookup"><span data-stu-id="59733-290">Update the **ContactManager** anchor in the *Pages/_Layout.cshtml* file:</span></span>

  ```cshtml
  <a asp-page="/Contacts/Index" class="navbar-brand">ContactManager</a>
  ```

* <span data-ttu-id="59733-291">Oluşturma, düzenleme ve silme kişi uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="59733-291">Test the app by creating, editing, and deleting a contact</span></span>

### <a name="seed-the-database"></a><span data-ttu-id="59733-292">Veritabanının çekirdeğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="59733-292">Seed the database</span></span>

<span data-ttu-id="59733-293">Ekleme [SeedData](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2.1/Data/SeedData.cs) sınıfının *veri* klasör.</span><span class="sxs-lookup"><span data-stu-id="59733-293">Add the [SeedData](https://github.com/aspnet/Docs/tree/master/aspnetcore/security/authorization/secure-data/samples/starter2.1/Data/SeedData.cs) class to the *Data* folder.</span></span>

<span data-ttu-id="59733-294">Çağrı `SeedData.Initialize` gelen `Main`:</span><span class="sxs-lookup"><span data-stu-id="59733-294">Call `SeedData.Initialize` from `Main`:</span></span>

[!code-csharp[](secure-data/samples/starter2.1/Program.cs?name=snippet)]

<span data-ttu-id="59733-295">Test, uygulama veritabanını sağlanmış.</span><span class="sxs-lookup"><span data-stu-id="59733-295">Test that the app seeded the database.</span></span> <span data-ttu-id="59733-296">DB ilgili herhangi bir satır varsa, seed yöntemi çalıştırılmaz.</span><span class="sxs-lookup"><span data-stu-id="59733-296">If there are any rows in the contact DB, the seed method doesn't run.</span></span>

<a name="secure-data-add-resources-label"></a>

### <a name="additional-resources"></a><span data-ttu-id="59733-297">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="59733-297">Additional resources</span></span>

* [<span data-ttu-id="59733-298">Azure App Service'te .NET Core ve SQL veritabanı web uygulaması derleme</span><span class="sxs-lookup"><span data-stu-id="59733-298">Build a .NET Core and SQL Database web app in Azure App Service</span></span>](/azure/app-service/app-service-web-tutorial-dotnetcore-sqldb)
* <span data-ttu-id="59733-299">[ASP.NET Core yetkilendirme Laboratuvar](https://github.com/blowdart/AspNetAuthorizationWorkshop).</span><span class="sxs-lookup"><span data-stu-id="59733-299">[ASP.NET Core Authorization Lab](https://github.com/blowdart/AspNetAuthorizationWorkshop).</span></span> <span data-ttu-id="59733-300">Bu Laboratuvar, bu öğreticide sunulan güvenlik özellikleri hakkında daha fazla ayrıntıya gider.</span><span class="sxs-lookup"><span data-stu-id="59733-300">This lab goes into more detail on the security features introduced in this tutorial.</span></span>
* <xref:security/authorization/introduction>
* [<span data-ttu-id="59733-301">Özel ilke tabanlı yetkilendirme</span><span class="sxs-lookup"><span data-stu-id="59733-301">Custom policy-based authorization</span></span>](xref:security/authorization/policies)

::: moniker-end
