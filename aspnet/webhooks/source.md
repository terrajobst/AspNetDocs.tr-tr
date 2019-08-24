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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>ASP.NET Web kancaları kaynak kodu ve NuGet paketleri

Microsoft ASP.NET Web kancaları Microsoft ASP.NET modül ailesinin bir parçasıdır ve [GitHub üzerinde açık kaynak proje](https://github.com/aspnet/WebHooks)olarak barındırılır. Bu, katkıların kabul ettiğimiz anlamına gelir ancak çekme isteği göndermeden önce lütfen [katkı yönergelerine](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) bakın.

Artık okuduğunuz bu çevrimiçi belgeler ayrıca [GitHub 'Da açık kaynak](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) olarak barındırılır ve ayrıca katkıları kabul eder.

## <a name="nuget-packages"></a>NuGet paketleri

[NuGet paketleri](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) üç parçaya ayrılmıştır:

* [Ortak](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Gönderenler ve alıcılar arasında paylaşılan ortak bir paket.

* [Gönderen](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Kendi web Kancalarınızı başkalarına göndermeyi destekleyen bir paket kümesi. Web kancaları gönderme işlevselliği, [Web kancaları gönderme](sending/senders.md)konusunda daha ayrıntılı olarak açıklanmıştır.

* [Alıcılar](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Başkalarından Web kancaları almayı destekleyen bir paket kümesi. Web kancalarını alma işlevselliği, [Web kancalarını alma](receiving/index.md)konusunda daha ayrıntılı olarak açıklanmıştır.
