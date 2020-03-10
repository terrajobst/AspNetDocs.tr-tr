---
uid: web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
title: Model bağlama ve Web formları kullanan bir projeye iş mantığı katmanı ekleme | Microsoft Docs
author: Rick-Anderson
description: Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir. Model bağlama, veri etkileşimini daha düz-... hale getirir
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 7ef664b3-1cc8-4cbf-bb18-9f0f3a3ada2b
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/adding-business-logic-layer
msc.type: authoredcontent
ms.openlocfilehash: a824d06d3781e11706f2a48d44ea3ad89bdb7c8b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634836"
---
# <a name="adding-business-logic-layer-to-a-project-that-uses-model-binding-and-web-forms"></a><span data-ttu-id="ff784-104">Model bağlama ve Web formları kullanan bir projeye iş mantığı katmanı ekleme</span><span class="sxs-lookup"><span data-stu-id="ff784-104">Adding business logic layer to a project that uses model binding and web forms</span></span>

<span data-ttu-id="ff784-105">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="ff784-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="ff784-106">Bu öğretici serisi, model bağlamayı bir ASP.NET Web Forms projesiyle kullanmanın temel yönlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff784-106">This tutorial series demonstrates basic aspects of using model binding with an ASP.NET Web Forms project.</span></span> <span data-ttu-id="ff784-107">Model bağlama veri kaynağı nesneleriyle (örneğin, ObjectDataSource veya SqlDataSource) çok daha basit hale getirir.</span><span class="sxs-lookup"><span data-stu-id="ff784-107">Model binding makes data interaction more straight-forward than dealing with data source objects (such as ObjectDataSource or SqlDataSource).</span></span> <span data-ttu-id="ff784-108">Bu seri giriş malzemesiyle başlar ve sonraki öğreticilerde daha gelişmiş kavramlara gider.</span><span class="sxs-lookup"><span data-stu-id="ff784-108">This series starts with introductory material and moves to more advanced concepts in later tutorials.</span></span>
> 
> <span data-ttu-id="ff784-109">Bu öğreticide, model bağlamanın bir iş mantığı katmanıyla nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ff784-109">This tutorial shows how to use model binding with a business logic layer.</span></span> <span data-ttu-id="ff784-110">Veri yöntemlerini çağırmak için geçerli sayfa dışında bir nesnenin kullanıldığını belirtmek için OnCallingDataMethods üyesini ayarlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ff784-110">You will set the OnCallingDataMethods member to specify that an object other than the current page is used to call the data methods.</span></span>
> 
> <span data-ttu-id="ff784-111">Bu öğreticide, serinin [önceki](retrieving-data.md) bölümlerinde oluşturulan projede derleme yapılır.</span><span class="sxs-lookup"><span data-stu-id="ff784-111">This tutorial builds on the project created in the [earlier](retrieving-data.md) parts of the series.</span></span>
> 
> <span data-ttu-id="ff784-112">Tüm projeyi [](https://go.microsoft.com/fwlink/?LinkId=286116) C# veya vb 'ye indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff784-112">You can [download](https://go.microsoft.com/fwlink/?LinkId=286116) the complete project in C# or VB.</span></span> <span data-ttu-id="ff784-113">İndirilebilir kod, Visual Studio 2012 veya Visual Studio 2013 ile birlikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff784-113">The downloadable code works with either Visual Studio 2012 or Visual Studio 2013.</span></span> <span data-ttu-id="ff784-114">Bu öğreticide gösterilen Visual Studio 2013 şablonundan biraz farklı olan Visual Studio 2012 şablonunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="ff784-114">It uses the Visual Studio 2012 template, which is slightly different than the Visual Studio 2013 template shown in this tutorial.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="ff784-115">Ne oluşturacağız?</span><span class="sxs-lookup"><span data-stu-id="ff784-115">What you'll build</span></span>

<span data-ttu-id="ff784-116">Model bağlama, veri etkileşimi kodunuzu bir Web sayfası için arka plan kod dosyasına veya ayrı bir iş mantığı sınıfına yerleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff784-116">Model binding enables you to put your data interaction code in either the code-behind file for a web page or in a separate business logic class.</span></span> <span data-ttu-id="ff784-117">Önceki öğreticilerde, veri etkileşimi kodu için arka plan kod dosyalarının nasıl kullanılacağı gösterilmekte.</span><span class="sxs-lookup"><span data-stu-id="ff784-117">The previous tutorials have shown how to use the code-behind files for data interaction code.</span></span> <span data-ttu-id="ff784-118">Bu yaklaşım küçük siteler için geçerlidir, ancak büyük bir site korunurken kod tekrarı ve daha zorluk ortaya çıkmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff784-118">This approach works for small sites but it can lead to code repetition and greater difficulty when maintaining a large site.</span></span> <span data-ttu-id="ff784-119">Özet katman olmadığından, kod arkasında bulunan kodu programlama yoluyla test etmek de çok zor olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff784-119">It can also be very difficult to programmatically test code that resides in code behind files because there is no abstraction layer.</span></span>

<span data-ttu-id="ff784-120">Veri etkileşim kodunu merkezileştirmek için verilerle etkileşimde bulunmak üzere tüm mantığı içeren bir iş mantığı katmanı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff784-120">To centralize the data interaction code, you can create a business logic layer that contains all of the logic for interacting with data.</span></span> <span data-ttu-id="ff784-121">Daha sonra Web sayfalarınızdaki iş mantığı katmanını çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff784-121">You then call the business logic layer from your web pages.</span></span> <span data-ttu-id="ff784-122">Bu öğreticide, önceki öğreticilerde yazdığınız kodun tümünü bir iş mantığı katmanına taşıma ve sonra bu kodu sayfalardan kullanma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ff784-122">This tutorial shows how to move all of the code you have written in the previous tutorials into a business logic layer, and then use that code from the pages.</span></span>

<span data-ttu-id="ff784-123">Bu öğreticide şunları yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ff784-123">In this tutorial, you'll:</span></span>

1. <span data-ttu-id="ff784-124">Kodu arka plan kod dosyalarından iş mantığı katmanına taşıma</span><span class="sxs-lookup"><span data-stu-id="ff784-124">Move the code from code-behind files to a business logic layer</span></span>
2. <span data-ttu-id="ff784-125">Veri bağlantılı denetimlerinizi iş mantığı katmanındaki yöntemleri çağırmak için değiştirin</span><span class="sxs-lookup"><span data-stu-id="ff784-125">Change your data bound controls to call the methods in the business logic layer</span></span>

## <a name="create-business-logic-layer"></a><span data-ttu-id="ff784-126">İş mantığı katmanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff784-126">Create business logic layer</span></span>

<span data-ttu-id="ff784-127">Şimdi, Web sayfalarından çağrılan sınıfını oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ff784-127">Now, you will create the class that is called from the web pages.</span></span> <span data-ttu-id="ff784-128">Bu sınıftaki Yöntemler, önceki öğreticilerde kullandığınız yöntemlere benzer ve değer sağlayıcısı özniteliklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ff784-128">The methods in this class look similar to the methods you used in the previous tutorials and include the value provider attributes.</span></span>

<span data-ttu-id="ff784-129">İlk olarak **BLL**adlı yeni bir klasör ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff784-129">First, add a new folder called **BLL**.</span></span>

![Klasör Ekle](adding-business-logic-layer/_static/image1.png)

<span data-ttu-id="ff784-131">BLL klasöründe, **SchoolBL.cs**adlı yeni bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff784-131">In the BLL folder, create a new class named **SchoolBL.cs**.</span></span> <span data-ttu-id="ff784-132">Bu, başlangıçta arka plan kod dosyalarında yer alan tüm veri işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="ff784-132">It will contain all of the data operations that originally resided in code-behind files.</span></span> <span data-ttu-id="ff784-133">Yöntemler, arka plan kod dosyasındaki yöntemlerle neredeyse aynıdır, ancak bazı değişiklikler içerir.</span><span class="sxs-lookup"><span data-stu-id="ff784-133">The methods are almost the same as the methods in the code-behind file, but will include some changes.</span></span>

<span data-ttu-id="ff784-134">Dikkat edilmesi gereken en önemli değişiklik, artık kodu **Page** sınıfının bir örneği içinden yürütmemenin bir örneğidir.</span><span class="sxs-lookup"><span data-stu-id="ff784-134">The most important change to note is that you are no longer executing the code from within an instance of **Page** class.</span></span> <span data-ttu-id="ff784-135">Sayfa sınıfı, **TryUpdateModel** yöntemini ve **ModelState** özelliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="ff784-135">The Page class contains the **TryUpdateModel** method and the **ModelState** property.</span></span> <span data-ttu-id="ff784-136">Bu kod bir iş mantığı katmanına taşındığında, artık bu üyeleri çağırmak için Page sınıfının bir örneğine sahip olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff784-136">When this code is moved to a business logic layer, you no longer have an instance of the Page class to call these members.</span></span> <span data-ttu-id="ff784-137">Bu sorunu çözmek için, TryUpdateModel veya ModelState 'e erişen herhangi bir yönteme **ModelMethodContext** parametresini eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff784-137">To get around this issue, you must add a **ModelMethodContext** parameter to any method that accesses TryUpdateModel or ModelState.</span></span> <span data-ttu-id="ff784-138">Bu ModelMethodContext parametresini TryUpdateModel ' i çağırmak veya ModelState almak için kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ff784-138">You use this ModelMethodContext parameter to call TryUpdateModel or retrieve ModelState.</span></span> <span data-ttu-id="ff784-139">Bu yeni parametre için Web sayfasındaki herhangi bir şeyi hesaba çevirmek zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff784-139">You do not need to change anything in the web page to account for this new parameter.</span></span>

<span data-ttu-id="ff784-140">SchoolBL.cs içindeki kodu aşağıdaki kodla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff784-140">Replace the code in SchoolBL.cs with the following code.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample1.cs)]

## <a name="revise-existing-pages-to-retrieve-data-from-business-logic-layer"></a><span data-ttu-id="ff784-141">Mevcut sayfaları, iş mantığı katmanından veri almak için gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="ff784-141">Revise existing pages to retrieve data from business logic layer</span></span>

<span data-ttu-id="ff784-142">Son olarak, iş mantığı katmanını kullanarak öğrenciler. aspx, Addöğrenci. aspx ve kurslar. aspx sayfalarını arka plan kod dosyasındaki sorguları kullanarak dönüştürmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ff784-142">Finally, you will convert the pages Students.aspx, AddStudent.aspx, and Courses.aspx from using queries in the code-behind file to using the business logic layer.</span></span>

<span data-ttu-id="ff784-143">Öğrenciler, Addöğrenci ve kurslar için arka plan kod dosyalarında aşağıdaki sorgu yöntemlerini silin veya not edin:</span><span class="sxs-lookup"><span data-stu-id="ff784-143">In the code-behind files for Students, AddStudent, and Courses, delete or comment out the following query methods:</span></span>

- <span data-ttu-id="ff784-144">studentsGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="ff784-144">studentsGrid\_GetData</span></span>
- <span data-ttu-id="ff784-145">studentsGrid\_UpdateItem</span><span class="sxs-lookup"><span data-stu-id="ff784-145">studentsGrid\_UpdateItem</span></span>
- <span data-ttu-id="ff784-146">studentsGrid\_DeleteItem</span><span class="sxs-lookup"><span data-stu-id="ff784-146">studentsGrid\_DeleteItem</span></span>
- <span data-ttu-id="ff784-147">addStudentForm\_InsertItem</span><span class="sxs-lookup"><span data-stu-id="ff784-147">addStudentForm\_InsertItem</span></span>
- <span data-ttu-id="ff784-148">coursesGrid\_GetData</span><span class="sxs-lookup"><span data-stu-id="ff784-148">coursesGrid\_GetData</span></span>

<span data-ttu-id="ff784-149">Artık, veri işlemleriyle ilgili arka plan kod dosyasında kod içermemelidir.</span><span class="sxs-lookup"><span data-stu-id="ff784-149">You now should have no code in the code-behind file that pertains to data operations.</span></span>

<span data-ttu-id="ff784-150">**Oncallingdatamethods** olay işleyicisi, veri yöntemleri için kullanılacak bir nesne belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff784-150">The **OnCallingDataMethods** event handler enables you to specify an object to use for the data methods.</span></span> <span data-ttu-id="ff784-151">Öğrenciler. aspx ' te, bu olay işleyicisi için bir değer ekleyin ve veri yöntemlerinin adlarını iş mantığı sınıfındaki yöntemlerin adlarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff784-151">In Students.aspx, add a value for that event handler and change the names of the data methods to the names of the methods in the business logic class.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample2.aspx?highlight=3-4,8)]

<span data-ttu-id="ff784-152">Öğrenciler. aspx için arka plan kod dosyasında, CallingDataMethods olayının olay işleyicisini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ff784-152">In the code-behind file for Students.aspx, define the event handler for the CallingDataMethods event.</span></span> <span data-ttu-id="ff784-153">Bu olay işleyicisinde, veri işlemleri için iş mantığı sınıfını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff784-153">In this event handler, you specify the business logic class for data operations.</span></span>

[!code-csharp[Main](adding-business-logic-layer/samples/sample3.cs)]

<span data-ttu-id="ff784-154">AddStudent. aspx dosyasında benzer değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="ff784-154">In AddStudent.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample4.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample5.cs)]

<span data-ttu-id="ff784-155">Kurslar. aspx ' te benzer değişiklikler yapın.</span><span class="sxs-lookup"><span data-stu-id="ff784-155">In Courses.aspx, make similar changes.</span></span>

[!code-aspx[Main](adding-business-logic-layer/samples/sample6.aspx?highlight=3-4)]

[!code-csharp[Main](adding-business-logic-layer/samples/sample7.cs)]

<span data-ttu-id="ff784-156">Uygulamayı çalıştırın ve sayfaların tümünün daha önce olduğu gibi işlev görür.</span><span class="sxs-lookup"><span data-stu-id="ff784-156">Run the application and notice that all of the pages function as they had previously.</span></span> <span data-ttu-id="ff784-157">Doğrulama mantığı da doğru şekilde çalışmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ff784-157">The validation logic also works correctly.</span></span>

## <a name="conclusion"></a><span data-ttu-id="ff784-158">Sonuç</span><span class="sxs-lookup"><span data-stu-id="ff784-158">Conclusion</span></span>

<span data-ttu-id="ff784-159">Bu öğreticide, bir veri erişim katmanını ve iş mantığı katmanını kullanmak için uygulamanızı yeniden yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ff784-159">In this tutorial, you re-structured your application to use a data access layer and business logic layer.</span></span> <span data-ttu-id="ff784-160">Veri denetimlerinin veri işlemleri için geçerli sayfa olmayan bir nesne kullanmasını belirttiniz.</span><span class="sxs-lookup"><span data-stu-id="ff784-160">You specified that the data controls use an object that is not the current page for data operations.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="ff784-161">Öncekini</span><span class="sxs-lookup"><span data-stu-id="ff784-161">Previous</span></span>](using-query-string-values-to-retrieve-data.md)
