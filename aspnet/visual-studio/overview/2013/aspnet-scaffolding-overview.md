---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: Visual Studio 2013 ASP.NET Scafkatlama | Microsoft Docs
author: Rick-Anderson
description: ASP.NET Scafkatlama, Visual Studio 2013 eklenen yeni bir özelliktir.
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557983"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="fef94-103">Visual Studio 2013’te ASP.NET İskeleti Oluşturma</span><span class="sxs-lookup"><span data-stu-id="fef94-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>

<span data-ttu-id="fef94-104">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="fef94-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="fef94-105">ASP.NET Scafkatlama, Visual Studio 2013 eklenen yeni bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="fef94-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>

## <a name="overview"></a><span data-ttu-id="fef94-106">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="fef94-106">Overview</span></span>

<span data-ttu-id="fef94-107">ASP.NET Scafkatlama, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="fef94-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="fef94-108">Visual Studio 2013, MVC ve Web API projeleri için önceden yüklenmiş kod oluşturucuları içerir.</span><span class="sxs-lookup"><span data-stu-id="fef94-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="fef94-109">Veri modelleriyle etkileşim kuran kodu hızlıca eklemek istediğinizde projenize yapı iskelesi eklersiniz.</span><span class="sxs-lookup"><span data-stu-id="fef94-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="fef94-110">Yapı iskelesi kullanmak, projenizde standart veri işlemlerinin geliştirilmesi için geçen süreyi azaltabilir.</span><span class="sxs-lookup"><span data-stu-id="fef94-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="fef94-111">Visual Studio 2013, varsayılan olarak, bir Web Forms projesi için kod oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek veya bir uzantı yükleyerek Web Forms ile yapı iskelesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef94-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="fef94-112">Her iki yaklaşım da aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fef94-112">Both approaches are shown below.</span></span>

<span data-ttu-id="fef94-113">Visual Studio 2013 güncelleştirme 2 (Şu anda RC), senaryolarınızın gereksinimlerini karşılamak için ASP.NET Scafkatını genişletme olanağı sunar.</span><span class="sxs-lookup"><span data-stu-id="fef94-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="fef94-114">Bu işlevle özelleştirilmiş bir yapı iskelesi şablonu oluşturabilir ve bunu yeni Scaffold iletişim kutusu Ekle ' ye ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef94-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="fef94-115">Özelleştirilmiş şablon içinde, bir yapı iskelesi öğesi eklenirken oluşturulan kodu belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef94-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="fef94-116">Daha fazla bilgi için bkz. [Visual Studio Için özel bir Scaffolder oluşturma](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span><span class="sxs-lookup"><span data-stu-id="fef94-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fef94-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fef94-117">Prerequisites</span></span>

<span data-ttu-id="fef94-118">ASP.NET Scafkatlamayı kullanmak için, şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="fef94-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="fef94-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="fef94-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="fef94-120">Web Geliştirici Araçları (varsayılan Visual Studio 2013 yüklemesinin parçası)</span><span class="sxs-lookup"><span data-stu-id="fef94-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="fef94-121">ASP.NET Web çerçeveleri ve Araçları 2013 (varsayılan Visual Studio 2013 yüklemesinin parçası)</span><span class="sxs-lookup"><span data-stu-id="fef94-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="fef94-122">MVC veya Web API 'sine bir yapı iskelesi öğesi ekleme</span><span class="sxs-lookup"><span data-stu-id="fef94-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="fef94-123">Bir yapı iskelesi eklemek için projeye veya proje içindeki bir klasöre sağ tıklayın ve aşağıdaki görüntüde gösterildiği gibi **Ekle** – **Yeni Scafkatlanmış öğe**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="fef94-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![Yapı iskelesi öğesi Ekle](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="fef94-125">**Yapı Iskelesi Ekle** penceresinde, eklenecek yapı iskelesi türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="fef94-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![Yapı iskelesi türünü seçin](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="fef94-127">**Denetleyici Ekle** penceresi, Entity Framework 6 ' dan yeni zaman uyumsuz özellikleri kullanmak isteyip istemediğiniz da dahil olmak üzere, denetleyiciyi oluşturma seçeneklerini seçmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fef94-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![denetleyici Ekle](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="fef94-129">Senaryonuz için ilgili sınıflar ve sayfalar oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fef94-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="fef94-130">Örneğin, aşağıdaki görüntüde, filmler adlı bir model sınıfı için scafkatlama aracılığıyla oluşturulan MVC denetleyicisi ve görünümleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fef94-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![Oluşturulan dosyalar](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="fef94-132">Web Forms bir yapı iskelesi öğesi ekleme</span><span class="sxs-lookup"><span data-stu-id="fef94-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="fef94-133">Web Forms kod üreten yapı iskelesi eklemek için, Visual Studio 'ya bir uzantı yüklemeli ya da MVC bağımlılıklarını eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fef94-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="fef94-134">Her iki yaklaşım da aşağıda gösterilmektedir, ancak yalnızca bu yaklaşımlardan birini yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fef94-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="fef94-135">Web Forms yapı Iskelesi uzantısı</span><span class="sxs-lookup"><span data-stu-id="fef94-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="fef94-136">Bir Web Forms projesiyle yapı iskelesi kullanmanıza imkan tanıyan bir Visual Studio uzantısı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef94-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="fef94-137">Visual Studio 'da **Araçlar** ve ardından **Uzantılar ve güncelleştirmeler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="fef94-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="fef94-138">Bu iletişim kutusunda, **Web Forms yapı iskelesi**Için Visual Studio Galerisi ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="fef94-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![Web Forms yapı iskelesi yüklemesi](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="fef94-140">Daha fazla bilgi için bkz. [Web Forms Scafkatlaması](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span><span class="sxs-lookup"><span data-stu-id="fef94-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="fef94-141">MVC bağımlılıkları</span><span class="sxs-lookup"><span data-stu-id="fef94-141">MVC Dependencies</span></span>

<span data-ttu-id="fef94-142">MVC bağımlılıklarını eklemek için - **yeni yapı Iskelesi öğesi** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="fef94-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="fef94-143">Yapı Iskelesi Ekle penceresinde, aşağıda gösterildiği gibi **MVC bağımlılıklarını**seçin.</span><span class="sxs-lookup"><span data-stu-id="fef94-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![MVC bağımlılıkları Ekle](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="fef94-145">Yapı iskelesi MVC için iki seçenek vardır; En az ve tam.</span><span class="sxs-lookup"><span data-stu-id="fef94-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="fef94-146">En az ' ı seçerseniz, projenize yalnızca NuGet paketleri ve ASP.NET MVC başvuruları eklenir.</span><span class="sxs-lookup"><span data-stu-id="fef94-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="fef94-147">Tam seçeneğini belirlerseniz, en düşük bağımlılıklar ve bir MVC projesi için gerekli içerik dosyaları eklenir.</span><span class="sxs-lookup"><span data-stu-id="fef94-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="fef94-148">Kolayca yapı iskelesi kullanmak için tam bağımlılıklar ' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="fef94-148">To easily use scaffolding, select Full dependencies.</span></span>

![Tam bağımlılıklar seçin](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="fef94-150">Bağımlılıkları ekledikten sonra bir **README. txt** dosyası görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fef94-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="fef94-151">Projenizin doğru çalıştığından emin olmak için bu dosyadaki yönergeleri dikkatle izleyin.</span><span class="sxs-lookup"><span data-stu-id="fef94-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="fef94-152">Readme. txt dosyasındaki adımları tamamladığınızda, MVC ve Web API 'SI ile ilgili önceki bölümde gösterildiği gibi yeni bir yapı iskelesi öğesi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef94-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="fef94-153">Otomatik olarak oluşturulan görünümler ve denetleyici projeniz içinde doğru şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="fef94-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="fef94-154">Öğreticiler</span><span class="sxs-lookup"><span data-stu-id="fef94-154">Tutorials</span></span>

<span data-ttu-id="fef94-155">Özelleştirilmiş bir scaffolder oluşturmak için bkz. [Visual Studio Için özel bir Scaffolder oluşturma](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span><span class="sxs-lookup"><span data-stu-id="fef94-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="fef94-156">Oluşturulan dosyaları özelleştirmek için, bkz. [oluşturulan dosyaları yeni Scafkatlanmış öğe iletişim kutusundan özelleştirme](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span><span class="sxs-lookup"><span data-stu-id="fef94-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="fef94-157">**Database First geliştirmeyle**yapı iskelesi kullanmanın bir örneği için bkz. [ASP.NET MVC ile EF Database First](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span><span class="sxs-lookup"><span data-stu-id="fef94-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="fef94-158">**MVC** projesinde scafkatlamayı kullanmanın bir örneği için bkz. [ASP.NET MVC 5 ile çalışmaya](../../../mvc/overview/getting-started/introduction/getting-started.md)başlama.</span><span class="sxs-lookup"><span data-stu-id="fef94-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="fef94-159">**Web API** projesinde yapı iskelesi kullanmanın bir örneği için bkz. [Web API 2 ' de öznitelik yönlendirme ile REST API oluşturma](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="fef94-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>
