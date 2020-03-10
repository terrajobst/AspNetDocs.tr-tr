---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: Dağıtım komut dosyası oluşturma ve çalıştırma | Microsoft Docs
author: jrjlee
description: Bu konuda, Microsoft Build Engine (MSBuild) proje dosyalarını tek adımlı, yeniden... kullanarak bir dağıtımı çalıştırmanıza imkan tanıyan bir komut dosyasının nasıl oluşturulacağı açıklanmaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634311"
---
# <a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="a4a17-103">Dağıtım Komut Dosyası Oluşturma ve Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a4a17-103">Creating and Running a Deployment Command File</span></span>

<span data-ttu-id="a4a17-104">[Jason Lee](https://github.com/jrjlee) tarafından</span><span class="sxs-lookup"><span data-stu-id="a4a17-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a4a17-105">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="a4a17-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a4a17-106">Bu konuda, Microsoft Build Engine (MSBuild) proje dosyalarını kullanarak bir dağıtımı tek adımlı, yinelenebilir bir işlem olarak çalıştırmanıza olanak tanıyan bir komut dosyasının nasıl oluşturulacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>

<span data-ttu-id="a4a17-107">Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, WINDOWS COMMUNICATION FOUNDATION&#x2014;(WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager](the-contact-manager-solution.md) çözümünü kullanır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="a4a17-108">Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren iki [](understanding-the-build-process.md)proje&#x2014;dosyası tarafından denetlendiği ve ortama özgü derleme ve dağıtım ayarlarını Içeren, derleme işlemini anlama bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="a4a17-109">Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="a4a17-110">İşleme genel bakış</span><span class="sxs-lookup"><span data-stu-id="a4a17-110">Process Overview</span></span>

<span data-ttu-id="a4a17-111">Bu konu başlığında, hedef ortamınıza yinelenebilir bir dağıtım gerçekleştirmek için bu proje dosyalarını kullanan bir komut dosyası oluşturmayı ve çalıştırmayı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="a4a17-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="a4a17-112">Temelde, komut dosyasının yalnızca bir MSBuild komutu içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4a17-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="a4a17-113">MSBuild 'in ortam-agstik *Publish. proj* dosyasını yürütmesini söyler.</span><span class="sxs-lookup"><span data-stu-id="a4a17-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="a4a17-114">*Publish. proj* dosyasına, ortama özgü proje ayarlarını ve nerede bulunacağı dosyayı içerdiğini söyler.</span><span class="sxs-lookup"><span data-stu-id="a4a17-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="a4a17-115">MSBuild komutu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4a17-115">Create an MSBuild Command</span></span>

<span data-ttu-id="a4a17-116">[Derleme işlemini anlama](understanding-the-build-process.md)bölümünde açıklandığı gibi, örneğin,&#x2014; *env-dev. proj*&#x2014;gibi ortama özgü proje dosyası, derleme zamanında ortam belirsiz *Publish. proj* dosyasına aktarılmak üzere tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="a4a17-117">Birlikte, bu iki dosya, çözümünüzü nasıl derleyip dağıtacağınızı söyleyen bir dizi yönerge sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4a17-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="a4a17-118">*Publish. proj* dosyası ortama özgü proje dosyasını içeri aktarmak Için bir **içeri aktarma** öğesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

<span data-ttu-id="a4a17-119">Bu nedenle, Contact Manager çözümünü derlemek ve dağıtmak için MSBuild. exe ' yi kullandığınızda şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a4a17-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="a4a17-120">*Publish. proj* dosyasında MSBuild. exe ' yi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a4a17-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="a4a17-121">**Targetenvpropsfile**adlı bir komut satırı parametresi sağlayarak ortama özgü proje dosyasının konumunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="a4a17-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="a4a17-122">Bunu yapmak için MSBuild komutunuz şuna benzemelidir:</span><span class="sxs-lookup"><span data-stu-id="a4a17-122">To do this, your MSBuild command should resemble this:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

<span data-ttu-id="a4a17-123">Buradan, yinelenebilir, tek adımlı bir dağıtıma geçiş yapmak için basit bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="a4a17-124">Tek yapmanız gereken, MSBuild komutlarınızı bir. cmd dosyasına eklemektir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="a4a17-125">Contact Manager çözümünde, Yayımla klasörü, tam olarak bunu yapan *Publish-dev. cmd* adlı bir dosya içerir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="a4a17-126">**/Fl** anahtarı, MSBuild. exe ' nin çağrıldığı çalışma dizininde *MSBuild. log* adlı bir günlük dosyası oluşturmak için MSBuild 'e bildirir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>

<span data-ttu-id="a4a17-127">Contact Manager çözümünü dağıtmak veya yeniden dağıtmak için tüm yapmanız gereken *Publish-dev. cmd* dosyasını çalıştırmaktır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="a4a17-128">Dosyayı çalıştırdığınızda MSBuild şu şekilde olur:</span><span class="sxs-lookup"><span data-stu-id="a4a17-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="a4a17-129">Çözümdeki tüm projeleri derleyin.</span><span class="sxs-lookup"><span data-stu-id="a4a17-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="a4a17-130">Web uygulaması projeleri için dağıtılabilir Web paketleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4a17-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="a4a17-131">Veritabanı projeleri için. dbschema ve. DeployManifest dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4a17-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="a4a17-132">Web paketlerini Web sunucusuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a4a17-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="a4a17-133">Veritabanını veritabanı sunucusuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="a4a17-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="a4a17-134">Dağıtımı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a4a17-134">Run the Deployment</span></span>

<span data-ttu-id="a4a17-135">Hedef ortamınız için bir komut dosyası oluşturduğunuzda, yalnızca dosyayı çalıştırarak tüm dağıtımı tamamlayabilmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a4a17-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="a4a17-136">**Iletişim Yöneticisi çözümünü test ortamınıza dağıtmak için**</span><span class="sxs-lookup"><span data-stu-id="a4a17-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="a4a17-137">Geliştirici iş istasyonunuzda Windows Gezgini ' ni açın ve *Publish-dev. cmd* dosyasının konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="a4a17-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="a4a17-138">Dosyayı çalıştırmak için çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4a17-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="a4a17-139">**Dosya Aç – güvenlik uyarısı** iletişim kutusu görüntülenirse **Çalıştır**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a4a17-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="a4a17-140">Yapılandırma ayarlarınız ve test sunucularınız doğru ayarlandıysa, MSBuild proje dosyalarını işlemeyi tamamladığında, komut Istemi penceresinde bir **Yapı başarılı** iletisi gösterilir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="a4a17-141">Çözümü bu ortama ilk kez dağıttığınız zaman, **ContactManager** veritabanındaki **DB\_datawriter** ve **DB\_DataReader** rollerine test Web sunucusu makine hesabını eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="a4a17-142">Bu yordam, [Web dağıtımı yayımlama için bir veritabanı sunucusunu yapılandırma](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)bölümünde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a4a17-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="a4a17-143">Bu izinleri yalnızca veritabanını oluştururken atamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="a4a17-144">Varsayılan olarak, derleme işlemi her dağıtımda&#x2014;veritabanını yeniden oluşturmayacak, var olan veritabanını en son şemayla karşılaştırır ve yalnızca gerekli değişiklikleri yapar.</span><span class="sxs-lookup"><span data-stu-id="a4a17-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="a4a17-145">Sonuç olarak, yalnızca çözümü ilk kez dağıttığınızda bu veritabanı rollerini eşlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="a4a17-146">Internet Explorer 'ı açın ve Contact Manager uygulamasının URL 'sine gidin (örneğin, `http://testweb1:85/ContactManager/`).</span><span class="sxs-lookup"><span data-stu-id="a4a17-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="a4a17-147">Uygulamanın beklendiği gibi çalıştığını ve kişiler ekleyebildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a4a17-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="a4a17-148">Sonuç</span><span class="sxs-lookup"><span data-stu-id="a4a17-148">Conclusion</span></span>

<span data-ttu-id="a4a17-149">MSBuild yönergelerinizi içeren bir komut dosyası oluşturmak, belirli bir hedef ortama çok projeli bir çözüm oluşturmanın ve dağıtmanın hızlı ve kolay bir yolunu sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4a17-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="a4a17-150">Çözümünüzü birden çok hedef ortama tekrar tekrar dağıtmanız gerekiyorsa, birden çok komut dosyası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4a17-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="a4a17-151">Her komut dosyasında, MSBuild komutu aynı evrensel proje dosyasını oluşturur, ancak ortama özgü farklı bir proje dosyası belirtir.</span><span class="sxs-lookup"><span data-stu-id="a4a17-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="a4a17-152">Örneğin, bir geliştirici veya test ortamında yayımlanacak bir komut dosyası bu MSBuild komutunu içerebilir:</span><span class="sxs-lookup"><span data-stu-id="a4a17-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

<span data-ttu-id="a4a17-153">Hazırlama ortamında yayımlanacak bir komut dosyası bu MSBuild komutunu içerebilir:</span><span class="sxs-lookup"><span data-stu-id="a4a17-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> <span data-ttu-id="a4a17-154">Kendi sunucu ortamlarınız için ortama özgü proje dosyalarını özelleştirmeye ilişkin yönergeler için bkz. [hedef ortam Için dağıtım özelliklerini yapılandırma](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span><span class="sxs-lookup"><span data-stu-id="a4a17-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>

<span data-ttu-id="a4a17-155">Ayrıca, MSBuild komutlarınızda özellikleri geçersiz kılarak veya farklı anahtarlar ayarlayarak her bir ortam için yapı işlemini özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4a17-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="a4a17-156">Daha fazla bilgi için bkz. [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4a17-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a4a17-157">[Önceki](deploying-database-projects.md)
> [İleri](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="a4a17-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
