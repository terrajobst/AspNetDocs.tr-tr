---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1,0 ve 1,1 ' nin yan yana yürütülmesi | Microsoft Docs
author: rick-anderson
description: Bu Teknik İnceleme, makinenizde hem .NET 1,0 hem de .NET 1,1 ' nin nasıl yükleneceğini ve bir ASP.NET Web uygulamasının her iki sürümünde de çalışmasına izin verir...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632974"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="e622d-103">ASP.NET .NET Framework 1.0 ve 1.1 Sürümlerini Yan Yana Yürütme</span><span class="sxs-lookup"><span data-stu-id="e622d-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="e622d-104">Bu Teknik İnceleme, makinenizde hem .NET 1,0 hem de .NET 1,1 ' nin nasıl yükleneceğini ve bir ASP.NET Web uygulamasının Framework 'ün herhangi bir sürümünde çalışmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="e622d-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="e622d-105">ASP.NET 1,0 ve ASP.NET 1,1 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e622d-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="e622d-106">ASP.NET ' de, uygulamalar aynı bilgisayara yüklendiklerinde yan yana çalışıyor olarak kabul edilir, ancak .NET Framework farklı sürümlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e622d-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="e622d-107">Aşağıdaki konu, yan yana yürütme için ASP.NET uygulamalarının nasıl yapılandırılacağını açıklar ve aşağıdakiler için ayrıntılı adımlar sağlar:</span><span class="sxs-lookup"><span data-stu-id="e622d-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="e622d-108">Yükleme sırasında Web uygulamanızın .NET Framework sürüm 1,0 ' e eşlenmesini koruyun</span><span class="sxs-lookup"><span data-stu-id="e622d-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="e622d-109">Bir Web uygulamasını .NET Framework belirli bir sürümüne eşleyin</span><span class="sxs-lookup"><span data-stu-id="e622d-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="e622d-110">Bir Web sitesinin kullandığı .NET Framework sürümünü bulma</span><span class="sxs-lookup"><span data-stu-id="e622d-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="e622d-111">Geleneksel olarak, bir bilgisayarda bir bileşen veya uygulama güncelleştirildiği zaman, eski sürüm kaldırılır ve daha yeni bir sürümle değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e622d-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="e622d-112">Yeni sürüm önceki sürümle uyumlu değilse, bu genellikle bileşeni veya uygulamayı kullanan diğer uygulamaları keser.</span><span class="sxs-lookup"><span data-stu-id="e622d-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="e622d-113">.NET Framework, bir derleme veya uygulamanın birden çok sürümünün aynı anda aynı bilgisayara yüklenmesine izin veren yan yana yürütme desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="e622d-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="e622d-114">Aynı anda birden çok sürüm yüklenebildiğinden, yönetilen uygulamalar farklı bir sürüm kullanan uygulamaları etkilemeden hangi sürümün kullanılacağını seçebilir.</span><span class="sxs-lookup"><span data-stu-id="e622d-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="e622d-115">Varsayılan olarak, .NET Framework sürüm 1,1 yüklemesi sırasında, tüm mevcut ASP.NET uygulamaları .NET Framework en son sürümünü kullanacak şekilde otomatik olarak yeniden yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e622d-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="e622d-116">ASP.NET uygulamalarınızın varsayılan .NET Framework 1,1 ' i kullanmasını istemiyorsanız, yükleme sırasında bunu nasıl önleyeceğinizi öğrenmek için [buraya](#1) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="e622d-117">Web sunucunuzu 1,1 .NET Framework ve bir veya daha fazla Web uygulamasının .NET Framework 1,0 ' i çalıştırmak istiyorsanız, Internet Information Services (IIS) betik eşlemesini güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e622d-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="e622d-118">Betik eşleme, belirli bir Web uygulaması için. aspx dosya uzantısını .NET Framework bir sürümüne eşlemek için bir mekanizmadır.</span><span class="sxs-lookup"><span data-stu-id="e622d-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="e622d-119">Bir Web uygulamasını .NET Framework belirli bir sürümüne nasıl eşleyeceğinizi öğrenmek için [buraya](#2) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="e622d-120">Belirli bir Web uygulamasını hangi .NET Framework sürümünün çalıştırmakta olduğunu bulmak için Internet Information Manager veya ASP.NET IIS kayıt aracı 'nı (ASPNET\_regııs. exe) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e622d-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="e622d-121">Bir Web sitesinin kullandığı .NET Framework sürümünü bulma hakkında bilgi edinmek için [buraya](#3) tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="e622d-122">.NET Framework 1,1 ' e geçiş yaparken bir içeri aktarma işlemi, .NET Framework her bir sürümünün kendi Machine. config dosyasını kullanmalarından biridir.</span><span class="sxs-lookup"><span data-stu-id="e622d-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="e622d-123">Sonuç olarak, bir Web Yöneticisi Machine. config dosyasında değişiklik yaptıysanız, bu değişikliklerin .NET Framework 1,1 Machine. config dosyasına geçirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e622d-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="e622d-124">Web uygulamanızın yükleme sırasında .NET Framework 1,0 ' e eşlenmesini koruma</span><span class="sxs-lookup"><span data-stu-id="e622d-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="e622d-125">Varsayılan olarak, tüm mevcut ASP.NET uygulamaları yükleme sırasında .NET Framework 'in daha yeni bir sürümünü kullanmak üzere otomatik olarak yeniden yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="e622d-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="e622d-126">.NET Framework daha yeni sürümünü kullanarak uygulamalar, yeni sürümde sunulan geliştirmelerden ve yeni özelliklerden tam olarak faydalanabilir.</span><span class="sxs-lookup"><span data-stu-id="e622d-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="e622d-127">Aynı zamanda, hangi uygulamaların güncelleştirildiği üzerinde ayrıntılı denetim yapmak isteyebileceğiniz Web Yöneticisi, .NET Framework yüklemesi sırasında var olan tüm ASP.NET uygulamalarının otomatik yeniden eşleştirmasını önleyebilir.</span><span class="sxs-lookup"><span data-stu-id="e622d-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="e622d-128">Tüm ASP.NET uygulamasının .NET Framework yeni sürümüne otomatik olarak yeniden eşleştirmeyi engellemek için Web Yöneticisi, Dotnetfx. exe Kurulum programı ile/noaspupgrade komut satırı seçeneğini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e622d-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="e622d-129">**ASP.NET uygulamasının toplam yeniden eşleştirmasını daha yeni bir sürüme engellemek için**</span><span class="sxs-lookup"><span data-stu-id="e622d-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="e622d-130">**Başlat**'a gidin.</span><span class="sxs-lookup"><span data-stu-id="e622d-130">Go to **Start**.</span></span>
2. <span data-ttu-id="e622d-131">**Çalıştır**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-131">Click on **run**.</span></span>
3. <span data-ttu-id="e622d-132">**Cmd**yazın.</span><span class="sxs-lookup"><span data-stu-id="e622d-132">Type **cmd**.</span></span>
4. <span data-ttu-id="e622d-133">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="e622d-134">Komut isteminde, .NET Framework: **Dotnetfx. exe/c: "/noaspupgrade yüklensin mi?** . yüklemesini başlatmak için aşağıdaki satırı yazın.</span><span class="sxs-lookup"><span data-stu-id="e622d-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="e622d-135">Microsoft .NET Framework 1,1 kurulumunda **Evet** ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="e622d-136">Bu işlem 1,1 .NET Framework kurulum işlemini başlatacak.</span><span class="sxs-lookup"><span data-stu-id="e622d-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="e622d-137">Bir Web uygulamasını .NET Framework belirli bir sürümüne eşleyin</span><span class="sxs-lookup"><span data-stu-id="e622d-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="e622d-138">.NET Framework her sürümü, ASP.NET IIS kayıt aracı 'nın (ASPNET\_regııs. exe) bir sürümünü içerir.</span><span class="sxs-lookup"><span data-stu-id="e622d-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="e622d-139">Bu araç, yöneticilerin bir Web uygulamasının .NET Framework belirli bir sürümü altında çalıştırıldığını belirtmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="e622d-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="e622d-140">Bu, bir Web uygulamasını .NET Framework bir sürümüne eşleme olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="e622d-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="e622d-141">Yöneticiler, Web uygulamasıyla ilişkilendirilecek .NET Framework sürümüne karşılık gelen ASPNET\_regııs. exe ' yi seçmelidir.</span><span class="sxs-lookup"><span data-stu-id="e622d-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="e622d-142">Örneğin, bir Web sitesinin 1,1 .NET Framework kullanmasını belirtmek isteyen bir yöneticinin .NET Framework 1,1 ile birlikte gelen ASPNET\_regııs. exe ' yi kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e622d-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="e622d-143">Sürüm 1,0 için ASPNET\_regııs. exe şu konumda bulunur:</span><span class="sxs-lookup"><span data-stu-id="e622d-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="e622d-144">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.0.3705**\aspnet\_regııs</span><span class="sxs-lookup"><span data-stu-id="e622d-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="e622d-145">Sürüm 1 için regııs. exe\_ASPNET, şu konumda bulunur:</span><span class="sxs-lookup"><span data-stu-id="e622d-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="e622d-146">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\aspnet\_regııs</span><span class="sxs-lookup"><span data-stu-id="e622d-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="e622d-147">ASPNET\_regııs. exe, bir Web uygulamasını betik eşleme için iki seçenek sunar:</span><span class="sxs-lookup"><span data-stu-id="e622d-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="e622d-148">**-s** , yol içindeki ve alt dizinlerinde betik eşlemesini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e622d-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="e622d-149">**-sn** yalnızca yoldaki betik eşlemesini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e622d-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="e622d-150">Yol, W3SVC/ROOT/{WebSiteNumber}/{Application\_Name} biçiminde tanımlanan Web uygulaması IIS meta veri yolunu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e622d-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="e622d-151">Örneğin, varsayılan Web sitesi altında bulunan Portal adlı bir Web uygulaması için, metatabanı yolu W3SVC/1/ROOT/Portal olur.</span><span class="sxs-lookup"><span data-stu-id="e622d-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="e622d-152">Ayrıca, metatabanı yolunu almak için metatabanı düzenleyicisi olarak adlandırılan bir araç da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e622d-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="e622d-153">Bu aracı, [https://support.microsoft.com/default.aspx?scid=kb, en-US; 232068](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068) konumundaki Microsoft desteği sitesinden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e622d-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="e622d-154">Portal IIS betik eşlemesini ve alt öğesini güncelleştirmek için ASPNET\_regııs. exe-s W3SVC/1/ROOT/Portal çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e622d-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="e622d-155">Portaldaki uygulamaları etkilemeden Portal IIS betik eşlemesini güncelleştirmek için ASPNET\_regııs. exe-sn W3SVC/1/ROOT/Portal çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e622d-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="e622d-156">Bir Web uygulamasının kullandığı .NET Framework sürümünü bulma</span><span class="sxs-lookup"><span data-stu-id="e622d-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="e622d-157">Yönetici, .NET Framework bir Web sitesi hangi sürümünün çalıştığını bulmak için Internet Service Manager kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="e622d-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="e622d-158">Farklı işletim sistemi sürümleri Internet Service Manager farklı şekilde başlatır.</span><span class="sxs-lookup"><span data-stu-id="e622d-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="e622d-159">Service Manager 'ı başlatmak için aşağıda listelenen adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e622d-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="e622d-160">**Internet Service Manager başlatmak için**</span><span class="sxs-lookup"><span data-stu-id="e622d-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="e622d-161">**Başlat**'a gidin.</span><span class="sxs-lookup"><span data-stu-id="e622d-161">Go to **Start**.</span></span>
2. <span data-ttu-id="e622d-162">**Çalıştır**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-162">Click on **run**.</span></span>
3. <span data-ttu-id="e622d-163">**İnetmgr**yazın.</span><span class="sxs-lookup"><span data-stu-id="e622d-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="e622d-164">Internet Service Manager, .NET Framework sürümünü kullanmak istediğiniz Web uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e622d-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="e622d-165">Web uygulamasına sağ tıklayın ve Özellikler ' e tıklayın **.**</span><span class="sxs-lookup"><span data-stu-id="e622d-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="e622d-166">Özellik penceresinde yapılandırma ' yı seçin **.**</span><span class="sxs-lookup"><span data-stu-id="e622d-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="e622d-167">Uygulama eşleme tablosundan **. aspx**' i seçin ve **Düzenle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e622d-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="e622d-168">**Yürütülebilir** metin kutusundan, kaydırma yoluyla sürüm dizinine bakın.</span><span class="sxs-lookup"><span data-stu-id="e622d-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="e622d-169">Sürüm dizini v. 1.1.4322 ise, uygulama .NET Framework 1,1 ile eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e622d-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="e622d-170">Buna karşılık, sürüm dizini v 1.0.3705 ise, uygulama .NET Framework 1,0 ile eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="e622d-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
