---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: TFS 'de bir takım projesi oluşturma | Microsoft Docs
author: jrjlee
description: Bu konu, Team Foundation Server (TFS) 2010 ' de yeni bir takım projesi oluşturmayı açıklar.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639659"
---
# <a name="creating-a-team-project-in-tfs"></a><span data-ttu-id="ecaab-103">TFS’de Takım Projesi Oluşturma</span><span class="sxs-lookup"><span data-stu-id="ecaab-103">Creating a Team Project in TFS</span></span>

<span data-ttu-id="ecaab-104">[Jason Lee](https://github.com/jrjlee) tarafından</span><span class="sxs-lookup"><span data-stu-id="ecaab-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="ecaab-105">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="ecaab-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ecaab-106">Bu konu, Team Foundation Server (TFS) 2010 ' de yeni bir takım projesi oluşturmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="ecaab-106">This topic describes how to create a new team project in Team Foundation Server (TFS) 2010.</span></span>

<span data-ttu-id="ecaab-107">Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.</span><span class="sxs-lookup"><span data-stu-id="ecaab-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="ecaab-108">Göreve genel bakış</span><span class="sxs-lookup"><span data-stu-id="ecaab-108">Task Overview</span></span>

<span data-ttu-id="ecaab-109">TFS 'de yeni bir takım projesi sağlamak ve kullanmak için, bu üst düzey adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ecaab-109">To provision and use a new team project in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="ecaab-110">Yeni takım projesini oluşturacak kullanıcıya izin verin.</span><span class="sxs-lookup"><span data-stu-id="ecaab-110">Grant permissions to the user who will create the new team project.</span></span>
- <span data-ttu-id="ecaab-111">Takım projesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ecaab-111">Create the team project.</span></span>
- <span data-ttu-id="ecaab-112">Proje üzerinde çalışacak takım üyelerine izin verin.</span><span class="sxs-lookup"><span data-stu-id="ecaab-112">Grant permissions to the team members who will work on the project.</span></span>
- <span data-ttu-id="ecaab-113">Bazı içerikleri iade edin.</span><span class="sxs-lookup"><span data-stu-id="ecaab-113">Check in some content.</span></span>

<span data-ttu-id="ecaab-114">Bu konu, bu yordamların nasıl gerçekleştirileceğini gösterir ve her yordamdan sorumlu olabilecek Kullanıcı ve iş rollerini belirler.</span><span class="sxs-lookup"><span data-stu-id="ecaab-114">This topic will show you how to perform these procedures, and it will identify the users and job roles that are likely to be responsible for each procedure.</span></span> <span data-ttu-id="ecaab-115">Kuruluşunuzun yapısına bağlı olarak, bu görevlerin her biri farklı bir kişinin sorumluluğunda olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-115">Be aware that, depending on the structure of your organization, each of these tasks may be the responsibility of a different person.</span></span>

<span data-ttu-id="ecaab-116">Bu konudaki görevler ve izlenecek yollar, TFS 'yi yüklediğinizi ve yapılandırdığınızı ve yapılandırma sürecinin bir parçası olarak bir takım projesi koleksiyonu oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="ecaab-116">The tasks and walkthroughs in this topic assume that you've installed and configured TFS, and that you've created a team project collection as part of the configuration process.</span></span> <span data-ttu-id="ecaab-117">Bu varsayımlar hakkında daha fazla bilgi edinmek ve senaryo hakkında daha genel arka plan bilgileri için bkz. [Web dağıtımı IÇIN TFS Build Server yapılandırma](configuring-a-tfs-build-server-for-web-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ecaab-117">For more information on these assumptions, and for more general background information on the scenario, see [Configure a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span>

## <a name="grant-permissions-to-the-team-project-creator"></a><span data-ttu-id="ecaab-118">Takım projesi oluşturucusuna Izin verme</span><span class="sxs-lookup"><span data-stu-id="ecaab-118">Grant Permissions to the Team Project Creator</span></span>

<span data-ttu-id="ecaab-119">Yeni bir takım projesi oluşturmak için bu izinlere ihtiyacınız vardır:</span><span class="sxs-lookup"><span data-stu-id="ecaab-119">In order to create a new team project, you need these permissions:</span></span>

- <span data-ttu-id="ecaab-120">TFS uygulama katmanında **Yeni proje oluştur** izninizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-120">You must have the **Create new projects** permission on the TFS application tier.</span></span> <span data-ttu-id="ecaab-121">Bu izni genellikle **proje koleksiyonu yöneticileri** TFS grubuna kullanıcı ekleyerek verirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecaab-121">You typically grant this permission by adding users to the **Project Collection Administrators** TFS group.</span></span> <span data-ttu-id="ecaab-122">**Team Foundation yöneticileri** genel grubu da bu izni içerir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-122">The **Team Foundation Administrators** global group also includes this permission.</span></span>
- <span data-ttu-id="ecaab-123">TFS takım projesi koleksiyonuna karşılık gelen SharePoint site koleksiyonu içinde yeni ekip siteleri oluşturmak için izninizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-123">You must have permission to create new team sites within the SharePoint site collection that corresponds to the TFS team project collection.</span></span> <span data-ttu-id="ecaab-124">Bu izni genellikle, kullanıcıyı SharePoint site koleksiyonunda **tam denetim** haklarına sahip bir SharePoint grubuna ekleyerek verirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecaab-124">You typically grant this permission by adding the user to a SharePoint group with **Full Control** rights on the SharePoint site collection.</span></span>
- <span data-ttu-id="ecaab-125">SQL Server Reporting Services özellikler kullanıyorsanız, Raporlama Hizmetleri 'nde **Team Foundation Içerik Yöneticisi** rolünün bir üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-125">If you're using SQL Server Reporting Services features, you must be a member of the **Team Foundation Content Manager** role in Reporting Services.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="ecaab-126">Bu yordamları kim gerçekleştiriyor?</span><span class="sxs-lookup"><span data-stu-id="ecaab-126">Who Performs These Procedures?</span></span>

<span data-ttu-id="ecaab-127">Genellikle, TFS dağıtımını yöneten kişi veya grup bu yordamları da gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-127">Typically, the person or group who administers the TFS deployment also performs these procedures.</span></span>

<span data-ttu-id="ecaab-128">Bu, yüksek ayrıcalıklı bir izin kümesi olduğundan, yeni takım projeleri genellikle bir TFS dağıtımını yönetme sorumluluğunu içeren küçük bir kullanıcı alt kümesi tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ecaab-128">Because this is a highly privileged set of permissions, new team projects are typically created by a small subset of users with responsibility for administering a TFS deployment.</span></span> <span data-ttu-id="ecaab-129">Geliştiricilere, genellikle yeni takım projeleri oluşturmak için gereken izinler verilmez.</span><span class="sxs-lookup"><span data-stu-id="ecaab-129">Developers will not usually be granted the permissions required to create new team projects.</span></span>

### <a name="grant-permissions-in-tfs"></a><span data-ttu-id="ecaab-130">TFS 'de Izin verme</span><span class="sxs-lookup"><span data-stu-id="ecaab-130">Grant Permissions in TFS</span></span>

<span data-ttu-id="ecaab-131">Bir kullanıcının yeni takım projeleri oluşturmasını etkinleştirmek istiyorsanız, ilk üst düzey görev, kullanıcıyı takım projesi koleksiyonu için **proje koleksiyonu yöneticileri** grubuna eklemektir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-131">If you want to enable a user to create new team projects, the first high-level task is to add the user to the **Project Collection Administrators** group for the team project collection.</span></span>

<span data-ttu-id="ecaab-132">**Proje koleksiyonu yöneticileri grubuna bir kullanıcı eklemek için**</span><span class="sxs-lookup"><span data-stu-id="ecaab-132">**To add a user to the Project Collection Administrators group**</span></span>

1. <span data-ttu-id="ecaab-133">TFS sunucusunda, **Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft Team Foundation Server 2010**' a ve ardından **Team Foundation Yönetim Konsolu**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-133">On the TFS server, on the **Start** menu, point to **All Programs**, click **Microsoft Team Foundation Server 2010**, and then click **Team Foundation Administration Console**.</span></span>
2. <span data-ttu-id="ecaab-134">Gezinti ağacı görünümünde, **uygulama katmanı**' nı genişletin ve ardından **Takım projesi koleksiyonları**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-134">In the navigation tree view, expand **Application Tier**, and then click **Team Project Collections**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. <span data-ttu-id="ecaab-135">**Takım projesi koleksiyonları** bölmesinde, yönetmek istediğiniz takım projesi koleksiyonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="ecaab-135">In the **Team Project Collections** pane, select the team project collection you want to manage.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. <span data-ttu-id="ecaab-136">**Genel** sekmesinde **Grup üyeliği**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-136">On the **General** tab, click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. <span data-ttu-id="ecaab-137">**Genel gruplar** iletişim kutusunda, **proje koleksiyonu yöneticileri** grubunu seçin ve ardından **Özellikler**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-137">In the **Global Groups** dialog box, select the **Project Collection Administrators** group, and then click **Properties**.</span></span>
6. <span data-ttu-id="ecaab-138">**Team Foundation Server grubu özellikleri** Iletişim kutusunda **Windows kullanıcısı veya grubu**' nu seçin ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-138">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. <span data-ttu-id="ecaab-139">**Kullanıcıları, bilgisayarları veya grupları seç** iletişim kutusunda, yeni takım projeleri oluşturmak istediğiniz kullanıcının Kullanıcı adını yazın, **adları denetle**' ye tıklayın ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-139">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to be able to create new team projects, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. <span data-ttu-id="ecaab-140">**Team Foundation Server grubu özellikleri** Iletişim kutusunda **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-140">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
9. <span data-ttu-id="ecaab-141">**Genel gruplar** Iletişim kutusunda **Kapat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-141">In the **Global Groups** dialog box, click **Close**.</span></span>

### <a name="grant-permissions-in-sharepoint-services"></a><span data-ttu-id="ecaab-142">SharePoint hizmetlerinde Izin verme</span><span class="sxs-lookup"><span data-stu-id="ecaab-142">Grant Permissions in SharePoint Services</span></span>

<span data-ttu-id="ecaab-143">Daha sonra, TFS takım projesi koleksiyonunuza karşılık gelen SharePoint site koleksiyonunda yeni ekip siteleri oluşturmak için kullanıcıya izin vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-143">Next, you need to give the user permission to create new team sites in the SharePoint site collection that corresponds to your TFS team project collection.</span></span>

<span data-ttu-id="ecaab-144">**SharePoint site koleksiyonunda tam denetim izinleri vermek için**</span><span class="sxs-lookup"><span data-stu-id="ecaab-144">**To grant Full Control permissions on the SharePoint site collection**</span></span>

1. <span data-ttu-id="ecaab-145">Team Foundation Server Yönetim Konsolu, **Takım projesi koleksiyonları** sayfasında, yönetmek istediğiniz takım projesi koleksiyonunu seçin.</span><span class="sxs-lookup"><span data-stu-id="ecaab-145">In the Team Foundation Server Administration Console, on the **Team Project Collections** page, select the team project collection you want to manage.</span></span>
2. <span data-ttu-id="ecaab-146">**SharePoint sitesi** sekmesinde, **geçerli varsayılan site konumu** URL 'sinin değerini aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="ecaab-146">On the **SharePoint Site** tab, note the value of the **Current Default Site Location** URL.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. <span data-ttu-id="ecaab-147">Internet Explorer 'ı açın ve ardından 2. adımda not ettiğiniz URL 'ye gidin.</span><span class="sxs-lookup"><span data-stu-id="ecaab-147">Open Internet Explorer, and then go to the URL you noted in step 2.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecaab-148">Takım projesi koleksiyonunu oluşturan kullanıcı olarak Windows 'da oturum açmadıysanız, devam edebilmek için bu kullanıcı olarak SharePoint 'te oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-148">If you're not logged on to Windows as the user who created the team project collection, you'll need to sign in to SharePoint as this user in order to continue.</span></span>
4. <span data-ttu-id="ecaab-149">**Site eylemleri** menüsünde, **site ayarları**' na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-149">On the **Site Actions** menu, click **Site Settings**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. <span data-ttu-id="ecaab-150">**Site ayarları** sayfasında, **Kullanıcılar ve Izinler**altında, **kişiler ve gruplar**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-150">On the **Site Settings** page, under **Users and Permissions**, click **People and groups**.</span></span>
6. <span data-ttu-id="ecaab-151">Sol gezinti panelinde, **gruplar**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-151">In the left navigation panel, click **Groups**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. <span data-ttu-id="ecaab-152">**Kişiler ve gruplar: tüm gruplar** sayfasında, **Bu site için grupları ayarla**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-152">On the **People and Groups: All Groups** page, click **Set Up Groups for this Site**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > <span data-ttu-id="ecaab-153">Çift HTTP kodlama hatası nedeniyle bir <strong>http 404 bulunamadı</strong> hatası alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecaab-153">You may receive an <strong>HTTP 404 Not Found</strong> error due to a double HTTP encoding bug.</span></span> <span data-ttu-id="ecaab-154">Bu gerçekleşirse URL 'YI şu şekilde değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ecaab-154">If this occurs, replace the URL with this:</span></span>   
   > <span data-ttu-id="ecaab-155">`[site_collection_URL]/_layouts/permsetup.aspx` örneğin:</span><span class="sxs-lookup"><span data-stu-id="ecaab-155">`[site_collection_URL]/_layouts/permsetup.aspx` For example:</span></span>  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. <span data-ttu-id="ecaab-156">**Bu sitenin gruplarını ayarla** sayfasında, takım projelerini oluşturacak kullanıcıyı **sahipler** grubuna ekleyin ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-156">On the **Set Up Groups for this Site** page, add the user who will create team projects to the **Owners** group, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image10.png)

<span data-ttu-id="ecaab-157">Kullanıcıların bir takım projesi koleksiyonu içinde yeni takım projeleri oluşturmalarına olanak sağlama hakkında daha fazla bilgi için bkz. [Takım projesi koleksiyonları Için yönetici Izinlerini ayarlama](https://msdn.microsoft.com/library/dd547204.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecaab-157">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span>

## <a name="create-a-new-team-project-and-add-users"></a><span data-ttu-id="ecaab-158">Yeni bir takım projesi oluşturun ve kullanıcı ekleyin</span><span class="sxs-lookup"><span data-stu-id="ecaab-158">Create a New Team Project and Add Users</span></span>

<span data-ttu-id="ecaab-159">Gerekli izinlere sahip olduktan sonra, yeni bir takım projesi oluşturmak için Visual Studio 2010 ' de **Takım Gezgini** penceresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecaab-159">Once you have the necessary permissions, you can use the **Team Explorer** window in Visual Studio 2010 to create a new team project.</span></span> <span data-ttu-id="ecaab-160">Bu yaklaşım, gerekli tüm bilgileri toplayan ve TFS, SharePoint ve SQL Server Reporting Services gerekli görevleri gerçekleştiren bir sihirbaz sağlar.</span><span class="sxs-lookup"><span data-stu-id="ecaab-160">This approach provides a wizard that collects all the required information and performs the necessary tasks in TFS, SharePoint, and SQL Server Reporting Services.</span></span> <span data-ttu-id="ecaab-161">Ayrıca, kullanıcıların içerik eklemesini ve değiştirmesini sağlamak için, geliştirici ekibinin üyelerine yeni takım projesi için izinler vermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-161">You'll also need to grant permissions on the new team project to members of the developer team, to enable them to add and modify content.</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="ecaab-162">Bu yordamları kim gerçekleştiriyor?</span><span class="sxs-lookup"><span data-stu-id="ecaab-162">Who Performs These Procedures?</span></span>

<span data-ttu-id="ecaab-163">Genellikle bir TFS Yöneticisi veya bir geliştirici ekibi lideri bu yordamları gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-163">Usually either a TFS administrator or a developer team leader performs these procedures.</span></span>

### <a name="create-a-new-team-project"></a><span data-ttu-id="ecaab-164">Yeni takım projesi oluştur</span><span class="sxs-lookup"><span data-stu-id="ecaab-164">Create a New Team Project</span></span>

<span data-ttu-id="ecaab-165">Sonraki yordamda TFS 2010 ' de yeni bir takım projesi oluşturma işlemi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ecaab-165">The next procedure describes how to create a new team project in TFS 2010.</span></span>

<span data-ttu-id="ecaab-166">**Yeni bir takım projesi oluşturmak için**</span><span class="sxs-lookup"><span data-stu-id="ecaab-166">**To create a new team project**</span></span>

1. <span data-ttu-id="ecaab-167">**Başlat** menüsünde **tüm programlar**' ın üzerine gelin, **Microsoft Visual Studio 2010**' ye tıklayın, **Microsoft Visual Studio 2010**' e sağ tıklayın ve ardından **yönetici olarak çalıştır**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-167">On the **Start** menu, point to **All Programs**, click **Microsoft Visual Studio 2010**, right-click **Microsoft Visual Studio 2010**, and then click **Run as administrator**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecaab-168">Visual Studio 2010 ' ı yönetici olarak çalıştırmazsanız, son adımda yeni takım projesi Sihirbazı başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ecaab-168">If you don't run Visual Studio 2010 as an administrator, the New Team Project Wizard will fail on the last step.</span></span>
2. <span data-ttu-id="ecaab-169">**Kullanıcı hesabı denetimi** iletişim kutusu görüntülenirse, **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-169">If the **User Account Control** dialog box appears, click **Yes**.</span></span>
3. <span data-ttu-id="ecaab-170">Visual Studio 'da, **Takım** menüsünde **Team Foundation Server Bağlan**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-170">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecaab-171">TFS sunucusuna zaten bir bağlantı yapılandırdıysanız 4-7 arasındaki adımları atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecaab-171">If you have already configured a connection to a TFS server, you can omit steps 4-7.</span></span>
4. <span data-ttu-id="ecaab-172">**Takım projesi bağlantısı** Iletişim kutusunda **sunucular**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-172">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
5. <span data-ttu-id="ecaab-173">**Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-173">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
6. <span data-ttu-id="ecaab-174">**Team Foundation Server Ekle** ILETIŞIM kutusunda TFS örneğinizin ayrıntılarını belirtin ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-174">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. <span data-ttu-id="ecaab-175">**Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Kapat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-175">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
8. <span data-ttu-id="ecaab-176">**Takım Projesine Bağlan** iletişim kutusunda, bağlanmak istediğiniz TFS örneğini seçin, eklemek istediğiniz takım projesi koleksiyonunu seçin ve ardından **Bağlan**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-176">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection you want to add to, and then click **Connect**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. <span data-ttu-id="ecaab-177">**Takım Gezgini** penceresinde, takım projesi koleksiyonuna sağ tıklayın ve sonra **Yeni takım projesi**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-177">In the **Team Explorer** window, right-click the team project collection, and then click **New Team Project**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. <span data-ttu-id="ecaab-178">**Yeni takım projesi** iletişim kutusunda, takım projesi için bir ad ve açıklama girin ve ardından **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-178">In the **New Team Project** dialog box, provide a name and a description for the team project, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecaab-179">Takım projeniz boşluk içeriyorsa, çıkış yolundan paketleri dağıtmak için Internet Information Services (IIS) Web Dağıtım aracı 'nı (Web Dağıtımı) kullandığınızda bazı sorunlar yaşayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecaab-179">If your team project includes spaces, you may face some issues when you come to use the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to deploy packages from the output path.</span></span> <span data-ttu-id="ecaab-180">Yoldaki boşluklar, Web Dağıtımı komutlarının çalıştırılması çok daha zor hale gelir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-180">Spaces in the path can make it a lot more difficult to run Web Deploy commands.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. <span data-ttu-id="ecaab-181">**Işlem şablonu seçin** sayfasında, geliştirme sürecini yönetmek için kullanmak istediğiniz işlem şablonunu seçin ve ardından **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-181">On the **Select a Process Template** page, select the process template that you want to use to manage the development process, and then click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ecaab-182">TFS için işlem şablonları hakkında daha fazla bilgi için bkz. [Işlem şablonları ve araçları](https://msdn.microsoft.com/vstudio/aa718795).</span><span class="sxs-lookup"><span data-stu-id="ecaab-182">For more information on process templates for TFS, see [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).</span></span>
12. <span data-ttu-id="ecaab-183">**Takım sitesi ayarları** sayfasında, varsayılan ayarları değiştirmeden bırakın ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-183">On the **Team Site Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
13. <span data-ttu-id="ecaab-184">Bu ayar, TFS takım projesiyle ilişkili bir SharePoint ekip sitesi oluşturur veya tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ecaab-184">This setting creates, or identifies, a SharePoint team site that is associated with the TFS team project.</span></span> <span data-ttu-id="ecaab-185">Geliştirme ekibiniz bu siteyi belgeleri yönetmek, tartışma zincirlerine katılmak, wiki sayfaları oluşturmak ve kodla ilgili olmayan çeşitli diğer görevleri gerçekleştirmek için kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-185">Your development team can use this site to manage documentation, participate in discussion threads, create wiki pages, and perform various other tasks that are not related to code.</span></span> <span data-ttu-id="ecaab-186">Daha fazla bilgi için bkz. [SharePoint ürünleri ve Team Foundation Server arasındaki etkileşimler](https://msdn.microsoft.com/library/ms253177.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecaab-186">For more information, see [Interactions Between SharePoint Products and Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).</span></span>
14. <span data-ttu-id="ecaab-187">**Kaynak denetimi ayarlarını belirtin** sayfasında, varsayılan ayarları değiştirmeden bırakın ve **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-187">On the **Specify Source Control Settings** page, leave the default settings unchanged, and then click **Next**.</span></span>
15. <span data-ttu-id="ecaab-188">Bu ayar, TFS klasör hiyerarşisinde, içeriğiniz için bir kök klasör olarak görev yapacak konumu tanımlar veya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ecaab-188">This setting identifies or creates the location in the TFS folder hierarchy that will act as a root folder for your content.</span></span>
16. <span data-ttu-id="ecaab-189">**Takım projesi ayarlarını Onayla** sayfasında, **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-189">On the **Confirm Team Project Settings** page, click **Finish**.</span></span>
17. <span data-ttu-id="ecaab-190">Yeni takım projesi başarıyla oluşturulduğunda, **Takım projesi oluşturulan** sayfasında **Kapat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-190">When the new team project is successfully created, on the **Team Project Created** page, click **Close**.</span></span>

### <a name="add-users-to-a-team-project"></a><span data-ttu-id="ecaab-191">Takım projesine Kullanıcı ekleme</span><span class="sxs-lookup"><span data-stu-id="ecaab-191">Add Users to a Team Project</span></span>

<span data-ttu-id="ecaab-192">Yeni takım projesini oluşturduğunuza göre, kullanıcılara içeriğe ekleme ve işbirliği yapmaya başlamasını sağlamak için izinler verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ecaab-192">Now that you've created the new team project, you can grant permissions to users to enable them to start adding and collaborating on content.</span></span>

<span data-ttu-id="ecaab-193">**Bir takım projesine Kullanıcı eklemek için**</span><span class="sxs-lookup"><span data-stu-id="ecaab-193">**To add users to a team project**</span></span>

1. <span data-ttu-id="ecaab-194">Visual Studio 2010 ' de, **Takım Gezgini** penceresinde, takım projesine sağ tıklayın, **Takım Projesi Ayarları**' nın üzerine gelin ve ardından **Grup üyeliği**' ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-194">In Visual Studio 2010, in the **Team Explorer** window, right-click the team project, point to **Team Project Settings**, and then click **Group Membership**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. <span data-ttu-id="ecaab-195">Bir kullanıcının kaynak denetimi altında kod eklemesini, değiştirmesini ve kaldırmasını sağlamak için, bunu **katkıda bulunanlar** grubuna eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-195">To enable a user to add, modify, and remove code under source control, you need to add him or her to the **Contributors** group.</span></span>
3. <span data-ttu-id="ecaab-196">**Proje grupları** iletişim kutusunda, **katkıda bulunanlar** grubunu seçin ve ardından **Özellikler**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-196">In the **Project Groups** dialog box, select the **Contributors** group, and then click **Properties**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. <span data-ttu-id="ecaab-197">**Team Foundation Server grubu özellikleri** Iletişim kutusunda **Windows kullanıcısı veya grubu**' nu seçin ve ardından **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-197">In the **Team Foundation Server Group Properties** dialog box, select **Windows User or Group**, and then click **Add**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. <span data-ttu-id="ecaab-198">**Kullanıcıları, bilgisayarları veya grupları seç** iletişim kutusunda, takım projesine eklemek istediğiniz kullanıcının Kullanıcı adını yazın, **adları denetle**' ye tıklayın ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-198">In the **Select Users, Computers, or Groups** dialog box, type the user name of the user you want to add to the team project, click **Check Names**, and then click **OK**.</span></span>

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. <span data-ttu-id="ecaab-199">**Team Foundation Server grubu özellikleri** Iletişim kutusunda **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-199">In the **Team Foundation Server Group Properties** dialog box, click **OK**.</span></span>
7. <span data-ttu-id="ecaab-200">**Proje grupları** Iletişim kutusunda **Kapat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ecaab-200">In the **Project Groups** dialog box, click **Close**.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ecaab-201">Sonuç</span><span class="sxs-lookup"><span data-stu-id="ecaab-201">Conclusion</span></span>

<span data-ttu-id="ecaab-202">Bu noktada, yeni takım projeniz kullanıma uygun hale gelmiştir ve geliştirici ekibiniz geliştirme sürecinde içerik eklemeye ve işbirliği yapmaya başlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ecaab-202">At this point, your new team project is ready to use, and your developer team can start adding content and collaborating on the development process.</span></span>

<span data-ttu-id="ecaab-203">Sonraki konu, [kaynak denetimine Içerik ekleme](adding-content-to-source-control.md), kaynak denetimine içerik eklemeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="ecaab-203">The next topic, [Adding Content to Source Control](adding-content-to-source-control.md), describes how to add content to source control.</span></span>

## <a name="further-reading"></a><span data-ttu-id="ecaab-204">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="ecaab-204">Further Reading</span></span>

<span data-ttu-id="ecaab-205">TFS 'de takım projeleri oluşturmaya yönelik daha geniş yönergeler için bkz. [Takım projesi oluşturma](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span><span class="sxs-lookup"><span data-stu-id="ecaab-205">For broader guidance on creating team projects in TFS, see [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx).</span></span> <span data-ttu-id="ecaab-206">Kullanıcıların bir takım projesi koleksiyonu içinde yeni takım projeleri oluşturmalarına olanak sağlama hakkında daha fazla bilgi için bkz. [Takım projesi koleksiyonları Için yönetici Izinlerini ayarlama](https://msdn.microsoft.com/library/dd547204.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecaab-206">For more information on enabling users to create new team projects within a team project collection, see [Set Administrator Permissions for Team Project Collections](https://msdn.microsoft.com/library/dd547204.aspx).</span></span> <span data-ttu-id="ecaab-207">Takım projelerine Kullanıcı ekleme hakkında daha fazla bilgi için bkz. [Takım projelerine Kullanıcı ekleme](https://msdn.microsoft.com/library/bb558971.aspx).</span><span class="sxs-lookup"><span data-stu-id="ecaab-207">For more information on adding users to team projects, see [Add Users to Team Projects](https://msdn.microsoft.com/library/bb558971.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ecaab-208">[Önceki](configuring-team-foundation-server-for-web-deployment.md)
> [İleri](adding-content-to-source-control.md)</span><span class="sxs-lookup"><span data-stu-id="ecaab-208">[Previous](configuring-team-foundation-server-for-web-deployment.md)
[Next](adding-content-to-source-control.md)</span></span>
