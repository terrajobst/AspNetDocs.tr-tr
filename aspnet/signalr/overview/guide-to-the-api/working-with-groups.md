---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: SignalR 'de gruplarla çalışma | Microsoft Docs
author: bradygaster
description: Bu konu başlığı altında, Grup üyeliği bilgilerinin Merkez API 'SI ile nasıl korunmakta olduğu açıklanır.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 46dd952fc4902b37c981a111dfa344dad79bb668
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558585"
---
# <a name="working-with-groups-in-signalr"></a><span data-ttu-id="c3279-103">SignalR’da Gruplarla Çalışma</span><span class="sxs-lookup"><span data-stu-id="c3279-103">Working with Groups in SignalR</span></span>

<span data-ttu-id="c3279-104">, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c3279-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c3279-105">Bu konuda, gruplara kullanıcı ekleme ve grup üyeliği bilgilerini kalıcı hale getirme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c3279-105">This topic describes how to add users to groups and persist group membership information.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="c3279-106">Bu konuda kullanılan yazılım sürümleri</span><span class="sxs-lookup"><span data-stu-id="c3279-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="c3279-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="c3279-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="c3279-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c3279-108">.NET 4.5</span></span>
> - <span data-ttu-id="c3279-109">SignalR sürüm 2</span><span class="sxs-lookup"><span data-stu-id="c3279-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="c3279-110">Bu konunun önceki sürümleri</span><span class="sxs-lookup"><span data-stu-id="c3279-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="c3279-111">SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="c3279-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="c3279-112">Sorular ve açıklamalar</span><span class="sxs-lookup"><span data-stu-id="c3279-112">Questions and comments</span></span>
>
> <span data-ttu-id="c3279-113">Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun.</span><span class="sxs-lookup"><span data-stu-id="c3279-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="c3279-114">Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3279-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="c3279-115">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="c3279-115">Overview</span></span>

<span data-ttu-id="c3279-116">SignalR içindeki gruplar, bağlı istemcilerin belirtilen alt kümelerine ileti yayınlamak için bir yöntem sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3279-116">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="c3279-117">Bir grup herhangi bir sayıda istemciye sahip olabilir ve bir istemci herhangi bir sayıda grubun üyesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3279-117">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="c3279-118">Açıkça grup oluşturmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c3279-118">You don't have to explicitly create groups.</span></span> <span data-ttu-id="c3279-119">Aslında bir grup, bir gruba yapılan çağrıda adını ilk kez belirttiğinizde otomatik olarak oluşturulur. ekleyin ve bu, içindeki üyeliğinden son bağlantıyı kaldırdığınızda silinir.</span><span class="sxs-lookup"><span data-stu-id="c3279-119">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="c3279-120">Grupları kullanmaya giriş için, bkz. hub API-sunucu kılavuzundaki [hub sınıfından grup üyeliğini yönetme](hubs-api-guide-server.md#groupsfromhub) .</span><span class="sxs-lookup"><span data-stu-id="c3279-120">For an introduction to using groups, see [How to manage group membership from the Hub class](hubs-api-guide-server.md#groupsfromhub) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="c3279-121">Grup üyeliği listesi veya Grup listesi almak için API yok.</span><span class="sxs-lookup"><span data-stu-id="c3279-121">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="c3279-122">SignalR bir yayın/alt modele göre istemcilere ve gruplara iletiler gönderir ve sunucu grup veya grup üyelikleri listesini korumaz.</span><span class="sxs-lookup"><span data-stu-id="c3279-122">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="c3279-123">Bu, bir Web grubuna düğüm eklediğiniz her durumda, SignalR 'nin koruduğu tüm durumun yeni düğüme yayılması nedeniyle ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c3279-123">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="c3279-124">`Groups.Add` yöntemi kullanarak bir kullanıcıyı bir gruba eklediğinizde, Kullanıcı o gruba yönlendirilen iletileri geçerli bağlantı süresince alır, ancak kullanıcının bu gruptaki üyeliği geçerli bağlantının ötesinde kalıcı olmaz.</span><span class="sxs-lookup"><span data-stu-id="c3279-124">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="c3279-125">Gruplar ve grup üyeliği hakkındaki bilgileri kalıcı olarak saklamak istiyorsanız, bu verileri bir veritabanı veya Azure Tablo depolaması gibi bir depoda saklamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3279-125">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="c3279-126">Ardından, bir Kullanıcı uygulamanıza her bağladığında, kullanıcının sahip olduğu havuzdan alınır ve o kullanıcıyı bu gruplara el ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c3279-126">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="c3279-127">Geçici bir kesintiden sonra yeniden bağlanıldığında Kullanıcı önceden atanmış grupları otomatik olarak yeniden birleştirir.</span><span class="sxs-lookup"><span data-stu-id="c3279-127">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="c3279-128">Bir gruba otomatik olarak yeniden katılmak, yeni bir bağlantı kurulurken değil, yalnızca yeniden bağlanıldığında geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="c3279-128">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="c3279-129">Dijital olarak imzalanan bir belirteç, daha önce atanmış grupların listesini içeren istemciden geçirilir.</span><span class="sxs-lookup"><span data-stu-id="c3279-129">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="c3279-130">Kullanıcının istenen gruplara ait olup olmadığını doğrulamak istiyorsanız, varsayılan davranışı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3279-130">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="c3279-131">Bu konu aşağıdaki bölümleri içermektedir:</span><span class="sxs-lookup"><span data-stu-id="c3279-131">This topic includes the following sections:</span></span>

- [<span data-ttu-id="c3279-132">Kullanıcı ekleme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="c3279-132">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="c3279-133">Bir grubun üyelerini çağırma</span><span class="sxs-lookup"><span data-stu-id="c3279-133">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="c3279-134">Grup üyeliğini bir veritabanında depolama</span><span class="sxs-lookup"><span data-stu-id="c3279-134">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="c3279-135">Azure Tablo Depolaması 'nda grup üyeliğini depolama</span><span class="sxs-lookup"><span data-stu-id="c3279-135">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="c3279-136">Yeniden bağlanırken grup üyeliği doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="c3279-136">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="c3279-137">Kullanıcı ekleme ve kaldırma</span><span class="sxs-lookup"><span data-stu-id="c3279-137">Adding and removing users</span></span>

<span data-ttu-id="c3279-138">Bir gruba kullanıcı eklemek veya kaldırmak için, [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) veya [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini çağırır ve kullanıcının bağlantı kimliğini ve grup adını parametreler olarak geçirin.</span><span class="sxs-lookup"><span data-stu-id="c3279-138">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="c3279-139">Bağlantı sona erdiğinde bir kullanıcıyı bir gruptan el ile kaldırmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c3279-139">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="c3279-140">Aşağıdaki örnek, hub yöntemlerinde kullanılan `Groups.Add` ve `Groups.Remove` yöntemlerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3279-140">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="c3279-141">`Groups.Add` ve `Groups.Remove` yöntemleri zaman uyumsuz olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="c3279-141">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="c3279-142">Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen ileti göndermek istiyorsanız, groups. Add yönteminin önce tamamlandığından emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3279-142">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="c3279-143">Aşağıdaki kod örnekleri bunun nasıl yapılacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="c3279-143">The following code examples show how to do that.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

<span data-ttu-id="c3279-144">Kaldırmaya çalıştığınız bağlantı kimliği artık kullanılamadığından, genel olarak, `Groups.Remove` metodunu çağırırken `await` eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="c3279-144">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="c3279-145">Bu durumda, `TaskCanceledException` istek zaman aşımına uğraydıktan sonra oluşturulur. Uygulamanız, gruba bir ileti göndermeden önce kullanıcının gruptan kaldırıldığından emin olması gerekiyorsa, `Groups.Remove`önce `await` ekleyebilir ve ardından, daha sonra ortaya çıkarılan `TaskCanceledException` özel durumunu yakalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c3279-145">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before `Groups.Remove`, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="c3279-146">Bir grubun üyelerini çağırma</span><span class="sxs-lookup"><span data-stu-id="c3279-146">Calling members of a group</span></span>

<span data-ttu-id="c3279-147">Aşağıdaki örneklerde gösterildiği gibi, bir grubun tüm üyelerine veya grubun yalnızca belirtilen üyelerine iletiler gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3279-147">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="c3279-148">Belirtilen bir gruptaki **Tüm** bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="c3279-148">**All** connected clients in a specified group.</span></span>

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- <span data-ttu-id="c3279-149">Belirtilen bir gruptaki, belirtilen **istemciler hariç**, bağlantı kimliğiyle tanımlanan tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="c3279-149">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span>

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- <span data-ttu-id="c3279-150">**Çağıran istemci hariç,** belirtilen bir gruptaki tüm bağlı istemciler.</span><span class="sxs-lookup"><span data-stu-id="c3279-150">All connected clients in a specified group **except the calling client**.</span></span>

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="c3279-151">Grup üyeliğini bir veritabanında depolama</span><span class="sxs-lookup"><span data-stu-id="c3279-151">Storing group membership in a database</span></span>

<span data-ttu-id="c3279-152">Aşağıdaki örneklerde, Grup ve Kullanıcı bilgilerinin bir veritabanında nasıl saklanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c3279-152">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="c3279-153">Herhangi bir veri erişim teknolojisini kullanabilirsiniz; Ancak, aşağıdaki örnekte Entity Framework kullanarak modellerin nasıl tanımlanacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="c3279-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="c3279-154">Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="c3279-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="c3279-155">Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde farklılık gösterebilir.</span><span class="sxs-lookup"><span data-stu-id="c3279-155">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="c3279-156">Bu örnek, kullanıcıların spor veya bahçe gibi farklı konularla ilgili konuşmaları katılmasına olanak sağlayan bir uygulama için benzersiz olan `ConversationRoom` adlı bir sınıf içerir.</span><span class="sxs-lookup"><span data-stu-id="c3279-156">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="c3279-157">Bu örnek ayrıca bağlantılar için bir sınıf içerir.</span><span class="sxs-lookup"><span data-stu-id="c3279-157">This example also includes a class for the connections.</span></span> <span data-ttu-id="c3279-158">Bağlantı sınıfı, Grup üyeliğini izlemek için kesinlikle gerekli değildir, ancak kullanıcıları izlemeye yönelik genellikle güçlü çözümün bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="c3279-158">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

<span data-ttu-id="c3279-159">Ardından, hub 'da, Grup ve Kullanıcı bilgilerini veritabanından alabilir ve kullanıcıyı uygun gruplara el ile ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3279-159">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="c3279-160">Örnek, Kullanıcı bağlantılarını izlemeye yönelik kodu içermez.</span><span class="sxs-lookup"><span data-stu-id="c3279-160">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="c3279-161">Bu örnekte, bir ileti doğrudan grubun üyelerine gönderilmediğinden, `await` anahtar sözcüğü `Groups.Add` önce uygulanmaz.</span><span class="sxs-lookup"><span data-stu-id="c3279-161">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="c3279-162">Yeni üye eklendikten hemen sonra grubun tüm üyelerine bir ileti göndermek istiyorsanız, zaman uyumsuz işlemin tamamlandığından emin olmak için `await` anahtar sözcüğünü uygulamak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3279-162">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="c3279-163">Azure Tablo Depolaması 'nda grup üyeliğini depolama</span><span class="sxs-lookup"><span data-stu-id="c3279-163">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="c3279-164">Grubu ve Kullanıcı bilgilerini depolamak için Azure Tablo depolama kullanmak, veritabanı kullanmaya benzer.</span><span class="sxs-lookup"><span data-stu-id="c3279-164">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="c3279-165">Aşağıdaki örnek, Kullanıcı adını ve grup adını depolayan bir tablo varlığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3279-165">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<span data-ttu-id="c3279-166">Hub 'da, Kullanıcı bağlanırken atanan grupları alırsınız.</span><span class="sxs-lookup"><span data-stu-id="c3279-166">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="c3279-167">Yeniden bağlanırken grup üyeliği doğrulanıyor</span><span class="sxs-lookup"><span data-stu-id="c3279-167">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="c3279-168">Varsayılan olarak, SignalR, bağlantı zaman aşımına uğramadan önce bir bağlantının düşürülme ve yeniden oluşturulması gibi geçici bir kesintiden yeniden bağlanıldığında bir kullanıcıyı uygun gruplara otomatik olarak yeniden atar. Kullanıcının grup bilgileri yeniden bağlanıldığında bir belirtece geçirilir ve bu belirteç sunucuda doğrulanır.</span><span class="sxs-lookup"><span data-stu-id="c3279-168">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="c3279-169">Kullanıcıların gruplara yeniden katılması için doğrulama süreci hakkında bilgi için bkz. [yeniden bağlanıldığında grupları yeniden birleştirme](../security/introduction-to-security.md#rejoingroup).</span><span class="sxs-lookup"><span data-stu-id="c3279-169">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](../security/introduction-to-security.md#rejoingroup).</span></span>

<span data-ttu-id="c3279-170">Genel olarak, yeniden bağlanma sırasında grupları otomatik olarak yeniden birleştirme varsayılan davranışını kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3279-170">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="c3279-171">SignalR grupları, gizli verilere erişimi kısıtlamak için bir güvenlik mekanizması olarak tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="c3279-171">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="c3279-172">Ancak, uygulamanızın yeniden bağlanırken bir kullanıcının grup üyeliğini iki kez denetlemesi gerekiyorsa, varsayılan davranışı geçersiz kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3279-172">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="c3279-173">Varsayılan davranışı değiştirmek, bir kullanıcının grup üyeliğinin yalnızca Kullanıcı bağlantısı yerine her yeniden bağlantı için alınması gerektiğinden veritabanınıza bir yük ekleyebilir.</span><span class="sxs-lookup"><span data-stu-id="c3279-173">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="c3279-174">Yeniden bağlanma sırasında grup üyeliğini doğrulamanız gerekiyorsa, aşağıda gösterildiği gibi, atanmış grupların bir listesini döndüren yeni bir hub işlem hattı modülü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3279-174">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<span data-ttu-id="c3279-175">Ardından, aşağıda vurgulanan şekilde bu modülü hub işlem hattına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="c3279-175">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]
