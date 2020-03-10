---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: Kaynak denetimine Içerik ekleme | Microsoft Docs
author: jrjlee
description: Bu konuda Team Foundation Server (TFS) 2010 ' de kaynak denetimine içerik ekleme açıklanmaktadır. Takım projesine nasıl çözüm ve proje ekleneceğini açıklar...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634465"
---
# <a name="adding-content-to-source-control"></a><span data-ttu-id="4d11b-104">Kaynak Denetimine İçerik Ekleme</span><span class="sxs-lookup"><span data-stu-id="4d11b-104">Adding Content to Source Control</span></span>

<span data-ttu-id="4d11b-105">[Jason Lee](https://github.com/jrjlee) tarafından</span><span class="sxs-lookup"><span data-stu-id="4d11b-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="4d11b-106">PDF 'YI indir</span><span class="sxs-lookup"><span data-stu-id="4d11b-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="4d11b-107">Bu konuda Team Foundation Server (TFS) 2010 ' de kaynak denetimine içerik ekleme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d11b-107">This topic explains how to add content to source control in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="4d11b-108">TFS 'deki bir ekip projesine çözüm ve proje eklemeyi açıklar ve kaynak denetimine çerçeveler veya derlemeler gibi dış bağımlılıkların nasıl ekleneceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4d11b-108">It describes how to add solutions and projects to a team project in TFS, and it explains how to add external dependencies like frameworks or assemblies to source control.</span></span>

<span data-ttu-id="4d11b-109">Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.</span><span class="sxs-lookup"><span data-stu-id="4d11b-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="4d11b-110">Göreve genel bakış</span><span class="sxs-lookup"><span data-stu-id="4d11b-110">Task Overview</span></span>

<span data-ttu-id="4d11b-111">Çoğu durumda, geliştirici ekibinin her üyesi kaynak denetimine içerik ekleyebilmelidir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-111">In most cases, every member of the developer team should be able to add content to source control.</span></span> <span data-ttu-id="4d11b-112">TFS 'deki kaynak denetimine bir çözüm eklemek için, bu üst düzey adımları gerçekleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="4d11b-112">To add a solution to source control in TFS, you'll need to complete these high-level steps:</span></span>

- <span data-ttu-id="4d11b-113">Bir takım projesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-113">Connect to a team project.</span></span>
- <span data-ttu-id="4d11b-114">Sunucudaki takım projesi klasörü yapısını yerel bilgisayarınızdaki bir klasör yapısına eşleyin.</span><span class="sxs-lookup"><span data-stu-id="4d11b-114">Map the team project folder structure on the server to a folder structure on your local computer.</span></span>
- <span data-ttu-id="4d11b-115">Çözümü ve içeriğini kaynak denetimine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d11b-115">Add the solution and its contents to source control.</span></span>
- <span data-ttu-id="4d11b-116">Kaynak denetimine herhangi bir dış bağımlılık ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4d11b-116">Add any external dependencies to source control.</span></span>

<span data-ttu-id="4d11b-117">Bu konu başlığı altında, bu yordamların nasıl gerçekleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-117">This topic will show you how to perform these procedures.</span></span>

<span data-ttu-id="4d11b-118">Bu konudaki görevler ve izlenecek yollar, içeriğinizi yönetmek için zaten yeni bir TFS takım projesi oluşturmuş olduğunuz varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4d11b-118">The tasks and walkthroughs in this topic assume that you've already created a new TFS team project to manage your content.</span></span> <span data-ttu-id="4d11b-119">Yeni bir takım projesi oluşturma hakkında daha fazla bilgi için bkz. [TFS 'de bir takım projesi oluşturma](creating-a-team-project-in-tfs.md).</span><span class="sxs-lookup"><span data-stu-id="4d11b-119">For more information on creating a new team project, see [Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span>

### <a name="who-performs-these-procedures"></a><span data-ttu-id="4d11b-120">Bu yordamları kim gerçekleştiriyor?</span><span class="sxs-lookup"><span data-stu-id="4d11b-120">Who Performs These Procedures?</span></span>

<span data-ttu-id="4d11b-121">Çoğu durumda, geliştirici ekibinin her üyesi belirli takım projeleri içinde içerik ekleyip değiştirebilmelidir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-121">In most cases, every member of the developer team should be able to add and modify content within specific team projects.</span></span>

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a><span data-ttu-id="4d11b-122">Bir takım projesine bağlanın ve bir klasör eşlemesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="4d11b-122">Connect to a Team Project and Create a Folder Mapping</span></span>

<span data-ttu-id="4d11b-123">Kaynak denetimine içerik eklemeden önce, bir ekip projesine bağlanmanız ve yerel makinenizde dosya sistemi ve sunucu üzerindeki klasör yapısı arasında bir eşleme oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-123">Before you add any content to source control, you need to connect to a team project and create a mapping between the folder structure on the server and the file system on your local machine.</span></span>

<span data-ttu-id="4d11b-124">**Bir takım projesine bağlanmak ve yerel bir yolu eşlemek için**</span><span class="sxs-lookup"><span data-stu-id="4d11b-124">**To connect to a team project and map a local path**</span></span>

1. <span data-ttu-id="4d11b-125">Geliştirici iş istasyonunuzda, Visual Studio 2010 ' u açın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-125">On your developer workstation, open Visual Studio 2010.</span></span>
2. <span data-ttu-id="4d11b-126">Visual Studio 'da, **Takım** menüsünde **Team Foundation Server Bağlan**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-126">In Visual Studio, on the **Team** menu, click **Connect to Team Foundation Server**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4d11b-127">TFS sunucusuna zaten bir bağlantı yapılandırdıysanız 3-6 arasındaki adımları atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-127">If you have already configured a connection to a TFS server, you can omit steps 3-6.</span></span>
3. <span data-ttu-id="4d11b-128">**Takım projesi bağlantısı** Iletişim kutusunda **sunucular**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-128">In the **Connection to Team Project** dialog box, click **Servers**.</span></span>
4. <span data-ttu-id="4d11b-129">**Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-129">In the **Add/Remove Team Foundation Server** dialog box, click **Add**.</span></span>
5. <span data-ttu-id="4d11b-130">**Team Foundation Server Ekle** ILETIŞIM kutusunda TFS örneğinizin ayrıntılarını belirtin ve ardından **Tamam**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-130">In the **Add Team Foundation Server** dialog box, provide the details of your TFS instance, and then click **OK**.</span></span>

    ![](adding-content-to-source-control/_static/image1.png)
6. <span data-ttu-id="4d11b-131">**Team Foundation Server Ekle/Kaldır** Iletişim kutusunda **Kapat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-131">In the **Add/Remove Team Foundation Server** dialog box, click **Close**.</span></span>
7. <span data-ttu-id="4d11b-132">**Takım Projesine Bağlan** iletişim kutusunda, bağlanmak istediğiniz TFS örneğini seçin, takım projesi koleksiyonunu seçin, eklemek istediğiniz takım projesini seçin ve ardından **Bağlan**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-132">In the **Connect to Team Project** dialog box, select the TFS instance you want to connect to, select the team project collection, select the team project you want to add to, and then click **Connect**.</span></span>

    ![](adding-content-to-source-control/_static/image2.png)
8. <span data-ttu-id="4d11b-133">**Takım Gezgini** penceresinde, takım projenizi genişletin ve ardından **kaynak denetimi**' ne çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-133">In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image3.png)
9. <span data-ttu-id="4d11b-134">**Kaynak Denetim Gezgini** sekmesinde **eşlenmemiş**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-134">On the **Source Control Explorer** tab, click **Not mapped**.</span></span>

    ![](adding-content-to-source-control/_static/image4.png)
10. <span data-ttu-id="4d11b-135">**Harita** iletişim kutusunda, **yerel klasör** kutusunda, takım projesi için kök klasör olarak davranacak yerel bir klasöre gidin (veya oluşturun) ve ardından **eşle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-135">In the **Map** dialog box, in the **Local folder** box, browse to (or create) a local folder to act as the root folder for the team project, and then click **Map**.</span></span>

    ![](adding-content-to-source-control/_static/image5.png)
11. <span data-ttu-id="4d11b-136">Kaynak dosyaları indirmek isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-136">When you're prompted to download source files, click **Yes**.</span></span>

    ![](adding-content-to-source-control/_static/image6.png)

<span data-ttu-id="4d11b-137">Bu noktada, takım projesi için sunucu tarafı klasörünü geliştirici iş istasyonunuzda yerel bir klasöre eşlediniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-137">At this point, you have mapped the server-side folder for the team project to a local folder on your developer workstation.</span></span> <span data-ttu-id="4d11b-138">Ayrıca, var olan tüm içeriği takım projesinden yerel klasör yapınıza indirdiniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-138">You've also downloaded any existing content from the team project to your local folder structure.</span></span> <span data-ttu-id="4d11b-139">Artık kaynak denetimine kendi içeriğinizi eklemeye başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-139">You can now start to add your own content to source control.</span></span>

## <a name="add-projects-and-solutions-to-source-control"></a><span data-ttu-id="4d11b-140">Kaynak denetimine proje ve çözüm ekleme</span><span class="sxs-lookup"><span data-stu-id="4d11b-140">Add Projects and Solutions to Source Control</span></span>

<span data-ttu-id="4d11b-141">Kaynak denetimine projeler ve çözümler eklemek için, önce bunları yerel makinenizde takım projesi için eşlenmiş klasöre taşımanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-141">To add projects and solutions to source control, you first need to move them to the mapped folder for the team project on your local machine.</span></span> <span data-ttu-id="4d11b-142">Daha sonra, eklemelerinizi sunucuyla eşitlemenize sonra içeriği iade edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-142">You can then check in the content to synchronize your additions with the server.</span></span>

<span data-ttu-id="4d11b-143">**Kaynak denetimine proje eklemek için**</span><span class="sxs-lookup"><span data-stu-id="4d11b-143">**To add projects to source control**</span></span>

1. <span data-ttu-id="4d11b-144">Geliştirici iş istasyonunuzda, projelerinizi ve çözümlerinizi takım projesi için eşlenmiş klasör yapısı içinde uygun bir konuma taşıyın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-144">On your developer workstation, move your projects and solutions to an appropriate location within the mapped folder structure for the team project.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4d11b-145">Birçok kuruluş, proje ve çözümlerin kaynak denetiminde nasıl düzenleneceğine yönelik tercih edilen bir yaklaşıma sahip olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4d11b-145">Many organizations will have a preferred approach to how projects and solutions should be organized in source control.</span></span> <span data-ttu-id="4d11b-146">Klasörleri nasıl yapılandıracağınıza ilişkin yönergeler için bkz. [nasıl yapılır: kaynak denetim klasörlerinizi yapılandırma Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d11b-146">For guidance on how to structure folders, see [How To: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).</span></span>
2. <span data-ttu-id="4d11b-147">Visual Studio 2010 ' de çözümü açın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-147">Open the solution in Visual Studio 2010.</span></span>
3. <span data-ttu-id="4d11b-148">**Çözüm Gezgini** penceresinde çözüme sağ tıklayın ve ardından **kaynak denetimine çözüm Ekle**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-148">In the **Solution Explorer** window, right-click the solution, and then click **Add Solution to Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="4d11b-149">Bazı durumlarda, kuruluşunuzun TFS 'de içerik yapısını nasıl sağladığına bağlı olarak kaynak denetimine proje eklemeniz gerekebilir. böylece, kaynak kodunuza nasıl düzenleneceğine daha ayrıntılı bir denetim sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-149">In some cases, depending on how your organization likes to structure content in TFS, you may need to add projects to source control individually to provide more fine-grained control over how your source code is organized.</span></span>
4. <span data-ttu-id="4d11b-150">**Kaynak Denetim Gezgini** sekmesinin, takım projesi için sunucu klasörü yapısı içinde eklediğiniz içeriği görüntülediğini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-150">Verify that the **Source Control Explorer** tab displays the content you've added within the server folder structure for the team project.</span></span>

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="4d11b-151">**Kaynak Denetim Gezgini** sekmesi, çözümünüzü yerel dosya sistemindeki eşlenmiş bir klasöre eklediğiniz için daha fazla istem yapmadan içeriğinizi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4d11b-151">The **Source Control Explorer** tab displays your content with no further prompting because you added your solution to a mapped folder on the local file system.</span></span> <span data-ttu-id="4d11b-152">Çözümünüz eşlenmemiş bir konumdaysa, hem TFS 'de hem de yerel dosya sisteminizde klasör konumları belirtmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-152">If your solution was in an unmapped location, you'd be prompted to specify folder locations in both TFS and your local file system.</span></span>
5. <span data-ttu-id="4d11b-153">**Kaynak Denetim Gezgini** sekmesinde, **Klasörler** bölmesinde, takım projesine (örneğin, **ContactManager**) sağ tıklayın ve ardından **bekleyen değişiklikleri iade et**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-153">On the **Source Control Explorer** tab, in the **Folders** pane, right-click the team project (for example, **ContactManager**), and then click **Check In Pending Changes**.</span></span>
6. <span data-ttu-id="4d11b-154">**Iade et – kaynak dosyalar** iletişim kutusunda bir açıklama yazın ve **iade et**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-154">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

    ![](adding-content-to-source-control/_static/image9.png)

<span data-ttu-id="4d11b-155">Bu noktada, çözümünüzü TFS 'deki kaynak denetimine eklediniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-155">At this point you have added your solution to source control in TFS.</span></span>

## <a name="add-external-dependencies-to-source-control"></a><span data-ttu-id="4d11b-156">Kaynak denetimine dış bağımlılıklar ekleme</span><span class="sxs-lookup"><span data-stu-id="4d11b-156">Add External Dependencies to Source Control</span></span>

<span data-ttu-id="4d11b-157">Kaynak denetimine bir proje veya çözüm eklediğinizde, projeniz veya çözümünüz içindeki tüm dosyalar ve klasörler de eklenir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-157">When you add a project or solution to source control, any files and folders within your project or solution will also be added.</span></span> <span data-ttu-id="4d11b-158">Ancak, çok sayıda durumda, projeler ve çözümler, yerel derlemeler gibi dış bağımlılıklara de dayanır, bu da düzgün şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="4d11b-158">However, in a lot of cases, projects and solutions also rely on external dependencies, like local assemblies, to function properly.</span></span> <span data-ttu-id="4d11b-159">Her iki ekip derlemesinin ve geliştirici ekibinin diğer üyelerinin kodunuzu başarıyla oluşturmasını sağlamak için kaynak denetimine bu tür kaynakları eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-159">You need to add any such resources to source control to let both Team Build and other members of the developer team build your code successfully.</span></span>

<span data-ttu-id="4d11b-160">Örneğin, Contact Manager örnek çözümünün klasör yapısı, paketler adlı bir klasör içerir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-160">For example, the folder structure for the Contact Manager sample solution includes a folder named packages.</span></span> <span data-ttu-id="4d11b-161">Bu, derlemeyi ve ADO.NET Entity Framework 4,1 için çeşitli destekleyici kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-161">This contains the assembly and various supporting resources for the ADO.NET Entity Framework 4.1.</span></span> <span data-ttu-id="4d11b-162">Paketler klasörü, Contact Manager çözümünün bir parçası değildir, ancak çözüm bu olmadan başarıyla derlenmeyecektir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-162">The packages folder is not part of the Contact Manager solution, but the solution will not build successfully without it.</span></span> <span data-ttu-id="4d11b-163">Çözümü oluşturmak üzere ekip yapısını etkinleştirmek için, kaynak denetimine paketler klasörünü eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-163">To enable Team Build to build the solution, you need to add the packages folder to source control.</span></span>

> [!NOTE]
> <span data-ttu-id="4d11b-164">Bir paketler klasörünün dahil edilmesi, Visual Studio 2010 için NuGet uzantısını kullanarak çözümünüze Entity Framework veya benzer kaynakları eklediğinizde ne olacağı hakkında tipik bir şeydir.</span><span class="sxs-lookup"><span data-stu-id="4d11b-164">The inclusion of a packages folder is typical of what happens when you add the Entity Framework, or similar resources, to your solution using the NuGet extension for Visual Studio 2010.</span></span>

<span data-ttu-id="4d11b-165">**Kaynak denetimine proje olmayan içerik eklemek için**</span><span class="sxs-lookup"><span data-stu-id="4d11b-165">**To add non-project content to source control**</span></span>

1. <span data-ttu-id="4d11b-166">Eklemek istediğiniz öğelerin (örneğin, paketler klasörü) yerel dosya sisteminizdeki eşlenmiş bir klasör içinde uygun bir konumda olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4d11b-166">Ensure that the items you want to add (for example, the packages folder) are in an appropriate location within a mapped folder on your local file system.</span></span>
2. <span data-ttu-id="4d11b-167">Visual Studio 2010 ' de **Takım Gezgini** penceresinde, takım projenizi genişletin ve ardından **kaynak denetimi**' ne çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-167">In Visual Studio 2010, In the **Team Explorer** window, expand your team project, and then double-click **Source Control**.</span></span>

    ![](adding-content-to-source-control/_static/image10.png)
3. <span data-ttu-id="4d11b-168">**Kaynak Denetim Gezgini** sekmesinde, **Klasörler** bölmesinde, eklemek istediğiniz öğe veya öğeleri içeren klasörü seçin.</span><span class="sxs-lookup"><span data-stu-id="4d11b-168">On the **Source Control Explorer** tab, in the **Folders** pane, select the folder that contains the item or items you want to add.</span></span>
4. <span data-ttu-id="4d11b-169">**Klasöre öğe Ekle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-169">Click the **Add Items to Folder** button.</span></span>

    ![](adding-content-to-source-control/_static/image11.png)
5. <span data-ttu-id="4d11b-170">**Kaynak denetimine Ekle** iletişim kutusunda, eklemek istediğiniz klasörü veya öğeleri seçin ve ardından **İleri**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-170">In the **Add to Source Control** dialog box, select the folder or items you want to add, and then click **Next**.</span></span>

    ![](adding-content-to-source-control/_static/image12.png)
6. <span data-ttu-id="4d11b-171">**Dışlanan öğeler** sekmesinde, otomatik olarak dışlanan gerekli öğeleri (örneğin, derlemeler) seçin ve ardından **öğeleri dahil et**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-171">On the **Excluded items** tab, select any required items that have been automatically excluded (for example, assemblies), and then click **Include item(s)**.</span></span>

    ![](adding-content-to-source-control/_static/image13.png)
7. <span data-ttu-id="4d11b-172">**Eklenecek öğeler** sekmesinde, dahil etmek istediğiniz tüm dosyaların listelendiğinden emin olun ve ardından **son**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-172">On the **Items to add** tab, verify that all the files you want to include are listed, and then click **Finish**.</span></span>

    ![](adding-content-to-source-control/_static/image14.png)
8. <span data-ttu-id="4d11b-173">**Kaynak Denetim Gezgini** penceresinde, **iade et** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-173">In the **Source Control Explorer** window, click the **Check In** button.</span></span>

    ![](adding-content-to-source-control/_static/image15.png)
9. <span data-ttu-id="4d11b-174">**Iade et – kaynak dosyalar** iletişim kutusunda bir açıklama yazın ve **iade et**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4d11b-174">In the **Check In – Source Files** dialog box, type a comment, and then click **Check In**.</span></span>

<span data-ttu-id="4d11b-175">Bu noktada, çözümünüz için dış bağımlılıkları kaynak denetimine eklediniz.</span><span class="sxs-lookup"><span data-stu-id="4d11b-175">At this point, you have added the external dependencies for your solution to source control.</span></span>

## <a name="conclusion"></a><span data-ttu-id="4d11b-176">Sonuç</span><span class="sxs-lookup"><span data-stu-id="4d11b-176">Conclusion</span></span>

<span data-ttu-id="4d11b-177">Bu konu, bir ekip projesine bağlanma, bir klasör yapısını eşleme ve kaynak denetimine içerik ekleme konularında anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="4d11b-177">This topic described how to connect to a team project, map a folder structure, and add content to source control.</span></span> <span data-ttu-id="4d11b-178">Kaynak denetimi altındaki öğelerle çalışma hakkında daha fazla bilgi için bkz. [Sürüm denetimini kullanma](https://msdn.microsoft.com/library/ms181368.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d11b-178">For more information on how to work with items under source control, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

<span data-ttu-id="4d11b-179">Bir sonraki konu, [Web dağıtımı için BIR TFS derleme sunucusu yapılandırırken](configuring-a-tfs-build-server-for-web-deployment.md), çözümünüzü derlemek ve dağıtmak IÇIN bir TFS ekip yapı sunucusunun nasıl hazırlanacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="4d11b-179">The next topic, [Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md), describes how to prepare a TFS Team Build server to build and deploy your solution.</span></span>

## <a name="further-reading"></a><span data-ttu-id="4d11b-180">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="4d11b-180">Further Reading</span></span>

<span data-ttu-id="4d11b-181">TFS 'de kaynak denetimiyle çalışma hakkında daha ayrıntılı bilgi için bkz. [Sürüm denetimini kullanma](https://msdn.microsoft.com/library/ms181368.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d11b-181">For more comprehensive information on working with source control in TFS, see [Using Version Control](https://msdn.microsoft.com/library/ms181368.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4d11b-182">[Önceki](creating-a-team-project-in-tfs.md)
> [İleri](configuring-a-tfs-build-server-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="4d11b-182">[Previous](creating-a-team-project-in-tfs.md)
[Next](configuring-a-tfs-build-server-for-web-deployment.md)</span></span>
