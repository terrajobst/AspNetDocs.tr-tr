---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: SignalR 1. x 'te SignalR kullanıcılarını bağlantılarla eşleme | Microsoft Docs
author: bradygaster
description: Bu konuda kullanıcılar ve bağlantılarıyla ilgili bilgilerin nasıl saklanacağı gösterilmektedir.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558487"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="5b39c-103">SignalR 1.x Sürümünde SignalR Kullanıcılarını Bağlantılarla Eşleme</span><span class="sxs-lookup"><span data-stu-id="5b39c-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="5b39c-104">, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5b39c-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5b39c-105">Bu konuda kullanıcılar ve bağlantılarıyla ilgili bilgilerin nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-105">This topic shows how to retain information about users and their connections.</span></span>

## <a name="introduction"></a><span data-ttu-id="5b39c-106">Giriş</span><span class="sxs-lookup"><span data-stu-id="5b39c-106">Introduction</span></span>

<span data-ttu-id="5b39c-107">Bir hub 'a bağlanan her istemci, benzersiz bir bağlantı kimliği geçirir. Hub bağlamının `Context.ConnectionId` özelliğindeki bu değeri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b39c-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="5b39c-108">Uygulamanız bir kullanıcıyı bağlantı kimliğiyle eşlemek ve bu eşlemeyi kalıcı hale getirmek için aşağıdakilerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5b39c-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="5b39c-109">Sözlük gibi [bellek içi depolama](#inmemory)</span><span class="sxs-lookup"><span data-stu-id="5b39c-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="5b39c-110">Her Kullanıcı için SignalR grubu</span><span class="sxs-lookup"><span data-stu-id="5b39c-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="5b39c-111">Veritabanı tablosu veya Azure Tablo depolaması gibi [kalıcı, dış depolama](#database)</span><span class="sxs-lookup"><span data-stu-id="5b39c-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="5b39c-112">Bu uygulamaların her biri, bu konuda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="5b39c-113">Kullanıcı bağlantı durumunu izlemek için `Hub` sınıfının `OnConnected`, `OnDisconnected`ve `OnReconnected` yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b39c-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="5b39c-114">Uygulamanız için en iyi yaklaşım şunlara bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="5b39c-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="5b39c-115">Uygulamanızı barındıran Web sunucularının sayısı.</span><span class="sxs-lookup"><span data-stu-id="5b39c-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="5b39c-116">Şu anda bağlı olan kullanıcıların listesini almanız gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="5b39c-117">Uygulama veya sunucu yeniden başlatıldığında Grup ve Kullanıcı bilgilerini kalıcı yapmanız gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="5b39c-118">Dış sunucu çağırma gecikmesinin bir sorun olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="5b39c-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="5b39c-119">Aşağıdaki tabloda bu noktalar için hangi yaklaşımın çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="5b39c-120">Birden çok sunucu</span><span class="sxs-lookup"><span data-stu-id="5b39c-120">More than one server</span></span> | <span data-ttu-id="5b39c-121">Şu anda bağlı olan kullanıcıların listesini al</span><span class="sxs-lookup"><span data-stu-id="5b39c-121">Get list of currently connected users</span></span> | <span data-ttu-id="5b39c-122">Yeniden başlatıldıktan sonra bilgileri kalıcı yap</span><span class="sxs-lookup"><span data-stu-id="5b39c-122">Persist information after restarts</span></span> | <span data-ttu-id="5b39c-123">En iyi performans</span><span class="sxs-lookup"><span data-stu-id="5b39c-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="5b39c-124">Bellek içi</span><span class="sxs-lookup"><span data-stu-id="5b39c-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="5b39c-125">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="5b39c-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="5b39c-126">Kalıcı, dış</span><span class="sxs-lookup"><span data-stu-id="5b39c-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="5b39c-127">Bellek içi depolama</span><span class="sxs-lookup"><span data-stu-id="5b39c-127">In-memory storage</span></span>

<span data-ttu-id="5b39c-128">Aşağıdaki örneklerde, bağlantı ve Kullanıcı bilgilerinin bellekte depolanan bir sözlükte nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="5b39c-129">Sözlük, bağlantı kimliğini depolamak için bir `HashSet` kullanır. Herhangi bir kullanıcının SignalR uygulamasına birden fazla bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="5b39c-130">Örneğin, birden çok cihaz veya birden çok tarayıcı sekmesinden bağlanmış bir kullanıcının birden fazla bağlantı kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="5b39c-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="5b39c-131">Uygulama kapatılırsa tüm bilgiler kaybolur, ancak kullanıcılar bağlantılarını yeniden kurduğundan, yeniden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="5b39c-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="5b39c-132">Her sunucunun ayrı bir bağlantı koleksiyonu olması nedeniyle, ortamınız birden fazla Web sunucusu içeriyorsa, bellek içi depolama çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="5b39c-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="5b39c-133">İlk örnek, kullanıcıların bağlantılardaki eşlemesini yöneten bir sınıfı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="5b39c-134">HashSet için anahtar, kullanıcının adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5b39c-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="5b39c-135">Sonraki örnekte, bağlantı eşleme sınıfının bir hub 'dan nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="5b39c-136">Sınıfının örneği `_connections`değişken adında depolanır.</span><span class="sxs-lookup"><span data-stu-id="5b39c-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="5b39c-137">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="5b39c-137">Single-user groups</span></span>

<span data-ttu-id="5b39c-138">Her Kullanıcı için bir grup oluşturabilir ve yalnızca bu kullanıcıya erişmek istediğinizde bu gruba bir ileti gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b39c-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="5b39c-139">Her grubun adı kullanıcının adıdır.</span><span class="sxs-lookup"><span data-stu-id="5b39c-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="5b39c-140">Kullanıcının birden fazla bağlantısı varsa, her bağlantı kimliği kullanıcının grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="5b39c-141">Kullanıcının bağlantısı kesildiğinde kullanıcıyı gruptan el ile kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="5b39c-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="5b39c-142">Bu eylem, SignalR çerçevesi tarafından otomatik olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="5b39c-143">Aşağıdaki örnek, tek kullanıcılı grupların nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="5b39c-144">Kalıcı, dış depolama</span><span class="sxs-lookup"><span data-stu-id="5b39c-144">Permanent, external storage</span></span>

<span data-ttu-id="5b39c-145">Bu konuda, bağlantı bilgilerini depolamak için bir veritabanının veya Azure Tablo depolamanın nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="5b39c-146">Her Web sunucusu aynı veri deposuyla etkileşime girebildiğinden, bu yaklaşım birden çok Web sunucunuz olduğunda işe yarar.</span><span class="sxs-lookup"><span data-stu-id="5b39c-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="5b39c-147">Web sunucularınız çalışmayı durdurmuş veya uygulama yeniden başlatılırsa `OnDisconnected` yöntemi çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="5b39c-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="5b39c-148">Bu nedenle, veri deponuzda artık geçerli olmayan bağlantı kimlikleri için kayıtlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="5b39c-149">Bu yalnız bırakılmış kayıtları temizlemek için, uygulamanız için uygun bir zaman çerçevesi dışında oluşturulmuş herhangi bir bağlantıyı geçersiz kılmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b39c-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="5b39c-150">Bu bölümdeki örneklerde, bağlantının oluşturulduğu sırada izleme için bir değer yer alır, ancak bunu arka plan işlemi olarak yapmak isteyebileceğiniz için eski kayıtların nasıl temizleyeceğini göstermeyin.</span><span class="sxs-lookup"><span data-stu-id="5b39c-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="5b39c-151">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="5b39c-151">Database</span></span>

<span data-ttu-id="5b39c-152">Aşağıdaki örneklerde, bağlantı ve Kullanıcı bilgilerinin bir veritabanında nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="5b39c-153">Herhangi bir veri erişim teknolojisini kullanabilirsiniz; Ancak, aşağıdaki örnekte Entity Framework kullanarak modellerin nasıl tanımlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="5b39c-154">Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="5b39c-155">Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="5b39c-156">İlk örnek, birçok bağlantı varlığı ile ilişkilendirilebilen bir Kullanıcı varlığının nasıl tanımlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="5b39c-157">Ardından, hub 'dan her bağlantının durumunu aşağıda gösterilen kodla izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b39c-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="5b39c-158">Azure tablo depolama</span><span class="sxs-lookup"><span data-stu-id="5b39c-158">Azure table storage</span></span>

<span data-ttu-id="5b39c-159">Aşağıdaki Azure Tablo depolama örneği, veritabanı örneğine benzer.</span><span class="sxs-lookup"><span data-stu-id="5b39c-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="5b39c-160">Azure Tablo Depolama hizmetini kullanmaya başlamak için ihtiyacınız olan tüm bilgileri içermez.</span><span class="sxs-lookup"><span data-stu-id="5b39c-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="5b39c-161">Bilgi için bkz. [.net 'Ten Tablo Depolamayı kullanma](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="5b39c-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="5b39c-162">Aşağıdaki örnek, bağlantı bilgilerini depolamak için bir tablo varlığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="5b39c-163">Verileri Kullanıcı adına göre bölümlendirir ve her bir varlığı bağlantı kimliğiyle tanımlar, böylece Kullanıcı istedikleri zaman birden çok bağlantıya sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="5b39c-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="5b39c-164">Hub 'da, her kullanıcının bağlantısının durumunu izlersiniz.</span><span class="sxs-lookup"><span data-stu-id="5b39c-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
