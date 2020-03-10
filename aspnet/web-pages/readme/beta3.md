---
uid: web-pages/readme/beta3
title: Web Matrix ve ASP.NET Web Pages (Razor) Beta 3 yayın Benioku | Microsoft Docs
author: rick-anderson
description: WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628900"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="1e220-103">WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası</span><span class="sxs-lookup"><span data-stu-id="1e220-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="1e220-104">WebMatrix ve ASP.NET Web Sayfaları (Razor) Beta 3 Yayını Benioku Dosyası</span><span class="sxs-lookup"><span data-stu-id="1e220-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="1e220-105">9 Kasım 2010</span><span class="sxs-lookup"><span data-stu-id="1e220-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="1e220-106">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="1e220-106">Contents</span></span>

- [<span data-ttu-id="1e220-107">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="1e220-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="1e220-108">Yükleme</span><span class="sxs-lookup"><span data-stu-id="1e220-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="1e220-109">Beta 3 sürümündeki yeni özellikler, değişiklikler ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="1e220-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="1e220-110">WebMatrix yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="1e220-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="1e220-111">ASP.NET Web Sayfaları</span><span class="sxs-lookup"><span data-stu-id="1e220-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="1e220-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="1e220-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="1e220-113">Uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="1e220-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="1e220-114">Uygulamaları yayımlama</span><span class="sxs-lookup"><span data-stu-id="1e220-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="1e220-115">Diğer Sorunlar</span><span class="sxs-lookup"><span data-stu-id="1e220-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="1e220-116">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="1e220-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="1e220-117">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="1e220-117">Overview</span></span>

> <span data-ttu-id="1e220-118">Microsoft WebMatrix Beta, dakikalar içinde yüklenen ücretsiz bir Web geliştirme yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="1e220-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="1e220-119">Tek ve tümleşik bir deneyim oluşturmak için veritabanı ve programlama çerçeveleri ile bir Web sunucusunu tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e220-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="1e220-120">WebMatrix Beta 'yı kullanarak kendi ASP.NET veya PHP Web sitenizi kodlamanıza, test etmeniz ve yayımlamanıza olanak sağlayabilir veya DotNetNuke, dönen Raco, WordPress veya Joomla gibi popüler açık kaynaklı uygulamaları kullanarak yeni bir Web sitesi başlatmak için WebMatrix Beta 'yı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="1e220-121">WebMatrix Beta, geliştirmeden üretime sorunsuz ve sorunsuz bir şekilde geçiş yapan web sitenizi Internet üzerinde çalıştıracak olan güçlü Web sunucusu, veritabanı altyapısı ve çerçeveler ortamını kullanır.</span><span class="sxs-lookup"><span data-stu-id="1e220-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="1e220-122">Yükleme</span><span class="sxs-lookup"><span data-stu-id="1e220-122">Installation</span></span>

> <span data-ttu-id="1e220-123">WebMatrix Beta 3 ' ü yüklemek için [Microsoft Web Platformu Yükleyicisi 3,0](https://go.microsoft.com/fwlink/?LinkID=194638)' i kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="1e220-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="1e220-124">Web Platformu Yükleyicisi 'ni yükledikten sonra, WebMatrix Beta 3 ' ü yüklemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="1e220-125">Yükleme sırasında sorunlarla karşılaşırsanız [Microsoft Web Platformu Yükleyicisi sorun giderme sorunları](https://go.microsoft.com/fwlink/?LinkId=196212)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="1e220-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="1e220-126">Uygulama yayımlama yönergeleri</span><span class="sxs-lookup"><span data-stu-id="1e220-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="1e220-127">Bkz. [uygulamaları yayımlamak Için adım adım yönergeler](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="1e220-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="1e220-128">Yeni özellikler, değişiklikler ve bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="1e220-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="1e220-129">WebMatrix Beta 3 yüklemesi</span><span class="sxs-lookup"><span data-stu-id="1e220-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="1e220-130">Sorun: WebMatrix Beta 3 yalnızca Microsoft .NET Framework 4 ' ü destekleyen platformlarda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1e220-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="1e220-131">WebMatrix Beta için .NET Framework sürüm 4 gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1e220-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="1e220-132">Bazı durumlarda, WebMatrix Beta yükleyicisi, desteklenen yapılandırma kümesinin parçası olmayan bir platforma yükleme denemenize imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="1e220-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="1e220-133">Özellikle, SP1 güncelleştirmesi olmayan Windows Vista, WebMatrix Beta yüklemesine başlamanızı sağlar, ancak .NET Framework 4 bileşeni başarısız olur ve yüklemenizi engeller.</span><span class="sxs-lookup"><span data-stu-id="1e220-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="1e220-134">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-134">**Workaround**</span></span>  
> <span data-ttu-id="1e220-135">Aşağıdakileri içeren desteklenen bir platforma yükler:</span><span class="sxs-lookup"><span data-stu-id="1e220-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="1e220-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="1e220-136">Windows 7</span></span>
> - <span data-ttu-id="1e220-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="1e220-137">Windows Server 2008</span></span>
> - <span data-ttu-id="1e220-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="1e220-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="1e220-139">Windows Vista SP1 veya sonraki sürümü</span><span class="sxs-lookup"><span data-stu-id="1e220-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="1e220-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="1e220-140">Windows XP SP3</span></span>
> - <span data-ttu-id="1e220-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="1e220-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="1e220-142">Sorun: Microsoft Visual Studio 2008 SP1 olmadan Microsoft Visual Studio 2008 yüklenirse WebMatrix Beta 3 yüklenemiyor</span><span class="sxs-lookup"><span data-stu-id="1e220-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="1e220-143">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-143">**Workaround**</span></span>  
> <span data-ttu-id="1e220-144">[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 'ı Microsoft İndirme Merkezi ' nden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e220-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="1e220-145">Sorun: SQL Server Compact 4,0 için bazı derlemeler GAC 'de yüklü değil</span><span class="sxs-lookup"><span data-stu-id="1e220-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="1e220-146">SQL Server Compact 4,0 için yönetilen derlemeler, SQL Server Compact 4,0 ' i bir 64 bit bilgisayara yüklediğinizde ve bilgisayarda yalnızca .NET Framework 3,5 SP1 Istemci profili yüklü olduğunda genel derleme önbelleği 'ne (GAC) yerleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="1e220-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="1e220-147">GAC 'de yüklü olmayan yönetilen derlemeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1e220-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="1e220-148">*System. Data. SqlServerCe. dll* (ADO.NET sağlayıcısı)</span><span class="sxs-lookup"><span data-stu-id="1e220-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="1e220-149">*System. Data. SqlServerCe. Entity. dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="1e220-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="1e220-150">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-150">**Workaround**</span></span>  
> <span data-ttu-id="1e220-151">SQL Server Compact 4,0 'yi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1e220-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="1e220-152">Aşağıdaki konumdan .NET Framework 3,5 SP1 'in tam sürümünü indirip yükleyin:</span><span class="sxs-lookup"><span data-stu-id="1e220-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="1e220-153">Microsoft .NET Framework 3,5 Service Pack 1 (tam paket)</span><span class="sxs-lookup"><span data-stu-id="1e220-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="1e220-154">SQL Server Compact 4,0 yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e220-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="1e220-155">Sorun: komut satırı kullanılarak SQL Server Compact kaldırılamıyor</span><span class="sxs-lookup"><span data-stu-id="1e220-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="1e220-156">Komut satırı seçeneklerini kullanarak SQL Server Compact kaldırılması bu sürümde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="1e220-157">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-157">**Workaround**</span></span>  
> <span data-ttu-id="1e220-158">4,0 Microsoft SQL Server Compact kaldırmak için Windows Denetim Masası 'ndaki *Programlar ve Özellikler ' i* kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e220-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="1e220-159">ASP.NET Web Sayfaları</span><span class="sxs-lookup"><span data-stu-id="1e220-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="1e220-160">Belgenin bu bölümünde, Razor söz dizimi ile ASP.NET Web sayfalarının Beta 3 sürümündeki yeni özellikler, değişiklikler ve bilinen sorunlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1e220-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="1e220-161">Yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="1e220-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="1e220-162">Değişikliklerine</span><span class="sxs-lookup"><span data-stu-id="1e220-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="1e220-163">Sorunlar</span><span class="sxs-lookup"><span data-stu-id="1e220-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="1e220-164">Razor sözdizimi olan ASP.NET Web sayfaları için Beta 3 ' teki yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="1e220-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="1e220-165">Yeni: "HTML. RAW" yöntemi, kodlanmamış biçimlendirmeyi işler</span><span class="sxs-lookup"><span data-stu-id="1e220-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="1e220-166">Yeni `Html.Raw` yöntemi, HTML işaretlemesini kodlanmış çıktıyı işlemek yerine biçimlendirme olarak işlemenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e220-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="1e220-167">(Varsayılan olarak, ASP.NET Razor dizeleri işlemeden önce kodlar.) Sözdizimi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1e220-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="1e220-168">Aşağıdaki örnek `Html.Raw`nasıl kullanacağınızı gösterir:</span><span class="sxs-lookup"><span data-stu-id="1e220-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="1e220-169">Razor sözdizimi olan ASP.NET Web sayfaları için Beta 3 değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1e220-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="1e220-170">Değişiklik: "HrefAttribute" yöntemi kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="1e220-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="1e220-171">`WebPage` sınıfının `HrefAttribute` yöntemi kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="1e220-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="1e220-172">Bu yardımcı, URL 'lerde güvenli olmayan karakterleri kodlamak için kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="1e220-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="1e220-173">ASP.NET Razor dizeleri otomatik olarak kodlarsa artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="1e220-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="1e220-174">(Kodlanmış dizeleri işlemek için yeni `Html.Raw` yöntemini kullanın.)</span><span class="sxs-lookup"><span data-stu-id="1e220-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="1e220-175">Değişiklik: bildirime dayalı "@helper" yardımcıları için sözdizimi değişti</span><span class="sxs-lookup"><span data-stu-id="1e220-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="1e220-176">Beta 3 sürümünde, ASP.NET `@helper` söz dizimi kullanılarak oluşturulan yardımcıları nasıl ayrıştırdığı de değişir.</span><span class="sxs-lookup"><span data-stu-id="1e220-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="1e220-177">Temelde `@helper` sözdizimi, kod içerebilen bir biçimlendirme bloğu yerine bir kod bloğu olarak ayrıştırılır.</span><span class="sxs-lookup"><span data-stu-id="1e220-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="1e220-178">Bu nedenle, yardım içindeki kodun `@{ }` blokları içine alınması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1e220-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="1e220-179">Buna karşılık, yardımın içindeki biçimlendirmenin HTML öğelerine veya ASP.NET Razor `<text></text>` etiketlerine açık bir şekilde eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e220-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="1e220-180">Örneğin, aşağıdaki `@helper` sözdizimi Beta 3 sürümünde çalışmaktadır:</span><span class="sxs-lookup"><span data-stu-id="1e220-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="1e220-181">Beta 3 sürümünde, bu yardımcının aşağıdaki örnekteki gibi görünmesi için değiştirilmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1e220-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="1e220-182">Yardımdaki ilk kod etrafında `@{ }` karakterlerin artık kullanılmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="1e220-183">Bunun nedeni, yardımcılar içeriğinin varsayılan olarak bir kod bloğu olarak kabul edilmesidir.</span><span class="sxs-lookup"><span data-stu-id="1e220-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="1e220-184">Yardımcısı, açma `<a>` etiketiyle başlayan biçimlendirmeyi işler.</span><span class="sxs-lookup"><span data-stu-id="1e220-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="1e220-185">Yardımcının bir kapanış etiketi içermeyen düz metin veya etiketleri işlemesi gerekiyorsa (örneğin, `<meta>` etiketleri), işlenecek içerik `<text></text>` etiketlerinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e220-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="1e220-186">Değişiklik: "WebPageContext. HttpContext" kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="1e220-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="1e220-187">`WebPageContext.HttpContext` özelliği kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1e220-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="1e220-188">Bunun yerine `HttpContext.Current` kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e220-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="1e220-189">(`WebPageContext.HttpContext` özelliği bunu sarmalanmış.)</span><span class="sxs-lookup"><span data-stu-id="1e220-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="1e220-190">Değişiklik: "Facebook" Yardımcısı yeni pakete taşındı</span><span class="sxs-lookup"><span data-stu-id="1e220-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="1e220-191">`Facebook` Yardımcısı, `Facebook` Yardımcısı ve ek işlevler içeren *Facebook. Helper* kitaplığına taşınmıştır.</span><span class="sxs-lookup"><span data-stu-id="1e220-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="1e220-192">Bu kitaplığı, [ASP.net Pages Ile çalışmaya](https://go.microsoft.com/fwlink/?LinkId=202889)başlama öğreticisindeki "Paket Yöneticisi Ile yükleme yardımcıları" bölümünde açıklandığı gibi ayrı bir paket olarak yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e220-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="1e220-193">Değişiklik: üyelik, rol ve güvenlik türleri yeni derlemeye gider</span><span class="sxs-lookup"><span data-stu-id="1e220-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="1e220-194">Aşağıdaki türler `WebMatrix.WebData` derlemesine taşındı:</span><span class="sxs-lookup"><span data-stu-id="1e220-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="1e220-195">Değişiklik: "TagBuilder" sınıfı System. Web. Web sayfası. dll derlemesine taşındı</span><span class="sxs-lookup"><span data-stu-id="1e220-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="1e220-196">`TagBuilde` r sınıfı System. Web. Web sayfası. dll derlemesine taşınmıştır.</span><span class="sxs-lookup"><span data-stu-id="1e220-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="1e220-197">Daha önce bu, ASP.NET MVC 'nin bir parçası olan bir derlemedir.</span><span class="sxs-lookup"><span data-stu-id="1e220-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="1e220-198">Bu değişiklik, `TagBuilder` sınıfını kullanabilmeniz için ASP.NET MVC 'yi yüklemek zorunda değilsiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1e220-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="1e220-199">Ancak, sınıfı hala `System.Web.Mvc` ad alanında bulunur.</span><span class="sxs-lookup"><span data-stu-id="1e220-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="1e220-200">`TagBuilder` sınıfını kullanmak için (örneğin, özel bir ASP.NET Razor Yardımcısı), ad alanına başvurmanız gerekir (örneğin, kodunuza `@using System.Web.Mvc` ekleyerek).</span><span class="sxs-lookup"><span data-stu-id="1e220-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="1e220-201">Değişiklik: Istek doğrulama sözdizimi değişti; "Doğrulama" sınıfı kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="1e220-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="1e220-202">Beta 3 sürümünde, tek bir alan veya alan kümesi için doğrulamayı devre dışı bırakmak üzere, doğrulamanın dışında tutulacak alanların adını veya adlarını geçirerek `Validation.Exclude` yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="1e220-203">Beta 3 sürümünde doğrulamayı atlamak için yeni bir sözdizimi mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="1e220-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="1e220-204">Beta 3 ' te kullanılan `Validation` yöntemi kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1e220-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="1e220-205">İstek doğrulamasını devre dışı bırakırsanız, kullanıcılar HTML işaretlemesini karşıya yüklemeye çalışır (örneğin, bir sayfada zengin metin düzenleyicisi kullanarak), Web sitesi potansiyel olarak tehlikeli bir Istek gibi bir hata bildirir *. Istemciden form değeri algılandı* ve Kullanıcı girişi kabul edilmedi.</span><span class="sxs-lookup"><span data-stu-id="1e220-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="1e220-206">İstek doğrulamayı devre dışı bırakırsanız, [Microsoft Anti-Cross site betik kitaplığı v 4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)gibi bir şey kullanarak potansiyel olarak tehlikeli biçimlendirme veya betik içermediğinden emin olmak için Kullanıcı girişini el ile denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e220-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="1e220-207">Otomatik istek doğrulamayı devre dışı bırakmak için `Request.Unvalidated` yöntemini çağırın, bu, alanı veya için istek doğrulamayı atlamak istediğiniz başka bir post nesnesinin adını geçirerek.</span><span class="sxs-lookup"><span data-stu-id="1e220-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="1e220-208">`Form`, `QueryString`, `Cookies`ve `ServerVariables` koleksiyonlarındaki öğelerin doğrulanmasını atlamak için bu yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="1e220-209">Aşağıdaki örneklerde `Unvalidated` yönteminin nasıl kullanılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1e220-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="1e220-210">Razor sözdizimi ile ASP.NET Web sayfaları için bilinen sorunlar</span><span class="sxs-lookup"><span data-stu-id="1e220-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="1e220-211">Sorun: üyelik için özel bir kullanıcı tablosu kullanılırken beklenmeyen davranış</span><span class="sxs-lookup"><span data-stu-id="1e220-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="1e220-212">Bir ASP.NET Razor Web sitesinin üyelik sağlayıcısını başlatmak için `WebSecurity.InitializeDatabaseConnection` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1e220-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="1e220-213">(WebMatrix 'te, başlatıcı site şablonu *\_AppStart. cshtml* dosyasında Bu metoda bir çağrı içerir.) Bu yöntemin `autoCreateTables` parametresi true olarak ayarlanmışsa (varsayılan olarak, başlatıcı site şablonunda true olarak ayarlanır) ve tanınmayan bir tablo adı yönteme (ikinci parametre) geçirilirse Yöntem bir hata oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="1e220-214">Bunun yerine, tabloyu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1e220-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="1e220-215">Bu, üyelik için özel bir kullanıcı tablosu kullanmayı amaçlıyorsanız ancak yanlış tablo adını `WebSecurity.InitializeDatabaseConnection` yöntemine geçirirseniz bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="1e220-216">Yöntemi varsayılan olarak, belirttiğiniz tablo yoksa ve bunun yerine yeni bir tablo oluşturduğunda bir hata oluşturmaz, uygulama çalışıyor olarak görünebilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="1e220-217">Ancak, Özel Kullanıcı tablonuza (ve içindeki alanlarda) bağlı olan uygulama kodu sonunda beklenmedik hatalarla başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="1e220-218">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-218">**Workaround**</span></span>  
> <span data-ttu-id="1e220-219">`InitializeDatabaseConnection` yönteminde geçirilen adın, üyelik veritabanındaki kullanıcı profili tablosuyla eşleştiğinden emin olun veya `autoCreateTables` parametresinin false olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e220-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="1e220-220">Sorun: "SQL Server bir kullanıcı örneği oluşturulamadı" hatası</span><span class="sxs-lookup"><span data-stu-id="1e220-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="1e220-221">Bir WebMatrix Web uygulaması SQL Server Express kullanıyorsa ve Windows 7 veya Windows Server 2008 R2 üzerinde IIS 7,5 çalıştırıyorsa, SQL Server kullanıcının yerel uygulama yolunu çalışma zamanında alamadığını belirten bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="1e220-222">**Geçici çözüm** Uygulamanın altında çalıştığı Windows hesabının (genellikle ağ HIZMETI) uygulamanın kök klasörleri ve *App\_verileri*gibi alt klasörler için okuma/yazma izinlerine sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1e220-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="1e220-223">[SQL Server Express Kullanıcı örneği oluşturma ve ASP.NET Web uygulaması projeleriyle](https://support.microsoft.com/kb/2002980)Ilgili Bilgi Bankası makalesi sorunlarını daha ayrıntılı olarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="1e220-224">Sorun: Visual Studio 'Da özel derlemeler (dll 'Ler) için ad alanları otomatik olarak içeri aktarılmaz</span><span class="sxs-lookup"><span data-stu-id="1e220-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="1e220-225">Visual Studio 'da bir projede özel derlemeler kullanıyorsanız, bu derlemelerde belirtilen ad alanları tasarım zamanında otomatik olarak içeri aktarılmaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="1e220-226">Sonuç olarak, özel türlere yapılan başvurular tasarım zamanında tanınmayabilir ve Visual Studio 'da tanınmıyor olarak işaretlenir ("dalgalı çizgi" kullanılarak).</span><span class="sxs-lookup"><span data-stu-id="1e220-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="1e220-227">Bu sorun yalnızca Visual Studio 'da tasarım zamanında oluşur; uygulamanın kendisi düzgün şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="1e220-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="1e220-228">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-228">**Workaround**</span></span>  
> <span data-ttu-id="1e220-229">Tasarım zamanında tanınmayan varlıklara başvuran bir `using` deyimin (Visual Basic`imports`) dahil edin.</span><span class="sxs-lookup"><span data-stu-id="1e220-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="1e220-230">Sorun: Visual Studio IntelliSense ve proje şablonları yalnızca ASP.NET MVC sürüm 3 ' te kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1e220-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="1e220-231">ASP.NET Web sayfalarının yüklenmesi, Visual Studio için IntelliSense ve ASP.NET Web sayfaları uygulamalarına yönelik proje şablonları gibi araçları da yüklemez.</span><span class="sxs-lookup"><span data-stu-id="1e220-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="1e220-232">**Geçici çözüm** Visual Studio 'da ASP.NET Web Pages uygulamaları için IntelliSense ve proje şablonları kullanmak üzere, Web Platformu Yükleyicisi veya [tek başına yükleyici](https://go.microsoft.com/fwlink/?LinkID=191797)aracılığıyla ASP.NET MVC 3 RC 'yi yükleme.</span><span class="sxs-lookup"><span data-stu-id="1e220-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="1e220-233">Sorun: "&lt;yardımcı&gt; sınıfı bulunamıyor" hatası</span><span class="sxs-lookup"><span data-stu-id="1e220-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="1e220-234">Beta 3 ' e yükselttikten sonra bir yardımcı sınıfın (örneğin, `Facebook` sınıfı) bulunamadığını belirten bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="1e220-235">Beta 2 ' den itibaren ve Beta 3 ' te devam eden yardımcılar, açıkça yüklenmesi gereken paketlere taşınmıştır.</span><span class="sxs-lookup"><span data-stu-id="1e220-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="1e220-236">Mevcut siteler bu paketleri içerecek şekilde yükseltilmemiştir; Bu, *\Belgelerim\iisexpress* veya *\Belgelerim\web siteleri* klasörlerindeki siteleri içerir.</span><span class="sxs-lookup"><span data-stu-id="1e220-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="1e220-237">Özellikle, *sitemdeki* (websitesi1) varsayılan siteyi kullanıyorsanız, `Twitter` Yardımcısı 'na bir başvuru içeren bu hatayı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1e220-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="1e220-238">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-238">**Workaround**</span></span>  
> <span data-ttu-id="1e220-239">Sitedeki herhangi bir yardımcıya yönelik çağrıları açıklama olarak *\_yönetici* sayfasını çalıştırın ve kullanmak istediğiniz yardımcıları içeren paketi veya paketleri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="1e220-240">Paketi yükledikten sonra, yardımcılar 'a başvuru yapan satırların açıklamasını kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="1e220-241">Sorun: Beta 3 ASP.NET Razor derlemelerini bin klasörüne dağıtmak barındırma sitelerinde çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="1e220-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="1e220-242">Bir barındırma sitesine ASP.NET Web sayfaları Web sitesini dağıtırsanız ve ASP.NET Razor Beta 3 derlemelerini sitenin *bin* klasörüne dağıtırsanız, aşağıdakiler de dahil olmak üzere hatalarla karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e220-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="1e220-243">Barındırma sağlayıcısı, ASP.NET Web sayfaları Beta 1 derlemelerini sunucunun genel uygulama önbelleğine (GAC) yüklemişse bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="1e220-244">GAC içindeki derlemeler, *bin* klasöründe yerel olarak yüklenen derlemelerin üzerine önceliğe sahip olur.</span><span class="sxs-lookup"><span data-stu-id="1e220-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="1e220-245">**Geçici çözüm** Gördüğünüz hataların sağlayıcının derlemelerin sürümleri ve sizinkilerle ilgili olduğunu doğrulamak için barındırma sağlayıcınızla iletişim kurun.</span><span class="sxs-lookup"><span data-stu-id="1e220-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="1e220-246">Bu durumda, barındırma sağlayıcısının derlemeleri sunucunun GAC 'de güncelleştirmesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="1e220-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="1e220-247">Sorun: bir ara sunucu aracılığıyla akışları veya diğer dış verileri okuma</span><span class="sxs-lookup"><span data-stu-id="1e220-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="1e220-248">Siteyi çalıştıran sunucu bir proxy sunucusunun arkasındaysa, sitenizin dışından gelen bilgileri okuyabilmeniz için *Web. config* dosyasındaki proxy bilgilerini yapılandırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="1e220-249">Örneğin, `ReCaptcha` yardımcısını kullanıyorsanız, yardımcı, reCAPTCHA hizmeti ile iletişim kurar, ancak proxy sunucunuz tarafından engelleniyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="1e220-250">Benzer şekilde, ASP.NET Web sayfalarında kullanılan ve paket yöneticisi tarafından kullanılan akış gibi akışlar ara sunucu yapılandırması gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="1e220-251">Bir dış hizmetle çalışırken veya paket akışı ile çalışırken sorunlarla karşılaşırsanız, aşağıdaki öğeleri uygulamanızın kök *Web. config* dosyasına yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="1e220-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="1e220-252">Proxy sunucu yapılandırma hakkında daha fazla bilgi için, MSDN Web sitesindeki [&lt;proxy&gt; öğesi (ağ ayarları)](https://msdn.microsoft.com/library/sa91de1e.aspx) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="1e220-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="1e220-253">Sorun: "Microsoft. Web. Infrastructure. dll yüklenemiyor" hatası</span><span class="sxs-lookup"><span data-stu-id="1e220-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="1e220-254">Daha önce ASP.NET Web sayfalarının Beta 1 sürümünü Razor söz dizimi ve ardından Beta 3 sürümünü yüklerseniz, tüm uygun derlemeler *Microsoft. Web. Infrastructure. dll*hariç GAC 'ye yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1e220-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="1e220-255">Sonuç olarak, ASP.NET Razor sayfaları çalıştırdığınızda, *Microsoft. Web. Infrastructure. dll ' nin* yüklenemediğini belirten bir hata görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1e220-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="1e220-256">Beta 3 sürümünü temiz bir bilgisayara yüklediyseniz bu sorun oluşmaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="1e220-257">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-257">**Workaround**</span></span>  
> <span data-ttu-id="1e220-258">Denetim Masası 'nda ASP.NET Web sayfalarını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1e220-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="1e220-259">Ardından Beta 3 sürümünü yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e220-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="1e220-260">Sorun: .NET Framework sürüm 4 ' ü kaldırmak, Razor sözdizimi ile ASP.NET Web sayfalarını devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="1e220-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="1e220-261">.NET Framework sürüm 4 ' ü kaldırıp yeniden yüklerseniz, Razor söz dizimi Web sayfaları devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="1e220-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="1e220-262">*. Cshtml* uzantılı sayfalar düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="1e220-263">ASP.NET Web sayfaları, bir derlemeyi makine kök *Web. config* dosyasına kaydeder ve .NET Framework kaldırıldığında bu dosya kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="1e220-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="1e220-264">.NET Framework yeniden yüklemek, yapılandırma dosyasının yeni bir sürümünü yüklüyor, ancak ASP.NET Web Pages derlemesinin başvurusunu eklemez.</span><span class="sxs-lookup"><span data-stu-id="1e220-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="1e220-265">**Geçici çözüm** .NET Framework yeniden yükledikten sonra, ASP.NET Web sayfalarını Razor söz dizimi yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e220-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="1e220-266">Bu, genellikle aşağıdaki konumda olan makine kökündeki *Web. config* dosyasına aşağıdaki öğeyi ekler:</span><span class="sxs-lookup"><span data-stu-id="1e220-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="1e220-267">Sorun: bin klasör deneyimi hatalarında daha önce ASP.NET Derlemeleriyle dağıtılan uygulamalar</span><span class="sxs-lookup"><span data-stu-id="1e220-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="1e220-268">Dağıtım sırasında, ASP.NET Web sayfaları derlemelerinin (örneğin, *Microsoft. Web sayfaları. dll*), sunucudaki Web sitesinin *bin* klasörüne kopyaları.</span><span class="sxs-lookup"><span data-stu-id="1e220-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="1e220-269">(Dağıtım sırasında veya geliştirici derlemeleri açıkça kopyalandığı için bu durum otomatik olarak oluşmuş olabilir.) Ancak, Beta 3 sürümü yüklendiğinde, belirli türlerin hataları gibi hatalar oluşur.</span><span class="sxs-lookup"><span data-stu-id="1e220-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="1e220-270">Bu durum, Beta 3 sürümü için bir dizi ASP.NET Web sayfası türünün farklı ad alanlarına taşındığı için oluşur.</span><span class="sxs-lookup"><span data-stu-id="1e220-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="1e220-271">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="1e220-271">**Workaround** </span></span>  
> <span data-ttu-id="1e220-272">Dağıtılan uygulamanın *bin* klasörünü temizleyin, yeni derlemeleri klasöre kopyalayın (veya uygulamayı yeniden dağıtın) ve uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1e220-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="1e220-273">Sorun: Extensionless URL 'Leri IIS 7 veya IIS 7,5 üzerinde. cshtml/. vbhtml dosyalarını bulamıyor</span><span class="sxs-lookup"><span data-stu-id="1e220-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="1e220-274">IIS 7 veya IIS 7,5 ' de, aşağıdakine benzer bir URL 'ye sahip istekler *. cshtml* veya *. vbhtml* uzantısına sahip sayfaları bulamaz:</span><span class="sxs-lookup"><span data-stu-id="1e220-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="1e220-275">Bu sorun ortaya çıkar çünkü URL yeniden yazma özelliği IIS 7 veya IIS 7,5 için varsayılan olarak etkinleştirilmemiştir.</span><span class="sxs-lookup"><span data-stu-id="1e220-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="1e220-276">Likeliest senaryosu, IIS Express kullanarak yerel olarak test ederken sorunu görmemelidir, ancak Web sitenizi bir barındırma web sitesine dağıttığınızda bu sorunla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="1e220-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="1e220-277">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="1e220-278">Sunucu bilgisayar üzerinde denetiminiz varsa, sunucu bilgisayarda, [belırlı ııs 7,0 veya ııs 7,5 işleyicilerinin, URL 'lerin noktayla bitmeyen istekleri işlemesini sağlayan bir güncelleştirmede](https://support.microsoft.com/kb/980368)açıklanan güncelleştirmeyi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="1e220-279">Sunucu bilgisayarı üzerinde denetiminiz yoksa (örneğin, bir barındırma web sitesine dağıtıyorsanız), aşağıdakileri Web sitesinin *Web. config* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1e220-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="1e220-280">Sorun: Web uygulaması projesi veya ASP.NET MVC ve ASP.NET Web sayfalarını aynı uygulamada kullanma</span><span class="sxs-lookup"><span data-stu-id="1e220-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="1e220-281">Web uygulaması projesinde veya ASP.NET MVC uygulamasında ASP.NET Web sayfaları kullanıyorsanız, *Webpagehttpapplication* 'un bulunamadığını belirten bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e220-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="1e220-282">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-282">**Workaround**</span></span>  
> <span data-ttu-id="1e220-283">Bu hatayı alırsanız, uygulamanın türettiği temel sınıfı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1e220-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="1e220-284">*Global. asax* dosyasında aşağıdaki satırı değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1e220-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="1e220-285">Bunun için:</span><span class="sxs-lookup"><span data-stu-id="1e220-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="1e220-286">Bu efekt, Razor söz dizimi ile ASP.NET Web sayfalarının Beta 1 sürümü için tanıtılan bir değişikliği tersine çevirir.</span><span class="sxs-lookup"><span data-stu-id="1e220-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="1e220-287">Sorun: SQL Server Compact yüklü olmayan bir bilgisayara uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="1e220-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="1e220-288">SQL Server Compact veritabanlarını içeren uygulamalar, SQL Server Compact yüklü olmayan bir bilgisayarda çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="1e220-289">Microsoft WebMatrix Beta 3, bu ikili dosyaları sizin için otomatik olarak kopyalar ve uygun *Web. config* dosyası dönüşümlerini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="1e220-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="1e220-290">**Geçici çözüm** Bu dosyaları kopyalamanız ve *Web. config* dosyasının el ile değişiklikleri yapmanız gerekiyorsa, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="1e220-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="1e220-291">Veritabanı altyapısı derlemelerini hedef bilgisayardaki uygulamanın *bin* klasörüne (ve alt klasörlerine) kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="1e220-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="1e220-292">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **'i** *\Bin* 'e Kopyala</span><span class="sxs-lookup"><span data-stu-id="1e220-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="1e220-293">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* \*  **'i** *\bin\x86* ' ya kopyalayın</span><span class="sxs-lookup"><span data-stu-id="1e220-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="1e220-294">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \*  **'i** *\bin\amd64* dizinine kopyalayın</span><span class="sxs-lookup"><span data-stu-id="1e220-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="1e220-295">Web sitesinin kök klasöründe bir *Web. config* dosyası oluşturun veya açın.</span><span class="sxs-lookup"><span data-stu-id="1e220-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="1e220-296">(WebMatrix Beta 3 ' te, **dosya türü seç** Iletişim kutusunda **Tümü** ' ne tıkladığınızda bu dosya türü kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="1e220-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="1e220-297">Aşağıdaki öğeyi **&lt;configuration&gt;** öğesinin bir alt öğesi olarak ekleyin ( **&lt;system. Web&gt;** öğesinin içinde değil):</span><span class="sxs-lookup"><span data-stu-id="1e220-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="1e220-298">Sorun: veritabanı ve WebGrid yardımcıları Visual Basic sürümünde Orta güvende çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="1e220-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="1e220-299">Visual Basic kullanıyorsanız ( *. vbhtml* dosyaları oluşturma), uygulama orta güveni kullanmak üzere ayarlandıysa `Database` ve `WebGrid` yardımcıları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="1e220-300">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-300">**Workaround**</span></span>  
> <span data-ttu-id="1e220-301">Uygulamayı tam güven kullanacak şekilde geçici olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="1e220-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="1e220-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="1e220-303">Sorun: "Encrypt" özelliği tanınmıyor</span><span class="sxs-lookup"><span data-stu-id="1e220-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="1e220-304">SQL Server Compact 4,0, `SqlCeConnection` sınıfının `Encrypt` özelliğini tanımıyor.</span><span class="sxs-lookup"><span data-stu-id="1e220-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="1e220-305">Veritabanı dosyalarını şifrelemek için bu özelliği kullanmamalısınız.</span><span class="sxs-lookup"><span data-stu-id="1e220-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="1e220-306">`Encrypt` özelliği SQL Server Compact 3,5 sürümünde kullanımdan kaldırılmıştır ve yalnızca geriye dönük uyumluluk için korunur.</span><span class="sxs-lookup"><span data-stu-id="1e220-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="1e220-307">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-307">**Workaround**</span></span>  
> <span data-ttu-id="1e220-308">SQL Server Compact 4,0 veritabanı dosyalarını şifrelemek için `SqlCeConnection` sınıfının `Encryption Mode` özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e220-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="1e220-309">Aşağıdaki örnek, `Encryption Mode` özelliğini kullanarak nasıl şifreli SQL Server Compact 4,0 veritabanı oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="1e220-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="1e220-310">Mevcut bir SQL Server Compact 4,0 veritabanının şifreleme modunu değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="1e220-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="1e220-311">Şifrelenmemiş bir SQL Server Compact 4,0 veritabanını şifrelemek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="1e220-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="1e220-312">Sorun: Microsoft Visual C++ 2008 çalışma zamanı kitaplıkları gereklidir</span><span class="sxs-lookup"><span data-stu-id="1e220-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="1e220-313">SQL Server Compact 4,0 ' in yerel dll 'Leri Microsoft Visual C++ 2008 çalışma zamanı kitaplıklarını (x86, IA64 ve x64), hizmet paketi 1 ' i gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1e220-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="1e220-314">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-314">**Workaround**</span></span>  
> <span data-ttu-id="1e220-315">.NET Framework 3,5 SP1 'i yükler.</span><span class="sxs-lookup"><span data-stu-id="1e220-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="1e220-316">Bu, Visual C++ 2008 çalışma zamanı kitaplıkları SP1 de yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1e220-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="1e220-317">Kitaplıkları aşağıdaki konumdan indirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e220-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="1e220-318">Microsoft Visual C++ 2008 Service Pack 1 yeniden DAĞITILABILIR paket ATL güvenlik güncelleştirmesi</span><span class="sxs-lookup"><span data-stu-id="1e220-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="1e220-319">2,0, 3,0 veya 4 *.NET Framework yükleme Visual* C++ 2008 çalışma zamanı kitaplıkları SP1 'i yüklemediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="1e220-320">Sorun: bilgisayara .NET Framework yüklemeden önce SQL Server Compact yüklüyse, sağlayıcının sabit adı .NET Framework Machine. config dosyasında kayıtlı değil</span><span class="sxs-lookup"><span data-stu-id="1e220-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="1e220-321">SQL Server Compact, SQL Server Compact .NET Framework gerektirdiğinden .NET Framework yüklü olmayan bir makineye yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="1e220-322">SQL Server Compact yüklemeden önce .NET Framework sürüm 3,5 veya 4 yüklü değilse SQL Server Compact kurulum, *Machine. config* dosyasına sağlayıcının sabit adını kaydetmez.</span><span class="sxs-lookup"><span data-stu-id="1e220-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="1e220-323">*Machine. config* dosyasında SQL Server Compact girişi kullanan herhangi bir uygulama başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="1e220-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="1e220-324">*Machine. config* dosyasındaki sabit ad kayıt girdisi aşağıdaki örneğe benzer şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="1e220-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="1e220-325">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-325">**Workaround**</span></span>  
> <span data-ttu-id="1e220-326">SQL Server Compact 4,0 CTP1 'yi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1e220-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="1e220-327">Aşağıdaki konumdan .NET Framework tam sürümlerini indirip yükleyin:</span><span class="sxs-lookup"><span data-stu-id="1e220-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="1e220-328">Microsoft .NET Framework 3,5 Service Pack 1 (tam paket)</span><span class="sxs-lookup"><span data-stu-id="1e220-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="1e220-329">Microsoft .NET Framework 4,0 sürümü (tam paket)</span><span class="sxs-lookup"><span data-stu-id="1e220-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="1e220-330">[SQL Server Compact 4,0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1e220-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="1e220-331">Uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="1e220-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="1e220-332">Sorun: kullanıcının Belgelerim klasörü bir ağ paylaşımında yeniden yönlendiriliyorsa, uygulamanın yüklenmesi uzun zaman alabilir</span><span class="sxs-lookup"><span data-stu-id="1e220-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="1e220-333">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-333">**Workaround**</span></span>  
> <span data-ttu-id="1e220-334">Yok.</span><span class="sxs-lookup"><span data-stu-id="1e220-334">None.</span></span> <span data-ttu-id="1e220-335">Uygulamanın yüklenmesi biraz zaman alabilir, ancak doğru şekilde yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1e220-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="1e220-336">Uygulamaları yayımlama</span><span class="sxs-lookup"><span data-stu-id="1e220-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="1e220-337">Sorun: "hedef URL" alanı http://veya https://ön eki değilse, site yayımlamadan sonra çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="1e220-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="1e220-338">**Yayımlama ayarları** iletişim kutusunda, hedef URL `http://` veya `https://`ile başlamadıysanız, site dağıtımdan sonra çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="1e220-339">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-339">**Workaround**</span></span>  
> <span data-ttu-id="1e220-340">Bir siteyi yayımlamadan önce, **yayınlama ayarları** iletişim KUTUSUNDAKI hedef URL 'nin `http://` veya `https://`ile başlayacağını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="1e220-341">Sorun: bir MySQL veritabanının yayımlanması "veritabanı yayımlanamadı.</span><span class="sxs-lookup"><span data-stu-id="1e220-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="1e220-342">Uzak veritabanı betiği çalıştıramadığı takdirde bu durum oluşabilir. "</span><span class="sxs-lookup"><span data-stu-id="1e220-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="1e220-343">Hata çeşitli nedenlerden kaynaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="1e220-344">Bu hatayı görebileceğiniz bir nedeni, veritabanı betiğinin tek tırnak karakteri (') içermesi ve hedef MySQL veritabanının varsayılan karakter kümesinin UTF-8 ' e olmaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e220-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="1e220-345">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-345">**Workaround**</span></span>  
> <span data-ttu-id="1e220-346">Uzak MySQL veritabanı için varsayılan karakter kümesini UTF-8 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="1e220-347">Diğer Sorunlar</span><span class="sxs-lookup"><span data-stu-id="1e220-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="1e220-348">Sorun: arama/filtreleme, gruplandırma ölçütü: sorun türü raporlarında çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="1e220-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="1e220-349">Bir site için rapor çalıştırdığınızda, *URL 'ye göre filtrele* kutusuna metin girip *Ara*' yı tıklatırsanız, hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="1e220-350">Bunun nedeni, raporun eyalet *ölçütü* , varsayılan değer olan durum *türü*olarak ayarlandığı sürece bu denetim işlevsel değildir.</span><span class="sxs-lookup"><span data-stu-id="1e220-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="1e220-351">**Geçici çözüm** Şerit 'in *Gruplandırma ölçütü* sekmesinde, GIRDILERI kaynak URL 'lerine göre gruplandırmak için *URL* ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="1e220-352">Bu durumda, girdileri filtrelemek için metin kutusu ve düğme işlevseldir.</span><span class="sxs-lookup"><span data-stu-id="1e220-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="1e220-353">Sorun: WCF uygulamaları IIS Express ile çalıştırılamaz</span><span class="sxs-lookup"><span data-stu-id="1e220-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="1e220-354">Bir WCF uygulamasına göz atmak aşağıdakine benzer bir hata ile sonuçlanır:</span><span class="sxs-lookup"><span data-stu-id="1e220-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="1e220-355">*Dosya veya derleme ' Microsoft. Web. Administration, version = 7.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' veya bağımlılıklarından biri yüklenemedi. Sistem belirtilen dosyayı bulamıyor.*</span><span class="sxs-lookup"><span data-stu-id="1e220-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="1e220-356">Bu durum IIS Express beta sürümü varsayılan olarak WCF 'yi desteklemediğinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="1e220-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="1e220-357">**Geçici çözüm** Aşağıdaki geçici çözümlerden birini kullanın (geçici çözüm #2 Microsoft Windows Vista veya üstünü gerektirir):</span><span class="sxs-lookup"><span data-stu-id="1e220-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="1e220-358">WebMatrix yükleme konumundan *Microsoft. Web. dll* ve *Microsoft. Web. Administration. dll* derlemelerini WCF uygulamasının *bin* dizinine kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="1e220-359">Varsayılan olarak, WebMatrix, sistemin *Program Files* klasörü altındaki *Microsoft WebMatrix* alt klasörüne yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1e220-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="1e220-360">Microsoft Windows Vista veya üzeri sürümlerde, *bin* dizinindeki derlemeler için aşağıdaki komutları kullanarak bir oluşturmaksızın oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e220-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="1e220-361">(Bu yaklaşım, derlemelerin bir kopyasını oluşturmadığından faydalanır.)</span><span class="sxs-lookup"><span data-stu-id="1e220-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="1e220-362">GAC 'de iki derlemeyi yükler.</span><span class="sxs-lookup"><span data-stu-id="1e220-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="1e220-363">Yükseltilmiş bir komut isteminden aşağıdaki komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1e220-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="1e220-364">Sorun: WebMatrix Beta 3, yükseltme gerektiren belirli görevleri gerçekleştiremiyor</span><span class="sxs-lookup"><span data-stu-id="1e220-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="1e220-365">WebMatrix Beta 3, aşağıdaki durumlarda ek bileşenler yükleme gibi yükseltme gerektiren belirli görevleri gerçekleştiremiyor:</span><span class="sxs-lookup"><span data-stu-id="1e220-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="1e220-366">Windows Vista veya Windows 7 ' de, yönetici ayrıcalıklarına sahip olmayan bir hesapla oturum açarsınız ve Kullanıcı hesabı denetimi (UAC) devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="1e220-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="1e220-367">Microsoft Windows XP veya Microsoft Windows Server 2003 kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="1e220-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="1e220-368">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-368">**Workaround**</span></span>  
> <span data-ttu-id="1e220-369">WebMatrix Beta 3 ' teki çoğu görev yönetici izni gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="1e220-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="1e220-370">Bu işlemler için, işlemi yönetici olarak gerçekleştirebilir veya aşağıdaki adımları izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e220-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="1e220-371">Windows Vista veya Windows 7 ' de UAC 'yi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1e220-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="1e220-372">Windows XP 'de, kullanıcıyı Administrators güvenlik grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e220-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="1e220-373">Sorun: "Web galerisinden site" devre dışı</span><span class="sxs-lookup"><span data-stu-id="1e220-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="1e220-374">Web Platformu Yükleyicisi 3,0 yüklü değilse, **Web galerisinden site** seçeneği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="1e220-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="1e220-375">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-375">**Workaround**</span></span>  
> <span data-ttu-id="1e220-376">[3,0 Microsoft Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkID=194638)'yi yükler.</span><span class="sxs-lookup"><span data-stu-id="1e220-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="1e220-377">Sorun: Windows Server 2003 ' de IIS Express yönetici olmayan bir kullanıcı için başlamıyor</span><span class="sxs-lookup"><span data-stu-id="1e220-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="1e220-378">Windows Server 2003 ' de, bir sayfa başlattığınızda veya IIS Express başlattığınızda IIS Express başlamaz.</span><span class="sxs-lookup"><span data-stu-id="1e220-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="1e220-379">Web sayfaları için, uygulamanın yönetici olmayan bir kullanıcı tarafından başlatıldığını belirten bir hata görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1e220-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="1e220-380">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-380">**Workaround**</span></span>  
> <span data-ttu-id="1e220-381">WebMatrix Beta 3 ' ü Yönetici Kullanıcı olarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="1e220-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="1e220-382">Daha fazla ayrıntı için aşağıdaki Bilgi Bankası makalesine bakın:</span><span class="sxs-lookup"><span data-stu-id="1e220-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="1e220-383">Yönetici olmayan bir kullanıcı tarafından başlatılan bir uygulama, uygulamanın Windows Vista, Windows Server 2003 veya Windows XP 'de çalıştığı bilgisayarın HTTP trafiğini dinleyemeyen bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="1e220-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="1e220-384">Sorun: Google Chrome bir çalıştır seçeneği olarak kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="1e220-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="1e220-385">Google Chrome, **giriş** sekmesinde **Çalıştır** altında bulunan tarayıcılar listesinde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="1e220-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="1e220-386">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-386">**Workaround**</span></span>  
> <span data-ttu-id="1e220-387">Google Chrome 'un bazı sürümleri, Windows 'daki varsayılan programlar özelliği ile kendilerini doğru bir şekilde kaydetmez.</span><span class="sxs-lookup"><span data-stu-id="1e220-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="1e220-388">Geçici bir çözüm olarak, Google Chrome 'u başlatın, *Google Chrome ' ı Özelleştir ve denetle* menüsüne tıklayın, *Seçenekler*' e ve ardından *Google Chrome varsayılan tarayıcımı oluştur*' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="1e220-389">Sorun: "yabancı anahtar" iletişim kutusu birincil anahtar girmeye izin vermiyor</span><span class="sxs-lookup"><span data-stu-id="1e220-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="1e220-390">**Yabancı anahtar** iletişim kutusu birincil anahtar tablosundan birincil anahtar adını girmenize izin vermez.</span><span class="sxs-lookup"><span data-stu-id="1e220-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="1e220-391">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-391">**Workaround**</span></span>  
> <span data-ttu-id="1e220-392">Bu bilerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="1e220-392">This is intentional.</span></span> <span data-ttu-id="1e220-393">Birincil anahtar tablosundan birincil anahtar adını girmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1e220-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="1e220-394">Sorun: "Ilişkiler" düğmesi devre dışı</span><span class="sxs-lookup"><span data-stu-id="1e220-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="1e220-395">**Veritabanları** çalışma alanındaki **tablo** sekmesinin altındaki **ilişkiler** düğmesi SQL Server Compact veritabanları için devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="1e220-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="1e220-396">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-396">**Workaround**</span></span>  
> <span data-ttu-id="1e220-397">Yok.</span><span class="sxs-lookup"><span data-stu-id="1e220-397">None.</span></span> <span data-ttu-id="1e220-398">SQL Server Compact, tablolar arasındaki ilişkileri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="1e220-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="1e220-399">Sorun: parametreli SQL sorguları özel durumlar oluşturur</span><span class="sxs-lookup"><span data-stu-id="1e220-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="1e220-400">SQL Server Compact 4,0 ' de, parametreli sorgularda parametreler için `SqlDbType` veya `DbType` gibi bir veri türü belirtmezseniz, sorgu çalıştırıldığında bir özel durum oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1e220-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="1e220-401">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="1e220-401">**Workaround**</span></span>  
> <span data-ttu-id="1e220-402">`SqlDbType` veya `DbType`gibi parametreler için veri türünü açık olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1e220-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="1e220-403">BLOB veri türleri (`image` ve `ntext`) söz konusu olduğunda bu kritik öneme sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1e220-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="1e220-404">Aşağıdaki gibi bir kod kullanın:</span><span class="sxs-lookup"><span data-stu-id="1e220-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="1e220-405">Daha Fazla Bilgi İçin</span><span class="sxs-lookup"><span data-stu-id="1e220-405">For More Information</span></span>

<span data-ttu-id="1e220-406">WebMatrix Beta 3 hakkında daha fazla bilgi için, aşağıdaki Web sitelerine bakın:</span><span class="sxs-lookup"><span data-stu-id="1e220-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="1e220-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="1e220-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="1e220-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1e220-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="1e220-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="1e220-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="1e220-410">© 2010 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="1e220-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="1e220-411">Tüm hakları saklıdır.</span><span class="sxs-lookup"><span data-stu-id="1e220-411">All Rights Reserved.</span></span> <span data-ttu-id="1e220-412">[Kullanım koşulları](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e220-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
