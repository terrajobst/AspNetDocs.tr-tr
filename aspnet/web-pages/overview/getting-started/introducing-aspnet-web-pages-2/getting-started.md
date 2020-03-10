---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: Başlarken | Microsoft Docs
author: Rick-Anderson
description: WebMatrix artık ASP.NET Web sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez. Visual Studio veya Visual Studio Code kullanın. Bu kılavuz bir...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: bb863f8605e6f8faca3b285607b63a3e88e83012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547105"
---
# <a name="getting-started"></a><span data-ttu-id="d8c2c-105">Başlarken</span><span class="sxs-lookup"><span data-stu-id="d8c2c-105">Getting Started</span></span>

<span data-ttu-id="d8c2c-106">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="d8c2c-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > <span data-ttu-id="d8c2c-107">WebMatrix artık ASP.NET Web sayfaları için tümleşik bir geliştirme ortamı olarak önerilmez.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-107">WebMatrix is no longer recommended as an integrated development environment for ASP.NET Web Pages.</span></span> <span data-ttu-id="d8c2c-108">[Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) veya [Visual Studio Code](https://code.visualstudio.com/)kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-108">Use [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) or [Visual Studio Code](https://code.visualstudio.com/).</span></span>
> 
> 
> <span data-ttu-id="d8c2c-109">Bu kılavuz ve uygulama, ASP.NET Web sayfalarına (sürüm 2 veya üzeri) genel bir bakış ve Razor söz dizimi, dinamik Web siteleri oluşturmaya yönelik basit bir çerçeve sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-109">This guidance and application gives you an overview of ASP.NET Web Pages (version 2 or later) and Razor syntax, a lightweight framework for creating dynamic websites.</span></span> <span data-ttu-id="d8c2c-110">Ayrıca, sayfa ve site oluşturmaya yönelik bir araç olan WebMatrix 'i de tanıtır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-110">It also introduces WebMatrix, a tool for creating pages and sites.</span></span>
> 
> <span data-ttu-id="d8c2c-111">**Düzey**: ASP.NET Web Pages 'e yeni.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-111">**Level**: New to ASP.NET Web Pages.</span></span>  
> <span data-ttu-id="d8c2c-112">**Kabul edilen yetenekler**: HTML, temel geçişli stil sayfaları (CSS).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-112">**Skills assumed**: HTML, basic cascading style sheets (CSS).</span></span>
> 
> <span data-ttu-id="d8c2c-113">Bu, küme ilk öğreticisinde öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-113">What you'll learn in the first tutorial of the set:</span></span>
> 
> - <span data-ttu-id="d8c2c-114">Web sayfaları teknolojisinin ne olduğu ve ne için ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-114">What ASP.NET Web Pages technology is and what it's for.</span></span>
> - <span data-ttu-id="d8c2c-115">WebMatrix nedir?</span><span class="sxs-lookup"><span data-stu-id="d8c2c-115">What WebMatrix is.</span></span>
> - <span data-ttu-id="d8c2c-116">Her şeyi nasıl yükleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-116">How to install everything.</span></span>
> - <span data-ttu-id="d8c2c-117">WebMatrix kullanarak Web sitesi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-117">How to create a website by using WebMatrix.</span></span>
>   
> 
> <span data-ttu-id="d8c2c-118">Ele alınan özellikler/teknolojiler:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-118">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="d8c2c-119">Microsoft Web Platformu Yükleyicisi.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-119">Microsoft Web Platform Installer.</span></span>
> - <span data-ttu-id="d8c2c-120">WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-120">WebMatrix.</span></span>
> - <span data-ttu-id="d8c2c-121">*. cshtml* sayfaları</span><span class="sxs-lookup"><span data-stu-id="d8c2c-121">*.cshtml* pages</span></span>
>   
> 
> <span data-ttu-id="d8c2c-122">Mike Pope başlangıçta bu öğreticiyi yazdı.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-122">Mike Pope originally wrote this tutorial.</span></span> <span data-ttu-id="d8c2c-123">Tom FitzMacken, Microsoft WebMatrix 3 için güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-123">Tom FitzMacken updated it for Microsoft WebMatrix 3.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d8c2c-124">Öğreticide kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="d8c2c-124">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d8c2c-125">ASP.NET Web sayfaları (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="d8c2c-125">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="d8c2c-126">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="d8c2c-126">WebMatrix 3</span></span>

## <a name="what-should-you-know"></a><span data-ttu-id="d8c2c-127">Ne bilmeniz gerekir?</span><span class="sxs-lookup"><span data-stu-id="d8c2c-127">What Should You Know?</span></span>

<span data-ttu-id="d8c2c-128">Hakkında bilgi sahibi olduğunuzu varsayıyoruz:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-128">We're assuming that you're familiar with:</span></span>

- <span data-ttu-id="d8c2c-129">**HTML**.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-129">**HTML**.</span></span> <span data-ttu-id="d8c2c-130">Ayrıntılı uzmanlık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-130">No in-depth expertise is required.</span></span> <span data-ttu-id="d8c2c-131">HTML açıklanmayacağız, ancak karmaşık bir şeyi de kullanmıyoruz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-131">We won't explain HTML, but we also don't use anything complex.</span></span> <span data-ttu-id="d8c2c-132">Yararlı olduğunu düşündüğdiğimiz HTML öğreticilerine bağlantılar sağlıyoruz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-132">We'll provide links to HTML tutorials where we think they're useful.</span></span>
- <span data-ttu-id="d8c2c-133">**Geçişli stil sayfaları (CSS)** .</span><span class="sxs-lookup"><span data-stu-id="d8c2c-133">**Cascading style sheets (CSS)**.</span></span> <span data-ttu-id="d8c2c-134">HTML ile aynı.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-134">Same as with HTML.</span></span>
- <span data-ttu-id="d8c2c-135">**Temel veritabanı fikirleri**.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-135">**Basic database ideas**.</span></span> <span data-ttu-id="d8c2c-136">Veriler için bir elektronik tablo kullandıysanız ve verileri sıraladıysanız ve filtrelediyseniz bu, genellikle bu öğretici kümesini kabul ettiğimiz uzmanlık düzeyidir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-136">If you've used a spreadsheet for data and sorted and filtered the data, that's the level of expertise we're generally assuming for this tutorial set.</span></span>

<span data-ttu-id="d8c2c-137">Ayrıca temel programlama hakkında bilgi edinmek istediğinizi varsayıyoruz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-137">We're also assuming that you're interested in learning basic programming.</span></span> <span data-ttu-id="d8c2c-138">ASP.NET Web sayfaları adlı C#bir programlama dili kullanır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-138">ASP.NET Web Pages use a programming language called C#.</span></span> <span data-ttu-id="d8c2c-139">Yalnızca bir ilgilendiğiniz bir arka plana sahip olmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-139">You don't have to have any background in programming, just an interest in it.</span></span> <span data-ttu-id="d8c2c-140">Bir Web sayfasında daha önce hiç JavaScript yazdıysanız, çok sayıda arka plana sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-140">If you've ever written any JavaScript in a web page before, you've got plenty of background.</span></span>

<span data-ttu-id="d8c2c-141">Programlama hakkında bilginiz varsa, yeni programcılar hızla hızlanırken Bu öğreticinin başlangıçta yavaş taşındığını fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-141">Note that if you are familiar with programming, you might find that this tutorial set initially moves slowly while we bring new programmers up to speed.</span></span> <span data-ttu-id="d8c2c-142">Ancak ilk birkaç öğreticiden yararlandığımız için, açıklanmanız gereken daha az temel programlama olacaktır ve diğer bir deyişle daha hızlı bir klibe göre hareket eder.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-142">As we get past the first few tutorials, though, there will be less basic programming to explain and things will move along at a faster clip.</span></span>

## <a name="what-do-you-need"></a><span data-ttu-id="d8c2c-143">Ne gerekir?</span><span class="sxs-lookup"><span data-stu-id="d8c2c-143">What Do You Need?</span></span>

<span data-ttu-id="d8c2c-144">İşte gerekenler:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-144">Here's what you'll need:</span></span>

- <span data-ttu-id="d8c2c-145">Windows 8, Windows 7, Windows Server 2008 veya Windows Server 2012 çalıştıran bir bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-145">A computer that is running Windows 8, Windows 7, Windows Server 2008, or Windows Server 2012.</span></span>
- <span data-ttu-id="d8c2c-146">Canlı bir internet bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-146">A live internet connection.</span></span>
- <span data-ttu-id="d8c2c-147">Yönetici ayrıcalıkları (yükleme işlemi için gereklidir).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-147">Administrator privileges (required for the installation process).</span></span>

## <a name="what-is-aspnet-web-pages"></a><span data-ttu-id="d8c2c-148">ASP.NET Web sayfaları nedir?</span><span class="sxs-lookup"><span data-stu-id="d8c2c-148">What Is ASP.NET Web Pages?</span></span>

<span data-ttu-id="d8c2c-149">ASP.NET Web sayfaları, dinamik Web sayfaları oluşturmak için kullanabileceğiniz bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-149">ASP.NET Web Pages is a framework that you can use to create dynamic web pages.</span></span> <span data-ttu-id="d8c2c-150">Basit bir HTML Web sayfası statiktir; içeriği, sayfada bulunan sabit HTML biçimlendirmesine göre belirlenir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-150">A simple HTML web page is static; its content is determined by the fixed HTML markup that's in the page.</span></span> <span data-ttu-id="d8c2c-151">ASP.NET Web sayfaları ile oluşturduğunuz gibi dinamik sayfalar, kod kullanarak sayfa içeriğini anında oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-151">Dynamic pages like those you create with ASP.NET Web Pages let you create the page content on the fly, by using code.</span></span>

<span data-ttu-id="d8c2c-152">Dinamik sayfalar her türlü şeyi yapmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-152">Dynamic pages let you do all sorts of things.</span></span> <span data-ttu-id="d8c2c-153">Bir form kullanarak kullanıcıdan giriş yapmasını isteyebilir ve sonra sayfanın ne şekilde görüneceğini veya görünüşünü değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-153">You can ask a user for input by using a form and then change what the page displays or how it looks.</span></span> <span data-ttu-id="d8c2c-154">Bir kullanıcıdan bilgi alabilir, veritabanını bir veritabanına kaydedebilir ve daha sonra listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-154">You can take information from a user, save it in a database, and then list it later.</span></span> <span data-ttu-id="d8c2c-155">Sitenizden e-posta gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-155">You can send email from your site.</span></span> <span data-ttu-id="d8c2c-156">Web üzerinde diğer hizmetlerle (örneğin, bir eşleme hizmeti) etkileşim kurabilir ve bu kaynaklardaki bilgileri tümleştiren sayfalar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-156">You can interact with other services on the web (for example, a mapping service) and produce pages that integrate information from those sources.</span></span>

## <a name="what-is-webmatrix"></a><span data-ttu-id="d8c2c-157">WebMatrix nedir?</span><span class="sxs-lookup"><span data-stu-id="d8c2c-157">What is WebMatrix?</span></span>

<span data-ttu-id="d8c2c-158">WebMatrix, bir Web sayfası düzenleyicisini, bir veritabanı yardımcı programını, sayfaları test etmek için bir Web sunucusunu ve Web sitenizi Internet 'Te yayımlamaya yönelik özellikleri tümleştiren bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-158">WebMatrix is a tool that integrates a web page editor, a database utility, a web server for testing pages, and features for publishing your website to the Internet.</span></span> <span data-ttu-id="d8c2c-159">WebMatrix ücretsizdir ve kolayca yüklenebilir ve kolayca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-159">WebMatrix is free, and it's easy to install and easy to use.</span></span> <span data-ttu-id="d8c2c-160">(Aynı zamanda yalnızca düz HTML sayfaları için de ve PHP gibi diğer teknolojiler için de kullanılır.)</span><span class="sxs-lookup"><span data-stu-id="d8c2c-160">(It also works for just plain HTML pages, as well as for other technologies like PHP.)</span></span>

<span data-ttu-id="d8c2c-161">ASP.NET Web sayfalarıyla çalışmak *için gerçekten WebMatrix kullanmanız gerekmez.*</span><span class="sxs-lookup"><span data-stu-id="d8c2c-161">You don't actually *have* to use WebMatrix to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="d8c2c-162">Bir metin düzenleyicisini kullanarak (örneğin, erişiminiz olan bir Web sunucusu kullanarak) sayfalar oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-162">You can create pages by using a text editor, for example, and test pages by using a web server that you have access to.</span></span> <span data-ttu-id="d8c2c-163">Ancak WebMatrix, bu öğreticiyi çok kolay hale getiriyor. böylece, bu öğreticiler genelinde WebMatrix kullanacaktır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-163">However, WebMatrix makes it all very easy, so these tutorials will use WebMatrix throughout.</span></span>

## <a name="about-these-tutorials"></a><span data-ttu-id="d8c2c-164">Bu öğreticiler hakkında</span><span class="sxs-lookup"><span data-stu-id="d8c2c-164">About These Tutorials</span></span>

<span data-ttu-id="d8c2c-165">Bu öğretici kümesi, ASP.NET Web sayfalarının nasıl kullanılacağına ilişkin bir giriş niteliğindedir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-165">This tutorial set is an introduction to how to use ASP.NET Web Pages.</span></span> <span data-ttu-id="d8c2c-166">Bu tanıtım öğreticisi kümesinde 9 öğretici toplamı vardır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-166">There are 9 tutorials total in this introductory tutorial set.</span></span> <span data-ttu-id="d8c2c-167">Bu, ASP.NET Web sayfalarından acemi olarak gerçek, profesyonel görünümlü Web siteleri oluşturmaya yönelik bir dizi öğretici kümesinin parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-167">It's part of a series of tutorial sets that takes you from ASP.NET Web Pages novice to creating real, professional-looking websites.</span></span>

<span data-ttu-id="d8c2c-168">Bu ilk öğretici, ASP.NET Web sayfalarıyla çalışma hakkında temel bilgileri göstermeye yönelik olarak yoğunlaşır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-168">This first tutorial set concentrates on showing you the basics of how to work with ASP.NET Web Pages.</span></span> <span data-ttu-id="d8c2c-169">İşiniz bittiğinde, bu en son nerede bittiğini ve Web sayfalarını daha ayrıntılı bir şekilde keşfetmenizi sağlayan ek öğretici kümeleriyle çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-169">When you're done, you can work with additional tutorial sets that pick up where this one ends and that explore Web Pages in more depth.</span></span>

<span data-ttu-id="d8c2c-170">Derinlemesine açıklamaları bilerek daha kolay bir şekilde geçtik.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-170">We deliberately go easy on the in-depth explanations.</span></span> <span data-ttu-id="d8c2c-171">Her şeyi gösterdiğimiz zaman, bu öğretici için en kolay anlaşılması gereken yöntemi her zaman seçtik.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-171">And whenever we show something, for this tutorial set we always choose the way that we think is easiest to understand.</span></span> <span data-ttu-id="d8c2c-172">Sonraki öğretici kümeleri daha ayrıntılı bir şekilde geçer ve daha verimli veya daha esnek yaklaşımlara (Ayrıca daha eğlenceli) sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-172">Later tutorial sets go into more depth and show you more efficient or more flexible approaches (also more fun).</span></span> <span data-ttu-id="d8c2c-173">Ancak bu öğreticiler öncelikle temel kavramları anlamanıza gerek duyar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-173">But those tutorials require you to understand the basics first.</span></span>

<span data-ttu-id="d8c2c-174">Yeni başlattığınız öğretici kümesi, ASP.NET Web sayfalarının şu özelliklerini içerir:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-174">The tutorial set you've just started covers these features of ASP.NET Web Pages:</span></span>

- <span data-ttu-id="d8c2c-175">Giriş ve yükleme her şeyi alma.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-175">Introduction and getting everything installed.</span></span> <span data-ttu-id="d8c2c-176">(Bu, okuduğunuz öğreticide.)</span><span class="sxs-lookup"><span data-stu-id="d8c2c-176">(That's in the tutorial you're reading.)</span></span>
- <span data-ttu-id="d8c2c-177">ASP.NET Web sayfaları programlamasına ilişkin temel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-177">The basics of ASP.NET Web Pages programming.</span></span>
- <span data-ttu-id="d8c2c-178">Veritabanı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-178">Creating a database.</span></span>
- <span data-ttu-id="d8c2c-179">Kullanıcı giriş formu oluşturma ve işleme.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-179">Creating and processing a user input form.</span></span>
- <span data-ttu-id="d8c2c-180">Veritabanına veri ekleme, güncelleştirme ve silme.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-180">Adding, updating, and deleting data in the database.</span></span>

## <a name="what-will-you-create"></a><span data-ttu-id="d8c2c-181">Ne oluşturmanız gerekir?</span><span class="sxs-lookup"><span data-stu-id="d8c2c-181">What Will You Create?</span></span>

<span data-ttu-id="d8c2c-182">Bu öğretici, ve sonraki bir Web sitesi etrafında, istediğiniz filmleri listeleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-182">This tutorial set and subsequent ones revolve around a website where you can list movies that you like.</span></span> <span data-ttu-id="d8c2c-183">Film girebilir, düzenleyebilir ve listeleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-183">You'll be able to enter movies, edit them, and list them.</span></span> <span data-ttu-id="d8c2c-184">Bu öğretici kümesinde oluşturacağınız sayfaların birkaç tanesini aşağıda bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-184">Here are a couple of the pages you'll create in this tutorial set.</span></span> <span data-ttu-id="d8c2c-185">İlki oluşturacağınız film listesi sayfasını gösterir:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-185">The first one shows the movie listing page that you'll create:</span></span>

![Bir film listesini gösteren ince bir film uygulaması](getting-started/_static/image1.png)

<span data-ttu-id="d8c2c-187">Sitenize yeni film bilgileri eklemenizi sağlayan sayfa:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-187">And here's the page that lets you add new movie information to your site:</span></span>

![Film Ekle sayfasını gösteren tamamlanmış film uygulaması](getting-started/_static/image2.png)

<span data-ttu-id="d8c2c-189">Sonraki öğretici, bu küme üzerinde derleme yapar ve resim yükleme, kullanıcıların oturum açmasına, e-posta göndererek ve sosyal medya tümleştirmesiyle tümleştirme gibi daha fazla işlevsellik ekler.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-189">Subsequent tutorial sets build on this set and add more functionality, like uploading pictures, letting people log in, sending email, and integrating with social media.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="d8c2c-190">Bkz. Azure 'da çalışan bu uygulama</span><span class="sxs-lookup"><span data-stu-id="d8c2c-190">See this App Running on Azure</span></span>

<span data-ttu-id="d8c2c-191">Canlı bir Web uygulaması olarak çalışan tamamlanmış siteyi görmek istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="d8c2c-191">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="d8c2c-192">Aşağıdaki düğmeye tıklayarak uygulamanın tüm sürümünü Azure hesabınıza dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-192">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

<span data-ttu-id="d8c2c-193">Bu çözümü Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-193">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="d8c2c-194">Henüz bir hesabınız yoksa, aşağıdaki seçeneklere sahip olursunuz:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-194">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="d8c2c-195">[Ücretsiz bir Azure hesabı açarak](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler edinin ve hatta kullanıldıktan sonra bile hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-195">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="d8c2c-196">[MSDN abonesi avantajlarınızı etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-196">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="installing-everything"></a><span data-ttu-id="d8c2c-197">Her şeyi yükleme</span><span class="sxs-lookup"><span data-stu-id="d8c2c-197">Installing Everything</span></span>

<span data-ttu-id="d8c2c-198">Her şeyi Microsoft 'un Web Platformu Yükleyicisi ' ni kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-198">You can install everything by using the Web Platform Installer from Microsoft.</span></span> <span data-ttu-id="d8c2c-199">Aslında, yükleyiciyi yüklersiniz ve ardından başka her şeyi yüklemek için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-199">In effect, you install the installer, and then use it to install everything else.</span></span>

<span data-ttu-id="d8c2c-200">Web sayfalarını kullanmak için, SP3 yüklü en az Windows XP veya Windows Server 2008 veya sonraki bir sürümü olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-200">To use Web Pages, you have to be have at least Windows XP with SP3 installed, or Windows Server 2008 or later.</span></span>

<span data-ttu-id="d8c2c-201">ASP.NET Web sitesinin [Web sayfaları sayfasında](../../../index.md) , **yükler**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-201">On the [Web Pages page](../../../index.md) of the ASP.NET website, click **Install**.</span></span>

![ASP.NET &quot;&quot; düğmesini gösteren Web sitesi](getting-started/_static/image3.png)

<span data-ttu-id="d8c2c-203">WebMatrix 'i yüklemeden önce lisans koşullarını ve gizlilik bildirimini kabul etmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-203">You are asked to accept the license terms and privacy statement before installing WebMatrix.</span></span>

![yüklemeyi başlatmak için terimi kabul et](getting-started/_static/image4.png)

<span data-ttu-id="d8c2c-205">Yüklemeyi başlatmak için **Çalıştır** ' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-205">Click **Run** to start the installation.</span></span> <span data-ttu-id="d8c2c-206">(Yükleyiciyi kaydetmek istiyorsanız **Kaydet** ' e tıklayın ve ardından dosyayı kaydettiğiniz klasörden çalıştırın.)</span><span class="sxs-lookup"><span data-stu-id="d8c2c-206">(If you want to save the installer, click **Save** and then run the installer from the folder where you saved it.)</span></span>

![](getting-started/_static/image5.png)

<span data-ttu-id="d8c2c-207">Web Platformu Yükleyicisi, WebMatrix yüklenmeye hazırlanmaya yönelik olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-207">The Web Platform Installer appears, ready to install WebMatrix.</span></span> <span data-ttu-id="d8c2c-208">**Yükle**'ye tıklatın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-208">Click **Install**.</span></span>

![](getting-started/_static/image6.png)

<span data-ttu-id="d8c2c-209">Yükleme işlemi, bilgisayarınıza yüklemek için neler olduğunu ve işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-209">The installation process figures out what it has to install on your computer and starts the process.</span></span> <span data-ttu-id="d8c2c-210">Tam olarak yüklenmesi gereken seçeneklere bağlı olarak, işlem birkaç dakika ile birkaç dakikaya kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-210">Depending on what exactly has to be installed, the process can take anywhere from a few moments to several minutes.</span></span> <span data-ttu-id="d8c2c-211">Lisans koşullarını kabul etmek için **kabul ediyorum** ' u seçin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-211">Select **I Accept** to accept the license terms.</span></span>

## <a name="hello-webmatrix"></a><span data-ttu-id="d8c2c-212">Merhaba, WebMatrix</span><span class="sxs-lookup"><span data-stu-id="d8c2c-212">Hello, WebMatrix</span></span>

<span data-ttu-id="d8c2c-213">İşlem tamamlandığında, yükleme işlemi WebMatrix 'i otomatik olarak başlatabilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-213">When it's done, the installation process can launch WebMatrix automatically.</span></span> <span data-ttu-id="d8c2c-214">Değilse, Windows 'ta, **Başlat** menüsünde **Microsoft WebMatrix**' i başlatın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-214">If it doesn't, in Windows, from the **Start** menu, launch **Microsoft WebMatrix**.</span></span>

<span data-ttu-id="d8c2c-215">WebMatrix 'i ilk kez başlattığınızda, Microsoft hesabı Microsoft Azure için oturum açma şansı vermiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-215">When you launch WebMatrix for the first time, you are given a chance to sign in to Microsoft Azure with your Microsoft account.</span></span> <span data-ttu-id="d8c2c-216">Oturum açarak, Azure üzerinden 10 Ücretsiz Web uygulaması alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-216">By signing in, you will receive 10 free web apps through Azure.</span></span> <span data-ttu-id="d8c2c-217">Bu ücretsiz web uygulamaları, uygulamalarınızı test etmek için kullanışlı bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-217">These free web apps provide a convenient way to test your apps.</span></span> <span data-ttu-id="d8c2c-218">Henüz bir Azure hesabınız yoksa ancak bir MSDN aboneliğiniz varsa, [MSDN abonelik avantajlarınızı etkinleştirebilirsiniz](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-218">If you don't already have an Azure account, but you do have an MSDN subscription, you can [activate your MSDN subscription benefits](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="d8c2c-219">Aksi takdirde, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-219">Otherwise, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d8c2c-220">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-220">For details, see [Azure Free Trial](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).</span></span>

<span data-ttu-id="d8c2c-221">Bu öğreticiye devam etmek için hemen oturum açmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-221">You do not have to sign in right now to continue with this tutorial.</span></span> <span data-ttu-id="d8c2c-222">Şimdi oturum açmanız durumunda daha sonra oturum açma seçeneğiniz de vardır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-222">If you do not sign in now, you will still have the option to sign in later.</span></span> <span data-ttu-id="d8c2c-223">Bu öğretici serisindeki son [Konu](publishing.md) , Web sitenizin Azure 'a nasıl dağıtılacağını anlatmaktadır; Bu nedenle, bu konuyu tamamlayabilmeniz için oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-223">The last [topic](publishing.md) in this tutorial series covers how to deploy your website to Azure; therefore, you would need to sign in to complete that topic.</span></span>

<span data-ttu-id="d8c2c-224">Bu noktada, Microsoft hesabı oturum açın ya da sağ alt köşede **Şimdi değil** ' i seçin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-224">At this point, either sign in with your Microsoft account or select **Not Now** in the lower right corner.</span></span>

![Oturum Açma](getting-started/_static/image7.png)

<span data-ttu-id="d8c2c-226">Başlamak için boş bir Web sitesi oluşturacak ve bir sayfa ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-226">To begin, you'll create a blank website and add a page.</span></span> <span data-ttu-id="d8c2c-227">Bu küme içindeki sonraki bir öğreticide, yerleşik web sitesi şablonlarından biriyle oynayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-227">In a later tutorial in this set you'll play with one of the built-in website templates.</span></span>

<span data-ttu-id="d8c2c-228">Başlat penceresinde **Yeni**' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-228">In the start window, click **New**.</span></span>

![WebMatrix başlangıç ekranı](getting-started/_static/image8.png)

<span data-ttu-id="d8c2c-230">Şablonlar, farklı Web sitesi türleri için önceden oluşturulmuş dosya ve sayfalardır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-230">Templates are prebuilt files and pages for different types of websites.</span></span> <span data-ttu-id="d8c2c-231">Varsayılan olarak kullanılabilen tüm şablonları görmek için Şablon Galerisi seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-231">To see all of the templates that are available by default, select the Template Gallery option.</span></span>

![Şablon galerisini seçin](getting-started/_static/image9.png)

<span data-ttu-id="d8c2c-233">**Hızlı başlangıç** penceresinde, **ASP.net** grubundan **boş site** ' yi seçin ve "webpagesfilmlerini" adlı yeni siteyi adlandırın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-233">In the **Quick Start** window, select **Empty Site** from the **ASP.NET** group and name the new site "WebPagesMovies".</span></span>

![Boş site şablonu seçiliyken WebMatrix hızlı başlangıç penceresi](getting-started/_static/image10.png)

<span data-ttu-id="d8c2c-235">**İleri**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-235">Click **Next**.</span></span>

<span data-ttu-id="d8c2c-236">Microsoft hesabı oturum açtıysanız, Azure 'da site oluşturma fırsatı vermiş olursunuz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-236">If you have signed in to your Microsoft account, you will be given the opportunity to create the site on Azure.</span></span> <span data-ttu-id="d8c2c-237">Sitenizin adına bağlı olarak, **WebPagesMovies.azurewebsites.net** varsayılan adı önerilir; Ancak, ünlem işareti bu adın Microsoft Azure 'da mevcut olmadığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-237">Based on the name of your site, the default name of **WebPagesMovies.azurewebsites.net** is suggested; however, the exclamation point indicates that this name is not available on Windows Azure.</span></span> <span data-ttu-id="d8c2c-238">Basitlik için, şimdi Web sitesini Azure 'da oluşturmayı atlamak için **Atla** ' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-238">For simplicity, select **Skip** to bypass creating the web site on Azure right now.</span></span> <span data-ttu-id="d8c2c-239">Bu serinin ilerleyen kısımlarında, siteyi Azure 'da yayımlayacağız.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-239">Later in this series, we will publish the site to Azure.</span></span>

![Azure sitesi oluştur](getting-started/_static/image11.png)

<span data-ttu-id="d8c2c-241">WebMatrix, siteyi oluşturur ve açar:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-241">WebMatrix creates and opens the site:</span></span>

![WebMatrix 'te yeni Webpagesfilmlerini sitesi açık](getting-started/_static/image12.png)

<span data-ttu-id="d8c2c-243">En üstte, hızlı erişim araç çubuğu ve bir şerit vardır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-243">At the top, there's a Quick Access Toolbar and a ribbon.</span></span> <span data-ttu-id="d8c2c-244">Sol altta, görevler arasında geçiş yaptığınız çalışma alanı seçiciyi görürsünüz (**site**, **dosyalar**, **veritabanları**, **raporlar**).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-244">At the bottom left, you see the workspace selector where you switch between tasks (**Site**, **Files**, **Databases**, **Reports**).</span></span> <span data-ttu-id="d8c2c-245">Sağ tarafta, düzenleyicinin ve raporların İçerik bölmesi bulunur.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-245">On the right is the content pane for the editor and for reports.</span></span> <span data-ttu-id="d8c2c-246">Ayrıca, iletiler için zaman zaman bir bildirim çubuğu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-246">And across the bottom you'll occasionally see a notification bar for messages.</span></span>

<span data-ttu-id="d8c2c-247">Bu öğreticilerle ilgili olarak WebMatrix ve özellikleri hakkında daha fazla bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-247">You'll learn more about WebMatrix and its features as you go through these tutorials.</span></span>

## <a name="creating-a-web-page"></a><span data-ttu-id="d8c2c-248">Web sayfası oluşturma</span><span class="sxs-lookup"><span data-stu-id="d8c2c-248">Creating a Web Page</span></span>

<span data-ttu-id="d8c2c-249">WebMatrix ve ASP.NET Web sayfalarıyla ilgili bilgi almak için basit bir sayfa oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-249">To become familiar with WebMatrix and ASP.NET Web Pages, you'll create a simple page.</span></span>

<span data-ttu-id="d8c2c-250">Çalışma alanı seçicide **dosyalar** çalışma alanını seçin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-250">In the workspace selector, select the **Files** workspace.</span></span> <span data-ttu-id="d8c2c-251">Bu çalışma alanı dosya ve klasörlerle çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-251">This workspace lets you work with files and folders.</span></span> <span data-ttu-id="d8c2c-252">Sol bölmede sitenizin dosya yapısı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-252">The left pane shows the file structure of your site.</span></span> <span data-ttu-id="d8c2c-253">Şerit, dosyayla ilgili görevleri gösterecek şekilde değişir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-253">The ribbon changes to show file-related tasks.</span></span>

![WebMatrix 'te dosya çalışma alanı](getting-started/_static/image13.png)

<span data-ttu-id="d8c2c-255">Şeritte, **Yeni** ' nin altındaki oka ve ardından **yeni dosya**' ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-255">In the ribbon, click the arrow under **New** and then click **New File**.</span></span>

![Yeni bir dosya oluşturmak için Şeritteki &quot;yeni&quot; komutunu kullanma](getting-started/_static/image14.png)

<span data-ttu-id="d8c2c-257">WebMatrix, dosya türlerinin bir listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-257">WebMatrix displays a list of file types.</span></span> <span data-ttu-id="d8c2c-258">**Cshtml**'yi seçin ve **ad** kutusuna "HelloWorld" yazın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-258">Select **CSHTML**, and in the **Name** box, type "HelloWorld".</span></span> <span data-ttu-id="d8c2c-259">CSHTML sayfası bir ASP.NET Web sayfaları sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-259">A CSHTML page is an ASP.NET Web Pages page.</span></span>

![HelloWorld. cshtml adlı yeni bir CSHTML sayfası oluşturuluyor](getting-started/_static/image15.png)

<span data-ttu-id="d8c2c-261">**Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-261">Click **OK**.</span></span>

<span data-ttu-id="d8c2c-262">WebMatrix sayfayı oluşturur ve düzenleyicide açar.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-262">WebMatrix creates the page and opens it in the editor.</span></span>

![WebMatrix düzenleyicideki yeni HelloWorld sayfası](getting-started/_static/image16.png)

<span data-ttu-id="d8c2c-264">Gördüğünüz gibi, en üstte yer alan bir blok haricinde, sayfada çoğunlukla sıradan HTML biçimlendirmesi bulunur:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-264">As you can see, the page contains mostly ordinary HTML markup, except for a block at the top that looks like this:</span></span>

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

<span data-ttu-id="d8c2c-265">Bu, kısa süre içinde göreceğiniz gibi kod ekleme içindir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-265">That's for adding code, as you'll see shortly.</span></span>

<span data-ttu-id="d8c2c-266">Sayfanın farklı bölümlerinin öğe adlarının, özniteliklerin ve metinlerin yanı sıra üstteki bloğun de &mdash; farklı renklerde olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-266">Notice that the different parts of the page &mdash; the element names, attributes, and text, plus the block at the top — are all in different colors.</span></span> <span data-ttu-id="d8c2c-267">Buna *sözdizimi vurgulama*denir ve her şeyin açık kalmasını kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-267">This is called *syntax highlighting*, and it makes it easier to keep everything clear.</span></span> <span data-ttu-id="d8c2c-268">WebMatrix 'te Web sayfalarıyla çalışmayı kolaylaştıran özelliklerden biridir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-268">It's one of the features that makes it easy to work with web pages in WebMatrix.</span></span>

<span data-ttu-id="d8c2c-269">Aşağıdaki örnekte olduğu gibi `<head>` ve `<body>` öğeleri için içerik ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-269">Add content for the `<head>` and `<body>` elements like in the following example.</span></span> <span data-ttu-id="d8c2c-270">(İsterseniz, yalnızca aşağıdaki bloğu kopyalayabilir ve var olan sayfanın tamamını bu kodla değiştirebilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="d8c2c-270">(If you want, you can just copy the following block and replace the entire existing page with this code.)</span></span>

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

<span data-ttu-id="d8c2c-271">Hızlı erişim araç çubuğunda veya **Dosya** menüsünde **Kaydet**' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-271">In the Quick Access Toolbar or in the **File** menu, click **Save**.</span></span>

![WebMatrix hızlı erişim araç çubuğunda Kaydet düğmesi](getting-started/_static/image17.png)

## <a name="testing-the-page"></a><span data-ttu-id="d8c2c-273">Sayfayı test etme</span><span class="sxs-lookup"><span data-stu-id="d8c2c-273">Testing the Page</span></span>

<span data-ttu-id="d8c2c-274">**Dosyalar** çalışma alanında *HelloWorld. cshtml* sayfasına sağ tıklayın ve ardından **tarayıcıda Başlat**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-274">In the **Files** workspace, right-click the *HelloWorld.cshtml* page and then click **Launch in browser**.</span></span>

![WebMatrix şeridinde Çalıştır düğmesini kullanarak bir sayfa çalıştırma](getting-started/_static/image18.png)

<span data-ttu-id="d8c2c-276">WebMatrix, bilgisayarınızdaki sayfaları test etmek için kullanabileceğiniz yerleşik bir Web sunucusu (IIS Express) başlatır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-276">WebMatrix starts a built-in web server (IIS Express) that you can use to test pages on your computer.</span></span> <span data-ttu-id="d8c2c-277">(WebMatrix 'te IIS Express olmadan, test etmeden önce sayfanızı bir Web sunucusuna yayımlamanız gerekir.) Sayfa varsayılan tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-277">(Without IIS Express in WebMatrix, you'd have to publish your page to a web server somewhere before you could test it.) The page is displayed in your default browser.</span></span>

![tarayıcıda çalışan &quot;Merhaba Dünya&quot; sayfası](getting-started/_static/image19.png)

<span data-ttu-id="d8c2c-279">WebMatrix 'te bir sayfayı test ettiğinizde, tarayıcıdaki URL, *localhost* adının yerel bir sunucuya başvurduğu `http://localhost:33651/HelloWorld.cshtml.` gibi bir şeydir, yani sayfanın kendi bilgisayarınızdaki bir Web sunucusu tarafından hizmet verdiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-279">Notice that when you test a page in WebMatrix, the URL in the browser is something like `http://localhost:33651/HelloWorld.cshtml.` The name *localhost* refers to a local server, meaning that the page is served by a web server that's on your own computer.</span></span> <span data-ttu-id="d8c2c-280">Belirtildiği gibi, WebMatrix bir sayfa başlattığınızda çalışan IIS Express adlı bir Web sunucusu programı içerir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-280">As noted, WebMatrix includes a web server program named IIS Express that runs when you launch a page.</span></span>

<span data-ttu-id="d8c2c-281">*Localhost* 'tan sonraki sayı (örneğin, *localhost: 33651*) bilgisayarınızdaki bir *bağlantı noktası numarasını* belirtir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-281">The number after *localhost* (for example, *localhost:33651*) refers to a *port number* on your computer.</span></span> <span data-ttu-id="d8c2c-282">Bu, bu Web sitesi için IIS Express kullandığı "kanal" sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-282">This is the number of the "channel" that IIS Express uses for this particular website.</span></span> <span data-ttu-id="d8c2c-283">Bağlantı noktası numarası, sitenizi oluştururken 1024 ile 65536 arasındaki aralıktan rastgele seçilir ve oluşturduğunuz her site için farklıdır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-283">The port number is selected at random from the range 1024 through 65536 when you create your site, and it's different for every site that you create.</span></span> <span data-ttu-id="d8c2c-284">(Kendi sitenizi test ettiğinizde, bağlantı noktası numarası neredeyse tamamen 33561 ' den farklı bir sayı olacaktır.) Her Web sitesi için farklı bir bağlantı noktası kullanarak IIS Express, Sitelerim 'in konuştuğu bir şekilde devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-284">(When you test your own site, the port number will almost certainly be a different number than 33561.) By using a different port for each website, IIS Express can keep straight which of your sites it's talking to.</span></span>

<span data-ttu-id="d8c2c-285">Daha sonra, sitenizi ortak bir Web sunucusuna yayımladığınızda artık URL 'de *localhost* görmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-285">Later when you publish your site to a public web server, you no longer see *localhost* in the URL.</span></span> <span data-ttu-id="d8c2c-286">Bu noktada, `http://myhostingsite/mywebsite/HelloWorld.cshtml` gibi daha tipik bir URL veya sayfanın ne olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-286">At that point, you'll see a more typical URL like `http://myhostingsite/mywebsite/HelloWorld.cshtml` or whatever the page is.</span></span> <span data-ttu-id="d8c2c-287">Bu öğretici serisinde daha sonra bir site yayımlama hakkında daha fazla bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-287">You'll learn more about publishing a site later in this tutorial series.</span></span>

## <a name="adding-some-server-side-code"></a><span data-ttu-id="d8c2c-288">Sunucu tarafı kod ekleme</span><span class="sxs-lookup"><span data-stu-id="d8c2c-288">Adding Some Server-Side Code</span></span>

<span data-ttu-id="d8c2c-289">Tarayıcıyı kapatın ve WebMatrix 'teki sayfaya geri dönün.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-289">Close the browser and go back to the page in WebMatrix.</span></span>

<span data-ttu-id="d8c2c-290">Kod bloğuna aşağıdaki kod gibi görünmesi için bir satır ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-290">Add a line to the code block so that it looks like the following code:</span></span>

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

<span data-ttu-id="d8c2c-291">Bu, çok sayıda Razor kodudur.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-291">This is a little bit of Razor code.</span></span> <span data-ttu-id="d8c2c-292">Bu, geçerli tarih ve saati aldığından ve bu değeri `currentDateTime`adlı bir *değişkene* yerleştirdiğinden büyük olasılıkla temizleyebilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-292">It's probably clear that it gets the current date and time and puts that value into a *variable* named `currentDateTime`.</span></span> <span data-ttu-id="d8c2c-293">Sonraki öğreticide Razor söz dizimi hakkında daha fazla bilgi edineceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-293">You'll read more about Razor syntax in the next tutorial.</span></span>

<span data-ttu-id="d8c2c-294">Sayfanın gövdesinde, `<p>Hello World!</p>` öğesinden sonra aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-294">In the body of the page, after the `<p>Hello World!</p>` element, add the following:</span></span>

[!code-html[Main](getting-started/samples/sample4.html)]

<span data-ttu-id="d8c2c-295">Bu kod, üstteki `currentDateTime` değişkenine yerleştirdiğiniz değeri alır ve sayfanın biçimlendirmesine ekler.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-295">This code gets the value that you put into the `currentDateTime` variable at the top and inserts it into the markup of the page.</span></span> <span data-ttu-id="d8c2c-296">`@` karakteri sayfadaki ASP.NET Web sayfaları kodunu işaretler.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-296">The `@` character marks the ASP.NET Web Pages code in the page.</span></span>

<span data-ttu-id="d8c2c-297">Sayfayı yeniden çalıştırın (WebMatrix, sayfayı çalıştırmadan önce değişiklikleri sizin için kaydeder).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-297">Run the page again (WebMatrix saves the changes for you before it runs the page).</span></span> <span data-ttu-id="d8c2c-298">Bu kez, sayfada tarih ve saati görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-298">This time you see the date and time in the page.</span></span>

![dinamik olarak üretilen zaman görüntüsü ile tarayıcıda çalışan &quot;Merhaba Dünya&quot; sayfası](getting-started/_static/image20.png)

<span data-ttu-id="d8c2c-300">Birkaç dakika bekleyin ve ardından tarayıcıda sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-300">Wait a few moments and then refresh the page in the browser.</span></span> <span data-ttu-id="d8c2c-301">Tarih ve saat görünümü güncellenir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-301">The date and time display is updated.</span></span>

<span data-ttu-id="d8c2c-302">Tarayıcıda, sayfa kaynağına bakın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-302">In the browser, look at the page source.</span></span> <span data-ttu-id="d8c2c-303">Aşağıdaki biçimlendirme gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-303">It looks like the following markup:</span></span>

[!code-html[Main](getting-started/samples/sample5.html)]

<span data-ttu-id="d8c2c-304">Üstteki `@{ }` bloğunun orada olmadığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-304">Notice that the `@{ }` block at the top isn't there.</span></span> <span data-ttu-id="d8c2c-305">Ayrıca, tarih ve saat görüntülemenin, *. cshtml* sayfasında sahip olduğunuz gibi `@currentDateTime` değil, gerçek bir karakter dizesi (`1/18/2012 2:49:50 PM` veya herhangi bir) gösterdiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-305">Also notice that the date and time display shows an actual string of characters (`1/18/2012 2:49:50 PM` or whatever), not `@currentDateTime` like you had in the *.cshtml* page.</span></span> <span data-ttu-id="d8c2c-306">Burada ne olur, sayfayı çalıştırdığınızda, ASP.NET `@`işaretlenen tüm kodları (Bu durumda çok küçük) işledi.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-306">What happened here is that when you ran the page, ASP.NET processed all the code (very little in this case) that was marked with `@`.</span></span> <span data-ttu-id="d8c2c-307">Kod çıktı üretir ve bu çıktı sayfaya eklenmiştir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-307">The code produces output, and that output was inserted into the page.</span></span>

## <a name="this-is-what-aspnet-web-pages-are-about"></a><span data-ttu-id="d8c2c-308">Bu, ASP.NET Web sayfaları hakkında</span><span class="sxs-lookup"><span data-stu-id="d8c2c-308">This Is What ASP.NET Web Pages Are About</span></span>

<span data-ttu-id="d8c2c-309">ASP.NET Web sayfalarının dinamik Web içeriği ürettiğini okuduğunuzda, bu fikir burada gördüğünüz şeydir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-309">When you read that ASP.NET Web Pages produces dynamic web content, what you've seen here is the idea.</span></span> <span data-ttu-id="d8c2c-310">Yeni oluşturduğunuz sayfa, daha önce gördüğünüz HTML işaretlemesini içerir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-310">The page you just created contains the same HTML markup that you've seen before.</span></span> <span data-ttu-id="d8c2c-311">Ayrıca, her türlü görevi gerçekleştirebilen kodu da içerebilir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-311">It can also contain code that can perform all sorts of tasks.</span></span> <span data-ttu-id="d8c2c-312">Bu örnekte, geçerli tarih ve saati alma, önemsiz bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-312">In this example, it did the trivial task of getting the current date and time.</span></span> <span data-ttu-id="d8c2c-313">Gördüğünüz gibi, sayfada çıktı üretmek için kodu bir HTML ile birlikte bırakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-313">As you saw, you can intersperse code with the HTML to produce output in the page.</span></span> <span data-ttu-id="d8c2c-314">Birisi tarayıcıda bir *. cshtml* sayfası istediğinde, ASP.NET sayfayı Web sunucusunda hala devam ederken işler.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-314">When someone requests a *.cshtml* page in the browser, ASP.NET processes the page while it's still in the hands of the web server.</span></span> <span data-ttu-id="d8c2c-315">ASP.NET kodun çıkışını (varsa) HTML olarak sayfaya ekler.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-315">ASP.NET inserts the output of the code (if any) into the page as HTML.</span></span> <span data-ttu-id="d8c2c-316">Kod işleme tamamlandığında, ASP.NET ortaya çıkan sayfayı tarayıcıya gönderir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-316">When the code processing is done, ASP.NET sends the resulting page to the browser.</span></span> <span data-ttu-id="d8c2c-317">Şimdiye kadar her bir tarayıcı HTML 'dir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-317">All the browser ever gets is HTML.</span></span> <span data-ttu-id="d8c2c-318">Diyagram aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="d8c2c-318">Here's a diagram:</span></span>

![ASP.NET 'in HTML 'i dinamik olarak nasıl üretmesinin kavramsal akışı](getting-started/_static/image21.png)

<span data-ttu-id="d8c2c-320">Fikir basittir, ancak kodun gerçekleştirebileceği çok sayıda ilginç görev vardır ve sayfaya dinamik olarak HTML içeriği ekleyebileceğiniz birçok ilginç yol vardır.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-320">The idea is simple, but there are many interesting tasks that the code can perform, and there are many interesting ways in which you can dynamically add HTML content to the page.</span></span> <span data-ttu-id="d8c2c-321">Ve ASP.NET *. cshtml* sayfaları, HERHANGI bir HTML sayfası gibi, tarayıcıda çalışan kodu da Içerebilir (JavaScript ve jQuery kodu).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-321">And ASP.NET *.cshtml* pages, like any HTML page, can also include code that runs in the browser itself (JavaScript and jQuery code).</span></span> <span data-ttu-id="d8c2c-322">Bu öğreticide ve sonraki olanlarda bu öğelerin tümünü keşfedeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-322">You'll explore all of these things in this tutorial set and in subsequent ones.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="d8c2c-323">Sonraki adımda</span><span class="sxs-lookup"><span data-stu-id="d8c2c-323">Coming Up Next</span></span>

<span data-ttu-id="d8c2c-324">Bu serinin bir sonraki öğreticide, ASP.NET Web sayfaları programlamayı biraz daha bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-324">In the next tutorial in this series, you explore ASP.NET Web Pages programming a little more.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8c2c-325">Ek Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="d8c2c-325">Additional Resources</span></span>

<span data-ttu-id="d8c2c-326">[Sıfırdan bir ASP.NET Web sitesi oluşturun](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span><span class="sxs-lookup"><span data-stu-id="d8c2c-326">[Create an ASP.NET website from scratch](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch).</span></span> <span data-ttu-id="d8c2c-327">Bu, özellikle WebMatrix (ASP.NET Web sayfaları değil) kullanımı hakkında bir öğreticidir.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-327">This is a tutorial that's specifically about using WebMatrix (not ASP.NET Web Pages).</span></span> <span data-ttu-id="d8c2c-328">Bu öğretici kümesinin kapsamayacağız bazı WebMatrix özellikleri hakkında biraz daha ayrıntıya gider.</span><span class="sxs-lookup"><span data-stu-id="d8c2c-328">It goes into a little more detail about some of the additional features of WebMatrix that we won't cover in this tutorial set.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="d8c2c-329">Next</span><span class="sxs-lookup"><span data-stu-id="d8c2c-329">Next</span></span>](intro-to-web-pages-programming.md)
