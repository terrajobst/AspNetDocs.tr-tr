---
uid: signalr/overview/older-versions/working-with-groups
title: SignalR 1. x içindeki gruplarla çalışma | Microsoft Docs
author: bradygaster
description: Bu konu başlığı altında, Grup üyeliği bilgilerinin Merkez API 'SI ile nasıl korunmakta olduğu açıklanır.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579368"
---
# <a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="5127a-103">SignalR 1.x Sürümünde Gruplarla Çalışma</span><span class="sxs-lookup"><span data-stu-id="5127a-103">Working with Groups in SignalR 1.x</span></span>

<span data-ttu-id="5127a-104">, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5127a-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5127a-105">Bu konuda, gruplara kullanıcı ekleme ve grup üyeliği bilgilerini kalıcı hale getirme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5127a-105">This topic describes how to add users to groups and persist group membership information.</span></span>

## <a name="overview"></a><span data-ttu-id="5127a-106">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="5127a-106">Overview</span></span>

<span data-ttu-id="5127a-107">SignalR içindeki gruplar, bağlı istemcilerin belirtilen alt kümelerine ileti yayınlamak için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="5127a-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="5127a-108">Bir grup herhangi bir sayıda istemciye sahip olabilir ve bir istemci herhangi bir sayıda grubun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="5127a-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="5127a-109">Açıkça grup oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5127a-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="5127a-110">Aslında bir grup, bir gruba yapılan çağrıda adını ilk kez belirttiğinizde otomatik olarak oluşturulur. ekleyin ve bu, içindeki üyeliğinden son bağlantıyı kaldırdığınızda silinir.</span><span class="sxs-lookup"><span data-stu-id="5127a-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="5127a-111">Grupları kullanmaya giriş için, bkz. hub API-sunucu kılavuzundaki [hub sınıfından grup üyeliğini yönetme](index.md) .</span><span class="sxs-lookup"><span data-stu-id="5127a-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="5127a-112">Grup üyeliği listesi veya Grup listesi almak için API yok.</span><span class="sxs-lookup"><span data-stu-id="5127a-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="5127a-113">SignalR bir yayın/alt modele göre istemcilere ve gruplara iletiler gönderir ve sunucu grup veya grup üyelikleri listesini korumaz.</span><span class="sxs-lookup"><span data-stu-id="5127a-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="5127a-114">Bu, bir Web grubuna düğüm eklediğiniz her durumda, SignalR 'nin koruduğu tüm durumun yeni düğüme yayılması nedeniyle ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5127a-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="5127a-115">`Groups.Add` yöntemi kullanarak bir kullanıcıyı bir gruba eklediğinizde, Kullanıcı o gruba yönlendirilen iletileri geçerli bağlantı süresince alır, ancak kullanıcının bu gruptaki üyeliği geçerli bağlantının ötesinde kalıcı olmaz.</span><span class="sxs-lookup"><span data-stu-id="5127a-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="5127a-116">Gruplar ve grup üyeliği hakkındaki bilgileri kalıcı olarak saklamak istiyorsanız, bu verileri bir veritabanı veya Azure Tablo depolaması gibi bir depoda saklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5127a-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="5127a-117">Ardından, bir Kullanıcı uygulamanıza her bağladığında, kullanıcının sahip olduğu havuzdan alınır ve o kullanıcıyı bu gruplara el ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5127a-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="5127a-118">Geçici bir kesintiden sonra yeniden bağlanıldığında Kullanıcı önceden atanmış grupları otomatik olarak yeniden birleştirir.</span><span class="sxs-lookup"><span data-stu-id="5127a-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="5127a-119">Bir gruba otomatik olarak yeniden katılmak, yeni bir bağlantı kurulurken değil, yalnızca yeniden bağlanıldığında geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5127a-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="5127a-120">Dijital olarak imzalanan bir belirteç, daha önce atanmış grupların listesini içeren istemciden geçirilir.</span><span class="sxs-lookup"><span data-stu-id="5127a-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="5127a-121">Kullanıcının istenen gruplara ait olup olmadığını doğrulamak istiyorsanız, varsayılan davranışı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5127a-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="5127a-122">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="5127a-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="5127a-123">Kullanıcı ekleme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="5127a-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="5127a-124">Bir grubun üyelerini çağırma</span><span class="sxs-lookup"><span data-stu-id="5127a-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="5127a-125">Grup üyeliğini bir veritabanında depolama</span><span class="sxs-lookup"><span data-stu-id="5127a-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="5127a-126">Azure Tablo Depolaması 'nda grup üyeliğini depolama</span><span class="sxs-lookup"><span data-stu-id="5127a-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="5127a-127">Yeniden bağlanırken grup üyeliği doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="5127a-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="5127a-128">Kullanıcı ekleme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="5127a-128">Adding and removing users</span></span>

<span data-ttu-id="5127a-129">Bir gruba kullanıcı eklemek veya kaldırmak için, [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) veya [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini çağırır ve kullanıcının bağlantı kimliğini ve grup adını parametreler olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="5127a-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="5127a-130">Bağlantı sona erdiğinde bir kullanıcıyı bir gruptan el ile kaldırmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="5127a-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="5127a-131">Aşağıdaki örnek, hub yöntemlerinde kullanılan `Groups.Add` ve `Groups.Remove` yöntemlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5127a-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="5127a-132">`Groups.Add` ve `Groups.Remove` yöntemleri zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="5127a-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="5127a-133">Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen ileti göndermek istiyorsanız, groups. Add yönteminin önce tamamlandığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5127a-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="5127a-134">Aşağıdaki kod örneklerinde bunun nasıl yapılacağı, biri .NET 4,5 ' de çalıştırılan ve bir .NET 4 ' te çalıştırılan kod kullanılarak nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5127a-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="5127a-135">Zaman uyumsuz .NET 4,5 örneği</span><span class="sxs-lookup"><span data-stu-id="5127a-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="5127a-136">Zaman uyumsuz .NET 4 örneği</span><span class="sxs-lookup"><span data-stu-id="5127a-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="5127a-137">Kaldırmaya çalıştığınız bağlantı kimliği artık kullanılamadığından, genel olarak, `Groups.Remove` metodunu çağırırken `await` eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="5127a-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="5127a-138">Bu durumda, `TaskCanceledException` istek zaman aşımına uğraydıktan sonra oluşturulur. Uygulamanız, gruba bir ileti göndermeden önce kullanıcının gruptan kaldırıldığından emin olması gerekiyorsa, gruplardan önce `await` ekleyebilirsiniz., daha sonra ortaya çıkarılan `TaskCanceledException` özel durumu silin ve sonra da yakalanamaz.</span><span class="sxs-lookup"><span data-stu-id="5127a-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="5127a-139">Bir grubun üyelerini çağırma</span><span class="sxs-lookup"><span data-stu-id="5127a-139">Calling members of a group</span></span>

<span data-ttu-id="5127a-140">Aşağıdaki örneklerde gösterildiği gibi, bir grubun tüm üyelerine veya grubun yalnızca belirtilen üyelerine iletiler gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5127a-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="5127a-141">Belirtilen bir gruptaki **Tüm** bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="5127a-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="5127a-142">Belirtilen bir gruptaki, belirtilen **istemciler hariç**, bağlantı kimliğiyle tanımlanan tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="5127a-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="5127a-143">**Çağıran istemci hariç,** belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="5127a-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="5127a-144">Grup üyeliğini bir veritabanında depolama</span><span class="sxs-lookup"><span data-stu-id="5127a-144">Storing group membership in a database</span></span>

<span data-ttu-id="5127a-145">Aşağıdaki örneklerde, Grup ve Kullanıcı bilgilerinin bir veritabanında nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5127a-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="5127a-146">Herhangi bir veri erişim teknolojisini kullanabilirsiniz; Ancak, aşağıdaki örnekte Entity Framework kullanarak modellerin nasıl tanımlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5127a-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="5127a-147">Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5127a-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="5127a-148">Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="5127a-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="5127a-149">Bu örnek, kullanıcıların spor veya bahçe gibi farklı konularla ilgili konuşmaları katılmasına olanak sağlayan bir uygulama için benzersiz olan `ConversationRoom` adlı bir sınıf içerir.</span><span class="sxs-lookup"><span data-stu-id="5127a-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="5127a-150">Bu örnek ayrıca bağlantılar için bir sınıf içerir.</span><span class="sxs-lookup"><span data-stu-id="5127a-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="5127a-151">Bağlantı sınıfı, Grup üyeliğini izlemek için kesinlikle gerekli değildir, ancak kullanıcıları izlemeye yönelik genellikle güçlü çözümün bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="5127a-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="5127a-152">Ardından, hub 'da, Grup ve Kullanıcı bilgilerini veritabanından alabilir ve kullanıcıyı uygun gruplara el ile ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5127a-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="5127a-153">Örnek, Kullanıcı bağlantılarını izlemeye yönelik kodu içermez.</span><span class="sxs-lookup"><span data-stu-id="5127a-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="5127a-154">Bu örnekte, bir ileti doğrudan grubun üyelerine gönderilmediğinden, `await` anahtar sözcüğü `Groups.Add` önce uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="5127a-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="5127a-155">Yeni üye eklendikten hemen sonra grubun tüm üyelerine bir ileti göndermek istiyorsanız, zaman uyumsuz işlemin tamamlandığından emin olmak için `await` anahtar sözcüğünü uygulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5127a-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="5127a-156">Azure Tablo Depolaması 'nda grup üyeliğini depolama</span><span class="sxs-lookup"><span data-stu-id="5127a-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="5127a-157">Grubu ve Kullanıcı bilgilerini depolamak için Azure Tablo depolama kullanmak, veritabanı kullanmaya benzer.</span><span class="sxs-lookup"><span data-stu-id="5127a-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="5127a-158">Aşağıdaki örnek, Kullanıcı adını ve grup adını depolayan bir tablo varlığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5127a-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="5127a-159">Hub 'da, Kullanıcı bağlanırken atanan grupları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5127a-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="5127a-160">Yeniden bağlanırken grup üyeliği doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="5127a-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="5127a-161">Varsayılan olarak, SignalR, bağlantı zaman aşımına uğramadan önce bir bağlantının düşürülme ve yeniden oluşturulması gibi geçici bir kesintiden yeniden bağlanıldığında bir kullanıcıyı uygun gruplara otomatik olarak yeniden atar. Kullanıcının grup bilgileri yeniden bağlanıldığında bir belirtece geçirilir ve bu belirteç sunucuda doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="5127a-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="5127a-162">Kullanıcıların gruplara yeniden katılması için doğrulama süreci hakkında bilgi için bkz. [yeniden bağlanıldığında grupları yeniden birleştirme](index.md).</span><span class="sxs-lookup"><span data-stu-id="5127a-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="5127a-163">Genel olarak, yeniden bağlanma sırasında grupları otomatik olarak yeniden birleştirme varsayılan davranışını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5127a-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="5127a-164">SignalR grupları, gizli verilere erişimi kısıtlamak için bir güvenlik mekanizması olarak tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="5127a-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="5127a-165">Ancak, uygulamanızın yeniden bağlanırken bir kullanıcının grup üyeliğini iki kez denetlemesi gerekiyorsa, varsayılan davranışı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5127a-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="5127a-166">Varsayılan davranışı değiştirmek, bir kullanıcının grup üyeliğinin yalnızca Kullanıcı bağlantısı yerine her yeniden bağlantı için alınması gerektiğinden veritabanınıza bir yük ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="5127a-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="5127a-167">Yeniden bağlanma sırasında grup üyeliğini doğrulamanız gerekiyorsa, aşağıda gösterildiği gibi, atanmış grupların bir listesini döndüren yeni bir hub işlem hattı modülü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5127a-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="5127a-168">Ardından, aşağıda vurgulanan şekilde bu modülü hub işlem hattına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5127a-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
