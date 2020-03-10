---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
title: Contact Manager çözümünü ayarlama | Microsoft Docs
author: jrjlee
description: Bu konuda, bir geliştirici iş istasyonunda yerel olarak çalışacak olan Contact Manager çözümünün nasıl indirileceği ve yapılandırılacağı açıklanmaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 200b973c-776b-4a9b-9e82-39fda6120a52
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/setting-up-the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: d9774ee01cb0515d7e733b24baa661f2648bd7c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629859"
---
# <a name="setting-up-the-contact-manager-solution"></a><span data-ttu-id="a1faf-103">Kişi Yöneticisi Çözümünü Ayarlama</span><span class="sxs-lookup"><span data-stu-id="a1faf-103">Setting Up the Contact Manager Solution</span></span>

<span data-ttu-id="a1faf-104">[Jason Lee](https://github.com/jrjlee) tarafından</span><span class="sxs-lookup"><span data-stu-id="a1faf-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="a1faf-105">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="a1faf-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="a1faf-106">Bu konuda, bir geliştirici iş istasyonunda yerel olarak çalışacak olan Contact Manager çözümünün nasıl indirileceği ve yapılandırılacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1faf-106">This topic describes how to download and configure the Contact Manager solution to run locally on a developer workstation.</span></span>

## <a name="system-requirements"></a><span data-ttu-id="a1faf-107">Sistem Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="a1faf-107">System Requirements</span></span>

<span data-ttu-id="a1faf-108">Contact Manager çözümünü yerel olarak çalıştırmak ve bu öğreticide açıklanan diğer görevleri gerçekleştirmek için, bu yazılımı geliştirici iş istasyonunuza yüklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1faf-108">To run the Contact Manager solution locally and to perform the other tasks described in this tutorial, you'll need to install this software on your developer workstation:</span></span>

- <span data-ttu-id="a1faf-109">Visual Studio 2010 Service Pack 1, Premium veya Ultimate sürümü</span><span class="sxs-lookup"><span data-stu-id="a1faf-109">Visual Studio 2010 Service Pack 1, Premium or Ultimate Edition</span></span>
- <span data-ttu-id="a1faf-110">Internet Information Services (IIS) 7,5 Express</span><span class="sxs-lookup"><span data-stu-id="a1faf-110">Internet Information Services (IIS) 7.5 Express</span></span>
- <span data-ttu-id="a1faf-111">SQL Server Express 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a1faf-111">SQL Server Express 2008 R2</span></span>
- <span data-ttu-id="a1faf-112">IIS Web Dağıtım Aracı (Web Dağıtımı) 2,1 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="a1faf-112">IIS Web Deployment Tool (Web Deploy) 2.1 or later</span></span>
- <span data-ttu-id="a1faf-113">ASP.NET 4.0</span><span class="sxs-lookup"><span data-stu-id="a1faf-113">ASP.NET 4.0</span></span>
- <span data-ttu-id="a1faf-114">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="a1faf-114">ASP.NET MVC 3</span></span>
- <span data-ttu-id="a1faf-115">.NET Framework 4</span><span class="sxs-lookup"><span data-stu-id="a1faf-115">.NET Framework 4</span></span>
- <span data-ttu-id="a1faf-116">.NET Framework 3.5 SP1</span><span class="sxs-lookup"><span data-stu-id="a1faf-116">.NET Framework 3.5 SP1</span></span>

<span data-ttu-id="a1faf-117">Visual Studio 2010 hariç olmak üzere, [Web Platformu Yükleyicisi](https://go.microsoft.com/?linkid=9805118)aracılığıyla bu ürünlerin ve bileşenlerin en son sürümlerini indirip yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1faf-117">With the exception of Visual Studio 2010, you can download and install the latest versions of all of these products and components through the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

## <a name="download-and-extract-the-solution"></a><span data-ttu-id="a1faf-118">Çözümü indirme ve ayıklama</span><span class="sxs-lookup"><span data-stu-id="a1faf-118">Download and Extract the Solution</span></span>

<span data-ttu-id="a1faf-119">[Burada](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0)MSDN kod galerisinden Contact Manager örnek uygulamasını indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1faf-119">You can download the Contact Manager sample application from the MSDN Code Gallery [here](https://code.msdn.microsoft.com/Deploying-Web-Applications-9d9093c0).</span></span>

## <a name="configure-and-run-the-solution"></a><span data-ttu-id="a1faf-120">Çözümü yapılandırma ve çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a1faf-120">Configure and Run the Solution</span></span>

<span data-ttu-id="a1faf-121">Yerel makinenizde Contact Manager çözümünü yapılandırmak ve çalıştırmak için aşağıdaki üst düzey adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1faf-121">To configure and run the Contact Manager solution on your local machine, you'll need to perform these high-level steps:</span></span>

1. <span data-ttu-id="a1faf-122">Henüz bir tane yoksa, üyelik ve rol yönetimi özellikleri etkin olan bir yerel ASP.NET uygulama Hizmetleri veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a1faf-122">If you don't have one already, create a local ASP.NET application services database with the membership and role management features enabled.</span></span>
2. <span data-ttu-id="a1faf-123">*Web. config* dosyalarındaki bağlantı dizelerini yerel SQL Server Express örneğinizi gösterecek şekilde düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="a1faf-123">Edit connection strings in the *web.config* files to point to your local SQL Server Express instance.</span></span>
3. <span data-ttu-id="a1faf-124">Çözümü Visual Studio 2010 ' dan çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-124">Run the solution from Visual Studio 2010.</span></span>

<span data-ttu-id="a1faf-125">Bu bölümün geri kalanında, bu görevlerin her birini tamamlamaya yönelik daha fazla rehberlik sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a1faf-125">The remainder of this section provides more guidance on how to complete each of these tasks.</span></span>

<span data-ttu-id="a1faf-126">**Uygulama Hizmetleri veritabanını oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="a1faf-126">**To create the application services database**</span></span>

1. <span data-ttu-id="a1faf-127">Bir Visual Studio 2010 komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-127">Open a Visual Studio 2010 command prompt.</span></span> <span data-ttu-id="a1faf-128">Bunu yapmak için, **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft Visual Studio 2010**' ye tıklayın, **Visual Studio Araçları**' a ve ardından **Visual Studio komut istemi (2010)** ' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-128">To do this, on the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, click **Visual Studio Tools**, and then click **Visual Studio Command Prompt (2010)**.</span></span>
2. <span data-ttu-id="a1faf-129">Komut isteminde şu komutu yazın ve ENTER tuşuna basın:</span><span class="sxs-lookup"><span data-stu-id="a1faf-129">At the command prompt, type this command, and then press Enter:</span></span>

    [!code-console[Main](setting-up-the-contact-manager-solution/samples/sample1.cmd)]

    1. <span data-ttu-id="a1faf-130">Veritabanı sunucunuzun bağlantı dizesini belirtmek için **– C** anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-130">Use the **–C** switch to specify the connection string for your database server.</span></span>
    2. <span data-ttu-id="a1faf-131">Veritabanına eklemek istediğiniz uygulama Hizmetleri özelliklerini belirtmek için **– A** anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-131">Use the **–A** switch to specify the application services features you want to add to the database.</span></span> <span data-ttu-id="a1faf-132">Bu durumda, **m** üyelik sağlayıcısı için destek eklemek istediğinizi ve **r** 'nin rol yöneticisi için destek eklemek istediğinizi belirtir.</span><span class="sxs-lookup"><span data-stu-id="a1faf-132">In this case, **m** indicates that you want to add support for the membership provider and **r** indicates that you want to add support for the role manager.</span></span>
    3. <span data-ttu-id="a1faf-133">Uygulama Hizmetleri veritabanınız için bir ad belirtmek üzere **– d** anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-133">Use the **–d** switch to specify a name for your application services database.</span></span> <span data-ttu-id="a1faf-134">Bu anahtarı atlarsanız, yardımcı program varsayılan **aspnetdb**adı ile bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1faf-134">If you omit this switch, the utility will create a database with the default name of **aspnetdb**.</span></span>
3. <span data-ttu-id="a1faf-135">Veritabanı başarılı bir şekilde oluşturulduğunda, komut isteminde bir onay gösterilecektir.</span><span class="sxs-lookup"><span data-stu-id="a1faf-135">When the database has been created successfully, the command prompt will show a confirmation.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="a1faf-136">ASPNET\_regsql yardımcı programı hakkında daha fazla bilgi için bkz. [ASP.NET SQL Server kayıt aracı (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="a1faf-136">For more information on the aspnet\_regsql utility, see [ASP.NET SQL Server Registration Tool (Aspnet\_regsql.exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).</span></span>

<span data-ttu-id="a1faf-137">Bir sonraki adım, Contact Manager çözümündeki bağlantı dizelerinin yerel SQL Server Express yerel örneğinizi işaret ettiğinizden emin olmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1faf-137">The next step is to make sure that the connection strings in the Contact Manager solution point to your local instance of SQL Server Express.</span></span>

<span data-ttu-id="a1faf-138">**Bağlantı dizelerini güncelleştirmek için**</span><span class="sxs-lookup"><span data-stu-id="a1faf-138">**To update the connection strings**</span></span>

1. <span data-ttu-id="a1faf-139">Visual Studio 2010 ' de Contact Manager çözümünü açın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-139">Open the Contact Manager solution in Visual Studio 2010.</span></span>
2. <span data-ttu-id="a1faf-140">**Çözüm Gezgini** penceresinde **ContactManager. Mvc** projesini genişletin ve **Web. config** düğümüne çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-140">In the **Solution Explorer** window, expand the **ContactManager.Mvc** project, and then double-click the **Web.config** node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a1faf-141">ContactManager. Mvc projesi iki *Web. config* dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="a1faf-141">The ContactManager.Mvc project includes two *web.config* files.</span></span> <span data-ttu-id="a1faf-142">Proje düzeyi dosyasını düzenlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1faf-142">You need to edit the project-level file.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image2.png)
3. <span data-ttu-id="a1faf-143">**ConnectionStrings** öğesinde, **ApplicationServices** adlı bağlantı dizesinin yerel ASP.NET uygulama hizmetleri veritabanınıza işaret ettiğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-143">In the **connectionStrings** element, verify that the connection string named **ApplicationServices** points to your local ASP.NET application services database.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample2.xml)]
4. <span data-ttu-id="a1faf-144">**Çözüm Gezgini** penceresinde **ContactManager. Service** projesini genişletin ve **Web. config** düğümüne çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-144">In the **Solution Explorer** window, expand the **ContactManager.Service** project, and then double-click the **Web.config** node.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image3.png)
5. <span data-ttu-id="a1faf-145">**ConnectionStrings** öğesinde, **contactmanagercontext**adlı bağlantı dizesinde, **veri kaynağı** özelliğinin yerel SQL Server Express olarak ayarlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-145">In the **connectionStrings** element, in the connection string named **ContactManagerContext**, verify that the **Data Source** property is set to your local instance of SQL Server Express.</span></span> <span data-ttu-id="a1faf-146">Bağlantı dizesinde başka herhangi bir şeyi değiştirmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a1faf-146">You don't need to change anything else in the connection string.</span></span>

    [!code-xml[Main](setting-up-the-contact-manager-solution/samples/sample3.xml)]
6. <span data-ttu-id="a1faf-147">Tüm açık dosyaları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a1faf-147">Save all open files.</span></span>

<span data-ttu-id="a1faf-148">Şimdi yerel makinenizde Contact Manager çözümünü çalıştırmaya hazır olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1faf-148">You should now be ready to run the Contact Manager solution on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="a1faf-149">Uygulama Hizmetleri veritabanı oluşturmadan önce bu adımları izlerseniz, ASP.NET ilk kez kullanıcı oluşturmaya çalıştığınızda veritabanını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1faf-149">If you follow these steps without first creating an application services database, ASP.NET will create the database the first time you attempt to create a user.</span></span> <span data-ttu-id="a1faf-150">Ancak, veritabanının el ile oluşturulması, desteklemek istediğiniz uygulama hizmetleri özellik kümesi üzerinde çok daha fazla denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1faf-150">However, manually creating the database gives you a lot more control over the application services feature set you want to support.</span></span>

<span data-ttu-id="a1faf-151">**Contact Manager çözümünü çalıştırmak için**</span><span class="sxs-lookup"><span data-stu-id="a1faf-151">**To run the Contact Manager solution**</span></span>

1. <span data-ttu-id="a1faf-152">Visual Studio 2010 ' de F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-152">In Visual Studio 2010, press F5.</span></span>
2. <span data-ttu-id="a1faf-153">Internet Explorer başlatılır ve Contact Manager ASP.NET MVC 3 uygulamasının URL 'sini ister.</span><span class="sxs-lookup"><span data-stu-id="a1faf-153">Internet Explorer starts up and requests the URL of the Contact Manager ASP.NET MVC 3 application.</span></span> <span data-ttu-id="a1faf-154">Varsayılan olarak, uygulama **tüm kişiler** sayfasını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a1faf-154">By default, the application displays the **All Contacts** page.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image4.png)
3. <span data-ttu-id="a1faf-155">Birkaç kişi ekleyin ve sonra uygulamanın beklendiği gibi çalıştığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-155">Add a few contacts, and then verify that the application works as expected.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image5.png)
4. <span data-ttu-id="a1faf-156">`http://localhost:50114/Account/Register` gidin (uygulamayı farklı bir bağlantı noktasında barındırıyorsanız URL 'YI ayarlayın).</span><span class="sxs-lookup"><span data-stu-id="a1faf-156">Browse to `http://localhost:50114/Account/Register` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="a1faf-157">Bir Kullanıcı adı, e-posta adresi ve parola ekleyin ve bir hesabı başarıyla kaydedebildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-157">Add a user name, email address, and password, and verify that you're able to register an account successfully.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image6.png)
5. <span data-ttu-id="a1faf-158">`http://localhost:50114/Account/LogOn` gidin (uygulamayı farklı bir bağlantı noktasında barındırıyorsanız URL 'YI ayarlayın).</span><span class="sxs-lookup"><span data-stu-id="a1faf-158">Browse to `http://localhost:50114/Account/LogOn` (adjust the URL if you're hosting the application on a different port).</span></span> <span data-ttu-id="a1faf-159">Yeni oluşturduğunuz hesabı kullanarak oturum açabildiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-159">Verify that you're able to log on using the account you just created.</span></span>

    ![](setting-up-the-contact-manager-solution/_static/image7.png)
6. <span data-ttu-id="a1faf-160">Hata ayıklamayı durdurmak için Internet Explorer 'ı kapatın.</span><span class="sxs-lookup"><span data-stu-id="a1faf-160">Close Internet Explorer to stop debugging.</span></span>

## <a name="conclusion"></a><span data-ttu-id="a1faf-161">Sonuç</span><span class="sxs-lookup"><span data-stu-id="a1faf-161">Conclusion</span></span>

<span data-ttu-id="a1faf-162">Bu noktada, Contact Manager çözümünün yerel makinenizde çalışacak şekilde tam olarak yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a1faf-162">At this point, the Contact Manager solution should be fully configured to run on your local machine.</span></span> <span data-ttu-id="a1faf-163">Bu öğreticideki diğer konularda çalışırken çözümü başvuru olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1faf-163">You can use the solution as a reference when you work through the other topics in this tutorial.</span></span>

<span data-ttu-id="a1faf-164">Bir sonraki konu, [Proje dosyasını anlamak](understanding-the-project-file.md)için, dağıtım işlemini denetlemek üzere Contact Manager çözümünde özel Microsoft Build Engine (MSBuild) proje dosyalarını nasıl kullanabileceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="a1faf-164">The next topic, [Understanding the Project File](understanding-the-project-file.md), explains how you can use the custom Microsoft Build Engine (MSBuild) project files within the Contact Manager solution to control the deployment process.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1faf-165">[Önceki](the-contact-manager-solution.md)
> [İleri](understanding-the-project-file.md)</span><span class="sxs-lookup"><span data-stu-id="a1faf-165">[Previous](the-contact-manager-solution.md)
[Next](understanding-the-project-file.md)</span></span>
