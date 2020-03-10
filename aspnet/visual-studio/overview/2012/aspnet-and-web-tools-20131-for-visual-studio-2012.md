---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Visual Studio 2012 için ASP.NET and Web Tools 2013,1 sürüm notları | Microsoft Docs
author: microsoft
description: Bu belgede, Visual Studio 2012 için ASP.NET and Web Tools 2013,1 sürümü açıklanmaktadır.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578444"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="5e182-103">Visual Studio 2012 için ASP.NET and Web Tools 2013.1 Sürüm Notları</span><span class="sxs-lookup"><span data-stu-id="5e182-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="5e182-104">[Microsoft](https://github.com/microsoft) tarafından</span><span class="sxs-lookup"><span data-stu-id="5e182-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5e182-105">Bu belgede, Visual Studio 2012 için ASP.NET and Web Tools 2013,1 sürümü açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5e182-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="5e182-106">İçindekiler</span><span class="sxs-lookup"><span data-stu-id="5e182-106">Contents</span></span>

- [<span data-ttu-id="5e182-107">Yükleme notları</span><span class="sxs-lookup"><span data-stu-id="5e182-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="5e182-108">Yazılım gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="5e182-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="5e182-109">Visual Studio 2012 için ASP.NET and Web Tools 2013,1 ' deki yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="5e182-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="5e182-110">Yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5e182-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="5e182-111">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="5e182-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="5e182-112">ASP.NET MVC 5 şablonu</span><span class="sxs-lookup"><span data-stu-id="5e182-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="5e182-113">ASP.NET Web API 2 şablonu</span><span class="sxs-lookup"><span data-stu-id="5e182-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="5e182-114">Öğe şablonları</span><span class="sxs-lookup"><span data-stu-id="5e182-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="5e182-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="5e182-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="5e182-116">ASP.NET Scafkatlama</span><span class="sxs-lookup"><span data-stu-id="5e182-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="5e182-117">Razor Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="5e182-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="5e182-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="5e182-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="5e182-119">Bilinen sorunlar ve son değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5e182-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="5e182-120">ASP.NET Scafkatlama</span><span class="sxs-lookup"><span data-stu-id="5e182-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="5e182-121">MVC ve Web API 'SI yapı Iskelesi-HTTP 404, bulunamadı hatası</span><span class="sxs-lookup"><span data-stu-id="5e182-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="5e182-122">Web için Visual Studio Express 2012, bir yapı iskelesi eklenen bir öğe eklendikten sonra çalışmayı durduruyor</span><span class="sxs-lookup"><span data-stu-id="5e182-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="5e182-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="5e182-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="5e182-124">Cshtml dosyasını ve F5 ile görüntüleme, bir sunucu hatasına neden oluyor</span><span class="sxs-lookup"><span data-stu-id="5e182-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="5e182-125">URL yeniden yazma ve tilde (~)</span><span class="sxs-lookup"><span data-stu-id="5e182-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="5e182-126">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="5e182-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="5e182-127">Yükleme notları</span><span class="sxs-lookup"><span data-stu-id="5e182-127">Installation Notes</span></span>

<span data-ttu-id="5e182-128">[Yüklemesi](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) Visual Studio 2012 için ASP.NET and Web Tools 2013,1.</span><span class="sxs-lookup"><span data-stu-id="5e182-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="5e182-129">Yazılım Gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="5e182-129">Software Requirements</span></span>

<span data-ttu-id="5e182-130">Web için Visual Studio 2012 veya Visual Studio Express 2012 ' ya sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e182-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="5e182-131">Visual Studio 2012 için ASP.NET and Web Tools 2013,1 ' deki yeni özellikler</span><span class="sxs-lookup"><span data-stu-id="5e182-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="5e182-132">Yükleyebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="5e182-132">Bootstrap</span></span>

<span data-ttu-id="5e182-133">Ffold MVC 5 denetleyicilerini ve görünümlerini yapılandırırken, görünümler için biçimlendirme [önyükleme](http://getbootstrap.com/)kullanır.</span><span class="sxs-lookup"><span data-stu-id="5e182-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="5e182-134">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="5e182-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="5e182-135">ASP.NET MVC 5 şablonu</span><span class="sxs-lookup"><span data-stu-id="5e182-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="5e182-136">Yeni bir MVC 5 şablonu ekledik.</span><span class="sxs-lookup"><span data-stu-id="5e182-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="5e182-137">En son MVC 5 NuGet paketlerine başvurur ve yapı ve görünüm eklemek için scafkatlamayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e182-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="5e182-138">ASP.NET Web API 2 şablonu</span><span class="sxs-lookup"><span data-stu-id="5e182-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="5e182-139">Yeni bir Web API 2 şablonu ekledik.</span><span class="sxs-lookup"><span data-stu-id="5e182-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="5e182-140">En son Web API 2 NuGet paketlerine başvurur ve yapı ve görünüm eklemek için scafkatlamayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e182-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="5e182-141">Öğe şablonları</span><span class="sxs-lookup"><span data-stu-id="5e182-141">Item Templates</span></span>

<span data-ttu-id="5e182-142">MVC 5 görünümleri, Web sayfaları (Razor 3) ve Web API 2 denetleyicileri için yeni öğe şablonları ekledik.</span><span class="sxs-lookup"><span data-stu-id="5e182-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="5e182-143">Yeni öğeler eklenirken ilgili NuGet paketlerini projeye yükler.</span><span class="sxs-lookup"><span data-stu-id="5e182-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="5e182-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="5e182-144">Entity Framework 6</span></span>

<span data-ttu-id="5e182-145">Entity Framework kullanarak bir MVC veya Web API denetleyicisi ile dolandırdığınızda, Framework 6 ' yı kullanırız.</span><span class="sxs-lookup"><span data-stu-id="5e182-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="5e182-146">Entity Framework hakkında daha fazla bilgi için, [Entity Framework sürüm geçmişine](https://msdn.com/data/jj574253)bakın.</span><span class="sxs-lookup"><span data-stu-id="5e182-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="5e182-147">Ayrıca, Visual Studio 2012 için Entity Framework 6 araçlarını indirebilir ve yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e182-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="5e182-148">Bkz. [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span><span class="sxs-lookup"><span data-stu-id="5e182-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="5e182-149">ASP.NET Scafkatlama</span><span class="sxs-lookup"><span data-stu-id="5e182-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="5e182-150">ASP.NET Scafkatlama, ASP.NET Web uygulamaları için bir kod oluşturma çerçevesidir.</span><span class="sxs-lookup"><span data-stu-id="5e182-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="5e182-151">Projenize bir veri modeliyle etkileşim kuran ortak kod eklemenizi kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5e182-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="5e182-152">Visual Studio 'nun önceki sürümlerinde, scafkatlama ASP.NET MVC projeleriyle sınırlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5e182-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="5e182-153">Bu güncelleştirmeyle, artık Web Forms dahil olmak üzere herhangi bir ASP.NET projesi için scafkatlamayı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e182-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="5e182-154">Bu güncelleştirme, bir Web Forms projesi için sayfa oluşturmayı desteklemez, ancak projeye MVC bağımlılıkları ekleyerek Web Forms ile yapı iskelesi kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e182-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="5e182-155">Web Forms için sayfa oluşturma desteği gelecekteki bir güncelleştirmeye eklenecektir.</span><span class="sxs-lookup"><span data-stu-id="5e182-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="5e182-156">Yapı iskelesi kullanılırken, gerekli tüm bağımlılıkların projede yüklü olduğundan emin veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="5e182-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="5e182-157">Örneğin, bir ASP.NET Web Forms projesiyle başlayıp bir Web API denetleyicisi eklemek için scafkatlamayı kullanıyorsanız, gerekli NuGet paketleri ve başvuruları projenize otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="5e182-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="5e182-158">Web Forms projesine MVC yapı iskelesi eklemek için **Yeni bir yapı** İskelesi ekleyin ve Iletişim penceresinde **MVC 5 bağımlılıklarını** seçin.</span><span class="sxs-lookup"><span data-stu-id="5e182-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="5e182-159">Yapı iskelesi MVC için iki seçenek vardır; En az ve tam.</span><span class="sxs-lookup"><span data-stu-id="5e182-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="5e182-160">En az ' ı seçerseniz, projenize yalnızca NuGet paketleri ve ASP.NET MVC başvuruları eklenir.</span><span class="sxs-lookup"><span data-stu-id="5e182-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="5e182-161">Tam seçeneğini belirlerseniz, en düşük bağımlılıklar ve bir MVC projesi için gerekli içerik dosyaları eklenir.</span><span class="sxs-lookup"><span data-stu-id="5e182-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="5e182-162">Yapı iskelesi zaman uyumsuz denetleyiciler desteği Entity Framework 6 ' dan gelen yeni zaman uyumsuz özellikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="5e182-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="5e182-163">Daha fazla bilgi ve öğretici için bkz. [ASP.net Scafkate genel bakış](../2013/aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e182-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="5e182-164">Bu öğreticiler Visual Studio 2013 ile yapı iskelesi gösterir, ancak Visual Studio 2012 için ASP.NET and Web Tools 2013,1 için de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5e182-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="5e182-165">Razor Düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="5e182-165">Razor Editor</span></span>

<span data-ttu-id="5e182-166">Visual Studio 2012, bu güncelleştirme ile Razor 3 araç oluşturma/düzenlemesini desteklemektedir.</span><span class="sxs-lookup"><span data-stu-id="5e182-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="5e182-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="5e182-167">NuGet 2.7</span></span>

<span data-ttu-id="5e182-168">NuGet 2,7, [nuget 2,7 sürüm notlarında](http://docs.nuget.org/docs/release-notes/nuget-2.7)ayrıntılı olarak açıklanan zengin bir dizi yeni özellik içerir.</span><span class="sxs-lookup"><span data-stu-id="5e182-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="5e182-169">NuGet 'in bu sürümü, kullanıcıların açıkça NuGet 'in eksik paketleri geri yüklemelerine izin verme gereksinimini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="5e182-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="5e182-170">NuGet 2,7 yüklenirken, kullanıcılar eksik paketleri otomatik olarak geri yüklemeye izin vermez.</span><span class="sxs-lookup"><span data-stu-id="5e182-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="5e182-171">Kullanıcılar, Visual Studio 'daki NuGet ayarları aracılığıyla paket geri yüklemesini açıkça devre dışı bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e182-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="5e182-172">Bu değişiklik, paket geri yüklemesinin nasıl çalıştığını basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="5e182-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="5e182-173">Bilinen sorunlar ve son değişiklikler</span><span class="sxs-lookup"><span data-stu-id="5e182-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="5e182-174">ASP.NET Scafkatlama</span><span class="sxs-lookup"><span data-stu-id="5e182-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="5e182-175">MVC ve Web API 'SI yapı Iskelesi-HTTP 404, bulunamadı hatası</span><span class="sxs-lookup"><span data-stu-id="5e182-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="5e182-176">Bir projeye yapı iskelesi eklenen bir öğe eklerken bir hatayla karşılaşırsanız projenizin tutarsız bir durumda bırakılması mümkündür.</span><span class="sxs-lookup"><span data-stu-id="5e182-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="5e182-177">Yapı iskelesi haline getirilen değişikliklerden bazıları geri alınacaktır, ancak yüklü NuGet paketleri gibi diğer değişiklikler geri alınmaz.</span><span class="sxs-lookup"><span data-stu-id="5e182-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="5e182-178">Yönlendirme yapılandırması değişiklikleri geri alınırsa, kullanıcılar, yapı iskelesi öğelerinde gezinilirken bir HTTP 404 hatası alırlar.</span><span class="sxs-lookup"><span data-stu-id="5e182-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="5e182-179">MVC için bu hatayı onarmak üzere yeni bir yapı iskelesi ekleyin ve MVC 5 bağımlılıklarını (en az ya da tam) seçin.</span><span class="sxs-lookup"><span data-stu-id="5e182-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="5e182-180">Bu işlem, gerekli tüm değişiklikleri projenize ekleyecek.</span><span class="sxs-lookup"><span data-stu-id="5e182-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="5e182-181">Web API 'SI için bu hatayı onarmak için:</span><span class="sxs-lookup"><span data-stu-id="5e182-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="5e182-182">Aşağıdaki WebApiConfig sınıfını projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5e182-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="5e182-183">WebApiConfig. Register öğesini Global. asax içindeki Application\_start yönteminde aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="5e182-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="5e182-184">Web için Visual Studio Express 2012, bir yapı iskelesi eklenen bir öğe eklendikten sonra çalışmayı durduruyor</span><span class="sxs-lookup"><span data-stu-id="5e182-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="5e182-185">Web için Visual Studio Express 2012 Entity Framework, Entity Framework sahip yapı iskelesi (Eylemler içeren Web API 2 denetleyicisi gibi) eklendikten sonra çalışmayı durduruyor, Visual Studio Express bir derlemenin yerel görüntüsünü yüklemede başarısız olabilir System. Web. Extensions 'a bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="5e182-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="5e182-186">Bu sorunu düzeltmek için Visual Studio Express, System. Web. Extensions MSIL görüntüsüyle çalışacak şekilde yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="5e182-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="5e182-187">Yönetici modunda komut Istemi ' ni açın.</span><span class="sxs-lookup"><span data-stu-id="5e182-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="5e182-188">%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\ıde veya% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\ıde (64 bit Windows için) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="5e182-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="5e182-189">Bir metin düzenleyicisinde, '. exe. config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="5e182-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="5e182-190">&lt;yapılandırma&gt;/&lt;çalışma zamanı&gt; öğesinin altına aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="5e182-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="5e182-191">Web için Visual Studio Express 2012 ' i yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="5e182-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="5e182-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="5e182-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="5e182-193">Cshtml dosyasını ve F5 ile görüntüleme, bir sunucu hatasına neden oluyor</span><span class="sxs-lookup"><span data-stu-id="5e182-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="5e182-194">Visual Studio 2012 ' de bir MVC 5 projesi oluşturduğunuzda (veya Visual Studio 2013 içinde oluşturulmuş bir MVC 5 projesinde Visual Studio 2012 ' de açın) ve bir cshtml dosyasını veya F5 'i kullanarak görüntülemeyi denerseniz, **'/' uygulamasında sunucu hatası**olduğunu bildiren bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5e182-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="5e182-195">Sunucu `http://localhost:XXXX/Views/../XXXX.cshtml` gitme girişiminde bulunur</span><span class="sxs-lookup"><span data-stu-id="5e182-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="5e182-196">Bu sorunu çözmek için, projenizdeki **Başlangıç eylemi** ayarını **belirli bir sayfada**değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5e182-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="5e182-197">Sayfa için bir değer belirtmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5e182-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="5e182-198">Bu değişikliği yaptıktan sonra F5 ' i seçtiğinizde uygulamanızın köküne (`http://localhost:XXXX`) gider.</span><span class="sxs-lookup"><span data-stu-id="5e182-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="5e182-199">Bu davranış, **geçerli sayfa** ayarının açık sayfayı BAŞLATTıĞıNDA Visual Studio 2013 MVC 5 projelerine yönelik davranışla aynı değildir.</span><span class="sxs-lookup"><span data-stu-id="5e182-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="5e182-200">URL yeniden yazma ve tilde (~)</span><span class="sxs-lookup"><span data-stu-id="5e182-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="5e182-201">ASP.NET Razor 3 veya ASP.NET MVC 5 sürümüne yükselttikten sonra, URL yeniden yazar kullanıyorsanız, tilde (~) gösterimi artık düzgün çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="5e182-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="5e182-202">URL yeniden yazma, &lt;A/&gt;, &lt;BETIK/&gt;, &lt;LINK/&gt;gibi HTML öğelerinde tilde (~) gösterimini etkiler ve bu nedenle, tilde artık kök dizine eşlememez.</span><span class="sxs-lookup"><span data-stu-id="5e182-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="5e182-203">Örneğin, **ASP.net/Content** için istekleri **ASP.net**'e yeniden verirseniz, &lt;A href = "~/content/"/&gt; içindeki href özniteliği **/** yerine **/Content/Content/** olarak çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="5e182-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="5e182-204">Bu değişikliği engellemek için, **ııs\_** IBU bağlamı her bir Web sayfasında yanlış olarak veya Global. asax dosyasındaki **BeginRequest\_** .</span><span class="sxs-lookup"><span data-stu-id="5e182-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="5e182-205">Şablonlar</span><span class="sxs-lookup"><span data-stu-id="5e182-205">Templates</span></span>

<span data-ttu-id="5e182-206">Windows 8.1 veya Windows Server 2012 R2 üzerinde Visual Studio 2012 ile ASP.NET MVC projeleri oluşturduğunuzda, Visual Studio "ASP.NET 4,5 için Web [URL] yapılandırma başarısız oldu." iletisini bildiren bir hata mesajı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="5e182-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![Yapılandırma hatası](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="5e182-208">Bu hata, Visual Studio 2012, ASP.NET 4,5 özelliğini Windows 'un bu sürümlerinde yüklü olduğunda etkinleştirmediği için görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5e182-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="5e182-209">ASP.NET 4,5 ' i etkinleştirmek için [Windows özelliklerini açma veya kapatma](https://windows.microsoft.com/windows-8/turn-windows-features-on-off)bölümünde açıklanan adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5e182-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Windows özelliklerini aç veya kapat](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="5e182-211">Alternatif olarak, komut satırı aracılığıyla ASP.NET 4,5 'yi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e182-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="5e182-212">Yönetici modunda komut Istemi ' ni açın.</span><span class="sxs-lookup"><span data-stu-id="5e182-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="5e182-213">ASP.NET 4,5 ' i etkinleştirmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5e182-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`
