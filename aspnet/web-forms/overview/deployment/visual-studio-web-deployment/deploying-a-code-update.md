---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 'Visual Studio kullanarak ASP.NET Web dağıtımı: kod güncelleştirmesini dağıtma | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74626775"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="12fb0-103">Visual Studio kullanarak ASP.NET Web dağıtımı: kod güncelleştirmesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="12fb0-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>

<span data-ttu-id="12fb0-104">[Tom Dykstra](https://github.com/tdykstra) tarafından</span><span class="sxs-lookup"><span data-stu-id="12fb0-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="12fb0-105">Başlatıcı projesi indir</span><span class="sxs-lookup"><span data-stu-id="12fb0-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="12fb0-106">Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="12fb0-107">Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="12fb0-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="12fb0-108">Overview</span></span>

<span data-ttu-id="12fb0-109">İlk dağıtımdan sonra, Web sitenizi sürdürme ve Geliştirme çalışmanız devam eder ve uzun bir güncelleştirme dağıtmak isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="12fb0-110">Bu öğretici, uygulama kodunuza bir güncelleştirme dağıtma sürecinde size kılavuzluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="12fb0-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="12fb0-111">Bu öğreticide uyguladığınız ve dağıttığınız güncelleştirme bir veritabanı değişikliği içermez; bir sonraki öğreticide veritabanı değişikliğini dağıtma hakkında ne farklılık olduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="12fb0-112">Anımsatıcı: bir hata iletisi alırsanız veya öğreticide ilerlediyseniz bir şey çalışmadıysanız [sorun giderme sayfasını](troubleshooting.md)kontrol ettiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="12fb0-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="12fb0-113">Kod değişikliği yapma</span><span class="sxs-lookup"><span data-stu-id="12fb0-113">Make a code change</span></span>

<span data-ttu-id="12fb0-114">Uygulamanıza yönelik bir güncelleştirmeye yönelik basit bir örnek olarak, **eğitmenler** sayfasına seçili eğitmen tarafından bir kurs listesi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="12fb0-115">**Eğitmenler** sayfasını çalıştırırsanız, kılavuzda **seçim** bağlantıları olduğunu fark edeceksiniz, ancak satır arka planını gri bir şekilde çevirip başka hiçbir şey yapmayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="12fb0-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![Seçimle ilgili eğitmenler sayfası](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="12fb0-117">Şimdi **Seç** bağlantısına tıklandığında çalışan kodu ekleyecek ve seçilen eğitmen tarafından bir kurs listesi görüntülemektedir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="12fb0-118">*Eğitmenler. aspx*' te, **errormessagelabel** `Label` denetiminden hemen sonra aşağıdaki biçimlendirmeyi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="12fb0-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="12fb0-119">Sayfayı çalıştırın ve bir eğitmen seçin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-119">Run the page and select an instructor.</span></span> <span data-ttu-id="12fb0-120">Bu eğitmenin bir kurs listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-120">You see a list of courses taught by that instructor.</span></span>

    ![Kurslar ile eğitmenler sayfasında eğitim](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="12fb0-122">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="12fb0-123">Kod güncelleştirmesini test ortamına dağıtma</span><span class="sxs-lookup"><span data-stu-id="12fb0-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="12fb0-124">Yayımlama profillerinizi test, hazırlama ve üretime dağıtmak üzere kullanabilmeniz için önce veritabanı yayımlama seçeneklerini değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="12fb0-125">Artık üyelik veritabanı için verme ve veri dağıtım betikleri çalıştırmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="12fb0-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="12fb0-126">ContosoUniversity projesine sağ tıklayıp **Yayımla**' ya tıklayarak **Web 'i Yayımla** Sihirbazı ' nı açın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="12fb0-127">**Profil** açılır listesinden **Test** profili ' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="12fb0-128">**Ayarlar** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="12fb0-129">**Veritabanları** bölümünde **DefaultConnection** ' ın altında **veritabanını güncelleştir** onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="12fb0-130">**Profil** sekmesine tıklayın ve ardından **profil** açılır listesinden **hazırlama** profili ' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="12fb0-131">**Test** profilinde yapılan değişiklikleri kaydetmek isteyip Istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="12fb0-132">Hazırlama profilinde aynı değişikliği yapın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="12fb0-133">Üretim profilinde aynı değişikliği yapmak için işlemi tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="12fb0-134">Web 'i **Yayımla** sihirbazını kapatın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="12fb0-135">Sınama ortamına dağıtım artık tek tıklamayla yayımlamayı yeniden çalıştırmanın basit bir sorunudur.</span><span class="sxs-lookup"><span data-stu-id="12fb0-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="12fb0-136">Bu işlemi daha hızlı hale getirmek için **Web 'ı tek tıklamayla Yayımla** araç çubuğunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="12fb0-137">**Görünüm** menüsünde **araç çubukları** ' nı ve ardından Web 'i **Yayımla ' yı**seçin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="12fb0-139">**Çözüm Gezgini**, contosouniversity projesini seçin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="12fb0-140">**Web 'de Yayımla araç çubuğu ' na tıklayın** , **Test** yayımlama profilini seçin ve ardından **Web 'i Yayımla** ' ya tıklayın (sol ve sağ işaret eden oklu simge).</span><span class="sxs-lookup"><span data-stu-id="12fb0-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="12fb0-142">Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcı otomatik olarak giriş sayfasına açılır.</span><span class="sxs-lookup"><span data-stu-id="12fb0-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="12fb0-143">Eğitmenler sayfasını çalıştırın ve güncelleştirmenin başarıyla dağıtıldığını doğrulamak için bir eğitmen seçin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="12fb0-144">Normal olarak, regresyon testi de yaparsınız (yani, yeni değişikliğin mevcut işlevselliği bozmadığından emin olmak için sitenin geri kalanını test edersiniz).</span><span class="sxs-lookup"><span data-stu-id="12fb0-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="12fb0-145">Ancak bu öğreticide, bu adımı atlayıp güncelleştirmeyi hazırlama ve üretime dağıtmaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="12fb0-146">Yeniden dağıtırken, Web Dağıtımı hangi dosyaların değiştirildiğini otomatik olarak belirler ve yalnızca değiştirilen dosyaları sunucuya kopyalar.</span><span class="sxs-lookup"><span data-stu-id="12fb0-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="12fb0-147">Web Dağıtımı, varsayılan olarak, hangilerinin değiştirildiğini anlamak için dosyalarda son değiştirme tarihlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="12fb0-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="12fb0-148">Bazı kaynak denetim sistemleri, dosya içeriklerini değiştirmeseniz bile dosya tarihlerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="12fb0-149">Bu durumda, hangi dosyaların değiştirildiğini belirleyebilmek için dosya sağlama toplamlarını kullanmak üzere Web Dağıtımı yapılandırmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="12fb0-150">Daha fazla bilgi için, bkz. ASP.NET dağıtımı SSS içinde, [Tüm dosyalarımı neden yeniden dağıtıldı?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum)</span><span class="sxs-lookup"><span data-stu-id="12fb0-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="12fb0-151">Dağıtım sırasında uygulamayı çevrimdışına alma</span><span class="sxs-lookup"><span data-stu-id="12fb0-151">Take the application offline during deployment</span></span>

<span data-ttu-id="12fb0-152">Şimdi dağıttığınız değişiklik, tek bir sayfada basit bir değişiklik.</span><span class="sxs-lookup"><span data-stu-id="12fb0-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="12fb0-153">Ancak bazen daha büyük değişiklikler dağıtabilir veya hem kod hem de veritabanı değişikliklerini dağıtırsınız ve bir Kullanıcı, dağıtım tamamlanmadan önce bir sayfa istediğinde site yanlış davranabilir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="12fb0-154">Dağıtım devam ederken kullanıcıların siteye erişmesini engellemek için, bir *uygulamayı çevrimdışı. htm dosyası\_* kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="12fb0-155">App\_adlı bir dosyayı uygulamanızın kök klasöründe *çevrimdışı. htm* olarak YERLEŞTIRDIĞINIZDE, IIS bu dosyayı uygulamanızı çalıştırmak yerine otomatik olarak görüntüler.</span><span class="sxs-lookup"><span data-stu-id="12fb0-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="12fb0-156">Bu nedenle, dağıtım sırasında erişimi engellemek için, *uygulamayı\_çevrimdışı. htm* dosyasını kök klasöre yerleştirip dağıtım sürecini çalıştırın ve ardından uygulamayı başarılı bir şekilde yüklemeden sonra *çevrimdışı. htm\_* kaldırın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="12fb0-157">Web Dağıtımı,\_otomatik olarak bir varsayılan *uygulamayı* sunucuya dağıtmaya başladığında ve bu dosyayı tamamlandığında kaldırdığınızda, bu dosyayı sunucusuna otomatik olarak koyabileceğiniz şekilde yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="12fb0-158">Yapmanız gereken tek şey, yayımlama profili (. pubxml) dosyanıza aşağıdaki XML öğesini eklemektir:</span><span class="sxs-lookup"><span data-stu-id="12fb0-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="12fb0-159">Bu öğreticide, *çevrimdışı. htm dosyası\_* özel bir uygulama oluşturma ve kullanma hakkında bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="12fb0-160">Hazırlama sitesine erişen kullanıcılarınız olmadığından, uygulamayı hazırlama sitesinde *çevrimdışı. htm\_* kullanmak gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="12fb0-161">Ancak her şeyi üretimde dağıtmayı planladığınız şekilde test etmek için hazırlama kullanmak iyi bir uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="12fb0-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-app_offlinehtm"></a><span data-ttu-id="12fb0-162">Çevrimdışı. htm\_uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="12fb0-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="12fb0-163">**Çözüm Gezgini**, çözüme sağ tıklayın ve **Ekle**' ye tıklayın ve ardından **Yeni öğe**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="12fb0-164">*App\_offline. htm* adlı bir **HTML sayfası** oluşturun (varsayılan olarak Visual Studio 'nun oluşturduğu *. html* uzantısında son "l" ı silin).</span><span class="sxs-lookup"><span data-stu-id="12fb0-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="12fb0-165">Şablon işaretlemesini aşağıdaki biçimlendirme ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="12fb0-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="12fb0-166">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-166">Save and close the file.</span></span>

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="12fb0-167">Uygulamayı çevrimdışı. htm\_Web sitesinin kök klasörüne kopyalayın</span><span class="sxs-lookup"><span data-stu-id="12fb0-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="12fb0-168">Web sitesine dosya kopyalamak için herhangi bir FTP aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="12fb0-169">[FileZilla](http://filezilla-project.org/) , popüler bir FTP aracıdır ve ekran görüntüleri içinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="12fb0-170">FTP aracını kullanmak için üç şey gerekir: FTP URL 'SI, Kullanıcı adı ve parola.</span><span class="sxs-lookup"><span data-stu-id="12fb0-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="12fb0-171">URL, Azure Yönetim Portalı Web sitesinin Pano sayfasında gösterilir ve FTP için Kullanıcı adı ve parola, daha önce indirdiğiniz *. publishsettings* dosyasında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="12fb0-172">Aşağıdaki adımlarda bu değerlerin nasıl alınacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="12fb0-173">Azure Yönetim Portalı ' de, **Web siteleri** sekmesi ' ne ve ardından hazırlama Web sitesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="12fb0-174">**Pano** sayfasında, **Hızlı bakış** bölümünde FTP ana bilgisayar adını bulmak için aşağı kaydırın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP konak adı](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="12fb0-176">Hazırlama *. publishsettings* dosyasını Not defteri 'nde veya başka bir metin düzenleyicisinde açın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="12fb0-177">FTP profili için `publishProfile` öğesini bulun.</span><span class="sxs-lookup"><span data-stu-id="12fb0-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="12fb0-178">`userName` ve `userPWD` değerlerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP kimlik bilgileri](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="12fb0-180">FTP aracınızı açın ve FTP URL 'sinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="12fb0-181">*App\_uygulamasını* çözüm klasöründen hazırlama sitesindeki */site/Wwwroot* klasörüne kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![App_offline Kopyala](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="12fb0-183">Hazırlama sitenizin URL 'sine gidin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="12fb0-184">*Uygulama\_çevrimdışı. htm* sayfasının giriş sayfanız yerine görüntülendiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![tarayıcı penceresinde app_offline. htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="12fb0-186">Şimdi hazırlama işlemine dağıtmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="12fb0-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="12fb0-187">Kod güncelleştirmesini hazırlama ve üretime dağıtma</span><span class="sxs-lookup"><span data-stu-id="12fb0-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="12fb0-188">Web 'de **Yayımla** araç çubuğunda, **hazırlama** yayımlama profilini seçin ve ardından **Web 'i Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="12fb0-189">Visual Studio, güncelleştirilmiş uygulamayı dağıtır ve tarayıcının sitenin giriş sayfasında açılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="12fb0-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="12fb0-190">*App\_offline. htm* dosyası görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="12fb0-191">Başarılı dağıtımı doğrulamayı test etmeden önce, *app\_offline. htm* dosyasını kaldırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="12fb0-192">FTP aracınızdan geri dönün ve uygulamayı hazırlama sitesinden **çevrimdışı. htm\_** silin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="12fb0-193">Tarayıcıda, hazırlama sitesinde eğitmenler sayfasını açın ve güncelleştirmenin başarıyla dağıtıldığını doğrulamak için bir eğitmen seçin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="12fb0-194">Hazırlama için yaptığınız gibi üretim için aynı yordamı izleyin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="12fb0-195">Değişiklikleri gözden geçirme ve belirli dosyaları dağıtma</span><span class="sxs-lookup"><span data-stu-id="12fb0-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="12fb0-196">Visual Studio 2012 ayrıca tek tek dosyaları dağıtmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="12fb0-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="12fb0-197">Seçili bir dosya için, yerel sürüm ile dağıtılan sürüm arasındaki farkları görüntüleyebilir, dosyayı hedef ortama dağıtabilir veya hedef ortamdaki dosyayı yerel projeye kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="12fb0-198">Öğreticinin bu bölümünde, bu özelliklerin nasıl kullanılacağını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="12fb0-199">Dağıtmak için bir değişiklik yapın</span><span class="sxs-lookup"><span data-stu-id="12fb0-199">Make a change to deploy</span></span>

1. <span data-ttu-id="12fb0-200">*Content/site. css*' yi açın ve `body` etiketinin bloğunu bulun.</span><span class="sxs-lookup"><span data-stu-id="12fb0-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="12fb0-201">`background-color` değerini `#fff` `darkblue`olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="12fb0-202">Yayımlama önizlemesi penceresinde değişikliği görüntüleme</span><span class="sxs-lookup"><span data-stu-id="12fb0-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="12fb0-203">Projeyi yayımlamak için **Web 'ı Yayımla** Sihirbazı 'nı kullandığınızda, **Önizleme** penceresinde dosyaya çift tıklayarak hangi değişikliklerin yayımlanacak olduğunu görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="12fb0-204">ContosoUniversity projesine sağ tıklayın ve **Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="12fb0-205">**Profil** açılan listesinden, **Test** yayımlama profilini seçin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="12fb0-206">**Önizleme**' ye ve ardından **önizlemeyi Başlat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="12fb0-207">**Önizleme** bölmesinde, **site. css**' ye çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![Site. css ' ye çift tıklayın](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="12fb0-209">**Değişiklikleri Önizle** iletişim kutusu, dağıtılacak değişikliklerin önizlemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![Site. css değişikliklerini Önizle](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="12fb0-211">*Web. config* dosyasına çift tıklarsanız, **Değişiklikleri Önizle** iletişim kutusu derleme yapılandırma dönüştürmelerinizin ve yayımlama profili dönüştürmelerinin etkisini gösterir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="12fb0-212">Bu noktada, sunucuda *Web. config* dosyasının değişmesine neden olacak hiçbir şey gerçekleştirmedi, bu nedenle hiçbir değişiklik olmadığını görmeyi düşünüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="12fb0-213">Ancak, **Değişiklikleri Önizle** penceresi yanlış bir şekilde iki değişiklik gösterir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="12fb0-214">İki XML öğesi, kaldırılacak şekilde görünür.</span><span class="sxs-lookup"><span data-stu-id="12fb0-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="12fb0-215">Bu öğeler, bir Code First bağlam sınıfı için **uygulama başlatıldığında Code First Migrations Çalıştır '** ı seçtiğinizde Yayımla işlemi tarafından eklenir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="12fb0-216">Karşılaştırma, yayımlama işlemi bu öğeleri eklemeden önce yapılır, bu nedenle kaldırılmasa da kaldırılmamaları gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="12fb0-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="12fb0-217">Bu hata gelecekteki bir sürümde düzeltilecektir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="12fb0-218">**Kapat**'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-218">Click **Close**.</span></span>
6. <span data-ttu-id="12fb0-219">**Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-219">Click **Publish**.</span></span>
7. <span data-ttu-id="12fb0-220">Tarayıcı, test sitesinin giriş sayfasında açıldığında, CSS değişikliğinin etkisini görmek için sabit yenilemeye yol açacak şekilde CTRL + F5 tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS değişikliğinin etkisi](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="12fb0-222">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="12fb0-223">Belirli dosyaları Çözüm Gezgini yayımlama</span><span class="sxs-lookup"><span data-stu-id="12fb0-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="12fb0-224">Mavi arka planı beğenmediğinizi ve orijinal renge dönmek istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="12fb0-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="12fb0-225">Bu bölümde, belirli bir dosyayı doğrudan **Çözüm Gezgini**yayımlayarak özgün ayarları geri yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="12fb0-226">*Content/site. css* ' i açın ve `background-color` ayarını `#fff`geri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="12fb0-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="12fb0-227">**Çözüm Gezgini**, *Content/site. css* dosyasına sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="12fb0-228">Bağlam menüsünde üç yayımlama seçeneği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-228">The context menu shows three publish options.</span></span>

    ![Çözüm Gezgini seçenekleri yayımlama](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="12fb0-230">**Site. css değişikliklerini Önizle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="12fb0-231">Yerel dosya ile hedef ortamdaki sürümü arasındaki farkları göstermek için bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="12fb0-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/site. css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="12fb0-233">**Çözüm Gezgini**, **site. css** ' ye yeniden sağ tıklayıp site. **CSS Yayımla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="12fb0-234">**Web yayımlama etkinliği** penceresi, dosyanın yayımlandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![Web yayımlama etkinliği penceresi](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="12fb0-236">`http://localhost/contosouniversity` URL 'SI için bir tarayıcı açın ve ardından CTRL + F5 tuşlarına basarak CSS değişikliğinin etkisini görmek için bir sabit yenilemeye neden olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="12fb0-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![Normal CSS ile ana sayfa](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="12fb0-238">Tarayıcıyı kapatın.</span><span class="sxs-lookup"><span data-stu-id="12fb0-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="12fb0-239">Özet</span><span class="sxs-lookup"><span data-stu-id="12fb0-239">Summary</span></span>

<span data-ttu-id="12fb0-240">Artık bir veritabanı değişikliği içermeyen bir uygulama güncelleştirmesi dağıtmanın birkaç yolunu gördünüz ve nelerin güncelleştirileceğini doğrulamak için değişikliklerin nasıl önizlendiğini gördünüz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="12fb0-241">Eğitmenler sayfasında şimdi bir **Kurslar taöğretme** bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="12fb0-241">The Instructors page now has a **Courses Taught** section.</span></span>

![Kurslar ile eğitmenler sayfasında eğitim](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="12fb0-243">Sonraki öğreticide bir veritabanı değişikliğini dağıtma gösterilmektedir: veritabanına ve eğitmenler sayfasına bir Doğum tarihi alanı ekleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="12fb0-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="12fb0-244">[Önceki](deploying-to-production.md)
> [İleri](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="12fb0-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
