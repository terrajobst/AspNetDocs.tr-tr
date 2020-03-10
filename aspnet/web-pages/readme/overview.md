---
uid: web-pages/readme/overview
title: WebMatrix Benioku | Microsoft Docs
author: rick-anderson
description: WebMatrix ve ASP.NET Web Pages (Razor) 1,0 yayın Benioku dosyası
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563471"
---
# <a name="webmatrix-readme"></a><span data-ttu-id="f147d-103">WebMatrix Benioku dosyası</span><span class="sxs-lookup"><span data-stu-id="f147d-103">WebMatrix Readme</span></span>

<span data-ttu-id="f147d-104">13 Ocak 2011</span><span class="sxs-lookup"><span data-stu-id="f147d-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="f147d-105">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="f147d-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="f147d-106">Bu benioku, WebMatrix 'in 1,0 sürümü için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="f147d-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="f147d-107">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="f147d-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="f147d-108">Yükleme</span><span class="sxs-lookup"><span data-stu-id="f147d-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="f147d-109">Uygulamaları yayımlama</span><span class="sxs-lookup"><span data-stu-id="f147d-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="f147d-110">Değişiklikler ve sorunlar</span><span class="sxs-lookup"><span data-stu-id="f147d-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="f147d-111">WebMatrix 1,0 yüklemesi</span><span class="sxs-lookup"><span data-stu-id="f147d-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="f147d-112">ASP.NET Web Sayfaları</span><span class="sxs-lookup"><span data-stu-id="f147d-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="f147d-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="f147d-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="f147d-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="f147d-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="f147d-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="f147d-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="f147d-116">Uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="f147d-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="f147d-117">Uygulamaları yayımlama</span><span class="sxs-lookup"><span data-stu-id="f147d-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="f147d-118">Daha fazla bilgi için</span><span class="sxs-lookup"><span data-stu-id="f147d-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="f147d-119">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="f147d-119">Overview</span></span>

> <span data-ttu-id="f147d-120">Microsoft WebMatrix 1,0, dakikalar içinde yüklenen ücretsiz bir Web geliştirme yığınıdır.</span><span class="sxs-lookup"><span data-stu-id="f147d-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="f147d-121">Tek ve tümleşik bir deneyim oluşturmak için veritabanı ve programlama çerçeveleri ile bir Web sunucusunu tümleştirir.</span><span class="sxs-lookup"><span data-stu-id="f147d-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="f147d-122">WebMatrix kullanarak kendi ASP.NET veya PHP Web sitenizi kodlayın, test edin ve yayımlayın ya da DotNetNuke, dönen Raco, WordPress veya Joomla gibi popüler açık kaynaklı uygulamaları kullanarak yeni bir Web sitesini başlatmak için WebMatrix 'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="f147d-123">WebMatrix, Web sitenizi Internet üzerinde çalıştıracak olan güçlü Web sunucusu, veritabanı altyapısı ve çerçeveler ortamını kullanır. Bu, geliştirmeden üretime sorunsuz ve sorunsuz bir şekilde geçiş yapar.</span><span class="sxs-lookup"><span data-stu-id="f147d-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="f147d-124">Yükleme</span><span class="sxs-lookup"><span data-stu-id="f147d-124">Installation</span></span>

> <span data-ttu-id="f147d-125">WebMatrix 1,0 ' ü yüklemek için, ilk olarak [Microsoft Web Platformu Yükleyicisi 3,0](https://go.microsoft.com/fwlink/?LinkID=194638)' ü yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f147d-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="f147d-126">Web Platformu Yükleyicisi 'ni yükledikten sonra WebMatrix 'i yüklemek için bu uygulamayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="f147d-127">Yükleme sırasında sorunlarla karşılaşırsanız [Microsoft Web Platformu Yükleyicisi sorun giderme sorunları](https://go.microsoft.com/fwlink/?LinkId=196212)bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f147d-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="f147d-128">Uygulamaları yayımlama</span><span class="sxs-lookup"><span data-stu-id="f147d-128">How to Publish Applications</span></span>

> <span data-ttu-id="f147d-129">Bkz. [uygulamaları yayımlamak Için adım adım yönergeler](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="f147d-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="f147d-130">Değişiklikler ve sorunlar</span><span class="sxs-lookup"><span data-stu-id="f147d-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="f147d-131">WebMatrix 1,0 yükleme sorunları</span><span class="sxs-lookup"><span data-stu-id="f147d-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="f147d-132">Sorun: WebMatrix 1,0 yalnızca Microsoft .NET Framework 4 ' ü destekleyen platformlarda kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f147d-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="f147d-133">WebMatrix için .NET Framework sürüm 4 gerekir.</span><span class="sxs-lookup"><span data-stu-id="f147d-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="f147d-134">Bazı durumlarda, WebMatrix 1,0 yükleyicisi, desteklenen yapılandırma kümesinin parçası olmayan bir platforma yükleme denemenize imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="f147d-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="f147d-135">Özellikle, SP1 güncelleştirmesi olmayan Windows Vista, WebMatrix yüklemesine başlamanızı sağlar, ancak .NET Framework 4 bileşeni başarısız olur ve yüklemenizi engeller.</span><span class="sxs-lookup"><span data-stu-id="f147d-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="f147d-136">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-136">**Workaround**</span></span>  
> <span data-ttu-id="f147d-137">Aşağıdakileri içeren desteklenen bir platforma yükler:</span><span class="sxs-lookup"><span data-stu-id="f147d-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="f147d-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="f147d-138">Windows 7</span></span>
> - <span data-ttu-id="f147d-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="f147d-139">Windows Server 2008</span></span>
> - <span data-ttu-id="f147d-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="f147d-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="f147d-141">Windows Vista SP1 veya sonraki sürümü</span><span class="sxs-lookup"><span data-stu-id="f147d-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="f147d-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="f147d-142">Windows XP SP3</span></span>
> - <span data-ttu-id="f147d-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="f147d-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="f147d-144">Sorun: Microsoft Visual Studio 2008 SP1 olmadan Microsoft Visual Studio 2008 yüklenirse WebMatrix 1,0 yüklenemiyor</span><span class="sxs-lookup"><span data-stu-id="f147d-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="f147d-145">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-145">**Workaround**</span></span>  
> <span data-ttu-id="f147d-146">[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 'ı Microsoft İndirme Merkezi ' nden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f147d-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="f147d-147">Sorun: SQL Server Compact 4,0 için bazı derlemeler GAC 'de yüklü değil</span><span class="sxs-lookup"><span data-stu-id="f147d-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="f147d-148">SQL Server Compact 4,0 için yönetilen derlemeler, SQL Server Compact 4,0 ' i bir 64 bit bilgisayara yüklediğinizde ve bilgisayarda yalnızca .NET Framework 3,5 SP1 Istemci profili yüklü olduğunda genel derleme önbelleği 'ne (GAC) yerleştirilmez.</span><span class="sxs-lookup"><span data-stu-id="f147d-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="f147d-149">GAC 'de yüklü olmayan yönetilen derlemeler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f147d-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="f147d-150">*System. Data. SqlServerCe. dll* (ADO.NET sağlayıcısı)</span><span class="sxs-lookup"><span data-stu-id="f147d-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="f147d-151">*System. Data. SqlServerCe. Entity. dll* (ADO.NET Entity Framework)</span><span class="sxs-lookup"><span data-stu-id="f147d-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="f147d-152">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-152">**Workaround**</span></span>  
> <span data-ttu-id="f147d-153">SQL Server Compact 4,0 'yi kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f147d-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="f147d-154">Aşağıdaki konumdan .NET Framework 3,5 SP1 'in tam sürümünü indirip yükleyin:</span><span class="sxs-lookup"><span data-stu-id="f147d-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="f147d-155">Microsoft .NET Framework 3,5 Service Pack 1 (tam paket)</span><span class="sxs-lookup"><span data-stu-id="f147d-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="f147d-156">SQL Server Compact 4,0 yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f147d-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="f147d-157">Sorun: komut satırı kullanılarak SQL Server Compact kaldırılamıyor</span><span class="sxs-lookup"><span data-stu-id="f147d-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="f147d-158">Komut satırı seçeneklerini kullanarak SQL Server Compact kaldırılması bu sürümde çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="f147d-159">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-159">**Workaround**</span></span>  
> <span data-ttu-id="f147d-160">4,0 Microsoft SQL Server Compact kaldırmak için Windows Denetim Masası 'ndaki *Programlar ve Özellikler ' i* kullanın.</span><span class="sxs-lookup"><span data-stu-id="f147d-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="f147d-161">ASP.NET Web Sayfaları</span><span class="sxs-lookup"><span data-stu-id="f147d-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="f147d-162">Belgenin bu bölümünde, Razor söz dizimi ile ASP.NET Web sayfalarının 1,0 sürümündeki yeni özellikler, değişiklikler ve bilinen sorunlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f147d-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="f147d-163">Yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="f147d-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="f147d-164">Değişikliklerine</span><span class="sxs-lookup"><span data-stu-id="f147d-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="f147d-165">Sorunlar</span><span class="sxs-lookup"><span data-stu-id="f147d-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a><span data-ttu-id="f147d-166">Yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="f147d-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="f147d-167">Yeni: paket yöneticisini devre dışı bırakmak için yapılandırma ayarı eklendi</span><span class="sxs-lookup"><span data-stu-id="f147d-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="f147d-168">*Web. config* dosyasındaki `<appSettings>` öğesi için yeni bir `asp:AdminManagerEnabled` anahtarı vardır ve bu, paket yöneticisini tamamen devre dışı bırakmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="f147d-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="f147d-169">Bu öğe için varsayılan değer true 'dur, yani *Web. config* dosyasına dahil edilmediğinde, Paket Yöneticisi etkindir.</span><span class="sxs-lookup"><span data-stu-id="f147d-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="f147d-170">Paket yöneticisini devre dışı bırakmak için, aşağıdaki öğeyi Web sitesinin kökündeki *Web. config* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f147d-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a><span data-ttu-id="f147d-171">Değişikliklerine</span><span class="sxs-lookup"><span data-stu-id="f147d-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="f147d-172">Değişiklik: "Web sayfaları: AdminFolderVirtualPath" anahtarı "ASP: AdminFolderVirtualPath" olarak yeniden adlandırıldı</span><span class="sxs-lookup"><span data-stu-id="f147d-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="f147d-173">Paket yöneticisinin konumunu belirtmek için *Web. config* dosyasına eklenebilen `webPages:AdminFolderVirtualPath` anahtarı, `webPages` ad alanı yerine `asp:` ad alanını kullanacak şekilde yeniden adlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="f147d-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="f147d-174">Bu öğeyi kullandıysanız yapılandırma dosyasında yeniden adlandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f147d-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a> <span data-ttu-id="f147d-175">Bilinen Sorunlar</span><span class="sxs-lookup"><span data-stu-id="f147d-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="f147d-176">Sorun: üyelik kullanıcıları için parolalar artık tanınmıyor</span><span class="sxs-lookup"><span data-stu-id="f147d-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="f147d-177">Üyelik (oturum açma) parolalarının oluşturulması ve depolanması için algoritma daha güvenli olacak şekilde değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="f147d-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="f147d-178">Sonuç olarak, ASP.NET Razor 'nin Beta sürümlerinde oluşturulan Üyeler (kullanıcılar) için depolanan parolalar tanınmaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="f147d-179">**Geçici çözüm** Site henüz üretime yerleştirmemişse, Kullanıcı kayıtlarını üyelik veritabanından kaldırın.</span><span class="sxs-lookup"><span data-stu-id="f147d-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="f147d-180">Veritabanı canlı ise, üyelik veritabanındaki mevcut parolaları program aracılığıyla yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f147d-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="f147d-181">Sorun: üyelik için özel bir kullanıcı tablosu kullanılırken beklenmeyen davranış</span><span class="sxs-lookup"><span data-stu-id="f147d-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="f147d-182">Bir ASP.NET Razor Web sitesinin üyelik sağlayıcısını başlatmak için `WebSecurity.InitializeDatabaseConnection` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f147d-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="f147d-183">(WebMatrix 'te, başlatıcı site şablonu *\_AppStart. cshtml* dosyasında Bu metoda bir çağrı içerir.) Bu yöntemin `autoCreateTables` parametresi true olarak ayarlanmışsa (varsayılan olarak, başlatıcı site şablonunda true olarak ayarlanır) ve tanınmayan bir tablo adı yönteme (ikinci parametre) geçirilirse Yöntem bir hata oluşturmaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="f147d-184">Bunun yerine, tabloyu otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f147d-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="f147d-185">Bu, üyelik için özel bir kullanıcı tablosu kullanmayı amaçlıyorsanız ancak yanlış tablo adını `WebSecurity.InitializeDatabaseConnection` yöntemine geçirirseniz bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="f147d-186">Yöntemi varsayılan olarak, belirttiğiniz tablo yoksa ve bunun yerine yeni bir tablo oluşturduğunda bir hata oluşturmaz, uygulama çalışıyor olarak görünebilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="f147d-187">Ancak, Özel Kullanıcı tablonuza (ve içindeki alanlarda) bağlı olan uygulama kodu sonunda beklenmedik hatalarla başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="f147d-188">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-188">**Workaround**</span></span>  
> <span data-ttu-id="f147d-189">`InitializeDatabaseConnection` yönteminde geçirilen adın, üyelik veritabanındaki kullanıcı profili tablosuyla eşleştiğinden emin olun veya `autoCreateTables` parametresinin false olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f147d-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a><span data-ttu-id="f147d-190">Sorun: "Yönetici modülü ~/App\_Data için erişim gerektiriyor" hata iletisi</span><span class="sxs-lookup"><span data-stu-id="f147d-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="f147d-191">Bazı durumlarda, kullanıcı oluşturmaya veya başka bir şekilde ASP.NET üyelik sistemiyle çalışmayı denemek sayfanın *Yönetim modülünün ~/App\_verilerine erişmesi gereken*hatayı görüntülemesine neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="f147d-192">Bu durum, IIS veya IIS Express 'nin altında çalıştığı hesabın, Web sitesi kökünde *uygulama\_veri* klasörü oluşturma ve bu klasöre yazma izinleri yoksa oluşur.</span><span class="sxs-lookup"><span data-stu-id="f147d-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="f147d-193">**Geçici çözüm** Web sitesi için el ile *uygulama\_veri* klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f147d-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="f147d-194">Daha sonra uygulamanın altında çalıştığı Windows hesabının (genellikle ağ HIZMETI) uygulamanın kök klasörleri ve App\_verileri gibi alt klasörler için okuma/yazma izinlerine sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f147d-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="f147d-195">[SQL Server Express Kullanıcı örneği oluşturma ve ASP.NET Web uygulaması projeleriyle](https://support.microsoft.com/kb/2002980)Ilgili Bilgi Bankası makalesi sorunlarını daha ayrıntılı olarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="f147d-196">Sorun: "SQL Server bir kullanıcı örneği oluşturulamadı" hatası</span><span class="sxs-lookup"><span data-stu-id="f147d-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="f147d-197">Bir WebMatrix Web uygulaması SQL Server Express kullanıyorsa ve Windows 7 veya Windows Server 2008 R2 üzerinde IIS 7,5 çalıştırıyorsa, SQL Server kullanıcının yerel uygulama yolunu çalışma zamanında alamadığını belirten bir hata görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="f147d-198">**Geçici çözüm** Uygulamanın altında çalıştığı Windows hesabının (genellikle ağ HIZMETI) uygulamanın kök klasörleri ve *App\_verileri*gibi alt klasörler için okuma/yazma izinlerine sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f147d-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="f147d-199">[SQL Server Express Kullanıcı örneği oluşturma ve ASP.NET Web uygulaması projeleriyle](https://support.microsoft.com/kb/2002980)Ilgili Bilgi Bankası makalesi sorunlarını daha ayrıntılı olarak bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="f147d-200">Sorun: Package Manager kaynakları veya Package-Manager parolalarını içeren dosyalar IIS 6,0 ve öncesi sürümlerde kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f147d-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="f147d-201">RC2 sürümü kullanılarak oluşturulmuş bir ASP.NET Web Pages (Razor) uygulaması dağıtırsanız ve uygulama */App\_Data/admin*altında bir *password. txt* veya *packageso,. txt* dosyası içeriyorsa, IIS 6,0, istenirse dosyayı kullanacaktır ve bu da paket yöneticisi örneğinizin parolalarını açığa çıkarmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="f147d-202">**Geçici çözüm** Password. *txt* veya *packageso,. txt* dosyasını *password. config* veya *packageso,. config*olarak yeniden adlandırın. Varsayılan olarak, IIS 6,0 *. config* uzantısına sahip dosyalara sahip değildir.</span><span class="sxs-lookup"><span data-stu-id="f147d-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="f147d-203">(IIS 7 ' de, *uygulama\_veri* klasörüne hiçbir dosya sunulmadığından, dosyaları yeniden adlandırmanıza gerek kalmaz.)</span><span class="sxs-lookup"><span data-stu-id="f147d-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="f147d-204">Sorun: Beta 3 sürümü kullanılarak yüklenen paketleri kaldırmak, paket bileşenlerini tamamen kaldırmaz</span><span class="sxs-lookup"><span data-stu-id="f147d-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="f147d-205">Beta 3 sürümündeki Paket Yöneticisi 'ni kullanarak bir paket yüklediyseniz ve sonra geçerli sürümü kullanarak kaldırmayı denerseniz, paket tümüyle kaldırılmaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="f147d-206">Paket yöneticisinin **Kaldır** düğmesinin kullanılması bazı bileşenleri kaldırır, ancak paketin kitaplık kodunu bırakır ve *Package. config* dosyasını güncelleştirmez.</span><span class="sxs-lookup"><span data-stu-id="f147d-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="f147d-207">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="f147d-207">**Workaround** </span></span>  
> <span data-ttu-id="f147d-208">Şu adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="f147d-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="f147d-209">*App\_Data\packages* klasörünü silin.</span><span class="sxs-lookup"><span data-stu-id="f147d-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="f147d-210">Bu, tüm paketleri kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f147d-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="f147d-211">Web sitesinin kökündeki *Packages. config* dosyasını silin.</span><span class="sxs-lookup"><span data-stu-id="f147d-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="f147d-212">Sorun: Visual Studio 'Da, Web tabanlı paket yöneticisini çağırmak uygulamayı çevrimdışı duruma getirir</span><span class="sxs-lookup"><span data-stu-id="f147d-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="f147d-213">Visual Studio 'da (WebMatrix değil) çalışıyorsanız ve Paket Yöneticisi 'ni başlatmak için *\_yönetici* işlevini kullanırsanız, Visual Studio uygulamayı çevrimdışına alır ve *uygulamayı çevrimdışı. htm\_* Web sitesi köküne gönderir ve bu da paket yöneticisini kullanma yeteneğinizi kesintiye uğraşır.</span><span class="sxs-lookup"><span data-stu-id="f147d-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="f147d-214">Web tabanlı Paket Yöneticisi arabirimini kullanırken genellikle bu davranışı görseniz de, *App\_veri* klasöründeki dosyaları ekler, kaldırırsanız veya değiştirirseniz aynı davranış oluşur.</span><span class="sxs-lookup"><span data-stu-id="f147d-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="f147d-215">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="f147d-215">**Workaround** </span></span>  
> <span data-ttu-id="f147d-216">Visual Studio 'da paketlerle çalışmak için, Web tabanlı Paket Yöneticisi yerine NuGet uzantısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="f147d-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="f147d-217">Daha fazla bilgi için bkz. [NuGet belgeleri](https://docs.microsoft.com/nuget/).</span><span class="sxs-lookup"><span data-stu-id="f147d-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="f147d-218">*App\_Data* klasöründeki diğer dosyalarla çalışıyorsanız, bu sorundan kaçınmak için dosyaları başka bir yerde tutmayı göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="f147d-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="f147d-219">Bu pratik değilse, *uygulamayı çevrimdışı. htm dosyası\_* el ile silin veya site yeniden çevrimiçi olana kadar bekleyin (varsayılan olarak 30 saniye sonra).</span><span class="sxs-lookup"><span data-stu-id="f147d-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="f147d-220">Sorun: Visual Studio IntelliSense ve proje şablonları yalnızca ASP.NET MVC sürüm 3 ' te kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="f147d-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="f147d-221">ASP.NET Web sayfalarının yüklenmesi, Visual Studio için IntelliSense ve ASP.NET Web sayfaları uygulamalarına yönelik proje şablonları gibi araçları da yüklemez.</span><span class="sxs-lookup"><span data-stu-id="f147d-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="f147d-222">**Geçici çözüm** Visual Studio 'da ASP.NET Web Pages uygulamaları için IntelliSense ve proje şablonları kullanmak üzere, Web Platformu Yükleyicisi veya [tek başına yükleyici](https://go.microsoft.com/fwlink/?LinkID=191797)aracılığıyla ASP.NET MVC 3 RC 'yi yükleme.</span><span class="sxs-lookup"><span data-stu-id="f147d-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="f147d-223">Sorun: bir ara sunucu aracılığıyla akışları veya diğer dış verileri okuma</span><span class="sxs-lookup"><span data-stu-id="f147d-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="f147d-224">Siteyi çalıştıran sunucu bir proxy sunucusunun arkasındaysa, sitenizin dışından gelen bilgileri okuyabilmeniz için *Web. config* dosyasındaki proxy bilgilerini yapılandırmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="f147d-225">Örneğin, `ReCaptcha` yardımcısını kullanıyorsanız, yardımcı, reCAPTCHA hizmeti ile iletişim kurar, ancak proxy sunucunuz tarafından engelleniyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="f147d-226">Benzer şekilde, ASP.NET Web sayfalarında kullanılan ve paket yöneticisi tarafından kullanılan akış gibi akışlar ara sunucu yapılandırması gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="f147d-227">Bir dış hizmetle çalışırken veya paket akışı ile çalışırken sorunlarla karşılaşırsanız, aşağıdaki öğeleri uygulamanızın kök *Web. config* dosyasına yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="f147d-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="f147d-228">Proxy sunucu yapılandırma hakkında daha fazla bilgi için, MSDN Web sitesindeki [&lt;proxy&gt; öğesi (ağ ayarları)](https://msdn.microsoft.com/library/sa91de1e.aspx) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f147d-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="f147d-229">Sorun: .NET Framework sürüm 4 ' ü kaldırmak, Razor sözdizimi ile ASP.NET Web sayfalarını devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="f147d-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="f147d-230">.NET Framework sürüm 4 ' ü kaldırıp yeniden yüklerseniz, Razor söz dizimi Web sayfaları devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="f147d-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="f147d-231">*. Cshtml* uzantılı sayfalar düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="f147d-232">ASP.NET Web sayfaları, bir derlemeyi makine kök *Web. config* dosyasına kaydeder ve .NET Framework kaldırıldığında bu dosya kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="f147d-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="f147d-233">.NET Framework yeniden yüklemek, yapılandırma dosyasının yeni bir sürümünü yüklüyor, ancak ASP.NET Web Pages derlemesinin başvurusunu eklemez.</span><span class="sxs-lookup"><span data-stu-id="f147d-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="f147d-234">**Geçici çözüm** .NET Framework yeniden yükledikten sonra, ASP.NET Web sayfalarını Razor söz dizimi yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f147d-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="f147d-235">Bu, genellikle aşağıdaki konumda olan makine kökündeki *Web. config* dosyasına aşağıdaki öğeyi ekler:</span><span class="sxs-lookup"><span data-stu-id="f147d-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="f147d-236">Sorun: Extensionless URL 'Leri IIS 7 veya IIS 7,5 üzerinde. cshtml/. vbhtml dosyalarını bulamıyor</span><span class="sxs-lookup"><span data-stu-id="f147d-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="f147d-237">IIS 7 veya IIS 7,5 ' de, aşağıdakine benzer bir URL 'ye sahip istekler *. cshtml* veya *. vbhtml* uzantısına sahip sayfaları bulamaz:</span><span class="sxs-lookup"><span data-stu-id="f147d-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="f147d-238">Bu sorun ortaya çıkar çünkü URL yeniden yazma özelliği IIS 7 veya IIS 7,5 için varsayılan olarak etkinleştirilmemiştir.</span><span class="sxs-lookup"><span data-stu-id="f147d-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="f147d-239">Likeliest senaryosu, IIS Express kullanarak yerel olarak test ederken sorunu görmemelidir, ancak Web sitenizi bir barındırma web sitesine dağıttığınızda bu sorunla karşılaşırsınız.</span><span class="sxs-lookup"><span data-stu-id="f147d-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="f147d-240">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="f147d-241">Sunucu bilgisayar üzerinde denetiminiz varsa, sunucu bilgisayarda, [belırlı ııs 7,0 veya ııs 7,5 işleyicilerinin, URL 'lerin noktayla bitmeyen istekleri işlemesini sağlayan bir güncelleştirmede](https://support.microsoft.com/kb/980368)açıklanan güncelleştirmeyi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="f147d-242">Sunucu bilgisayarı üzerinde denetiminiz yoksa (örneğin, bir barındırma web sitesine dağıtıyorsanız), aşağıdakileri Web sitesinin *Web. config* dosyasına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f147d-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="f147d-243">Sorun: SQL Server Compact yüklü olmayan bir bilgisayara uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="f147d-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="f147d-244">SQL Server Compact veritabanlarını içeren uygulamalar, SQL Server Compact yüklü olmayan bir bilgisayarda çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="f147d-245">Microsoft WebMatrix 1,0, bu ikili dosyaları sizin için otomatik olarak kopyalar ve uygun *Web. config* dosyası dönüşümlerini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="f147d-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="f147d-246">**Geçici çözüm** Bu dosyaları kopyalamanız ve *Web. config* dosyasının el ile değişiklikleri yapmanız gerekiyorsa, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="f147d-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="f147d-247">Veritabanı altyapısı derlemelerini hedef bilgisayardaki uygulamanın *bin* klasörüne (ve alt klasörlerine) kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="f147d-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="f147d-248">*C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*  Kopyala</span><span class="sxs-lookup"><span data-stu-id="f147d-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="f147d-249">*\Bin* 'e</span><span class="sxs-lookup"><span data-stu-id="f147d-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="f147d-250">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* dosyasını *\bin\x86* ' ya kopyalayın</span><span class="sxs-lookup"><span data-stu-id="f147d-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="f147d-251">*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \*  **'i** *\bin\amd64* dizinine kopyalayın</span><span class="sxs-lookup"><span data-stu-id="f147d-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="f147d-252">Web sitesinin kök klasöründe bir *Web. config* dosyası oluşturun veya açın.</span><span class="sxs-lookup"><span data-stu-id="f147d-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="f147d-253">(WebMatrix 1,0 ' de, **dosya türü seç** Iletişim kutusunda **Tümü** ' ne tıkladığınızda bu dosya türü kullanılabilir.)</span><span class="sxs-lookup"><span data-stu-id="f147d-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="f147d-254">Aşağıdaki öğeyi `<configuration>` öğesinin bir alt öğesi olarak ekleyin (`<system.web>` öğesinin içinde değil):</span><span class="sxs-lookup"><span data-stu-id="f147d-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="f147d-255">Sorun: "Database" ve "WebGrid" yardımcıları Visual Basic sürümünde Orta güvende çalışmıyor</span><span class="sxs-lookup"><span data-stu-id="f147d-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="f147d-256">Visual Basic kullanıyorsanız ( *. vbhtml* dosyaları oluşturma), uygulama orta güveni kullanmak üzere ayarlandıysa `Database` ve `WebGrid` yardımcıları çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="f147d-257">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-257">**Workaround**</span></span>  
> <span data-ttu-id="f147d-258">Visual Studio 2010 kullanıyorsanız, Service Pack 1 sürümünü yükleyerek bu sorunu çözebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="f147d-259">SP1 sürümünün son sürümü kullanılabilir olana kadar, Microsoft Indirme merkezi 'ndeki [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) sayfasından SP1 'in beta sürümünü indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="f147d-260">Bu pratik değilse veya Visual Studio 2010 kullanmıyorsanız, geçici olarak uygulamayı tam güven kullanacak şekilde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="f147d-261">Sorun: "ApplicationPart" kaynaklarına dışarıdan erişilebilir</span><span class="sxs-lookup"><span data-stu-id="f147d-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="f147d-262">Bir derleme `ApplicationPart` sınıfından türetilen nesneler içeriyorsa, bu derlemenin kaynakları `ResourceRouteHandler` sınıfı tarafından gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="f147d-263">Örneğin, aşağıdaki URL 'YI göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="f147d-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="f147d-264">Bu istek, *System. Web. Web sayfası. Administration. dll* derlemesindeki tüm kaynak dizelerini indirir.</span><span class="sxs-lookup"><span data-stu-id="f147d-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="f147d-265">Tüm katıştırılmış kaynaklar (statik içerik olarak sunulmayı amaçlananlar bile) indirilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="f147d-266">Katıştırılmış kaynaklar hassas bilgiler içeriyorsa bu, bir güvenlik riskini temsil edebilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="f147d-267">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="f147d-267">**Workaround** </span></span>  
> <span data-ttu-id="f147d-268">Bir **applicationpart** nesnesi oluşturursanız, bu **applicationpart** nesnesinin derlemesi ile ilişkili gömülü kaynakların hassas bilgiler içermediğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f147d-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="f147d-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="f147d-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="f147d-270">WebMatrix 'e yönelik yükleme sorunları hakkında daha fazla bilgi için bu belgede daha önce [WebMatrix yükleme sorunları](#Known_Issues_Installation) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f147d-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="f147d-271">Belgenin bu bölümünde, WebMatrix geliştirme ortamı için bilinen sorunlar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f147d-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="f147d-272">Sorun: Web. config dosyasındaki bir veritabanı bağlantı dizesinin Kullanıcı adı veya Paroladaki değişiklikler veritabanları çalışma alanına yansıtılmıyor</span><span class="sxs-lookup"><span data-stu-id="f147d-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="f147d-273">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="f147d-274">*Web. config* dosyasında, bağlantı dizesindeki veritabanı adını değiştirin (örneğin, "1" ekleyin).</span><span class="sxs-lookup"><span data-stu-id="f147d-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="f147d-275">*Web. config* dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f147d-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="f147d-276">**Veritabanları** ' na tıklayın ve yenileyin.</span><span class="sxs-lookup"><span data-stu-id="f147d-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="f147d-277">*Web. config* dosyasındaki bağlantı dizesindeki veritabanı adını özgün veritabanı adına geri değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f147d-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="f147d-278">*Web. config* dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f147d-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="f147d-279">**Veritabanları** ' na tıklayın ve yenileyin.</span><span class="sxs-lookup"><span data-stu-id="f147d-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="f147d-280">Sorun: WebMatrix tarafından oluşturulan klasörler silinemez</span><span class="sxs-lookup"><span data-stu-id="f147d-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="f147d-281">WebMatrix yükseltilmiş izinler kullanılarak çalışıyorsa (yani, Windows 'ta **yönetici olarak çalıştır** seçeneğini kullanarak WebMatrix 'i başlattığınızda), WebMatrix tarafından oluşturulan klasörler Windows Gezgini kullanılarak silinemez.</span><span class="sxs-lookup"><span data-stu-id="f147d-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="f147d-282">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-282">**Workaround**</span></span>  
> <span data-ttu-id="f147d-283">Yükseltilmiş izinleri kullanarak Windows Gezgini 'ni çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f147d-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="f147d-284">Aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="f147d-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="f147d-285">Windows 'ta **Başlat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="f147d-286">"Windows Gezgini" yazın ve **Windows Gezgini**için girişe sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="f147d-287">**Yönetici olarak çalıştır**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="f147d-288">Daha sonra klasörleri silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="f147d-289">Sorun: WebMatrix 1,0, yükseltme gerektiren belirli görevleri gerçekleştiremiyor</span><span class="sxs-lookup"><span data-stu-id="f147d-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="f147d-290">WebMatrix 1,0, aşağıdaki durumlarda ek bileşenler yükleme gibi yükseltme gerektiren belirli görevleri gerçekleştiremiyor:</span><span class="sxs-lookup"><span data-stu-id="f147d-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="f147d-291">Windows Vista veya Windows 7 ' de, yönetici ayrıcalıklarına sahip olmayan bir hesapla oturum açarsınız ve Kullanıcı hesabı denetimi (UAC) devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="f147d-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="f147d-292">Microsoft Windows XP veya Microsoft Windows Server 2003 kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f147d-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="f147d-293">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-293">**Workaround**</span></span>  
> <span data-ttu-id="f147d-294">WebMatrix 1,0 ' deki görevlerin çoğu, yönetici izni gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="f147d-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="f147d-295">Bu işlemler için, işlemi yönetici olarak gerçekleştirebilir veya aşağıdaki adımları izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f147d-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="f147d-296">Windows Vista veya Windows 7 ' de UAC 'yi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f147d-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="f147d-297">Windows XP 'de, kullanıcıyı Administrators güvenlik grubuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f147d-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="f147d-298">Sorun: "Web galerisinden site" devre dışı</span><span class="sxs-lookup"><span data-stu-id="f147d-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="f147d-299">Web Platformu Yükleyicisi 3,0 yüklü değilse, **Web galerisinden site** seçeneği devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="f147d-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="f147d-300">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-300">**Workaround**</span></span>  
> <span data-ttu-id="f147d-301">[3,0 Microsoft Web Platformu Yükleyicisi](https://go.microsoft.com/fwlink/?LinkID=194638)'yi yükler.</span><span class="sxs-lookup"><span data-stu-id="f147d-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="f147d-302">Sorun: Google Chrome bir çalıştır seçeneği olarak kullanılamıyor</span><span class="sxs-lookup"><span data-stu-id="f147d-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="f147d-303">Google Chrome, **giriş** sekmesinde **Çalıştır** altında bulunan tarayıcılar listesinde gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="f147d-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="f147d-304">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-304">**Workaround**</span></span>  
> <span data-ttu-id="f147d-305">Google Chrome 'un bazı sürümleri, Windows 'daki varsayılan programlar özelliği ile kendilerini doğru bir şekilde kaydetmez.</span><span class="sxs-lookup"><span data-stu-id="f147d-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="f147d-306">Geçici bir çözüm olarak, Google Chrome 'u başlatın, *Google Chrome ' ı Özelleştir ve denetle* menüsüne tıklayın, *Seçenekler*' e ve ardından *Google Chrome varsayılan tarayıcımı oluştur*' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="f147d-307">Sorun: "yabancı anahtar" iletişim kutusu birincil anahtar girmeye izin vermiyor</span><span class="sxs-lookup"><span data-stu-id="f147d-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="f147d-308">**Yabancı anahtar** iletişim kutusu birincil anahtar tablosundan birincil anahtar adını girmenize izin vermez.</span><span class="sxs-lookup"><span data-stu-id="f147d-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="f147d-309">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-309">**Workaround**</span></span>  
> <span data-ttu-id="f147d-310">Bu bilerek yapılır.</span><span class="sxs-lookup"><span data-stu-id="f147d-310">This is intentional.</span></span> <span data-ttu-id="f147d-311">Birincil anahtar tablosundan birincil anahtar adını girmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f147d-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="f147d-312">Sorun: IntelliSense Razor söz dizimi, C#veya Visual Basic için WebMatrix 'te kullanılamaz</span><span class="sxs-lookup"><span data-stu-id="f147d-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="f147d-313">IntelliSense, HTML ve CSS için WebMatrix 'te desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f147d-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="f147d-314">Ancak, diğer diller için kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="f147d-315">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="f147d-315">**Workaround** </span></span>  
> <span data-ttu-id="f147d-316">Yok.</span><span class="sxs-lookup"><span data-stu-id="f147d-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="f147d-317">Sorun: HTML ve CSS için IntelliSense, bağlamsal olarak uygun olmayan öğeler önerir</span><span class="sxs-lookup"><span data-stu-id="f147d-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="f147d-318">WebMatrix 'te biçimlendirme için IntelliSense, [css 2,1 şemasını](http://www.w3.org/TR/CSS2/)kullanarak [XHTML 1,0 GEÇIŞLI şema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) ve CSS kullanarak HTML 'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="f147d-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="f147d-319">IntelliSense bu belirli şemaları temel aldığı için, belirli Etiketler, öznitelikler veya özellikler geçerli sayfa veya stil tanımına uygun olmayan önerilebilir olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="f147d-320">HTML için Ayrıca, hatalı oluşturulmuş XHTML (örneğin, Etiketler kapatılmadığı zaman) olarak yorumlanabilecek içerikte beklenmedik önerilere yol açabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="f147d-321">Bu sorun, ekleme noktası tamamlanmamış bir etiketin içindeyse daha belirgin olabilir; Bu durumda, IntelliSense yeni açma etiketleri önerebilir veya diğer hatalı öneriler sunabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="f147d-322">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="f147d-322">**Workaround** </span></span>  
> <span data-ttu-id="f147d-323">HTML için iyi biçimlendirilmiş, tam bir XHTML sayfasında çalıştığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f147d-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="f147d-324">CSS için geçici çözüm yoktur.</span><span class="sxs-lookup"><span data-stu-id="f147d-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="f147d-325">Sorun: IntelliSense siz yazarken çağrılmıyor</span><span class="sxs-lookup"><span data-stu-id="f147d-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="f147d-326">Bazen, IntelliSense HTML olarak çağrılamaz veya düzenleyicide CSS girilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="f147d-327">Özellikle, ekleme noktası başka bir öğenin veya bir dosyanın sonunda doğrudan olduğunda bu durum oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="f147d-328">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="f147d-328">**Workaround** </span></span>  
> <span data-ttu-id="f147d-329">Ekleme noktasının etrafında boşluk olduğundan ve ekleme noktasının bir dosyanın sonunda olmadığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f147d-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="f147d-330">Ayrıca, Ctrl + Space tuşlarına basarak IntelliSense 'i el ile çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f147d-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="f147d-331">Sorun: IntelliSense devre dışı bırakmak için kullanılabilir bir kullanıcı arabirimi yok</span><span class="sxs-lookup"><span data-stu-id="f147d-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="f147d-332">WebMatrix 1,0, IntelliSense 'i devre dışı bırakmak için Kullanıcı arabirimi veya hareket sağlar.</span><span class="sxs-lookup"><span data-stu-id="f147d-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="f147d-333">**Geçici çözüm** </span><span class="sxs-lookup"><span data-stu-id="f147d-333">**Workaround** </span></span>  
> <span data-ttu-id="f147d-334">, IntelliSense 'i devre dışı bırakan bir anahtar içeren aşağıdaki komutu kullanarak WebMatrix 'i başlatın:</span><span class="sxs-lookup"><span data-stu-id="f147d-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="f147d-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="f147d-335">IIS Express</span></span>

<span data-ttu-id="f147d-336">IIS Express, aşağıdaki URL 'de bulunan kendi Benioku dosyasına sahiptir:</span><span class="sxs-lookup"><span data-stu-id="f147d-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="f147d-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp; CLCID = 0x409</span><span class="sxs-lookup"><span data-stu-id="f147d-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="f147d-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="f147d-338">SQL Server Compact</span></span>

<span data-ttu-id="f147d-339">SQL Server Compact, aşağıdaki URL 'de bulunan kendi Benioku dosyasına sahiptir:</span><span class="sxs-lookup"><span data-stu-id="f147d-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="f147d-340">WebMatrix 'in bir parçası olarak SQL Server Compact yükleme ile ilgili sorunlar hakkında bilgi için, bu belgenin önceki bölümlerinde bulunan [WebMatrix yükleme sorunları](#Known_Issues_Installation) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f147d-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a><span data-ttu-id="f147d-341">Uygulamaları yükleme</span><span class="sxs-lookup"><span data-stu-id="f147d-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="f147d-342">Sorun: kullanıcının Belgelerim klasörü bir ağ paylaşımında yeniden yönlendiriliyorsa, uygulamanın yüklenmesi uzun zaman alabilir</span><span class="sxs-lookup"><span data-stu-id="f147d-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="f147d-343">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-343">**Workaround**</span></span>  
> <span data-ttu-id="f147d-344">Yok.</span><span class="sxs-lookup"><span data-stu-id="f147d-344">None.</span></span> <span data-ttu-id="f147d-345">Uygulamanın yüklenmesi biraz zaman alabilir, ancak doğru şekilde yüklenir.</span><span class="sxs-lookup"><span data-stu-id="f147d-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a><span data-ttu-id="f147d-346">Uygulamaları yayımlama</span><span class="sxs-lookup"><span data-stu-id="f147d-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="f147d-347">Sorun: bir SQL Compact veritabanı yayımlanırken "gerekli izinler alınamıyor" hatası</span><span class="sxs-lookup"><span data-stu-id="f147d-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="f147d-348">WebMatrix, .NET Framework sürüm 3,5 çalıştıran bir sunucuya SQL Server Compact için destek ikililerini, orta düzeydeki bir yapılandırma ile tam olarak desteklemez.</span><span class="sxs-lookup"><span data-stu-id="f147d-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="f147d-349">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-349">**Workaround**</span></span>  
> <span data-ttu-id="f147d-350">Tercih edilen geçici çözüm, .NET Framework 4 ' ü sunucuya yüklemektir.</span><span class="sxs-lookup"><span data-stu-id="f147d-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="f147d-351">Alternatif olarak, şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="f147d-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="f147d-352">Aşağıdaki öğeleri *Web\_düz güven. config* dosyasındaki `SecurityClasses` bölümüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f147d-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="f147d-353">*Web\_düz güven. config* dosyasında aşağıdaki gerekli izinlerle yeni bir izin kümesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f147d-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="f147d-354">Aşağıdaki öğeleri *Web\_düz güven. config* dosyasına yerleştirerek SQL Server Compact izin kümesini uygulayın:</span><span class="sxs-lookup"><span data-stu-id="f147d-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="f147d-355">Sorun: Galeri ve PhpBB Web uygulamaları, yayımlamadan sonra bir "hizmet kullanılamıyor" hatası görüntüler</span><span class="sxs-lookup"><span data-stu-id="f147d-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="f147d-356">Bazı durumlarda, bir uygulamanın yayımlanması "hizmet kullanılamıyor" hatası oluşmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="f147d-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="f147d-357">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-357">**Workaround**</span></span>  
> <span data-ttu-id="f147d-358">WebMatrix 'te, **yayınlama ayarları** penceresinde sunucu adının sonuna bir ters eğik çizgi ekleyin (\) ve uygulamayı yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="f147d-359">Sorun: Bu web sitesi yerleşimi ve bağlantılar yayımlandıktan sonra kopuk</span><span class="sxs-lookup"><span data-stu-id="f147d-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="f147d-360">Bir Mooteksiz uygulamayı yayımladıktan sonra, uygulama düzgün çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="f147d-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="f147d-361">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-361">**Workaround**</span></span>  
> <span data-ttu-id="f147d-362">WebMatrix 'te, **yayınlama ayarları** penceresinde **site adı** alanının sonuna bir eğik çizgi (/) ekleyin ve uygulamayı yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="f147d-363">Sorun: nopCommerce yayımlama bir veritabanı hatasıyla başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="f147d-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="f147d-364">NopCommerce 'i yayımlama başarısız oluyor ve "NOP\_günlük tablosuna ekle" gibi bir veritabanı hatası oluştu.</span><span class="sxs-lookup"><span data-stu-id="f147d-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="f147d-365">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="f147d-366">WebMatrix 'te, nopCommerce 'i yerel olarak başlatmak için **Çalıştır** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="f147d-367">Yönetim sayfasında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f147d-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="f147d-368">**Sistem** menüsüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="f147d-369">**Günlük** seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="f147d-370">**Günlüğü Temizle** düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="f147d-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="f147d-371">NopCommerce 'i yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="f147d-372">Sorun: yayımlanmış bir siteyi karşıdan yüklerken SilverStripe CMS bir "HTTP 500 PHP FCGı hatası" görüntülüyor</span><span class="sxs-lookup"><span data-stu-id="f147d-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="f147d-373">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-373">**Workaround**</span></span>  
> <span data-ttu-id="f147d-374">**Yayımlanan siteyi karşıdan yükle**' ye tıkladıktan sonra, **Yayımlama önizlemesi**' nde `silverstripe-cache/manifest_main` atlayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="f147d-375">Bu dosya, önbelleğe alma amacıyla kullanılır ve her bilgisayara özeldir.</span><span class="sxs-lookup"><span data-stu-id="f147d-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="f147d-376">Sorun: yayımlanmış bir siteyi karşıdan yüklerken "'/' uygulamasında sunucu hatası" alt metin görüntülenir</span><span class="sxs-lookup"><span data-stu-id="f147d-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="f147d-377">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-377">**Workaround**</span></span>  
> <span data-ttu-id="f147d-378">Sitenin *Web. config* dosyasını açın ve veritabanı bağlantı DIZESINDEKI Kullanıcı kimliğini ve parolayı SQL Server yönetici kimlik bilgileri ("sa" kimlik bilgileri) ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f147d-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="f147d-379">Alternatif olarak, oturum açtığınız kullanıcı hesabına `db_owner` izinlerle izin vermek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f147d-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="f147d-380">Web platformu yükleyicisini kullanarak SQL Server Management Studio yükleme.</span><span class="sxs-lookup"><span data-stu-id="f147d-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="f147d-381">Yerel SQL Server Express örneğine bağlanın (varsayılan olarak, `.\SQLEXPRESS`).</span><span class="sxs-lookup"><span data-stu-id="f147d-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="f147d-382">&gt; [ *Localsubtextdatabase]* &gt; **güvenlik** &gt; **Kullanıcılar** &gt; *[localsubtextuser*] (varsayılan değer `subtextuser`], sağ tıklayın ve **Özellikler**' **e tıklayın.**</span><span class="sxs-lookup"><span data-stu-id="f147d-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="f147d-383">Rol üyeliği bölümünde **db\_Owner** ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f147d-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="f147d-384">Sorun: "hedef URL" alanı http://veya https://ön eki değilse, site yayımlamadan sonra çalışmayabilir</span><span class="sxs-lookup"><span data-stu-id="f147d-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="f147d-385">**Yayımlama ayarları** iletişim kutusunda, hedef URL `http://` veya `https://`ile başlamadıysanız, site dağıtımdan sonra çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="f147d-386">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-386">**Workaround**</span></span>  
> <span data-ttu-id="f147d-387">Bir siteyi yayımlamadan önce, **yayınlama ayarları** iletişim KUTUSUNDAKI hedef URL 'nin `http://` veya `https://`ile başlayacağını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="f147d-388">Sorun: bir MySQL veritabanının yayımlanması "veritabanı yayımlanamadı.</span><span class="sxs-lookup"><span data-stu-id="f147d-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="f147d-389">Uzak veritabanı betiği çalıştıramadığı takdirde bu durum oluşabilir. "</span><span class="sxs-lookup"><span data-stu-id="f147d-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="f147d-390">Hata çeşitli nedenlerden kaynaklanabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="f147d-391">Bu hatayı görebileceğiniz bir nedeni, veritabanı betiğinin tek tırnak karakteri (') içermesi ve hedef MySQL veritabanının varsayılan karakter kümesinin UTF-8 ' e olmaması olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="f147d-392">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-392">**Workaround**</span></span>  
> <span data-ttu-id="f147d-393">Uzak MySQL veritabanı için varsayılan karakter kümesini UTF-8 olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="f147d-394">Sorun: site yayımladıktan veya indirildikten sonra bazı bağlantılar DotNetNuke 'da görünür değil</span><span class="sxs-lookup"><span data-stu-id="f147d-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="f147d-395">Bir DotNetNuke sitesi yayımladığınızda veya indirdiğinizde, sitede yeni bağlantıların görünmesini sağlamak için Önbelleği temizlemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="f147d-396">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="f147d-397">"Konak" olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f147d-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="f147d-398">Konak menüsüne gidin ve **konak ayarları**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="f147d-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="f147d-399">Aşağı kaydırın ve **Gelişmiş ayarlar**altında **performans ayarları**' nı genişletin.</span><span class="sxs-lookup"><span data-stu-id="f147d-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="f147d-400">Sayfalar için **önbelleği temizle** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="f147d-401">Sayfanın en altına gidin ve uygulamayı yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f147d-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="f147d-402">Sorun: yayımlanmış bir siteyi indirdikten sonra Atomsıte içindeki bazı bağlantılar kopuk</span><span class="sxs-lookup"><span data-stu-id="f147d-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="f147d-403">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-403">**Workaround**</span></span>  
> <span data-ttu-id="f147d-404">*Service. config* dosyasında, *Users. config* dosyasında ve tüm *. xml* dosyalarında, URL dizesini (örneğin, `http://myhost.com/atomsite`) yerel bir dosyayla değiştirin (örneğin, `http://localhost:1239`).</span><span class="sxs-lookup"><span data-stu-id="f147d-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="f147d-405">Sorun: WordPress gibi MySQL tabanlı uygulamalar bir veritabanı hatasını yayımlayamaz ve bildiremez</span><span class="sxs-lookup"><span data-stu-id="f147d-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="f147d-406">WebMatrix, varsayılan olarak MySQL 'i UTF-8 karakter kümesiyle birlikte yüklüyor.</span><span class="sxs-lookup"><span data-stu-id="f147d-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="f147d-407">MySQL 'i kendinize yüklerseniz ve karakter kümesi UTF-8 değilse (örneğin, Latin1), veritabanları için yayımlama işlemi başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="f147d-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="f147d-408">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="f147d-409">MySQL için karakter kümesini UTF-8 olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f147d-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="f147d-410">(Ayrıntılar için bkz. MySQL web sitesinde [sunucu karakter kümesi ve harmanlama](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) .)</span><span class="sxs-lookup"><span data-stu-id="f147d-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="f147d-411">Uygulamayı yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f147d-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="f147d-412">Uygulamayı yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="f147d-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="f147d-413">Sorun: tarayıcı tabanlı kurulum özellikli uygulamalar için "yayımlanmış siteyi Indirme" başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="f147d-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="f147d-414">Bazı uygulamalar (örneğin, Kentico CMS), bir veritabanı oluşturma gibi yükleme sonrası kurulumu gerçekleştirmek için bunları tarayıcıda açmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f147d-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="f147d-415">Tarayıcı tabanlı kurulumu tamamlamadan bunun gibi bir uygulamayı yayımlarsanız, uzak bir sunucudan aynı siteyi indirmeyi denemek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f147d-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="f147d-416">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-416">**Workaround**</span></span>  
> <span data-ttu-id="f147d-417">Siteyi yayımlamadan önce tarayıcı tabanlı kurulumu sona erdirin.</span><span class="sxs-lookup"><span data-stu-id="f147d-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="f147d-418">Sorun: "yayımlanmış siteyi Indirme" DotNetNuke ve Kooboo CMS için bir veritabanı hatasıyla başarısız oluyor</span><span class="sxs-lookup"><span data-stu-id="f147d-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="f147d-419">Bir sunucudan bir uygulamayı indirmeye çalışırsanız ve **Yayımlama ayarları** iletişim kutusunda veritabanı bağlantı dizesinde yönetici kimlik bilgileriniz varsa, yayımlama günlüğünde şu hatayı görebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f147d-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="f147d-420">**Geçici çözüm**</span><span class="sxs-lookup"><span data-stu-id="f147d-420">**Workaround**</span></span>  
> <span data-ttu-id="f147d-421">Pratik ise, veritabanı için yönetici olmayan kimlik bilgilerini kullanarak siteyi yeniden yayımlayın (veya yayımladınız).</span><span class="sxs-lookup"><span data-stu-id="f147d-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="f147d-422">Daha Fazla Bilgi İçin</span><span class="sxs-lookup"><span data-stu-id="f147d-422">For More Information</span></span>

<span data-ttu-id="f147d-423">WebMatrix 1,0 hakkında daha fazla bilgi için aşağıdaki Web sitelerine bakın:</span><span class="sxs-lookup"><span data-stu-id="f147d-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="f147d-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="f147d-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="f147d-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f147d-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="f147d-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="f147d-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="f147d-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="f147d-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="f147d-428">Tüm hakları saklıdır.</span><span class="sxs-lookup"><span data-stu-id="f147d-428">All Rights Reserved.</span></span> <span data-ttu-id="f147d-429">[Kullanım koşulları](https://msdn.microsoft.cos/cc300389.aspx).</span><span class="sxs-lookup"><span data-stu-id="f147d-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
