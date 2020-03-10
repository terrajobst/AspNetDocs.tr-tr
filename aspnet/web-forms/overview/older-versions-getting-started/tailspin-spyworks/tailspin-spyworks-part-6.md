---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: 'Bölüm 6: ASP.NET üyeliği | Microsoft Docs'
author: JoeStagner
description: Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır. Bölüm 6, ASP.NET üyeliği ekler.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564185"
---
# <a name="part-6-aspnet-membership"></a><span data-ttu-id="b3912-104">6\. Bölüm: ASP.NET Üyeliği</span><span class="sxs-lookup"><span data-stu-id="b3912-104">Part 6: ASP.NET Membership</span></span>

<span data-ttu-id="b3912-105">[ali Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="b3912-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="b3912-106">Tailspin Spyworks, .NET platformu için güçlü ve ölçeklenebilir uygulamalar oluşturmanın ne kadar kolay olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b3912-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="b3912-107">Alışveriş, kullanıma alma ve yönetim dahil olmak üzere çevrimiçi mağaza oluşturmak için ASP.NET 4 ' te harika yeni özelliklerin nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b3912-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="b3912-108">Bu öğretici serisi, Tailspin Spyworks örnek uygulamasını oluşturmak için kullanılan adımların tümünü ayrıntılarıyla ayrıntılardır.</span><span class="sxs-lookup"><span data-stu-id="b3912-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="b3912-109">Bölüm 6, ASP.NET üyeliği ekler.</span><span class="sxs-lookup"><span data-stu-id="b3912-109">Part 6 adds ASP.NET Membership.</span></span>

## <a id="_Toc260221672"></a><span data-ttu-id="b3912-110">ASP.NET üyeliğiyle çalışma</span><span class="sxs-lookup"><span data-stu-id="b3912-110">Working with ASP.NET Membership</span></span>

![](tailspin-spyworks-part-6/_static/image1.png)

<span data-ttu-id="b3912-111">Güvenlik 'e tıklayın</span><span class="sxs-lookup"><span data-stu-id="b3912-111">Click Security</span></span>

![](tailspin-spyworks-part-6/_static/image1.jpg)

<span data-ttu-id="b3912-112">Forms kimlik doğrulaması kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b3912-112">Make sure that we are using forms authentication.</span></span>

![](tailspin-spyworks-part-6/_static/image2.jpg)

<span data-ttu-id="b3912-113">Birkaç kullanıcı oluşturmak için "Kullanıcı Oluştur" bağlantısını kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3912-113">Use the "Create User" link to create a couple of users.</span></span>

![](tailspin-spyworks-part-6/_static/image3.jpg)

<span data-ttu-id="b3912-114">İşiniz bittiğinde Çözüm Gezgini penceresine bakın ve görünümü yenileyin.</span><span class="sxs-lookup"><span data-stu-id="b3912-114">When done, refer to the Solution Explorer window and refresh the view.</span></span>

![](tailspin-spyworks-part-6/_static/image2.png)

<span data-ttu-id="b3912-115">ASPNETDB 'nin olduğunu unutmayın. MDF ince oluşturulmuş.</span><span class="sxs-lookup"><span data-stu-id="b3912-115">Note that the ASPNETDB.MDF fine has been created.</span></span> <span data-ttu-id="b3912-116">Bu dosya, üyelik gibi çekirdek ASP.NET hizmetlerini destekleyecek tabloları içerir.</span><span class="sxs-lookup"><span data-stu-id="b3912-116">This file contains the tables to support the core ASP.NET services like membership.</span></span>

<span data-ttu-id="b3912-117">Artık kullanıma alma işlemini uygulamaya başlayabiliriz.</span><span class="sxs-lookup"><span data-stu-id="b3912-117">Now we can begin implementing the checkout process.</span></span>

<span data-ttu-id="b3912-118">Bir kullanıma alma. aspx sayfası oluşturarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="b3912-118">Begin by creating a CheckOut.aspx page.</span></span>

<span data-ttu-id="b3912-119">CheckOut. aspx sayfası yalnızca oturum açmış kullanıcılar tarafından kullanılabilir olmalıdır, bu sayede oturum açan kullanıcılara erişimi kısıtlayacağız ve oturum açan kullanıcıları oturum açma sayfasında yeniden yönlendiririz.</span><span class="sxs-lookup"><span data-stu-id="b3912-119">The CheckOut.aspx page should only be available to users who are logged in so we will restrict access to logged in users and redirect users who are not logged in to the LogIn page.</span></span>

<span data-ttu-id="b3912-120">Bunu yapmak için, Web. config dosyasının yapılandırma bölümüne aşağıdakileri ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="b3912-120">To do this we'll add the following to the configuration section of our web.config file.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

<span data-ttu-id="b3912-121">ASP.NET Web Forms uygulamalar şablonu, Web. config dosyasına otomatik olarak bir kimlik doğrulama bölümü ekledi ve varsayılan oturum açma sayfasını kurdu.</span><span class="sxs-lookup"><span data-stu-id="b3912-121">The template for ASP.NET Web Forms applications automatically added an authentication section to our web.config file and established the default login page.</span></span>

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

<span data-ttu-id="b3912-122">Kullanıcı oturum açtığında anonim bir alışveriş sepetini geçirmek için login. aspx kodu dosyasının arkasında değişiklik yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3912-122">We must modify the Login.aspx code behind file to migrate an anonymous shopping cart when the user logs in.</span></span> <span data-ttu-id="b3912-123">Sayfa\_yükleme olayını aşağıda gösterildiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b3912-123">Change the Page\_Load event as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

<span data-ttu-id="b3912-124">Ardından, oturum adını yeni oturum açmış olan kullanıcıya ayarlamak için bu şekilde bir "LoggedIn" olay işleyicisi ekleyin ve MyShoppingCart sınıfımızda MigrateCart yöntemini çağırarak alışveriş sepetindeki geçici oturum kimliğini kullanıcıya değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b3912-124">Then add a "LoggedIn" event handler like this to set the session name to the newly logged in user and change the temporary session id in the shopping cart to that of the user by calling the MigrateCart method in our MyShoppingCart class.</span></span> <span data-ttu-id="b3912-125">(. Cs dosyasında uygulandı)</span><span class="sxs-lookup"><span data-stu-id="b3912-125">(Implemented in the .cs file)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

<span data-ttu-id="b3912-126">Bunun gibi MigrateCart () yöntemini uygulayın.</span><span class="sxs-lookup"><span data-stu-id="b3912-126">Implement the MigrateCart() method like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

<span data-ttu-id="b3912-127">Kullanıma alma. aspx ' te, alışveriş sepeti sayfamızda yaptığımız kadar çok sayıda kullanıma alma sayfamızda bir EntityDataSource ve GridView kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b3912-127">In checkout.aspx we'll use an EntityDataSource and a GridView in our check out page much as we did in our shopping cart page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

<span data-ttu-id="b3912-128">GridView Denetimimizin, MyList\_Rowveriye bağlı bir "onumuza" olay işleyicisini belirttiğinden emin olmak için bu olay işleyicisini bu şekilde uygulayalim.</span><span class="sxs-lookup"><span data-stu-id="b3912-128">Note that our GridView control specifies an "ondatabound" event handler named MyList\_RowDataBound so let's implement that event handler like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

<span data-ttu-id="b3912-129">Bu yöntem, her satır bağlandığı ve GridView 'un alt satırını güncelleştiren bir alışveriş sepetinin çalışma toplamı tutar.</span><span class="sxs-lookup"><span data-stu-id="b3912-129">This method keeps a running total of the shopping cart as each row is bound and updates the bottom row of the GridView.</span></span>

<span data-ttu-id="b3912-130">Bu aşamada, yerleştirilecek siparişin bir "Gözden geçirme" sunumunu uyguladık.</span><span class="sxs-lookup"><span data-stu-id="b3912-130">At this stage we have implemented a "review" presentation of the order to be placed.</span></span>

<span data-ttu-id="b3912-131">Sayfa\_Load olayına birkaç satır kod ekleyerek boş bir sepet senaryosunu işleyelim:</span><span class="sxs-lookup"><span data-stu-id="b3912-131">Let's handle an empty cart scenario by adding a few lines of code to our Page\_Load event:</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

<span data-ttu-id="b3912-132">Kullanıcı "Gönder" düğmesine tıkladığında, Gönder düğmesine tıklama olay işleyicisi ' nde aşağıdaki kodu yürütecektir.</span><span class="sxs-lookup"><span data-stu-id="b3912-132">When the user clicks on the "Submit" button we will execute the following code in the Submit Button Click Event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

<span data-ttu-id="b3912-133">Order gönderim işleminin "et" i MyShoppingCart sınıfımız SubmitOrder () yönteminde uygulanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b3912-133">The "meat" of the order submission process is to be implemented in the SubmitOrder() method of our MyShoppingCart class.</span></span>

<span data-ttu-id="b3912-134">SubmitOrder:</span><span class="sxs-lookup"><span data-stu-id="b3912-134">SubmitOrder will:</span></span>

- <span data-ttu-id="b3912-135">Alışveriş sepetindeki tüm satır öğelerini alıp yeni bir sipariş kaydı ve ilişkili OrderDetails kayıtları oluşturmak için bunları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3912-135">Take all the line items in the shopping cart and use them to create a new Order Record and the associated OrderDetails records.</span></span>
- <span data-ttu-id="b3912-136">Sevkiyat tarihini hesaplayın.</span><span class="sxs-lookup"><span data-stu-id="b3912-136">Calculate Shipping Date.</span></span>
- <span data-ttu-id="b3912-137">Alışveriş sepetini temizleyin.</span><span class="sxs-lookup"><span data-stu-id="b3912-137">Clear the shopping cart.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

<span data-ttu-id="b3912-138">Bu örnek uygulamanın amaçları doğrultusunda, geçerli tarihe yalnızca iki gün ekleyerek bir sevk tarihi hesaplayacağız.</span><span class="sxs-lookup"><span data-stu-id="b3912-138">For the purposes of this sample application we'll calculate a ship date by simply adding two days to the current date.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

<span data-ttu-id="b3912-139">Şimdi uygulamayı çalıştırmak, alışveriş sürecini baştan sona test etmemize olanak sağlayacak.</span><span class="sxs-lookup"><span data-stu-id="b3912-139">Running the application now will permit us to test the shopping process from start to finish.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b3912-140">[Önceki](tailspin-spyworks-part-5.md)
> [İleri](tailspin-spyworks-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="b3912-140">[Previous](tailspin-spyworks-part-5.md)
[Next](tailspin-spyworks-part-7.md)</span></span>
