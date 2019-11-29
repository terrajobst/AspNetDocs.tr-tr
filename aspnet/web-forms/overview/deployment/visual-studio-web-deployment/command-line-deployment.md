---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 'Visual Studio kullanarak Web dağıtımı ASP.NET: komut satırı dağıtımı | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634200"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="e155d-103">Visual Studio kullanarak Web dağıtımı ASP.NET: komut satırı dağıtımı</span><span class="sxs-lookup"><span data-stu-id="e155d-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="e155d-104">[Tom Dykstra](https://github.com/tdykstra) tarafından</span><span class="sxs-lookup"><span data-stu-id="e155d-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="e155d-105">Başlatıcı projesi indir</span><span class="sxs-lookup"><span data-stu-id="e155d-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="e155d-106">Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir.</span><span class="sxs-lookup"><span data-stu-id="e155d-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="e155d-107">Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.</span><span class="sxs-lookup"><span data-stu-id="e155d-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="e155d-108">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="e155d-108">Overview</span></span>

<span data-ttu-id="e155d-109">Bu öğreticide, komut satırından Visual Studio Web yayımlama ardışık düzenini çağırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e155d-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="e155d-110">Bu, genellikle [kaynak kodu sürüm denetim sistemi](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)kullanarak Visual Studio 'da el ile yapmak yerine [dağıtım sürecini otomatikleştirmek](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) istediğiniz senaryolar için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e155d-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="e155d-111">Dağıtmak için bir değişiklik yapın</span><span class="sxs-lookup"><span data-stu-id="e155d-111">Make a change to deploy</span></span>

<span data-ttu-id="e155d-112">Şu anda hakkında sayfasında Şablon kodu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e155d-112">Currently the About page displays the template code.</span></span>

![Şablon kodu içeren sayfa hakkında](command-line-deployment/_static/image1.png)

<span data-ttu-id="e155d-114">Bunu, öğrenci kaydı özetini görüntüleyen kodla değiştirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e155d-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="e155d-115">*About. aspx* sayfasını açın, `MainContent` `Content` öğesi içindeki tüm biçimlendirmeyi silin ve aşağıdaki biçimlendirmeyi onun yerine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e155d-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="e155d-116">Projeyi çalıştırın ve **hakkında** sayfasını seçin.</span><span class="sxs-lookup"><span data-stu-id="e155d-116">Run the project and select the **About** page.</span></span>

![Sayfa hakkında](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="e155d-118">Komut satırını kullanarak test 'e dağıtın</span><span class="sxs-lookup"><span data-stu-id="e155d-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="e155d-119">Başka bir veritabanı değişikliği dağıtmayacağız. bu nedenle, ASPNET-ContosoUniversity veritabanı için dbDacFx veritabanı dağıtımını devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="e155d-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="e155d-120">Web 'i **Yayımla** sihirbazını açın ve üç yayımlama profilinin her birinde, **Ayarlar** sekmesindeki **veritabanını güncelleştir** onay kutusunun işaretini kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e155d-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="e155d-121">Windows 8 başlangıç sayfasında, **VS2012 için geliştirici komut istemi**aratın.</span><span class="sxs-lookup"><span data-stu-id="e155d-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="e155d-122">**VS2012 için geliştirici komut istemi** simgeye sağ tıklayın ve **yönetici olarak çalıştır**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="e155d-123">Komut istemine aşağıdaki komutu girin ve çözüm dosyası yolunu çözüm dosyası yoluyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e155d-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="e155d-124">MSBuild çözümü oluşturur ve test ortamına dağıtır.</span><span class="sxs-lookup"><span data-stu-id="e155d-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![Komut satırı çıkışı](command-line-deployment/_static/image3.png)

<span data-ttu-id="e155d-126">Bir tarayıcı açın ve `http://localhost/ContosoUniversity`gidin ve sonra dağıtımın başarılı olduğunu doğrulamak için **hakkında** sayfasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="e155d-127">Testte herhangi bir öğrenci oluşturmadıysanız, **öğrenci gövdesi istatistikleri** başlığının altında boş bir sayfa görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e155d-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="e155d-128">**Öğrenciler** sayfasına gidin, **öğrenci Ekle**' ye tıklayın ve bazı öğrenciler ekleyin ve sonra öğrenci istatistiklerini görmek için **hakkında** sayfasına dönün.</span><span class="sxs-lookup"><span data-stu-id="e155d-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![Test ortamında sayfa hakkında](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="e155d-130">Anahtar komut satırı seçenekleri</span><span class="sxs-lookup"><span data-stu-id="e155d-130">Key command line options</span></span>

<span data-ttu-id="e155d-131">Girdiğiniz komut çözüm dosyası yolunu ve MSBuild 'e iki özelliği geçti:</span><span class="sxs-lookup"><span data-stu-id="e155d-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="e155d-132">Tek tek projeleri dağıtmaya karşı çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="e155d-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="e155d-133">Çözüm dosyası belirtildiğinde Çözümdeki tüm projelerin oluşturulmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="e155d-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="e155d-134">Çözümde birden çok Web projeniz varsa, aşağıdaki MSBuild davranışı geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="e155d-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="e155d-135">Komut satırında belirttiğiniz özellikler her projeye geçirilir.</span><span class="sxs-lookup"><span data-stu-id="e155d-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="e155d-136">Bu nedenle, her Web projesinin belirttiğiniz ada sahip bir yayımlama profili olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155d-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="e155d-137">`/p:PublishProfile=Test`belirtirseniz, her Web projesinin *Test*adlı bir yayımlama profili olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155d-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="e155d-138">Başka bir proje bile derlenmezse, bir projeyi başarıyla yayımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e155d-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="e155d-139">Daha fazla bilgi için bkz. StackOverflow thread [MSBuild, iki paket ile başarısız oluyor](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span><span class="sxs-lookup"><span data-stu-id="e155d-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="e155d-140">Çözüm yerine bireysel bir proje belirtirseniz, Visual Studio sürümünü belirten bir parametre eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155d-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="e155d-141">Visual Studio 2012 kullanıyorsanız komut satırı aşağıdaki örneğe benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="e155d-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="e155d-142">Visual Studio 2010 sürüm numarası 10,0 ' dir.</span><span class="sxs-lookup"><span data-stu-id="e155d-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="e155d-143">Daha fazla bilgi için bkz. [Visual Studio proje uyumluluğu ve VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on hashed 'in blogu.</span><span class="sxs-lookup"><span data-stu-id="e155d-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="e155d-144">Yayımlama profilini belirtme</span><span class="sxs-lookup"><span data-stu-id="e155d-144">Specifying the publish profile</span></span>

<span data-ttu-id="e155d-145">Aşağıdaki örnekte gösterildiği gibi, yayımlama profilini adına göre veya *. pubxml* dosyasının tam yolu ile belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e155d-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="e155d-146">Komut satırı yayımlama için desteklenen Web yayımlama yöntemleri</span><span class="sxs-lookup"><span data-stu-id="e155d-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="e155d-147">Komut satırı yayımlama için üç yayımlama yöntemi desteklenir:</span><span class="sxs-lookup"><span data-stu-id="e155d-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="e155d-148">`MSDeploy`-Web Dağıtımı kullanarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="e155d-149">`Package`-Web Dağıtımı bir paket oluşturarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="e155d-150">Paketi, onu oluşturan MSBuild komutundan ayrı olarak yüklemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="e155d-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="e155d-151">`FileSystem`-dosyaları belirtilen klasöre kopyalayarak yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="e155d-152">Yapı yapılandırmasını ve platformunu belirtme</span><span class="sxs-lookup"><span data-stu-id="e155d-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="e155d-153">Derleme yapılandırması ve platformun Visual Studio 'da veya komut satırında ayarlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155d-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="e155d-154">Yayımlama profilleri `LastUsedBuildConfiguration` ve `LastUsedPlatform`adlı özellikleri içerir, ancak projenin nasıl oluşturulduğunu belirleyebilmek için bu özellikleri ayarlayamazsınız.</span><span class="sxs-lookup"><span data-stu-id="e155d-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="e155d-155">Daha fazla bilgi için bkz. MSBuild: saymış Hashbir Web bloguna [yapılandırma özelliğini ayarlama](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) .</span><span class="sxs-lookup"><span data-stu-id="e155d-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="e155d-156">Hazırlama için dağıt</span><span class="sxs-lookup"><span data-stu-id="e155d-156">Deploy to staging</span></span>

<span data-ttu-id="e155d-157">Azure 'a dağıtmak için, parolayı komut satırına eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155d-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="e155d-158">Parolayı Visual Studio 'daki Yayımla profilinde kaydettiyseniz, *. pubxml. User* dosyanızda şifreli biçimde depolanmıştı.</span><span class="sxs-lookup"><span data-stu-id="e155d-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="e155d-159">Bir komut satırı dağıtımı yaptığınızda bu dosyaya MSBuild tarafından erişilmez, bu nedenle parolayı bir komut satırı parametresinde geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155d-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="e155d-160">Daha önce hazırlama Web sitesi için indirdiğiniz *. publishsettings* dosyasından gereken parolayı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="e155d-161">Parola, Web Dağıtımı `publishProfile` öğesi için `userPWD` özniteliğinin değeridir.</span><span class="sxs-lookup"><span data-stu-id="e155d-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Web Dağıtımı parolası](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="e155d-163">Windows 8 başlangıç sayfasında, **VS2012 için geliştirici komut istemi**arayın ve komut istemi ' ni açmak için simgeye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="e155d-164">(Yerel bilgisayarda IIS 'e dağıtmıyorsanız, bu kez yönetici olarak açmanız gerekmez.)</span><span class="sxs-lookup"><span data-stu-id="e155d-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="e155d-165">Komut istemine aşağıdaki komutu girin, çözüm dosyası yolunu çözüm dosyası yoluyla ve parolanızla parolayla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e155d-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="e155d-166">Bu komut satırının ek bir parametre içerdiğine dikkat edin: `/p:AllowUntrustedCertificate=true`.</span><span class="sxs-lookup"><span data-stu-id="e155d-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="e155d-167">Bu öğretici yazıldığı için, komut satırından Azure 'da yayımladığınızda `AllowUntrustedCertificate` özelliği ayarlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e155d-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="e155d-168">Bu hata için düzeltildiğinde bu parametreye gerek kalmaz.</span><span class="sxs-lookup"><span data-stu-id="e155d-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="e155d-169">Bir tarayıcı açın ve hazırlama sitenizin URL 'sine gidin ve sonra dağıtımın başarılı olduğunu doğrulamak için **hakkında** sayfasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="e155d-170">Daha önce test ortamı için gördüğünüz gibi, **hakkında** sayfasında istatistikleri görmek için bazı öğrenciler oluşturmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="e155d-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="e155d-171">Üretime dağıtma</span><span class="sxs-lookup"><span data-stu-id="e155d-171">Deploy to production</span></span>

<span data-ttu-id="e155d-172">Üretime dağıtma işlemi, hazırlama işlemine benzerdir.</span><span class="sxs-lookup"><span data-stu-id="e155d-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="e155d-173">Daha önce üretim web sitesi için indirdiğiniz *. publishsettings* dosyasından gereken parolayı kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="e155d-174">**VS2012 için geliştirici komut istemi**açın.</span><span class="sxs-lookup"><span data-stu-id="e155d-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="e155d-175">Komut istemine aşağıdaki komutu girin, çözüm dosyası yolunu çözüm dosyası yoluyla ve parolanızla parolayla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="e155d-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="e155d-176">Gerçek bir üretim sitesi için aynı zamanda bir veritabanı değişikliği varsa, genellikle *uygulamayı çevrimdışı. htm dosyası\_* dağıtımdan önce siteye kopyalayabilir ve başarılı dağıtımdan sonra silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155d-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="e155d-177">Bir tarayıcı açın ve hazırlama sitenizin URL 'sine gidin ve sonra dağıtımın başarılı olduğunu doğrulamak için **hakkında** sayfasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e155d-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="e155d-178">Özet</span><span class="sxs-lookup"><span data-stu-id="e155d-178">Summary</span></span>

<span data-ttu-id="e155d-179">Artık komut satırını kullanarak bir uygulama güncelleştirmesi dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="e155d-179">You have now deployed an application update by using the command line.</span></span>

![Test ortamında sayfa hakkında](command-line-deployment/_static/image6.png)

<span data-ttu-id="e155d-181">Sonraki öğreticide, Web yayımlama işlem hattının nasıl uzatılayabileceğinizi gösteren bir örnek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e155d-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="e155d-182">Örnek, projeye dahil olmayan dosyaları nasıl dağıtacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e155d-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e155d-183">[Önceki](deploying-a-database-update.md)
> [İleri](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="e155d-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
