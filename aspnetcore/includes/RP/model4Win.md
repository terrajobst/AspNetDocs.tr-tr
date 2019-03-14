---
ms.openlocfilehash: 85fa9f8b18dc7dfb3e9d37703549dc5c28dc7a4a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077442"
---
<a name="scaffold"></a>
### <a name="scaffold-the-movie-model"></a><span data-ttu-id="e65be-101">Film modeli iskelesini</span><span class="sxs-lookup"><span data-stu-id="e65be-101">Scaffold the Movie model</span></span>

* <span data-ttu-id="e65be-102">Komut satırından aşağıdaki komutu çalıştırın (içeren proje dizininde *Program.cs*, *Startup.cs*, ve *.csproj* dosyaları):</span><span class="sxs-lookup"><span data-stu-id="e65be-102">Run the following from the command line (in the project directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files):</span></span>

  ```console
  dotnet restore
  dotnet aspnet-codegenerator razorpage -m Movie -dc MovieContext -udl -outDir Pages\Movies --referenceScriptLibraries
  ```

<span data-ttu-id="e65be-103">Hatası alırsanız:</span><span class="sxs-lookup"><span data-stu-id="e65be-103">If you get the error:</span></span>
  ```
No executable found matching command "dotnet-aspnet-codegenerator"
  ```

<span data-ttu-id="e65be-104">Önceki hata yanlış dizine olduğunda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="e65be-104">The preceeding error happens when you are in the wrong directory.</span></span> <span data-ttu-id="e65be-105">Proje dizini için bir komut kabuğunu açın (içeren dizine *Program.cs*, *Startup.cs*, ve *.csproj* dosyaları), ve ardından önceki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e65be-105">Open a command shell to the project directory (The directory that contains the *Program.cs*, *Startup.cs*, and *.csproj* files), and then run the preceeding command.</span></span>

<span data-ttu-id="e65be-106">Hatası alırsanız:</span><span class="sxs-lookup"><span data-stu-id="e65be-106">If you get the error:</span></span>
  ```
  The process cannot access the file 
 'RazorPagesMovie/bin/Debug/netcoreapp2.0/RazorPagesMovie.dll' 
  because it is being used by another process.
  ```

<span data-ttu-id="e65be-107">Visual Studio çıkın ve komutu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e65be-107">Exit Visual Studio and run the command again.</span></span>
