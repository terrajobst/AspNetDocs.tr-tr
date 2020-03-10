---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET IIS dizinlerine erişimi reddedildi | Microsoft Docs
author: rick-anderson
description: Bu teknik incelemede, ASP.NET uygulamanıza yönelik bir istek, "DirectoryName dizinine erişim engellendi" hatasını döndürürse ne yapmanız gerektiğini açıklar. Başarısız oldu...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638504"
---
# <a name="aspnet-denied-access-to-iis-directories"></a><span data-ttu-id="9458c-104">ASP.NET IIS Dizinlerine Erişim Reddedildi</span><span class="sxs-lookup"><span data-stu-id="9458c-104">ASP.NET Denied Access to IIS Directories</span></span>

> <span data-ttu-id="9458c-105">Bu teknik incelemede, ASP.NET uygulamanıza yönelik bir istek, " *DirectoryName* dizinine erişim engellendi" hatasını döndürürse ne yapmanız gerektiğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="9458c-105">This whitepaper describes what you must do if a request to your ASP.NET application returns the error, "Denied Access to *DirectoryName* directory.</span></span> <span data-ttu-id="9458c-106">Dizin değişikliklerini izleme işlemi başlatılamadı. "</span><span class="sxs-lookup"><span data-stu-id="9458c-106">Failed to start monitoring directory changes."</span></span>
> 
> <span data-ttu-id="9458c-107">ASP.NET 1,0 ve ASP.NET 1,1 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="9458c-107">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="9458c-108">ASP.NET v1 RTM artık yerel bir makinede "ASPNET" hesabı olarak kaydedilmiş daha az ayrıcalıklı bir Windows hesabı kullanarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="9458c-108">ASP.NET V1 RTM now runs using a less privileged windows account - registered as the "ASPNET" account on a local machine.</span></span>

<span data-ttu-id="9458c-109">Bazı kilitli sistemlerde, bu hesap varsayılan olarak bir Web sitesinin içerik dizinlerine, uygulama kök dizinine veya Web sitesi kök dizinine okuma güvenlik erişimine sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="9458c-109">On some locked down systems, this account may not by default have read security access to a website's content directories, the application root directory, or the web site root directory.</span></span> <span data-ttu-id="9458c-110">Bu durumda, belirli bir Web uygulamasından sayfa istenirken aşağıdaki hatayı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="9458c-110">In this case you will receive the following error when requesting pages from a given web application:</span></span>

![](denied-access-to-iis-directories/_static/image1.jpg)

<span data-ttu-id="9458c-111">Bu hatayı düzeltemedi, uygun dizinlerde güvenlik izinlerini değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9458c-111">To fix this you will need to change the security permissions on the appropriate directories.</span></span>

<span data-ttu-id="9458c-112">Özellikle, ASP.NET Web sitesi köküne yönelik ASPNET hesabı için okuma, yürütme ve listeleme erişimi gerektirir (örneğin, c:\ınetpub\wwwroot veya IIS 'de yapılandırdığınız alternatif site dizini), içerik dizini ve uygulama kök dizini yapılandırma dosyası değişikliklerini izlemek için.</span><span class="sxs-lookup"><span data-stu-id="9458c-112">Specifically, ASP.NET requires read, execute, and list access for the ASPNET account for the web site root (for example: c:\inetpub\wwwroot or any alternative site directory you may have configured in IIS), the content directory and the application root directory in order to monitor for configuration file changes.</span></span> <span data-ttu-id="9458c-113">Uygulama kökü, IIS Yönetim Aracı 'nda (inetmgr) uygulama sanal diziniyle ilişkili klasör yoluna karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="9458c-113">The application root corresponds to the folder path associated with the application virtual directory in the IIS Administration tool (inetmgr).</span></span>

<span data-ttu-id="9458c-114">Örneğin, Wwwroot klasörü altında aşağıdaki uygulama hiyerarşisini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="9458c-114">For example, consider the following application hierarchy under the wwwroot folder.</span></span>

`C:\inetpub\wwwroot\myapp\default.aspx`

<span data-ttu-id="9458c-115">Bu örnekte, ASPNET hesabının hem MyApp hem de Wwwroot dizinindeki içerik için yukarıda tanımlanan okuma izinlerine ihtiyacı vardır.</span><span class="sxs-lookup"><span data-stu-id="9458c-115">For this example, the ASPNET account needs the read permissions defined above for content in both the myapp and the wwwroot directory.</span></span> <span data-ttu-id="9458c-116">Kök klasördeki tek bir devralınan ACL, iç içe yerleştirilmiş olmaları durumunda her iki dizin için de isteğe bağlı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9458c-116">A single inherited ACL on the root folder can also be optionally used for both directories if they're nested.</span></span>

<span data-ttu-id="9458c-117">Bir dizine izinler eklemek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="9458c-117">To add permissions to a directory, perform the following steps:</span></span>

- <span data-ttu-id="9458c-118">Windows Gezgini 'ni kullanarak dizine gidin</span><span class="sxs-lookup"><span data-stu-id="9458c-118">Using the Windows explorer, navigate to the directory</span></span>
- <span data-ttu-id="9458c-119">Dizin klasörüne sağ tıklayın ve "Özellikler" i seçin</span><span class="sxs-lookup"><span data-stu-id="9458c-119">Right click on the directory folder and choose "Properties"</span></span>
- <span data-ttu-id="9458c-120">Özellik iletişim kutusunda "güvenlik" sekmesine gidin</span><span class="sxs-lookup"><span data-stu-id="9458c-120">Navigate to the "Security" tab on the property dialog</span></span>
- <span data-ttu-id="9458c-121">"Ekle" düğmesine tıklayın ve ardından ASPNET hesap adının ardından makine adını girin.</span><span class="sxs-lookup"><span data-stu-id="9458c-121">Click the "Add" button and enter the machine name followed by the ASPNET account name.</span></span> <span data-ttu-id="9458c-122">Örneğin, "WebDev" adlı bir makinede, Web Dev\aspnet yazın ve "Tamam" a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9458c-122">For example, on a machine named "webdev", you would enter webdev\ASPNET and hit "OK".</span></span>
- <span data-ttu-id="9458c-123">ASPNET hesabının "okuma &amp; yürütme", "klasör Içeriğini listeleme" ve "okuma" onay kutularının işaretli olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="9458c-123">Ensure that the ASPNET account has the "Read &amp; Execute", "List Folder Contents", and "Read" checkboxes checked.</span></span>
- <span data-ttu-id="9458c-124">İletişim kutusunu kapatmak ve değişiklikleri kaydetmek için Tamam 'a basın.</span><span class="sxs-lookup"><span data-stu-id="9458c-124">Hit OK to dismiss the dialog and save the changes.</span></span>

![](denied-access-to-iis-directories/_static/image2.jpg)

<span data-ttu-id="9458c-125">İsterseniz, bu değişiklikler, Windows ile birlikte gelen betikler veya "cacls. exe" Aracı kullanılarak otomatikleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9458c-125">If desired, these changes can be automated using scripts or the "cacls.exe" tool that ships with Windows.</span></span> <span data-ttu-id="9458c-126">ASPNET hesabı hakkında daha fazla bilgi için lütfen [SSS belgesine](https://go.microsoft.com/fwlink/?LinkId=5828)bakın.</span><span class="sxs-lookup"><span data-stu-id="9458c-126">For more information on the ASPNET account, please see the [FAQ document](https://go.microsoft.com/fwlink/?LinkId=5828).</span></span>

<span data-ttu-id="9458c-127">Belirli bir Web uygulamasının belirli bir klasör veya dosyaya yazma veya değiştirme izinleri varsa, bu, aynı yordam ve "yazma" ve/veya "Değiştir" onay kutularını işaretleyerek verilebilir.</span><span class="sxs-lookup"><span data-stu-id="9458c-127">If a given web application relies on having write or modify permissions to a particular folder or file, this can be granted by following the same procedure and checking the "Write" and/or "Modify" checkboxes.</span></span>

<span data-ttu-id="9458c-128">Herkese veya kullanıcılar grubuna bu dizinlere okuma erişimi sağlayan makinelerde (varsayılan yapılandırma), hiçbir sorunla karşılaşılmaz ve yukarıdaki adımlar gerekli olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="9458c-128">On machines that allow Everyone or the Users group read access to these directories (which is the default configuration), no issues will be encountered and the above steps will not be required.</span></span>
