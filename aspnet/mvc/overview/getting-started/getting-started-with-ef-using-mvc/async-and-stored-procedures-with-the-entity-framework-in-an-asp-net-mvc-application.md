---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Öğretici: bir ASP.NET MVC uygulamasında EF ile zaman uyumsuz ve saklı yordamlar kullanın'
description: Bu öğreticide, zaman uyumsuz programlama modelini uygulamayı ve saklı yordamları nasıl kullanacağınızı öğreneceksiniz.
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583442"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="98437-103">Öğretici: bir ASP.NET MVC uygulamasında EF ile zaman uyumsuz ve saklı yordamlar kullanın</span><span class="sxs-lookup"><span data-stu-id="98437-103">Tutorial: Use async and stored procedures with EF in an ASP.NET MVC App</span></span>

<span data-ttu-id="98437-104">Önceki öğreticilerde, zaman uyumlu programlama modelini kullanarak verileri okuma ve güncelleştirme hakkında bilgi edinirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98437-104">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="98437-105">Bu öğreticide, zaman uyumsuz programlama modelinin nasıl uygulanacağını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="98437-105">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="98437-106">Zaman uyumsuz kod, sunucu kaynaklarını daha iyi kullandığından, uygulamanın daha iyi performans sağlanmasına yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="98437-106">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="98437-107">Bu öğreticide, bir varlıkta ekleme, güncelleştirme ve silme işlemleri için saklı yordamları nasıl kullanacağınızı da görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="98437-107">In this tutorial you also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="98437-108">Son olarak, uygulamayı Azure 'a yeniden dağıtırsınız ve ilk kez dağıttığınız zamandan beri uyguladığınız tüm veritabanı değişiklikleri vardır.</span><span class="sxs-lookup"><span data-stu-id="98437-108">Finally, you redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="98437-109">Aşağıdaki çizimlerde, üzerinde çalıştığınız sayfaların bazıları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="98437-109">The following illustrations show some of the pages that you'll work with.</span></span>

![Departmanlar sayfası](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Departman oluşturma](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="98437-112">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="98437-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98437-113">Zaman uyumsuz kod hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="98437-113">Learn about asynchronous code</span></span>
> * <span data-ttu-id="98437-114">Departman denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="98437-114">Create a Department controller</span></span>
> * <span data-ttu-id="98437-115">Saklı yordamları kullanma</span><span class="sxs-lookup"><span data-stu-id="98437-115">Use stored procedures</span></span>
> * <span data-ttu-id="98437-116">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="98437-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98437-117">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="98437-117">Prerequisites</span></span>

* [<span data-ttu-id="98437-118">İlgili Verileri Güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="98437-118">Updating Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a><span data-ttu-id="98437-119">Neden zaman uyumsuz kod kullanılmalıdır?</span><span class="sxs-lookup"><span data-stu-id="98437-119">Why use asynchronous code</span></span>

<span data-ttu-id="98437-120">Sınırlı sayıda iş parçacığı kullanılabilir bir web sunucusuna sahip ve yüksek yük durumlarda tüm kullanılabilir iş parçacıklarının kullanımda olabilir.</span><span class="sxs-lookup"><span data-stu-id="98437-120">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="98437-121">Bu durum oluştuğunda, sunucunun iş parçacıklarının serbest bırakılana kadar yeni istekleri işleyemiyor.</span><span class="sxs-lookup"><span data-stu-id="98437-121">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="98437-122">G/ç tamamlanması bekleniyor çünkü bunlar herhangi bir iş gerçekten yapmamanız sırasında eş zamanlı kod ile birçok iş parçacığı bağlanması.</span><span class="sxs-lookup"><span data-stu-id="98437-122">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="98437-123">İşlemi tamamlamak, g/ç için beklerken zaman uyumsuz kod ile diğer istekleri işlemek için kullanılacak sunucuyu için kendi iş parçacığı serbest bırakılır.</span><span class="sxs-lookup"><span data-stu-id="98437-123">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="98437-124">Sonuç olarak, zaman uyumsuz kod sunucu kaynaklarının daha verimli bir şekilde kullanılmasını ve sunucunun gecikmeler olmadan daha fazla trafiği işlemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="98437-124">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="98437-125">.NET 'in önceki sürümlerinde, zaman uyumsuz kodu yazma ve test etme karmaşık, hataya açık ve hata ayıklama zor idi.</span><span class="sxs-lookup"><span data-stu-id="98437-125">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="98437-126">.NET 4,5 ' de, zaman uyumsuz kodu yazma, test etme ve hata ayıklama gibi bir nedeniniz olmadığı takdirde genellikle zaman uyumsuz kod yazmanız çok daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="98437-126">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="98437-127">Zaman uyumsuz kod, az miktarda yük getirir, ancak düşük trafik durumlarında performans artışı göz ardı edilebilir, ancak yüksek trafik durumları için olası performans iyileştirmesi oldukça önemlidir.</span><span class="sxs-lookup"><span data-stu-id="98437-127">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="98437-128">Zaman uyumsuz programlama hakkında daha fazla bilgi için bkz. [çağrı engellemeyi önlemek için .NET 4.5 'in zaman uyumsuz desteğini kullanma](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span><span class="sxs-lookup"><span data-stu-id="98437-128">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-department-controller"></a><span data-ttu-id="98437-129">Departman denetleyicisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="98437-129">Create Department controller</span></span>

<span data-ttu-id="98437-130">Daha önceki denetleyicilerle aynı şekilde bir departman denetleyicisi oluşturun, bu süre dışında **zaman uyumsuz denetleyici eylemlerini kullan** onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="98437-130">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller actions** check box.</span></span>

<span data-ttu-id="98437-131">Aşağıdaki önemli noktalar, zaman uyumsuz hale getirmek için `Index` yöntemi için zaman uyumlu koda nelerin eklendiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="98437-131">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="98437-132">Entity Framework veritabanı sorgusunun zaman uyumsuz olarak yürütülmesine olanak tanımak için dört değişiklik uygulandı:</span><span class="sxs-lookup"><span data-stu-id="98437-132">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="98437-133">Yöntemi, derleyicinin Yöntem gövdesinin bölümlerine geri çağrılar oluşturmasını ve döndürülen `Task<ActionResult>` nesnesini otomatik olarak oluşturmasını bildiren `async` anahtar sözcüğüyle işaretlenir.</span><span class="sxs-lookup"><span data-stu-id="98437-133">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="98437-134">Dönüş türü, `ActionResult` `Task<ActionResult>`olarak değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="98437-134">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="98437-135">`Task<T>` türü, `T`türünde bir sonuçla devam eden işi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="98437-135">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="98437-136">`await` anahtar sözcüğü Web hizmeti çağrısına uygulandı.</span><span class="sxs-lookup"><span data-stu-id="98437-136">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="98437-137">Derleyici bu anahtar sözcüğü gördüğünde, arka planda yöntemi iki parçaya böler.</span><span class="sxs-lookup"><span data-stu-id="98437-137">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="98437-138">İlk bölüm, zaman uyumsuz olarak başlatılan işlemle biter.</span><span class="sxs-lookup"><span data-stu-id="98437-138">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="98437-139">İkinci bölüm, işlem tamamlandığında çağrılan bir geri çağırma yöntemine konur.</span><span class="sxs-lookup"><span data-stu-id="98437-139">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="98437-140">`ToList` uzantısı yönteminin zaman uyumsuz sürümü çağrıldı.</span><span class="sxs-lookup"><span data-stu-id="98437-140">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="98437-141">`departments.ToList` deyimleri neden değiştirildi, ancak `departments = db.Departments` deyimleri değil mi?</span><span class="sxs-lookup"><span data-stu-id="98437-141">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="98437-142">Bu nedenle, yalnızca sorgu veya komutların veritabanına gönderilmesine neden olan deyimler zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="98437-142">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="98437-143">`departments = db.Departments` ifade bir sorgu ayarlıyor, ancak `ToList` yöntemi çağrılana kadar sorgu yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="98437-143">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="98437-144">Bu nedenle, yalnızca `ToList` yöntemi zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="98437-144">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="98437-145">`Details` yönteminde ve `HttpGet` `Edit` ve `Delete` yöntemlerinde, `Find` yöntemi bir sorgunun veritabanına gönderilmesine neden olan bir yöntemdir, böylece zaman uyumsuz olarak yürütülen yöntem olur:</span><span class="sxs-lookup"><span data-stu-id="98437-145">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="98437-146">`Create`, `HttpPost Edit`ve `DeleteConfirmed` yöntemlerinde, bu, yalnızca bellekte bulunan varlıkların değiştirilmesine neden olan `db.Departments.Add(department)` gibi deyimler değil, bir komutun yürütülmesine neden olan `SaveChanges` yöntem çağrıdır.</span><span class="sxs-lookup"><span data-stu-id="98437-146">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="98437-147">*Views\Department\Index.cshtml*'i açın ve şablon kodunu şu kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="98437-147">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="98437-148">Bu kod, başlığı dizinden departmanlar olarak değiştirir, yönetici adını sağa taşımakta ve yöneticinin tam adını sağlar.</span><span class="sxs-lookup"><span data-stu-id="98437-148">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="98437-149">Oluşturma, silme, Ayrıntılar ve düzenleme görünümlerinde, `InstructorID` alanının başlığını, Bölüm adı alanını kurs görünümlerinde "Departman" olarak değiştirdiğiniz şekilde "Yönetici" olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="98437-149">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="98437-150">Oluşturma ve düzenleme görünümlerinde aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="98437-150">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="98437-151">Silme ve Ayrıntılar görünümlerinde aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="98437-151">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="98437-152">Uygulamayı çalıştırın ve **Departmanlar** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98437-152">Run the application, and click the **Departments** tab.</span></span>

<span data-ttu-id="98437-153">Her şey diğer denetleyicilerle aynı şekilde çalışıyor, ancak bu denetleyicide tüm SQL sorguları zaman uyumsuz olarak yürütülüyor.</span><span class="sxs-lookup"><span data-stu-id="98437-153">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="98437-154">Entity Framework zaman uyumsuz programlama kullanırken dikkat etmeniz gereken bazı şeyler:</span><span class="sxs-lookup"><span data-stu-id="98437-154">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="98437-155">Zaman uyumsuz kod iş parçacığı güvenli değildir.</span><span class="sxs-lookup"><span data-stu-id="98437-155">The async code is not thread safe.</span></span> <span data-ttu-id="98437-156">Diğer bir deyişle, diğer bir deyişle, aynı bağlam örneğini kullanarak paralel olarak birden çok işlem yapmayı denemeyin.</span><span class="sxs-lookup"><span data-stu-id="98437-156">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="98437-157">Zaman uyumsuz kodun performans avantajlarından yararlanmak isterseniz, kullanmakta olduğunuz tüm kitaplık paketlerinin (örneğin, sayfalama için), sorguların veritabanına gönderilmesine neden olan herhangi bir Entity Framework yöntemini çağırıyorsa, zaman uyumsuz olarak da kullanılmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="98437-157">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures"></a><span data-ttu-id="98437-158">Saklı yordamları kullanma</span><span class="sxs-lookup"><span data-stu-id="98437-158">Use stored procedures</span></span>

<span data-ttu-id="98437-159">Bazı geliştiriciler ve DBAs, veritabanı erişimi için saklı yordamları kullanmayı tercih eder.</span><span class="sxs-lookup"><span data-stu-id="98437-159">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="98437-160">Entity Framework önceki sürümlerinde, [Ham BIR SQL sorgusu yürüterek](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)saklı yordam kullanarak verileri alabilirsiniz, ancak güncelleştirme işlemlerine yönelik saklı yordamları kullanmak için EF 'e talimat verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98437-160">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="98437-161">EF 6 ' da, saklı yordamları kullanmak için Code First yapılandırmak kolaydır.</span><span class="sxs-lookup"><span data-stu-id="98437-161">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="98437-162">*DAL\SchoolContext.cs*' de, vurgulanan kodu `OnModelCreating` yöntemine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="98437-162">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="98437-163">Bu kod, `Department` varlığındaki ekleme, güncelleştirme ve silme işlemleri için saklı yordamları kullanmayı Entity Framework söyler.</span><span class="sxs-lookup"><span data-stu-id="98437-163">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="98437-164">Paket Yönetimi Konsolu ' nda, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="98437-164">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="98437-165">*\\&lt;zaman damgası&gt;\_* , ekleme, güncelleştirme ve silme saklı yordamlarını oluşturan `Up` yönteminde kodu görmek için zaman damgası ' nı açın:</span><span class="sxs-lookup"><span data-stu-id="98437-165">Open *Migrations\\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="98437-166">Paket Yönetimi Konsolu ' nda, aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="98437-166">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="98437-167">Uygulamayı hata ayıklama modunda çalıştırın, **Departmanlar** sekmesine tıklayın ve ardından **Yeni oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98437-167">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="98437-168">Yeni bir departman için veri girin ve ardından **Oluştur**' a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98437-168">Enter data for a new department, and then click **Create**.</span></span>

6. <span data-ttu-id="98437-169">Visual Studio 'da, yeni departman satırını eklemek için bir saklı yordamın kullanıldığını görmek için **Çıkış** penceresindeki günlüklere bakın.</span><span class="sxs-lookup"><span data-stu-id="98437-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![Bölüm ekleme SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="98437-171">Code First varsayılan saklı yordam adlarını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="98437-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="98437-172">Var olan bir veritabanını kullanıyorsanız, veritabanında önceden tanımlanmış saklı yordamları kullanabilmeniz için saklı yordam adlarını özelleştirmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="98437-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="98437-173">Bunun nasıl yapılacağı hakkında bilgi için, bkz. [Entity Framework Code First saklı yordamları ekleme/güncelleştirme/silme](https://msdn.microsoft.com/data/dn468673).</span><span class="sxs-lookup"><span data-stu-id="98437-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="98437-174">Oluşturulan saklı yordamları özelleştirmek istiyorsanız, saklı yordamı oluşturan geçişler `Up` yöntemi için yapı iskelesi kodunu düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98437-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="98437-175">Bu şekilde, geçiş her çalıştırıldığında yaptığınız değişiklikler yansıtılır ve dağıtımdan sonra geçişler otomatik olarak çalıştırıldığında üretim veritabanınıza uygulanır.</span><span class="sxs-lookup"><span data-stu-id="98437-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="98437-176">Önceki bir geçişte oluşturulmuş mevcut bir saklı yordamı değiştirmek istiyorsanız, bir boş geçiş oluşturmak için Add-Migration komutunu kullanabilir ve ardından [Alterstoredprocedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) metodunu çağıran kodu el ile yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98437-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="98437-177">Azure’a dağıtma</span><span class="sxs-lookup"><span data-stu-id="98437-177">Deploy to Azure</span></span>

<span data-ttu-id="98437-178">Bu bölüm, bu serinin [geçişler ve dağıtım](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) öğreticisinde **uygulamayı Azure 'a** isteğe bağlı olarak dağıtma bölümünü tamamladığınıza gerek duyar.</span><span class="sxs-lookup"><span data-stu-id="98437-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="98437-179">Yerel projenizde veritabanını silerek çözümladığınız hataları geçirseniz, bu bölümü atlayın.</span><span class="sxs-lookup"><span data-stu-id="98437-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="98437-180">Visual Studio 'da **Çözüm Gezgini** projeye sağ tıklayın ve bağlam menüsünden **Yayımla** ' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="98437-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="98437-181">**Yayımla**’ta tıklayın.</span><span class="sxs-lookup"><span data-stu-id="98437-181">Click **Publish**.</span></span>

    <span data-ttu-id="98437-182">Visual Studio uygulamayı Azure 'a dağıtır ve uygulama, Azure 'da çalışan varsayılan tarayıcınızda açılır.</span><span class="sxs-lookup"><span data-stu-id="98437-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="98437-183">Çalışıp çalışmadığını doğrulamak için uygulamayı test edin.</span><span class="sxs-lookup"><span data-stu-id="98437-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="98437-184">Veritabanına erişen bir sayfayı ilk kez çalıştırdığınızda Entity Framework, geçerli veri modeliyle veritabanını güncel hale getirmek için gereken tüm geçişleri `Up` yöntemlerini çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="98437-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="98437-185">Artık bu öğreticide eklediğiniz departman sayfaları dahil olmak üzere, son dağıttığınız zamandan sonra eklediğiniz tüm Web sayfalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98437-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="98437-186">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="98437-186">Get the code</span></span>

[<span data-ttu-id="98437-187">Tamamlanmış projeyi indirin</span><span class="sxs-lookup"><span data-stu-id="98437-187">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="98437-188">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="98437-188">Additional resources</span></span>

<span data-ttu-id="98437-189">Diğer Entity Framework kaynaklarına bağlantılar [ASP.NET Data Access-önerilen kaynaklarda](../../../../whitepapers/aspnet-data-access-content-map.md)bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="98437-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="98437-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98437-190">Next steps</span></span>

<span data-ttu-id="98437-191">Bu öğreticide şunları yaptınız:</span><span class="sxs-lookup"><span data-stu-id="98437-191">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98437-192">Zaman uyumsuz kod hakkında öğrenildi</span><span class="sxs-lookup"><span data-stu-id="98437-192">Learned about asynchronous code</span></span>
> * <span data-ttu-id="98437-193">Bir departman denetleyicisi oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="98437-193">Created a Department controller</span></span>
> * <span data-ttu-id="98437-194">Kullanılan saklı yordamlar</span><span class="sxs-lookup"><span data-stu-id="98437-194">Used stored procedures</span></span>
> * <span data-ttu-id="98437-195">Azure 'a dağıtıldı</span><span class="sxs-lookup"><span data-stu-id="98437-195">Deployed to Azure</span></span>

<span data-ttu-id="98437-196">Aynı anda birden çok kullanıcı aynı varlığı güncelleştirilişinde çakışmaların nasıl işleneceğini öğrenmek için sonraki makaleye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="98437-196">Advance to the next article to learn how to handle conflicts when multiple users update the same entity at the same time.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="98437-197">Eşzamanlılık işleme</span><span class="sxs-lookup"><span data-stu-id="98437-197">Handling concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
