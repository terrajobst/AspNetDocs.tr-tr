---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: 'Bölüm 8: Son sayfalar, özel durum işleme ve sonuç | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır. 8. Bölüm sayfası ve özel durum hakkında bir kişi sayfası ekler...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130598"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="fe883-104">Bölüm 8: Son Sayfalar, Özel Durum İşleme ve Sonuç</span><span class="sxs-lookup"><span data-stu-id="fe883-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="fe883-105">tarafından [ALi Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="fe883-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="fe883-106">Tailspin Spyworks .NET platformu için güçlü, ölçeklenebilir uygulamalar oluşturmak için nasıl çok basit olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fe883-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="fe883-107">Bu, alışveriş, kullanıma alma ve yönetim gibi bir çevrimiçi mağaza oluşturmak için ASP.NET 4'te harika yeni özellikleri kullanmak nasıl devre dışı gösterir.</span><span class="sxs-lookup"><span data-stu-id="fe883-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="fe883-108">Bu öğretici serisinin tüm Tailspin Spyworks örnek uygulamayı oluşturmak için gerçekleştirilen adımlar ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fe883-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="fe883-109">8. Bölüm sayfası ve özel durum işleme hakkında bir kişi sayfası ekler.</span><span class="sxs-lookup"><span data-stu-id="fe883-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="fe883-110">Dizi sonuç budur.</span><span class="sxs-lookup"><span data-stu-id="fe883-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a>  <span data-ttu-id="fe883-111">İlgili kişi sayfası (ASP.NET postadan gönderme)</span><span class="sxs-lookup"><span data-stu-id="fe883-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="fe883-112">ContactUs.aspx adlı yeni bir sayfa oluşturun</span><span class="sxs-lookup"><span data-stu-id="fe883-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="fe883-113">Tasarımcı kullanarak, aşağıdaki form ToolkitScriptManager ve AjaxControlToolkit Düzenleyicisi denetiminden dahil edilecek özel not alma oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe883-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="fe883-114">biçimindeki telefon numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="fe883-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="fe883-115">Dosyanın arkasındaki kodda bir click olay işleyicisi oluşturmak ve kişi bilgilerini bir e-posta göndermek için bir yöntem uygulamak için "Gönder" düğmesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fe883-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="fe883-116">Bu kod, web.config dosyanız posta göndermek için kullanılacak SMTP sunucusu belirten yapılandırma bölümünde bir giriş içermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fe883-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>  <span data-ttu-id="fe883-117">Sayfa hakkında</span><span class="sxs-lookup"><span data-stu-id="fe883-117">About Page</span></span>

<span data-ttu-id="fe883-118">AboutUs.aspx adlı bir sayfa oluşturun ve dilediğiniz ne olursa olsun içeriği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe883-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a>  <span data-ttu-id="fe883-119">Genel özel durum işleyicisi</span><span class="sxs-lookup"><span data-stu-id="fe883-119">Global Exception Handler</span></span>

<span data-ttu-id="fe883-120">Son olarak, uygulamanın tamamında size özel durumlar ve başka bir öngörülemeyen durumlarda bu soğuk de web uygulamamızı neden işlenmeyen özel durumları.</span><span class="sxs-lookup"><span data-stu-id="fe883-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="fe883-121">Hiçbir zaman web site ziyaretçilerini görüntülenecek işlenmeyen bir özel durum istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="fe883-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="fe883-122">İşlenmeyen özel durumları saltanatı kullanıcı deneyimi olan dışında bir güvenlik sorunu da olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe883-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="fe883-123">Bu sorunu çözmek için bir genel özel durum işleyicisi uygular.</span><span class="sxs-lookup"><span data-stu-id="fe883-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="fe883-124">Bunu yapmak için Global.asax dosyası açın ve aşağıdaki önceden oluşturulan olay işleyicisini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fe883-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="fe883-125">Uygulama için kod ekleyin\_hata işleyicisi aşağıdaki gibi.</span><span class="sxs-lookup"><span data-stu-id="fe883-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="fe883-126">Ardından Error.aspx çözüme adlı bir sayfa ekleyin ve bu biçimlendirme kod parçacığı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fe883-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="fe883-127">Artık sayfasındaki\_hata iletileri olay işleyicisi ayıklama istek nesnesinden yükleme.</span><span class="sxs-lookup"><span data-stu-id="fe883-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>  <span data-ttu-id="fe883-128">Sonuç</span><span class="sxs-lookup"><span data-stu-id="fe883-128">Conclusion</span></span>

<span data-ttu-id="fe883-129">ASP.NET WebForms kolaylaştırır olduğunu gördük veritabanı erişimi, üyelik, AJAX, Gelişmiş bir Web sitesi oluşturmak için vs.</span><span class="sxs-lookup"><span data-stu-id="fe883-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="fe883-130">oldukça hızlı bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="fe883-130">pretty quickly.</span></span>

<span data-ttu-id="fe883-131">Umarım Bu öğretici, kendi ASP.NET WebForms uygulamalar oluşturmaya başlamak için ihtiyacınız olan araçları verdiği!</span><span class="sxs-lookup"><span data-stu-id="fe883-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="fe883-132">Önceki</span><span class="sxs-lookup"><span data-stu-id="fe883-132">Previous</span></span>](tailspin-spyworks-part-7.md)
