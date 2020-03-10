---
uid: whitepapers/aspnet-and-iis6
title: IIS 6,0 ile ASP.NET 1,1 çalıştırma | Microsoft Docs
author: rick-anderson
description: Windows Server 2003 hem IIS 6,0 hem de ASP.NET 1,1 içerdiğinde, bu bileşenler varsayılan olarak devre dışıdır. Bu teknik incelemede IIS 6,0 a 'nın nasıl etkinleştirileceği açıklanmaktadır...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 5a5537bf-2aaa-49e7-839f-9e6522b829d8
msc.legacyurl: /whitepapers/aspnet-and-iis6
msc.type: content
ms.openlocfilehash: 2e7812f34481afe9a71927c0d9ba2a9abc9632e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523312"
---
# <a name="running-aspnet-11-with-iis-60"></a><span data-ttu-id="c15d2-104">IIS 6.0 ile Çalışan ASP.NET 1.1</span><span class="sxs-lookup"><span data-stu-id="c15d2-104">Running ASP.NET 1.1 with IIS 6.0</span></span>

> <span data-ttu-id="c15d2-105">Windows Server 2003 hem IIS 6,0 hem de ASP.NET 1,1 içerdiğinde, bu bileşenler varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="c15d2-105">While Windows Server 2003 includes both IIS 6.0 and ASP.NET 1.1, these components are disabled by default.</span></span> <span data-ttu-id="c15d2-106">Bu teknik incelemede IIS 6,0 ve ASP.NET 1,1 ' nin nasıl etkinleştirileceği açıklanır ve IIS ve ASP.NET ' den en iyi performansı elde etmek için çeşitli yapılandırma ayarları önerilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-106">This whitepaper describes how to enable IIS 6.0 and ASP.NET 1.1, and recommends several configuration settings to get the optimal performance from IIS and ASP.NET.</span></span>
> 
> <span data-ttu-id="c15d2-107">ASP.NET 1,1 ve IIS 6,0 için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-107">Applies to ASP.NET 1.1 and IIS 6.0.</span></span>

<span data-ttu-id="c15d2-108">ASP.NET 1,1, Internet Information Server (IIS) sürüm 6,0 ' nin en son sürümünü de içeren Windows Server 2003 ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-108">ASP.NET 1.1 ships with Windows Server 2003, which also includes the latest version of Internet Information Server (IIS) version 6.0.</span></span> <span data-ttu-id="c15d2-109">IIS 6,0 ve ASP.NET 1,1, sorunsuz ve ASP.NET Now varsayılan olarak yeni IIS 6,0 çalışan işlem modeliyle tümleştirilecek şekilde tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="c15d2-109">IIS 6.0 and ASP.NET 1.1 are designed to integrate seamlessly and ASP.NET now defaults to the new IIS 6.0 worker process model.</span></span>

## <a name="aspnet-11-is-not-installed-by-default"></a><span data-ttu-id="c15d2-110">ASP.NET 1,1 varsayılan olarak yüklü değildir</span><span class="sxs-lookup"><span data-stu-id="c15d2-110">ASP.NET 1.1 is not installed by default</span></span>

<span data-ttu-id="c15d2-111">Microsoft 'un sunucu işletim sistemlerinin önceki sürümlerinden farklı olarak Internet Information Server (IIS) varsayılan olarak etkinleştirilmemiştir; ASP.NET 1,1.</span><span class="sxs-lookup"><span data-stu-id="c15d2-111">Unlike previous versions of Microsoft's server operating systems, Internet Information Server (IIS) is not enabled by default; nor is ASP.NET 1.1.</span></span> <span data-ttu-id="c15d2-112">IIS 'yi etkinleştirmek için iki seçenek vardır:</span><span class="sxs-lookup"><span data-stu-id="c15d2-112">There are two options for enabling IIS:</span></span>

### <a name="enabling-iis-option-1---configure-your-server-wizard"></a><span data-ttu-id="c15d2-113">IIS 'yi etkinleştirme, seçenek #1-Sunucu Yapılandırma Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="c15d2-113">Enabling IIS, option #1 - Configure Your Server Wizard</span></span>

<span data-ttu-id="c15d2-114">Windows Server 2003, sunucunuzu istediğiniz modda doğru bir şekilde yapılandırmanıza yardımcı olmak için yeni bir ' Sunucu Yapılandırma Sihirbazı ' ' nı sevk eder.</span><span class="sxs-lookup"><span data-stu-id="c15d2-114">Windows Server 2003 ships a new 'Configure Your Server Wizard' to help you properly configure your server in the desired mode.</span></span>

<span data-ttu-id="c15d2-115">Sihirbazı başlatmak için, Sihirbazı çalıştırmak üzere yönetici olarak oturum açmış olmanız gerekir; şuraya gidin: Başlat | Programlar | Yönetim Araçları ve ' sunucunuzu yapılandırın ' seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c15d2-115">To start the wizard - note, to run the wizard you must be logged in as an administrator - go to: Start | Programs | Administrative Tools and select 'Configure Your Server'.</span></span>

<span data-ttu-id="c15d2-116">' İ seçtikten sonra, ' Sunucu Yapılandırma Sihirbazı ' açma ekranını görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="c15d2-116">Once selected you should see the 'Configure Your Server Wizard' opening screen:</span></span>

![](aspnet-and-iis6/_static/image1.jpg)

<span data-ttu-id="c15d2-117">' Ileri &gt;' seçeneğine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="c15d2-117">Click 'Next &gt;':</span></span>

![](aspnet-and-iis6/_static/image2.jpg)

<span data-ttu-id="c15d2-118">' Ileri &gt;' seçeneğine tıklayın</span><span class="sxs-lookup"><span data-stu-id="c15d2-118">Click 'Next &gt;'</span></span>

![](aspnet-and-iis6/_static/image3.jpg)

<span data-ttu-id="c15d2-119">Bu ekranda, yapılandırma seçenekleri olarak ' uygulama sunucusu (IIS, ASP.NET) seçeneğini belirlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-119">On this screen you will need to select 'Application server (IIS, ASP.NET) as the options to configure.</span></span>

<span data-ttu-id="c15d2-120">' Ileri &gt;' seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-120">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image4.jpg)

<span data-ttu-id="c15d2-121">Sunucuyu bir uygulama sunucusu olarak yapılandırmayı seçtikten sonra bu ekran, hangi ek yeteneklerin yüklenmesi gerektiğine ilişkin istem görüntülenecektir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-121">After selecting to configure the server as an Application Server, this screen will be displayed prompting what additional capabilities should be installed.</span></span> <span data-ttu-id="c15d2-122">Hiçbir seçenek varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-122">Neither option is selected by default.</span></span> <span data-ttu-id="c15d2-123">ASP.NET otomatik olarak etkinleştirmek için, ' ASP 'yi etkinleştir ' i seçmeniz gerekir. NET '.</span><span class="sxs-lookup"><span data-stu-id="c15d2-123">To enable ASP.NET automatically, you need to select 'Enable ASP.NET'.</span></span>

<span data-ttu-id="c15d2-124">' Ileri &gt;' seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-124">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image5.jpg)

<span data-ttu-id="c15d2-125">Bu ekran hangi seçeneklerin yükleneceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-125">This screen displays what options are to be installed.</span></span>

<span data-ttu-id="c15d2-126">' Ileri &gt;' seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-126">Click 'Next &gt;'.</span></span>

![](aspnet-and-iis6/_static/image6.jpg)

<span data-ttu-id="c15d2-127">Seçtiğiniz seçenekler yüklenirken bu ekran görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-127">You will see this screen while the options you selected are being installed.</span></span> <span data-ttu-id="c15d2-128">Hizmetler yüklendiği sürece diğer iletişim kutularının görünmesine bakmak normaldir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-128">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="c15d2-129">Ayrıca, Windows 2003 Server yükleme CD 'sinin konumu istenebilir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-129">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="c15d2-130">Tamamlandığında ' Ileri &gt;' seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-130">Click 'Next &gt;' when complete.</span></span>

![](aspnet-and-iis6/_static/image7.jpg)

<span data-ttu-id="c15d2-131">' Son ' düğmesine tıklayın. Windows Server 2003 artık IIS 6,0 ve ASP.NET 1,1 ' i destekleyecek şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c15d2-131">Click 'Finish' - the Windows Server 2003 is now configured to support IIS 6.0 and ASP.NET 1.1.</span></span>

### <a name="enabling-iis-option-2---manually-configuring-iis-and-aspnet"></a><span data-ttu-id="c15d2-132">IIS, seçenek #2 etkinleştirme-IIS ve ASP.NET El Ile yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c15d2-132">Enabling IIS, option #2 - Manually configuring IIS and ASP.NET</span></span>

<span data-ttu-id="c15d2-133">' Sunucu Yapılandırma Sihirbazı ' nı kullanmak istemiyorsanız, Denetim Masası 'ndan ' Program Ekle veya Kaldır ' öğesini kullanarak IIS 6,0 ve ASP.NET 1,1 ' ü isteğe bağlı olarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c15d2-133">If you do not wish to use the 'Configure Your Server Wizard' you can optionally install IIS 6.0 and ASP.NET 1.1 using 'Add or Remove Programs' from the Control Panel.</span></span>

<span data-ttu-id="c15d2-134">Önce denetim masasını açın:</span><span class="sxs-lookup"><span data-stu-id="c15d2-134">First open the Control Panel:</span></span>

![](aspnet-and-iis6/_static/image8.jpg)

<span data-ttu-id="c15d2-135">Sonra ' Windows Bileşenleri Sihirbazı ' ' nı açacak ' Windows Bileşenlerini Ekle/Kaldır ' seçeneğine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="c15d2-135">Next, click on 'Add/Remove Windows Components' which will open the 'Windows Components Wizard':</span></span>

![](aspnet-and-iis6/_static/image9.jpg)

<span data-ttu-id="c15d2-136">' Uygulama sunucusu ' nu vurgulayın ve denetleyin ve sonra ' Ayrıntılar? ' düğmesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="c15d2-136">Highlight and check 'Application Server' and then click the 'Details?'</span></span> <span data-ttu-id="c15d2-137">Bu</span><span class="sxs-lookup"><span data-stu-id="c15d2-137">button:</span></span>

![](aspnet-and-iis6/_static/image10.jpg)

<span data-ttu-id="c15d2-138">ASP.NET yüklemek için, ' ASP ' yi kontrol edin. NET '.</span><span class="sxs-lookup"><span data-stu-id="c15d2-138">To install ASP.NET, check 'ASP.NET'.</span></span>

<span data-ttu-id="c15d2-139">Windows Bileşen sihirbazına dönmek için ' Tamam 'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-139">Click 'OK' to return to the Windows Component Wizard.</span></span> <span data-ttu-id="c15d2-140">Yüklemeye başlamak için Windows Bileşen Sihirbazı 'nda ' Ileri &gt;' seçeneğine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="c15d2-140">Click 'Next &gt;' from the Windows Component Wizard to begin installing:</span></span>

![](aspnet-and-iis6/_static/image11.jpg)

<span data-ttu-id="c15d2-141">Hizmetler yüklendiği sürece diğer iletişim kutularının görünmesine bakmak normaldir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-141">It is normal to see other dialog boxes appear as services are being installed.</span></span> <span data-ttu-id="c15d2-142">Ayrıca, Windows 2003 Server yükleme CD 'sinin konumu istenebilir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-142">You may additionally be prompted for the location of the Windows 2003 Server installation CD.</span></span>

<span data-ttu-id="c15d2-143">Yükleme tamamlandığında, Windows Bileşen Sihirbazı 'nın son ekranını görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="c15d2-143">When installation is complete you will see the last screen of the Windows Component Wizard:</span></span>

![](aspnet-and-iis6/_static/image12.jpg)

<span data-ttu-id="c15d2-144">IIS 6,0 ve ASP.NET 1,1 artık yapılandırılmıştır ve kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-144">IIS 6.0 and ASP.NET 1.1 are now configured and available.</span></span>

## <a name="recommended-settings"></a><span data-ttu-id="c15d2-145">Önerilen ayarlar</span><span class="sxs-lookup"><span data-stu-id="c15d2-145">Recommended Settings</span></span>

<span data-ttu-id="c15d2-146">IIS 6,0 ile ASP.NET 1,1 çalıştırılırken, ASP.NET adresinden en iyi performansı elde etmek için önerilen birkaç yapılandırma ayarı vardır:</span><span class="sxs-lookup"><span data-stu-id="c15d2-146">When running ASP.NET 1.1 with IIS 6.0 there are several configuration settings that are recommended to get the optimal performance from ASP.NET:</span></span>

- <span data-ttu-id="c15d2-147">Çalışan işlem belleği sınırlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c15d2-147">Configuring worker process memory limits</span></span>
- <span data-ttu-id="c15d2-148">Çalışan işlemi geri dönüşümünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c15d2-148">Configuring worker process recycling</span></span>

### <a name="configuring-worker-process-memory-limits"></a><span data-ttu-id="c15d2-149">Çalışan işlem belleği sınırlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c15d2-149">Configuring worker process memory limits</span></span>

<span data-ttu-id="c15d2-150">Varsayılan olarak IIS 6,0, IIS 'nin kullanmasına izin verilen bellek miktarı için bir sınır yapmaz.</span><span class="sxs-lookup"><span data-stu-id="c15d2-150">By default IIS 6.0 does not set a limit on the amount of memory that IIS is allowed to use.</span></span> <span data-ttu-id="c15d2-151">ASP.net. NET ' in önbellek özelliği bir bellek sınırlaması kullanır, bu sayede önbelleğin kullanılmayan öğeleri bellekten önceden kaldırabilmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c15d2-151">ASP.NET's Cache feature relies on a limitation of memory so the Cache can proactively remove unused items from memory.</span></span>

<span data-ttu-id="c15d2-152">IIS 6,0 'nin bellek geri dönüştürme özelliğini yapılandırmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-152">It is recommended that you configure the memory recycling feature of IIS 6.0.</span></span> <span data-ttu-id="c15d2-153">Bu açık Internet Information Services yöneticisini yapılandırmak için (Başlat | Programlar | Yönetim Araçları | Internet Information Services).</span><span class="sxs-lookup"><span data-stu-id="c15d2-153">To configure this open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="c15d2-154">' İ açtıktan sonra ' uygulama havuzları ' klasörünü genişletin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-154">Once open, expand the 'Application Pools' folder:</span></span>

<span data-ttu-id="c15d2-155">Her uygulama havuzu için:</span><span class="sxs-lookup"><span data-stu-id="c15d2-155">For each application pool:</span></span>

![](aspnet-and-iis6/_static/image13.jpg)

1. <span data-ttu-id="c15d2-156">Uygulama havuzuna sağ tıklayın, örn. ' DefaultAppPool ' ve ' Özellikler ' öğesini seçin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-156">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image14.jpg)

2. <span data-ttu-id="c15d2-157">Daha sonra, ' en fazla kullanılan bellek ' i (megabayt cinsinden) tıklatarak belleği geri dönüştürmeyi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c15d2-157">Next, enable Memory recycling by clicking on either 'Maximum used memory (in megabytes):'.</span></span> <span data-ttu-id="c15d2-158">Değer, sunucudaki fiziksel (sanal değil) bellek miktarından daha fazla olmamalıdır; Örneğin, 512 MB fiziksel belleği olan bir sunucu için, yaklaşık olarak %60, fiziksel belleğin% ' i 310 seçin.</span><span class="sxs-lookup"><span data-stu-id="c15d2-158">The value should not be more than the amount of physical (not virtual) memory on the server, a good approximation is 60% of the physical memory, i.e. for a server with 512MB of physical memory select 310.</span></span> <span data-ttu-id="c15d2-159">2 GB 'LIK bir adres alanı kullanırken en fazla 800MB 'yi aşmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c15d2-159">It is also recommended that the maximum not exceed 800MB when using a 2GB address space.</span></span> <span data-ttu-id="c15d2-160">Sunucunun bellek adres alanı 3GB ise, çalışan işlem için en fazla bellek sınırı 1, 800MB olarak yüksek olabilir:</span><span class="sxs-lookup"><span data-stu-id="c15d2-160">If the memory address space of the server is 3GB, the maximum memory limit for the worker process can be as high as 1,800MB:</span></span>

![](aspnet-and-iis6/_static/image15.jpg)

<span data-ttu-id="c15d2-161">Özellikler iletişim kutusundan çıkmak için ' Uygula ' ve ' Tamam ' seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-161">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="c15d2-162">Bunu, kullanılabilir tüm uygulama havuzları için tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-162">Repeat this for all available application pools.</span></span>

### <a name="configuring-worker-recycling"></a><span data-ttu-id="c15d2-163">Çalışan geri dönüşümünü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c15d2-163">Configuring worker recycling</span></span>

<span data-ttu-id="c15d2-164">Varsayılan olarak IIS 6,0, çalışan işlemini 29 saatte bir geri dönüştürmek üzere yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c15d2-164">By default IIS 6.0 is configured to recycle its worker process every 29 hours.</span></span> <span data-ttu-id="c15d2-165">Bu, ASP.NET çalıştıran bir uygulama için biraz ısrarlı ve otomatik çalışan işlem geri dönüştürme işleminin devre dışı bırakılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-165">This is a bit aggressive for an application running ASP.NET and it is recommended that automatic worker process recycling is disabled.</span></span>

<span data-ttu-id="c15d2-166">Otomatik çalışan işlemi geri dönüşümünü devre dışı bırakmak için önce Internet Information Services Manager 'ı açın (Başlat | Programlar | Yönetim Araçları | Internet Information Services).</span><span class="sxs-lookup"><span data-stu-id="c15d2-166">To disable automatic worker process recycling, first open Internet Information Services Manager (Start | Programs | Administrative Tools | Internet Information Services).</span></span> <span data-ttu-id="c15d2-167">' İ açtıktan sonra ' uygulama havuzları ' klasörünü genişletin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-167">Once open, expand the 'Application Pools' folder:</span></span>

![](aspnet-and-iis6/_static/image16.jpg)

<span data-ttu-id="c15d2-168">Her uygulama havuzu için:</span><span class="sxs-lookup"><span data-stu-id="c15d2-168">For each application pool:</span></span>

1. <span data-ttu-id="c15d2-169">Uygulama havuzuna sağ tıklayın, örn. ' DefaultAppPool ' ve ' Özellikler ' öğesini seçin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-169">Right-click on the application pool, e.g. 'DefaultAppPool', and select 'Properties':</span></span>

![](aspnet-and-iis6/_static/image17.jpg)

2. <span data-ttu-id="c15d2-170">' Çalışan işlemini geri kazan (dakika): ' işaretini kaldırın:</span><span class="sxs-lookup"><span data-stu-id="c15d2-170">Uncheck 'Recycle worker process (in minutes):':</span></span>

![](aspnet-and-iis6/_static/image18.jpg)

<span data-ttu-id="c15d2-171">Özellikler iletişim kutusundan çıkmak için ' Uygula ' ve ' Tamam ' seçeneğine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-171">Click 'Apply' and the 'OK' to exit the properties dialog.</span></span> <span data-ttu-id="c15d2-172">Bunu, kullanılabilir tüm uygulama havuzları için tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-172">Repeat this for all available application pools.</span></span>

## <a name="granting-write-access-to-the-file-system"></a><span data-ttu-id="c15d2-173">Dosya sistemine yazma erişimi verme</span><span class="sxs-lookup"><span data-stu-id="c15d2-173">Granting write access to the file system</span></span>

<span data-ttu-id="c15d2-174">Uygulamanız dosya sistemine yazma erişimi gerektiriyorsa ve NTFS kullanıyorsanız, ASP.NET erişimi sağlamak için klasör veya dosya üzerinde bir Access Control listesini (ACL) değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-174">If your application requires write access to the file system and you are using NTFS you will need to modify an Access Control List (ACL) on the folder or file to grant ASP.NET access to.</span></span>

<span data-ttu-id="c15d2-175">Örneğin, c:\ınetpub\wwwroot ilk kez açık gezgin 'e ASP.NET yazma erişimi vermek ve dizine gitmek için:</span><span class="sxs-lookup"><span data-stu-id="c15d2-175">For example, to grant ASP.NET write access to the c:\inetpub\wwwroot first open explorer and navigate to the directory:</span></span>

![](aspnet-and-iis6/_static/image19.jpg)

<span data-ttu-id="c15d2-176">Ardından, dizine sağ tıklayıp, örneğin ' Wwwroot ' ve Özellikler ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c15d2-176">Next, right-click on the directory, e.g. 'wwwroot' and select properties.</span></span> <span data-ttu-id="c15d2-177">Özellikler iletişim kutusu açıldıktan sonra ' Güvenlik ' sekmesini seçin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-177">After the properties dialog opens, select the 'Security' tab:</span></span>

![](aspnet-and-iis6/_static/image20.jpg)

<span data-ttu-id="c15d2-178">C:\Inetpub\Wwwroot\ Dizin, ' IIS\_WPG ' özel IIS 6,0 grubunun zaten okuma &amp; yürütme, klasör Içeriğini listeleme ve okuma izinleri vermiş olduğu özel bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-178">The c:\inetpub\wwwroot\ directory is a special directory in that the special IIS 6.0 group 'IIS\_WPG' is already granted Read &amp; Execute, List Folder Contents, and Read permissions.</span></span> <span data-ttu-id="c15d2-179">Bununla birlikte, yazma izni vermek için, yazma için Izin ver onay kutusuna tıklamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c15d2-179">However, to grant Write permission, you need to click the Allow checkbox for Write:</span></span>

![](aspnet-and-iis6/_static/image21.jpg)

<span data-ttu-id="c15d2-180">IIS 6,0 artık bu klasörde yazma iznine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-180">IIS 6.0 now has write permission on this folder.</span></span> <span data-ttu-id="c15d2-181">Diğer klasörlerde yazma izinleri vermek için, bu adımları izleyin, zaten yoksa IIS\_WPG grubunu eklemeniz gerekebileceğini göz önünde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c15d2-181">To grant write permissions on other folders, follow these steps - note, you may need to add the IIS\_WPG group if it does not already exist.</span></span>

> [!CAUTION]
> <span data-ttu-id="c15d2-182">IIS\_WPG 'ye yazma izni verilmesi, tüm ASP.NET uygulamalarının bu dizine yazmasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-182">Granting write permission to IIS\_WPG will allow any ASP.NET application to write to this directory.</span></span>

## <a name="supporting-integrated-authentication-with-sql-server"></a><span data-ttu-id="c15d2-183">SQL Server ile tümleşik kimlik doğrulamayı destekleme</span><span class="sxs-lookup"><span data-stu-id="c15d2-183">Supporting integrated authentication with SQL Server</span></span>

<span data-ttu-id="c15d2-184">Tümleşik kimlik doğrulaması, SQL Server SQL Server oturum açma hesaplarını doğrulamak için Windows NT kimlik doğrulamasının yararlanmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="c15d2-184">Integrated authentication allows for SQL Server to leverage Windows NT authentication to validate SQL Server logon accounts.</span></span> <span data-ttu-id="c15d2-185">Bu, kullanıcının standart SQL Server oturum açma işlemini atlamasına izin verir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-185">This allows the user to bypass the standard SQL Server logon process.</span></span> <span data-ttu-id="c15d2-186">Bu yaklaşımda, SQL Server Windows NT ağ güvenlik işlemindeki Kullanıcı ve parola bilgilerini elde ettiğinden, bir ağ kullanıcısı ayrı bir oturum açma kimliği veya parola sağlamadan SQL Server veritabanına erişebilir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-186">With this approach, a network user can access a SQL Server database without supplying a separate logon identification or password because SQL Server obtains the user and password information from the Windows NT network security process.</span></span>

<span data-ttu-id="c15d2-187">Uygulamanız için bağlantı dizeniz içinde hiçbir kimlik bilgisi depolanmadığından, ASP.NET uygulamaları için tümleşik kimlik doğrulaması seçme iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-187">Choosing integrated authentication for ASP.NET applications is a good choice because no credentials are ever stored within your connection string for your application.</span></span> <span data-ttu-id="c15d2-188">Bunun yerine, SQL 'e bağlanmak için kullanılan bağlantı dizesi aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="c15d2-188">Rather the connection string used to connect to SQL will look as follows:</span></span>

`"server=localhost; database=Northwind;Trusted_Connection=true"`

<span data-ttu-id="c15d2-189">Bu bağlantı dizesi, SQL Server SQL Server erişmeye çalışan uygulamanın Windows kimlik bilgilerini kullanmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="c15d2-189">This connection string tells SQL Server to use the Windows credentials of the application attempting to access SQL Server.</span></span> <span data-ttu-id="c15d2-190">ASP.NET/IIS 6 durumunda bu, IIS\_WPG grubunda bir hesap olabilir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-190">In the case of ASP.NET/IIS 6 this would be an account in the IIS\_WPG group.</span></span>

<span data-ttu-id="c15d2-191">SQL Server ve ASP.NET arasında tümleşik kimlik doğrulamasını etkinleştirmek için öncelikle SQL Server tümleşik kimlik doğrulaması veya karma mod kimlik doğrulaması için yapılandırılmış olduğundan emin olmanız gerekir. bunu öğrenmek için</span><span class="sxs-lookup"><span data-stu-id="c15d2-191">To enable integrated authentication between SQL Server and ASP.NET, you will need to first ensure that SQL Server is configured for either Integrated authentication or Mixed-Mode authentication - check with your DBA to determine this.</span></span> <span data-ttu-id="c15d2-192">SQL Server bu iki moddan birinde ise, tümleşik kimlik doğrulaması kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c15d2-192">If SQL Server is in one of these two modes, you can use integrated authentication.</span></span>

<span data-ttu-id="c15d2-193">SQL Server Enterprise Yöneticisi 'Ni açın (Başlat | Programlar | Microsoft SQL Server | Enterprise Manager), uygun sunucuyu seçin ve Güvenlik klasörünü genişletin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-193">Open SQL Server Enterprise Manager (Start | Programs | Microsoft SQL Server | Enterprise Manager), select the appropriate server, and expand the Security folder:</span></span>

![](aspnet-and-iis6/_static/image22.jpg)

<span data-ttu-id="c15d2-194">' BUıLT\ııS\_WPG ' grubu listelenmiyorsa, oturum açma bilgileri ' ne sağ tıklayın ve ' yeni Login' ' ı seçin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-194">If 'BUILTINT\IIS\_WPG' group is not listed, right-click on Logins and select 'New Login':</span></span>

![](aspnet-and-iis6/_static/image23.jpg)

<span data-ttu-id="c15d2-195">' Name: ' metin kutusunda ' [sunucu/etki alanı adı] \ııS\_WPG ' girin veya Windows NT Kullanıcı/Grup seçicisini açmak için üç nokta düğmesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="c15d2-195">In the 'Name:' textbox either enter '[Server/Domain Name]\IIS\_WPG' or click on the ellipses button to open the Windows NT user/group picker:</span></span>

![](aspnet-and-iis6/_static/image24.jpg)

<span data-ttu-id="c15d2-196">Geçerli makinenin IIS\_WPG grubunu seçin ve seçiciyi kapatmak için ' Ekle ' ve Tamam ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-196">Select the current machine's IIS\_WPG group and click 'Add' and OK to close the picker.</span></span>

<span data-ttu-id="c15d2-197">Daha sonra, varsayılan veritabanını ve veritabanına erişmek için izinleri de ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-197">You then need to also set the default database and the permissions to access the database.</span></span> <span data-ttu-id="c15d2-198">Varsayılan Veritabanı Seç ' i açılan listeden seçin. Örneğin, Northwind 'nin altında:</span><span class="sxs-lookup"><span data-stu-id="c15d2-198">To set the default database choose from the drop down list, e.g. below Northwind is selected:</span></span>

![](aspnet-and-iis6/_static/image25.jpg)

<span data-ttu-id="c15d2-199">Ardından, veritabanı erişimi sekmesine tıklayın:</span><span class="sxs-lookup"><span data-stu-id="c15d2-199">Next, click on the Database Access tab:</span></span>

![](aspnet-and-iis6/_static/image26.jpg)

<span data-ttu-id="c15d2-200">Erişimine izin vermek istediğiniz her veritabanı için Izin ver onay kutusuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-200">Click on the Permit checkbox for every database that you wish to allow access to.</span></span> <span data-ttu-id="c15d2-201">Ayrıca, veritabanı rolleri ' ni seçmeniz gerekir. veritabanı\_sahibi, oturum açma izninizin seçili veritabanını yönetmek ve kullanmak için gereken tüm izinlere sahip olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="c15d2-201">You will also need to select database roles, checking db\_owner will ensure your login has all necessary permissions to manage and use the selected database.</span></span>

<span data-ttu-id="c15d2-202">Özellik iletişim kutusundan çıkmak için Tamam ' ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c15d2-202">Click OK to exit the property dialog.</span></span> <span data-ttu-id="c15d2-203">ASP.NET uygulamanız artık tümleşik SQL Server kimlik doğrulamasını destekleyecek şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="c15d2-203">Your ASP.NET application is now configured to support integrated SQL Server authentication.</span></span>

## <a name="dont-run-aspnet-10-in-iis-60-native-mode"></a><span data-ttu-id="c15d2-204">IIS 6,0 Native modda ASP.NET 1,0 çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c15d2-204">Don't run ASP.NET 1.0 in IIS 6.0 native mode</span></span>

<span data-ttu-id="c15d2-205">IIS 6,0 üzerinde ASP.NET 1,0 yalnızca IIS 5 uyumluluk modunda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="c15d2-205">ASP.NET 1.0 on IIS 6.0 is only supported in IIS 5 compatibility mode.</span></span>

<span data-ttu-id="c15d2-206">ASP.NET 1,0 'i IIS 5,0 uyumluluk modunda çalışacak şekilde yapılandırmak için İnternet Hizmetleri Yöneticisi açın ve Web siteleri ' ne sağ tıklayıp Özellikler ' i seçin:</span><span class="sxs-lookup"><span data-stu-id="c15d2-206">To configure ASP.NET 1.0 to run in IIS 5.0 compatibility mode, open Internet Services Manager and right click Web Sites and select properties:</span></span>

![](aspnet-and-iis6/_static/image27.jpg)

<span data-ttu-id="c15d2-207">Hizmet sekmesine geçip emin misiniz? WWW hizmetini IIS 5,0 yalıtım modunda çalıştırın mi?:</span><span class="sxs-lookup"><span data-stu-id="c15d2-207">Switch to the Service Tab and check ?Run WWW Service in IIS 5.0 Isolation Mode?:</span></span>

![](aspnet-and-iis6/_static/image28.jpg)
