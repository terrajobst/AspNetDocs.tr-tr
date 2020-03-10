---
uid: webhooks/diagnostics/logging
title: ASP.NET Web kancaları günlüğü | Microsoft Docs
author: rick-anderson
description: ASP.NET Web kancalarında günlüğe kaydetme.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: f71bc442-5f80-481b-a32c-a0ec18dee9d6
ms.openlocfilehash: a05b32c4a8f9577bcf6170bd19a9e440b1aeb75b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547882"
---
# <a name="aspnet-webhooks-logging"></a>ASP.NET Web kancaları günlüğü

Microsoft ASP.NET Web kancaları, sorunları ve sorunları bildiren bir yöntem olarak günlüğe kaydetme kullanır. Varsayılan olarak Günlükler, diğer tüm günlük akışları gibi [Izleme dinleyicilerinin](https://msdn.microsoft.com/library/system.diagnostics.tracelistener.aspx) kullanılması için [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) kullanılarak yazılır.

Web uygulamanızı bir Azure Web uygulaması olarak dağıttığınızda Günlükler otomatik olarak alınır ve diğer [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace) günlüğü ile birlikte yönetilebilir. Ayrıntılar için lütfen bkz. [Azure App Service Web Apps için tanılama günlüğünü etkinleştirme](https://azure.microsoft.com/documentation/articles/web-sites-enable-diagnostic-log/)

Ayrıca, Günlükler Visual Studio 'nun içinden Visual Studio ['yu kullanarak Azure App Service bir Web uygulamasında sorun giderme](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs)konusunda açıklandığı gibi, Visual Studio içinden doğrudan elde edilebilir.

## <a name="redirecting-logs"></a>Günlükleri yeniden yönlendirme

[System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace)'e Günlükler yazmak yerine, [Log4Net](http://logging.apache.org/log4net/) ve [NLog](http://nlog-project.org/)gibi bir günlük yöneticisine doğrudan oturum açabilme alternatif bir günlük uygulama sağlamak mümkündür. Yalnızca bir [ILogger](https://github.com/aspnet/AspNetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Common/Diagnostics/ILogger.cs) uygulamasını sağlamanız ve bunu tercih ettiğiniz bir bağımlılık ekleme altyapısına kaydederek, Web kancaları Microsoft ASP.NET tarafından alınır. Ayrıntılar için lütfen bkz. [ASP.NET Web API 2 ' ye bağımlılık ekleme](https://www.asp.net/web-api/overview/advanced/dependency-injection) .
