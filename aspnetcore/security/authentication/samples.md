---
title: ASP.NET Core kimlik doğrulaması örnekleri
author: rick-anderson
description: ASP.NET Core depodaki kimlik doğrulaması örneklere bağlantılar sağlar.
ms.author: riande
ms.date: 01/31/2019
uid: security/authentication/samples
ms.openlocfilehash: 7b3c911d60ad4737ebd12ce6f7628ad624b11658
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57076611"
---
# <a name="authentication-samples-for-aspnet-core"></a><span data-ttu-id="0894a-103">ASP.NET Core kimlik doğrulaması örnekleri</span><span class="sxs-lookup"><span data-stu-id="0894a-103">Authentication samples for ASP.NET Core</span></span>

<span data-ttu-id="0894a-104">Tarafından [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="0894a-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="0894a-105">[ASP.NET Core depo](https://github.com/aspnet/AspNetCore) aşağıdaki kimlik doğrulama örnekleri içeren *AspNetCore/src/güvenlik/samples* klasörü:</span><span class="sxs-lookup"><span data-stu-id="0894a-105">The [ASP.NET Core repository](https://github.com/aspnet/AspNetCore) contains the following authentication samples in the *AspNetCore/src/Security/samples* folder:</span></span>

* [<span data-ttu-id="0894a-106">Talep dönüştürme</span><span class="sxs-lookup"><span data-stu-id="0894a-106">Claims transformation</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/ClaimsTransformation)
* [<span data-ttu-id="0894a-107">Tanımlama bilgisi kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="0894a-107">Cookie authentication</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/Cookies)
* [<span data-ttu-id="0894a-108">Özel ilke sağlayıcısı - IAuthorizationPolicyProvider</span><span class="sxs-lookup"><span data-stu-id="0894a-108">Custom policy provider - IAuthorizationPolicyProvider</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/CustomPolicyProvider)
* [<span data-ttu-id="0894a-109">Dinamik kimlik doğrulama düzenleri ve seçenekleri</span><span class="sxs-lookup"><span data-stu-id="0894a-109">Dynamic authentication schemes and options</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/DynamicSchemes)
* [<span data-ttu-id="0894a-110">Dış talep</span><span class="sxs-lookup"><span data-stu-id="0894a-110">External claims</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/Identity.ExternalClaims)
* [<span data-ttu-id="0894a-111">Tanımlama bilgisi ve yanıtı temel alarak başka bir kimlik doğrulama düzeni arasında seçme</span><span class="sxs-lookup"><span data-stu-id="0894a-111">Selecting between cookie and another authentication scheme based on the request</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/PathSchemeSelection)
* [<span data-ttu-id="0894a-112">Statik dosyalar için erişimi kısıtlar</span><span class="sxs-lookup"><span data-stu-id="0894a-112">Restricts access to static files</span></span>](https://github.com/aspnet/AspNetCore/tree/release/2.2/src/Security/samples/StaticFilesAuth)

## <a name="run-the-samples"></a><span data-ttu-id="0894a-113">Örnekleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="0894a-113">Run the samples</span></span>

* <span data-ttu-id="0894a-114">Seçin bir [dal](https://github.com/aspnet/AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="0894a-114">Select a [branch](https://github.com/aspnet/AspNetCore).</span></span> <span data-ttu-id="0894a-115">Örneğin, `release/2.2`</span><span class="sxs-lookup"><span data-stu-id="0894a-115">For example, `release/2.2`</span></span>
* <span data-ttu-id="0894a-116">Kopyala veya indir [ASP.NET Core depo](https://github.com/aspnet/AspNetCore).</span><span class="sxs-lookup"><span data-stu-id="0894a-116">Clone or download the [ASP.NET Core repository](https://github.com/aspnet/AspNetCore).</span></span>
* <span data-ttu-id="0894a-117">Yüklediğiniz doğrulayın [.NET Core SDK'sı](https://www.microsoft.com/net/download/all) ASP.NET Core deponun kopyasını eşleşen sürümü.</span><span class="sxs-lookup"><span data-stu-id="0894a-117">Verify you have installed the [.NET Core SDK](https://www.microsoft.com/net/download/all) version matching the clone of the ASP.NET Core repository.</span></span>
* <span data-ttu-id="0894a-118">Bir örnek gidin *AspNetCore/src/güvenlik/samples* örnekle çalıştırıp `dotnet run`.</span><span class="sxs-lookup"><span data-stu-id="0894a-118">Navigate to a sample in *AspNetCore/src/Security/samples* and run the sample with `dotnet run`.</span></span>
