---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 'SQL Server Visual Studio veya Visual Web Developer kullanarak Compact ile ASP.NET Web uygulaması dağıtma: Yalnızca kod bir güncelleştirmesi - 12 8 dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisinde, nasıl dağıtılacağı gösterilir (bir ASP.NET Yayımlama) Visual Stu'ı kullanarak bir SQL Server Compact veritabanı içeren web uygulaması projesi...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: cc994f989734153592ce78af5f4be57953b24458
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57072444"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="d2fde-103">SQL Server Visual Studio veya Visual Web Developer kullanarak Compact ile ASP.NET Web uygulaması dağıtma: Yalnızca kod bir güncelleştirmesi - 12 8 dağıtma</span><span class="sxs-lookup"><span data-stu-id="d2fde-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>
====================
<span data-ttu-id="d2fde-104">tarafından [Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d2fde-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="d2fde-105">Başlangıç projesini indirin</span><span class="sxs-lookup"><span data-stu-id="d2fde-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="d2fde-106">Bu öğretici serisinde, nasıl dağıtılacağı gösterilir (bir ASP.NET Yayımlama) Web için Visual Studio 2012 RC veya Visual Studio Express 2012 RC'Yİ'ı kullanarak bir SQL Server Compact veritabanı içeren web uygulaması projesi.</span><span class="sxs-lookup"><span data-stu-id="d2fde-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="d2fde-107">Web yayımlama güncelleştirme yüklerseniz, Visual Studio 2010'u kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2fde-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="d2fde-108">Serinin bir giriş için bkz [serideki ilk öğreticide](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="d2fde-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="d2fde-109">Visual Studio 2012 RC sürümünden sonra sunulan dağıtım özellikleri gösterir, SQL Server sürümlerinde SQL Server Compact dışında dağıtmayı gösterir ve Azure App Service Web Apps'e dağıtma işlemi gösterilmektedir bir öğretici için bkz. [ASP.NET Web dağıtımı Visual Studio kullanarak](../../deployment/visual-studio-web-deployment/introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d2fde-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="d2fde-110">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d2fde-110">Overview</span></span>

<span data-ttu-id="d2fde-111">İlk dağıtımdan sonra Bakım ve web sitenizi geliştirme iş devam eder ve uzun süre önce bir güncelleştirme dağıtmak istersiniz.</span><span class="sxs-lookup"><span data-stu-id="d2fde-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="d2fde-112">Bu öğretici, uygulama kodunuz için bir güncelleştirme dağıtma işlemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="d2fde-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="d2fde-113">Bu güncelleştirme, veritabanı değişikliği gerektirmez; farklı bir veritabanı değişiklik sonraki öğreticide dağıtma hakkında nedir görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d2fde-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="d2fde-114">Anımsatıcı: Bir hata iletisi alıyorum veya Bu öğreticide ilerlerken bir sorun oluşması durumunda kontrol ettiğinizden emin olun [sorun giderme sayfası](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span><span class="sxs-lookup"><span data-stu-id="d2fde-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="d2fde-115">Bir kod değişikliği yapmadan</span><span class="sxs-lookup"><span data-stu-id="d2fde-115">Making a Code Change</span></span>

<span data-ttu-id="d2fde-116">Basit bir örnek, bir güncelleştirme uygulamanıza, için ekleyeceksiniz **Eğitmenler** seçili Eğitmenler tarafından verilen derslerimiz Listesi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="d2fde-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="d2fde-117">Çalıştırırsanız **Eğitmenler** sayfasında seçeneğinde olduğunu **seçin** bağlantıları kılavuzunda, ancak yapma dışında bir satır arka plan Aç gri uygulamayın.</span><span class="sxs-lookup"><span data-stu-id="d2fde-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

<span data-ttu-id="d2fde-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span></span>

<span data-ttu-id="d2fde-119">Şimdi ne zaman çalışan kod ekleyeceksiniz **seçin** bağlantı tıklatıldığında ve seçili Eğitmenler tarafından verilen derslerimiz listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d2fde-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="d2fde-120">İçinde *Instructors.aspx*, aşağıdaki işaretlemeyi ekleyin hemen sonra **ErrorMessageLabel** `Label` denetimi:</span><span class="sxs-lookup"><span data-stu-id="d2fde-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="d2fde-121">Sayfayı çalıştırın ve bir eğitmen seçin.</span><span class="sxs-lookup"><span data-stu-id="d2fde-121">Run the page and select an instructor.</span></span> <span data-ttu-id="d2fde-122">Bu eğitmen tarafından verilen derslerimiz listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d2fde-122">You see a list of courses taught by that instructor.</span></span>

<span data-ttu-id="d2fde-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="d2fde-124">Test ortamı için kod güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="d2fde-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="d2fde-125">Test ortamına dağıtma ibarettir çalıştırmanın tek tıklamayla yayımlama yeniden olur.</span><span class="sxs-lookup"><span data-stu-id="d2fde-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="d2fde-126">Bu işlem daha hızlı hale getirmek için kullanabileceğiniz **Web tek tık Yayımla** araç çubuğu.</span><span class="sxs-lookup"><span data-stu-id="d2fde-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="d2fde-127">İçinde **görünümü** menüsünde seçin **araç çubukları** seçip **Web tek tık Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="d2fde-129">İçinde **Çözüm Gezgini**, ContosoUniversity projeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="d2fde-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="d2fde-130">**Web tek tık Yayımla** araç seçin **Test** yayımlama profili ve ardından **Web'i Yayımla** (sağa ve sola işaret eden oklarla simgesiyle).</span><span class="sxs-lookup"><span data-stu-id="d2fde-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="d2fde-132">Visual Studio güncelleştirilmiş uygulamayı dağıtır ve tarayıcı giriş sayfasına otomatik olarak açılır.</span><span class="sxs-lookup"><span data-stu-id="d2fde-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="d2fde-133">Eğitmenler çalıştırırsanız ve güncelleştirme başarıyla dağıtıldığını doğrulamak için bir eğitmen seçin.</span><span class="sxs-lookup"><span data-stu-id="d2fde-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="d2fde-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span></span>

<span data-ttu-id="d2fde-135">Normalde ayrıca gerileme sınaması işlemi (diğer bir deyişle, yeni değişiklik herhangi bir mevcut işlevsellik yarıda yaramadı emin olmak için sitenin geri kalanını test).</span><span class="sxs-lookup"><span data-stu-id="d2fde-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="d2fde-136">Ancak bu öğretici için bu adımı atlayın ve güncelleştirmeyi üretime dağıtmak için devam edin.</span><span class="sxs-lookup"><span data-stu-id="d2fde-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="d2fde-137">Üretim için ilk veritabanı durumu çözümünüzün yeniden dağıtımını önleme</span><span class="sxs-lookup"><span data-stu-id="d2fde-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="d2fde-138">Gerçek bir uygulama kullanıcıların ilk dağıtımınızdan sonra üretim sitenizi etkileşim ve veritabanlarını Canlı verilerle doldurulur.</span><span class="sxs-lookup"><span data-stu-id="d2fde-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="d2fde-139">Bu nedenle, tüm canlı verileri silme, başlangıç durumunda üyelik veritabanında yeniden istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2fde-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="d2fde-140">SQL Server Compact veritabanları dosyalarında olduğundan *uygulama\_veri* klasörüne sahip dosyalar, bu nedenle dağıtım ayarlarını değiştirerek Bunu önlemek *uygulama\_veri* klasörü dağıtılan değildir.</span><span class="sxs-lookup"><span data-stu-id="d2fde-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="d2fde-141">Açık **proje özellikleri** ContosoUniversity proje ve Seç penceresi **Paketle/Yayımla Web** sekmesi. Emin olun **yapılandırma** açılan kutu ya da sahip **etkin (sürüm)** veya **yayın** seçili seçin **uygulamadandosyalarıdışlama\_Veri klasörü**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="d2fde-143">Gelecekte bir hata ayıklama derlemesi dağıtmak karar durumda, hata ayıklama derleme yapılandırması için aynı değişikliği yapmanız için iyi bir fikirdir: değiştirmek **yapılandırma** için **hata ayıklama** seçip **Dışla Uygulama dosyaları\_veri klasörü**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="d2fde-144">Kaydet ve Kapat **Paketle/Yayımla Web** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d2fde-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="d2fde-145">Yoksa emin **hedefteki ek dosyaları Kaldır** , yayımlama profillerine seçildi.</span><span class="sxs-lookup"><span data-stu-id="d2fde-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="d2fde-146">Bu seçeneği seçerseniz, dağıtım işlemi uygulamada olan veritabanlarını silecek\_sitesi dağıtıldı ve bu verileri, uygulama silinecek\_veri klasörü kendisi.</span><span class="sxs-lookup"><span data-stu-id="d2fde-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>


## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="d2fde-147">Kullanıcı erişimini üretim sitesini güncelleştirme sırasında engelliyor.</span><span class="sxs-lookup"><span data-stu-id="d2fde-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="d2fde-148">Dağıtım yapıyorsanız artık bir tek sayfalı basit bir değişiklik değişikliktir.</span><span class="sxs-lookup"><span data-stu-id="d2fde-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="d2fde-149">Ancak bazen daha büyük değişiklikler dağıttığınızda ve dağıtım tamamlanmadan önce bir kullanıcı bir sayfa istediğinde bu durumda site garip davranabilir.</span><span class="sxs-lookup"><span data-stu-id="d2fde-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="d2fde-150">Bunu önlemek için kullanabileceğiniz bir *uygulama\_offline.htm* dosya.</span><span class="sxs-lookup"><span data-stu-id="d2fde-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="d2fde-151">Adlı bir dosya yerleştirdiğinizde *uygulama\_offline.htm* uygulamanızın kök klasöründe, IIS uygulamanızı çalıştırmak yerine bu dosyayı otomatik olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d2fde-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="d2fde-152">Dağıtım sırasında erişimi engellemek için bu nedenle *uygulama\_offline.htm* kök klasöründe dağıtım işlemini çalıştırın ve Kaldır'ı *uygulama\_offline.htm*.</span><span class="sxs-lookup"><span data-stu-id="d2fde-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="d2fde-153">İçinde **Çözüm Gezgini**, çözüm (değil projelerden birine) sağ tıklayıp **yeni çözüm klasörü**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="d2fde-155">Klasör adı *SolutionFiles*.</span><span class="sxs-lookup"><span data-stu-id="d2fde-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="d2fde-156">Yeni klasöre adlı bir HTML sayfası oluşturma *uygulama\_offline.htm*.</span><span class="sxs-lookup"><span data-stu-id="d2fde-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="d2fde-157">Aşağıdaki biçimlendirme mevcut içeriğini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="d2fde-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="d2fde-158">Kopyalayabilirsiniz *uygulama\_offline.htm* site bir FTP bağlantısı kullanarak bir dosyaya veya **Dosya Yöneticisi** barındırma sağlayıcısının Denetim Masası'ndaki yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="d2fde-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="d2fde-159">Bu öğretici için kullanacağınız **Dosya Yöneticisi**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="d2fde-160">Denetim Masası'nı açın ve seçin **Dosya Yöneticisi** yaptığınız gibi [üretim ortamına dağıtma](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) öğretici.</span><span class="sxs-lookup"><span data-stu-id="d2fde-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="d2fde-161">Seçin **contosouniversity.com** ardından **wwwroot** uygulamanızın kök klasörüne almak ve ardından **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

<span data-ttu-id="d2fde-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span></span>

<span data-ttu-id="d2fde-163">İçinde **dosyasını karşıya yükle** iletişim kutusunda *uygulama\_offline.htm* dosya ve ardından **karşıya**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

<span data-ttu-id="d2fde-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span></span>

<span data-ttu-id="d2fde-165">Sitenizin URL'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="d2fde-165">Browse to your site's URL.</span></span> <span data-ttu-id="d2fde-166">Gördüğünüz *uygulama\_offline.htm* sayfası, giriş sayfanızın yerine artık görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d2fde-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

<span data-ttu-id="d2fde-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span></span>

<span data-ttu-id="d2fde-168">Artık üretime dağıtmaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d2fde-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="d2fde-169">Kod güncelleştirmesi üretim ortamına dağıtma</span><span class="sxs-lookup"><span data-stu-id="d2fde-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="d2fde-170">İçinde **Web tek tık Yayımla** araç seçin **üretim** yayımlama profili ve ardından **Web'i Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="d2fde-171">Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı sitenin ana sayfasını açar.</span><span class="sxs-lookup"><span data-stu-id="d2fde-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="d2fde-172">*Uygulama\_offline.htm* dosyası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d2fde-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="d2fde-173">Başarılı dağıtımı doğrulamak için test edebilmek için önce kaldırmanız gerekir *uygulama\_offline.htm* dosya.</span><span class="sxs-lookup"><span data-stu-id="d2fde-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="d2fde-174">Geri dönüp **Dosya Yöneticisi** Denetim Masası'nda uygulama.</span><span class="sxs-lookup"><span data-stu-id="d2fde-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="d2fde-175">Seçin **contosouniversity.com** ve **wwwroot**seçin **uygulama\_offline.htm**ve ardından **Sil**.</span><span class="sxs-lookup"><span data-stu-id="d2fde-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

<span data-ttu-id="d2fde-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span></span>

<span data-ttu-id="d2fde-177">Tarayıcıda genel sitede Eğitmenler sayfasını açın ve bir eğitmen güncelleştirme başarıyla dağıtıldığını doğrulamak için seçin.</span><span class="sxs-lookup"><span data-stu-id="d2fde-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="d2fde-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="d2fde-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span></span>

<span data-ttu-id="d2fde-179">Artık veritabanı değişikliği ilgili olmayan bir uygulama güncelleştirmesi dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="d2fde-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="d2fde-180">Sonraki öğreticiye nasıl veritabanı değişikliği dağıtılacağı gösterir.</span><span class="sxs-lookup"><span data-stu-id="d2fde-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d2fde-181">[Önceki](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [İleri](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="d2fde-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>