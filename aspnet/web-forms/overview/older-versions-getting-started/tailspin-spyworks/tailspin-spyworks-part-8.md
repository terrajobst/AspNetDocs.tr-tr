---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: '8\. kısım: son sayfalar, özel durum Işleme ve sonuç | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. 5\. bölüm, sayfa ve özel durum hakkında bir kişi sayfası ekler...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586886"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="d4cb8-104">8\. Bölüm: Son Sayfalar, Özel Durum İşleme ve Sonuç</span><span class="sxs-lookup"><span data-stu-id="d4cb8-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="d4cb8-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="d4cb8-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="d4cb8-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="d4cb8-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="d4cb8-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="d4cb8-109">5\. bölüm, sayfa ve özel durum işleme hakkında bir kişi sayfası ekler.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="d4cb8-110">Bu, serinin bir sonucu olur.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a><span data-ttu-id="d4cb8-111">İletişim sayfası (ASP.NET 'den e-posta gönderme)</span><span class="sxs-lookup"><span data-stu-id="d4cb8-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="d4cb8-112">Yeni bir sayfa oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="d4cb8-113">Tasarımcıyı kullanarak, ToolkitScriptManager ve düzenleyici denetimini AjaxControlToolkit öğesinden dahil etmek için aşağıdaki formu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="d4cb8-114">arasında yetersiz alanla karşılaştı.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="d4cb8-115">"Gönder" düğmesine çift tıklayarak, arka plan kodu dosyasında bir tıklama olayı işleyicisi oluşturun ve iletişim bilgilerini bir e-posta olarak göndermek için bir yöntem uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="d4cb8-116">Bu kod, Web. config dosyanızın, posta göndermek için kullanılacak SMTP sunucusunu belirten yapılandırma bölümünde bir giriş içermesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="d4cb8-117">Sayfa hakkında</span><span class="sxs-lookup"><span data-stu-id="d4cb8-117">About Page</span></span>

<span data-ttu-id="d4cb8-118">AboutUs. aspx adlı bir sayfa oluşturun ve dilediğiniz içeriği ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="d4cb8-119">Genel özel durum Işleyicisi</span><span class="sxs-lookup"><span data-stu-id="d4cb8-119">Global Exception Handler</span></span>

<span data-ttu-id="d4cb8-120">Son olarak, uygulama genelinde özel durumlar oluşturduğumuzdan, ayrıca web uygulamamız içinde işlenmemiş özel durumlara neden olan öngörülemeyen durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="d4cb8-121">İşlenmeyen bir özel durumun bir Web sitesi ziyaretçisine görüntülenmesini hiç istemedik.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="d4cb8-122">Farklı bir kullanıcı deneyimi dışında, işlenmemiş özel durumlar da güvenlik sorunu oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="d4cb8-123">Bu sorunu çözmek için genel bir özel durum işleyicisi uygulayacağız.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="d4cb8-124">Bunu yapmak için Global. asax dosyasını açın ve aşağıdaki önceden oluşturulmuş olay işleyicisine göz önünde edin.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="d4cb8-125">Uygulama\_hata işleyicisini aşağıdaki şekilde uygulamak için kod ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="d4cb8-126">Sonra çözüme Error. aspx adlı bir sayfa ekleyin ve bu biçimlendirme kod parçacığını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="d4cb8-127">Şimdi sayfada olay işleyicisini yükle\_, Istek nesnesinden hata iletilerini ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="d4cb8-128">İşleminin</span><span class="sxs-lookup"><span data-stu-id="d4cb8-128">Conclusion</span></span>

<span data-ttu-id="d4cb8-129">ASP.NET WebForms 'in veritabanı erişimi, üyeliği, AJAX vb. ile gelişmiş bir Web sitesi oluşturmayı daha kolay bir şekilde gördük.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="d4cb8-130">oldukça hızlı.</span><span class="sxs-lookup"><span data-stu-id="d4cb8-130">pretty quickly.</span></span>

<span data-ttu-id="d4cb8-131">Bu öğreticide, kendi ASP.NET WebForms uygulamalarınızı oluşturmaya başlamak için ihtiyacınız olan araçları vermiş olursunuz!</span><span class="sxs-lookup"><span data-stu-id="d4cb8-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d4cb8-132">Öncekini</span><span class="sxs-lookup"><span data-stu-id="d4cb8-132">Previous</span></span>](tailspin-spyworks-part-7.md)
