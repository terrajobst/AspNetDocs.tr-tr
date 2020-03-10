---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: SignalR kullanıcılarını bağlantılarla eşleme | Microsoft Docs
author: bradygaster
description: Bu konuda kullanıcılar ve bağlantılarıyla ilgili bilgilerin nasıl saklanacağı gösterilmektedir. Patrick Fleti bu konuyu yazmayı Bu konuda kullanılan yazılım sürümleri...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536780"
---
# <a name="mapping-signalr-users-to-connections"></a><span data-ttu-id="ccd51-105">SignalR Kullanıcılarını Bağlantılarla Eşleme</span><span class="sxs-lookup"><span data-stu-id="ccd51-105">Mapping SignalR Users to Connections</span></span>

<span data-ttu-id="ccd51-106">[Tom FitzMacken](https://github.com/tfitzmac) tarafından</span><span class="sxs-lookup"><span data-stu-id="ccd51-106">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ccd51-107">Bu konuda kullanıcılar ve bağlantılarıyla ilgili bilgilerin nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-107">This topic shows how to retain information about users and their connections.</span></span>
>
> <span data-ttu-id="ccd51-108">Patrick Fleti bu konuyu yazmayı</span><span class="sxs-lookup"><span data-stu-id="ccd51-108">Patrick Fletcher helped write this topic.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="ccd51-109">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="ccd51-109">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="ccd51-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ccd51-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="ccd51-111">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ccd51-111">.NET 4.5</span></span>
> - <span data-ttu-id="ccd51-112">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="ccd51-112">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="ccd51-113">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="ccd51-113">Previous versions of this topic</span></span>
>
> <span data-ttu-id="ccd51-114">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="ccd51-114">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ccd51-115">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="ccd51-115">Questions and comments</span></span>
>
> <span data-ttu-id="ccd51-116">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="ccd51-116">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ccd51-117">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-117">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="introduction"></a><span data-ttu-id="ccd51-118">Giriş</span><span class="sxs-lookup"><span data-stu-id="ccd51-118">Introduction</span></span>

<span data-ttu-id="ccd51-119">Bir hub 'a bağlanan her istemci, benzersiz bir bağlantı kimliği geçirir. Hub bağlamının `Context.ConnectionId` özelliğindeki bu değeri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-119">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="ccd51-120">Uygulamanız bir kullanıcıyı bağlantı kimliğiyle eşlemek ve bu eşlemeyi kalıcı hale getirmek için aşağıdakilerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ccd51-120">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- [<span data-ttu-id="ccd51-121">Kullanıcı KIMLIĞI sağlayıcısı (SignalR 2)</span><span class="sxs-lookup"><span data-stu-id="ccd51-121">The User ID Provider (SignalR 2)</span></span>](#IUserIdProvider)
- <span data-ttu-id="ccd51-122">Sözlük gibi [bellek içi depolama](#inmemory)</span><span class="sxs-lookup"><span data-stu-id="ccd51-122">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="ccd51-123">Her Kullanıcı için SignalR grubu</span><span class="sxs-lookup"><span data-stu-id="ccd51-123">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="ccd51-124">Veritabanı tablosu veya Azure Tablo depolaması gibi [kalıcı, dış depolama](#database)</span><span class="sxs-lookup"><span data-stu-id="ccd51-124">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="ccd51-125">Bu uygulamaların her biri, bu konuda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-125">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="ccd51-126">Kullanıcı bağlantı durumunu izlemek için `Hub` sınıfının `OnConnected`, `OnDisconnected`ve `OnReconnected` yöntemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ccd51-126">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="ccd51-127">Uygulamanız için en iyi yaklaşım şunlara bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="ccd51-127">The best approach for your application depends on:</span></span>

- <span data-ttu-id="ccd51-128">Uygulamanızı barındıran Web sunucularının sayısı.</span><span class="sxs-lookup"><span data-stu-id="ccd51-128">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="ccd51-129">Şu anda bağlı olan kullanıcıların listesini almanız gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-129">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="ccd51-130">Uygulama veya sunucu yeniden başlatıldığında Grup ve Kullanıcı bilgilerini kalıcı yapmanız gerekip gerekmediğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-130">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="ccd51-131">Dış sunucu çağırma gecikmesinin bir sorun olup olmadığı.</span><span class="sxs-lookup"><span data-stu-id="ccd51-131">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="ccd51-132">Aşağıdaki tabloda bu noktalar için hangi yaklaşımın çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-132">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="ccd51-133">Birden çok sunucu</span><span class="sxs-lookup"><span data-stu-id="ccd51-133">More than one server</span></span> | <span data-ttu-id="ccd51-134">Şu anda bağlı olan kullanıcıların listesini al</span><span class="sxs-lookup"><span data-stu-id="ccd51-134">Get list of currently connected users</span></span> | <span data-ttu-id="ccd51-135">Yeniden başlatıldıktan sonra bilgileri kalıcı yap</span><span class="sxs-lookup"><span data-stu-id="ccd51-135">Persist information after restarts</span></span> | <span data-ttu-id="ccd51-136">En iyi performans</span><span class="sxs-lookup"><span data-stu-id="ccd51-136">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ccd51-137">UserID sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="ccd51-137">UserID Provider</span></span> | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="ccd51-138">Bellek içi</span><span class="sxs-lookup"><span data-stu-id="ccd51-138">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="ccd51-139">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="ccd51-139">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| <span data-ttu-id="ccd51-140">Kalıcı, dış</span><span class="sxs-lookup"><span data-stu-id="ccd51-140">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a><span data-ttu-id="ccd51-141">Iuserıd sağlayıcısı</span><span class="sxs-lookup"><span data-stu-id="ccd51-141">IUserID provider</span></span>

<span data-ttu-id="ccd51-142">Bu özellik, kullanıcıların yeni bir ıuserıdprovider arabirimi aracılığıyla bir ırequest 'e göre kimliğini belirlemesine izin verir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-142">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider.</span></span>

<span data-ttu-id="ccd51-143">**Iuserıdprovider**</span><span class="sxs-lookup"><span data-stu-id="ccd51-143">**The IUserIdProvider**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="ccd51-144">Varsayılan olarak, Kullanıcı adı olarak Kullanıcı `IPrincipal.Identity.Name` kullanan bir uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ccd51-144">By default, there will be an implementation that uses the user's `IPrincipal.Identity.Name` as the user name.</span></span> <span data-ttu-id="ccd51-145">Bunu değiştirmek için, uygulamanız başlatıldığında `IUserIdProvider` uygulamanızı küresel ana bilgisayara kaydedin:</span><span class="sxs-lookup"><span data-stu-id="ccd51-145">To change this, register your implementation of `IUserIdProvider` with the global host when your application starts:</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<span data-ttu-id="ccd51-146">Hub 'ın içinden aşağıdaki API aracılığıyla bu kullanıcılara ileti gönderebileceksiniz:</span><span class="sxs-lookup"><span data-stu-id="ccd51-146">From within a hub, you'll be able to send messages to these users via the following API:</span></span>

<span data-ttu-id="ccd51-147">**Belirli bir kullanıcıya ileti gönderme**</span><span class="sxs-lookup"><span data-stu-id="ccd51-147">**Sending a message to a specific user**</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="ccd51-148">Bellek içi depolama</span><span class="sxs-lookup"><span data-stu-id="ccd51-148">In-memory storage</span></span>

<span data-ttu-id="ccd51-149">Aşağıdaki örneklerde, bağlantı ve Kullanıcı bilgilerinin bellekte depolanan bir sözlükte nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-149">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="ccd51-150">Sözlük, bağlantı kimliğini depolamak için bir `HashSet` kullanır. Herhangi bir kullanıcının SignalR uygulamasına birden fazla bağlantısı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-150">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="ccd51-151">Örneğin, birden çok cihaz veya birden çok tarayıcı sekmesinden bağlanmış bir kullanıcının birden fazla bağlantı kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="ccd51-151">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="ccd51-152">Uygulama kapatılırsa tüm bilgiler kaybolur, ancak kullanıcılar bağlantılarını yeniden kurduğundan, yeniden doldurulur.</span><span class="sxs-lookup"><span data-stu-id="ccd51-152">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="ccd51-153">Her sunucunun ayrı bir bağlantı koleksiyonu olması nedeniyle, ortamınız birden fazla Web sunucusu içeriyorsa, bellek içi depolama çalışmaz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-153">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="ccd51-154">İlk örnek, kullanıcıların bağlantılardaki eşlemesini yöneten bir sınıfı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-154">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="ccd51-155">HashSet için anahtar, kullanıcının adı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ccd51-155">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="ccd51-156">Sonraki örnekte, bağlantı eşleme sınıfının bir hub 'dan nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-156">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="ccd51-157">Sınıfının örneği `_connections`değişken adında depolanır.</span><span class="sxs-lookup"><span data-stu-id="ccd51-157">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="ccd51-158">Tek Kullanıcı grupları</span><span class="sxs-lookup"><span data-stu-id="ccd51-158">Single-user groups</span></span>

<span data-ttu-id="ccd51-159">Her Kullanıcı için bir grup oluşturabilir ve yalnızca bu kullanıcıya erişmek istediğinizde bu gruba bir ileti gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-159">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="ccd51-160">Her grubun adı kullanıcının adıdır.</span><span class="sxs-lookup"><span data-stu-id="ccd51-160">The name of each group is the name of the user.</span></span> <span data-ttu-id="ccd51-161">Kullanıcının birden fazla bağlantısı varsa, her bağlantı kimliği kullanıcının grubuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-161">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="ccd51-162">Kullanıcının bağlantısı kesildiğinde kullanıcıyı gruptan el ile kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="ccd51-162">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="ccd51-163">Bu eylem, SignalR çerçevesi tarafından otomatik olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-163">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="ccd51-164">Aşağıdaki örnek, tek kullanıcılı grupların nasıl uygulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-164">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="ccd51-165">Kalıcı, dış depolama</span><span class="sxs-lookup"><span data-stu-id="ccd51-165">Permanent, external storage</span></span>

<span data-ttu-id="ccd51-166">Bu konuda, bağlantı bilgilerini depolamak için bir veritabanının veya Azure Tablo depolamanın nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-166">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="ccd51-167">Her Web sunucusu aynı veri deposuyla etkileşime girebildiğinden, bu yaklaşım birden çok Web sunucunuz olduğunda işe yarar.</span><span class="sxs-lookup"><span data-stu-id="ccd51-167">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="ccd51-168">Web sunucularınız çalışmayı durdurmuş veya uygulama yeniden başlatılırsa `OnDisconnected` yöntemi çağrılmaz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-168">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="ccd51-169">Bu nedenle, veri deponuzda artık geçerli olmayan bağlantı kimlikleri için kayıtlar olabilir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-169">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="ccd51-170">Bu yalnız bırakılmış kayıtları temizlemek için, uygulamanız için uygun bir zaman çerçevesi dışında oluşturulmuş herhangi bir bağlantıyı geçersiz kılmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-170">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="ccd51-171">Bu bölümdeki örneklerde, bağlantının oluşturulduğu sırada izleme için bir değer yer alır, ancak bunu arka plan işlemi olarak yapmak isteyebileceğiniz için eski kayıtların nasıl temizleyeceğini göstermeyin.</span><span class="sxs-lookup"><span data-stu-id="ccd51-171">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="ccd51-172">Veritabanı</span><span class="sxs-lookup"><span data-stu-id="ccd51-172">Database</span></span>

<span data-ttu-id="ccd51-173">Aşağıdaki örneklerde, bağlantı ve Kullanıcı bilgilerinin bir veritabanında nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-173">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="ccd51-174">Herhangi bir veri erişim teknolojisini kullanabilirsiniz; Ancak, aşağıdaki örnekte Entity Framework kullanarak modellerin nasıl tanımlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-174">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="ccd51-175">Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-175">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="ccd51-176">Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-176">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="ccd51-177">İlk örnek, birçok bağlantı varlığı ile ilişkilendirilebilen bir Kullanıcı varlığının nasıl tanımlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-177">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

<span data-ttu-id="ccd51-178">Ardından, hub 'dan her bağlantının durumunu aşağıda gösterilen kodla izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-178">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a><span data-ttu-id="ccd51-179">Azure tablo depolama</span><span class="sxs-lookup"><span data-stu-id="ccd51-179">Azure table storage</span></span>

<span data-ttu-id="ccd51-180">Aşağıdaki Azure Tablo depolama örneği, veritabanı örneğine benzer.</span><span class="sxs-lookup"><span data-stu-id="ccd51-180">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="ccd51-181">Azure Tablo Depolama hizmetini kullanmaya başlamak için ihtiyacınız olan tüm bilgileri içermez.</span><span class="sxs-lookup"><span data-stu-id="ccd51-181">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="ccd51-182">Bilgi için bkz. [.net 'Ten Tablo Depolamayı kullanma](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="ccd51-182">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="ccd51-183">Aşağıdaki örnek, bağlantı bilgilerini depolamak için bir tablo varlığı gösterir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-183">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="ccd51-184">Verileri Kullanıcı adına göre bölümlendirir ve her bir varlığı bağlantı kimliğiyle tanımlar, böylece Kullanıcı istedikleri zaman birden çok bağlantıya sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="ccd51-184">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

<span data-ttu-id="ccd51-185">Hub 'da, her kullanıcının bağlantısının durumunu izlersiniz.</span><span class="sxs-lookup"><span data-stu-id="ccd51-185">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]
