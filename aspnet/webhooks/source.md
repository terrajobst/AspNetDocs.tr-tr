---
uid: webhooks/source
title: ASP.NET Web kancaları kaynak kodu ve NuGet paketleri | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancaları kaynak kodu ve NuGet paketlerinin bağlantıları
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000708"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="b6d76-103">ASP.NET Web kancaları kaynak kodu ve NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="b6d76-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="b6d76-104">Microsoft ASP.NET Web kancaları Microsoft ASP.NET modül ailesinin bir parçasıdır ve [GitHub üzerinde açık kaynak proje](https://github.com/aspnet/WebHooks)olarak barındırılır.</span><span class="sxs-lookup"><span data-stu-id="b6d76-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="b6d76-105">Bu, katkıların kabul ettiğimiz anlamına gelir ancak çekme isteği göndermeden önce lütfen [katkı yönergelerine](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="b6d76-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="b6d76-106">Artık okuduğunuz bu çevrimiçi belgeler ayrıca [GitHub 'Da açık kaynak](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) olarak barındırılır ve ayrıca katkıları kabul eder.</span><span class="sxs-lookup"><span data-stu-id="b6d76-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="b6d76-107">NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="b6d76-107">NuGet packages</span></span>

<span data-ttu-id="b6d76-108">[NuGet paketleri](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) üç parçaya ayrılmıştır:</span><span class="sxs-lookup"><span data-stu-id="b6d76-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="b6d76-109">[Ortak](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Gönderenler ve alıcılar arasında paylaşılan ortak bir paket.</span><span class="sxs-lookup"><span data-stu-id="b6d76-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="b6d76-110">[Gönderen](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Kendi web Kancalarınızı başkalarına göndermeyi destekleyen bir paket kümesi.</span><span class="sxs-lookup"><span data-stu-id="b6d76-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="b6d76-111">Web kancaları gönderme işlevselliği, [Web kancaları gönderme](sending/senders.md)konusunda daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6d76-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="b6d76-112">[Alıcılar](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Başkalarından Web kancaları almayı destekleyen bir paket kümesi.</span><span class="sxs-lookup"><span data-stu-id="b6d76-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="b6d76-113">Web kancalarını alma işlevselliği, [Web kancalarını alma](receiving/index.md)konusunda daha ayrıntılı olarak açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6d76-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>
