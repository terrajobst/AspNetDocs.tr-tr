---
ms.openlocfilehash: 6b2bc386ec179e786de205af0ca6dbd610e000d9
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075609"
---
# <a name="aspnet-core-background-tasks-sample-generic-host"></a><span data-ttu-id="4d2ac-101">ASP.NET Core arka plan görevleri örnek (genel ana bilgisayar)</span><span class="sxs-lookup"><span data-stu-id="4d2ac-101">ASP.NET Core Background Tasks Sample (Generic Host)</span></span>

<span data-ttu-id="4d2ac-102">Bu örnek kullanımını gösterir [Ihostedservice](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span><span class="sxs-lookup"><span data-stu-id="4d2ac-102">This sample illustrates the use of [IHostedService](https://docs.microsoft.com/dotnet/api/microsoft.extensions.hosting.ihostedservice).</span></span> <span data-ttu-id="4d2ac-103">Bu örnek, açıklanan özellikleri gösterir. [arka plan görevleri ASP.NET Core, barındırılan hizmetler ile](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) konu.</span><span class="sxs-lookup"><span data-stu-id="4d2ac-103">This sample demonstrates the features described in the [Background tasks with hosted services in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/host/hosted-services) topic.</span></span>

<span data-ttu-id="4d2ac-104">Örnek çalışırken [Visual Studio Code](https://code.visualstudio.com/)ayarlayın **konsol** Konsolu yapılandırmasında değerini *.vscode/launch.json* ya da `externalTerminal` veya `integratedTerminal`.</span><span class="sxs-lookup"><span data-stu-id="4d2ac-104">When running the sample in [Visual Studio Code](https://code.visualstudio.com/), set the **console** value of the console configuration in *.vscode/launch.json* to either `externalTerminal` or `integratedTerminal`.</span></span> <span data-ttu-id="4d2ac-105">Kullanım `internalConsole` sıraya alma arka plan iş öğeleri için uygulamanın kullandığı konsol tuş vuruşu girdisi ile uyumlu değil.</span><span class="sxs-lookup"><span data-stu-id="4d2ac-105">Use of the `internalConsole` is incompatible with console keystroke input that the app uses to enqueue background work items.</span></span>
