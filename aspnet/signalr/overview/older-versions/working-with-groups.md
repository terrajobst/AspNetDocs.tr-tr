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
# <a name="working-with-groups-in-signalr-1x"></a>SignalR 1.x Sürümünde Gruplarla Çalışma

, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konuda, gruplara kullanıcı ekleme ve grup üyeliği bilgilerini kalıcı hale getirme açıklanmaktadır.

## <a name="overview"></a>Genel bakış

SignalR içindeki gruplar, bağlı istemcilerin belirtilen alt kümelerine ileti yayınlamak için bir yöntem sağlar. Bir grup herhangi bir sayıda istemciye sahip olabilir ve bir istemci herhangi bir sayıda grubun üyesi olabilir. Açıkça grup oluşturmanız gerekmez. Aslında bir grup, bir gruba yapılan çağrıda adını ilk kez belirttiğinizde otomatik olarak oluşturulur. ekleyin ve bu, içindeki üyeliğinden son bağlantıyı kaldırdığınızda silinir. Grupları kullanmaya giriş için, bkz. hub API-sunucu kılavuzundaki [hub sınıfından grup üyeliğini yönetme](index.md) .

Grup üyeliği listesi veya Grup listesi almak için API yok. SignalR bir yayın/alt modele göre istemcilere ve gruplara iletiler gönderir ve sunucu grup veya grup üyelikleri listesini korumaz. Bu, bir Web grubuna düğüm eklediğiniz her durumda, SignalR 'nin koruduğu tüm durumun yeni düğüme yayılması nedeniyle ölçeklenebilirliği en üst düzeye çıkarmaya yardımcı olur.

`Groups.Add` yöntemi kullanarak bir kullanıcıyı bir gruba eklediğinizde, Kullanıcı o gruba yönlendirilen iletileri geçerli bağlantı süresince alır, ancak kullanıcının bu gruptaki üyeliği geçerli bağlantının ötesinde kalıcı olmaz. Gruplar ve grup üyeliği hakkındaki bilgileri kalıcı olarak saklamak istiyorsanız, bu verileri bir veritabanı veya Azure Tablo depolaması gibi bir depoda saklamanız gerekir. Ardından, bir Kullanıcı uygulamanıza her bağladığında, kullanıcının sahip olduğu havuzdan alınır ve o kullanıcıyı bu gruplara el ile ekleyin.

Geçici bir kesintiden sonra yeniden bağlanıldığında Kullanıcı önceden atanmış grupları otomatik olarak yeniden birleştirir. Bir gruba otomatik olarak yeniden katılmak, yeni bir bağlantı kurulurken değil, yalnızca yeniden bağlanıldığında geçerlidir. Dijital olarak imzalanan bir belirteç, daha önce atanmış grupların listesini içeren istemciden geçirilir. Kullanıcının istenen gruplara ait olup olmadığını doğrulamak istiyorsanız, varsayılan davranışı geçersiz kılabilirsiniz.

Bu konu aşağıdaki bölümleri içermektedir:

- [Kullanıcı ekleme ve kaldırma](#add)
- [Bir grubun üyelerini çağırma](#call)
- [Grup üyeliğini bir veritabanında depolama](#storedatabase)
- [Azure Tablo Depolaması 'nda grup üyeliğini depolama](#storeazuretable)
- [Yeniden bağlanırken grup üyeliği doğrulanıyor](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>Kullanıcı ekleme ve kaldırma

Bir gruba kullanıcı eklemek veya kaldırmak için, [Ekle](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) veya [Kaldır](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) yöntemlerini çağırır ve kullanıcının bağlantı kimliğini ve grup adını parametreler olarak geçirin. Bağlantı sona erdiğinde bir kullanıcıyı bir gruptan el ile kaldırmanız gerekmez.

Aşağıdaki örnek, hub yöntemlerinde kullanılan `Groups.Add` ve `Groups.Remove` yöntemlerini gösterir.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

`Groups.Add` ve `Groups.Remove` yöntemleri zaman uyumsuz olarak yürütülür.

Bir gruba bir istemci eklemek ve grubu kullanarak istemciye hemen ileti göndermek istiyorsanız, groups. Add yönteminin önce tamamlandığından emin olmanız gerekir. Aşağıdaki kod örneklerinde bunun nasıl yapılacağı, biri .NET 4,5 ' de çalıştırılan ve bir .NET 4 ' te çalıştırılan kod kullanılarak nasıl yapılacağı gösterilmektedir.

#### <a name="asynchronous-net-45-example"></a>Zaman uyumsuz .NET 4,5 örneği

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>Zaman uyumsuz .NET 4 örneği

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

Kaldırmaya çalıştığınız bağlantı kimliği artık kullanılamadığından, genel olarak, `Groups.Remove` metodunu çağırırken `await` eklemeyin. Bu durumda, `TaskCanceledException` istek zaman aşımına uğraydıktan sonra oluşturulur. Uygulamanız, gruba bir ileti göndermeden önce kullanıcının gruptan kaldırıldığından emin olması gerekiyorsa, gruplardan önce `await` ekleyebilirsiniz., daha sonra ortaya çıkarılan `TaskCanceledException` özel durumu silin ve sonra da yakalanamaz.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>Bir grubun üyelerini çağırma

Aşağıdaki örneklerde gösterildiği gibi, bir grubun tüm üyelerine veya grubun yalnızca belirtilen üyelerine iletiler gönderebilirsiniz.

- Belirtilen bir gruptaki **Tüm** bağlı istemciler. 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- Belirtilen bir gruptaki, belirtilen **istemciler hariç**, bağlantı kimliğiyle tanımlanan tüm bağlı istemciler. 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- **Çağıran istemci hariç,** belirtilen bir gruptaki tüm bağlı istemciler. 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>Grup üyeliğini bir veritabanında depolama

Aşağıdaki örneklerde, Grup ve Kullanıcı bilgilerinin bir veritabanında nasıl saklanacağı gösterilmektedir. Herhangi bir veri erişim teknolojisini kullanabilirsiniz; Ancak, aşağıdaki örnekte Entity Framework kullanarak modellerin nasıl tanımlanacağı gösterilmektedir. Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir. Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde farklılık gösterebilir. Bu örnek, kullanıcıların spor veya bahçe gibi farklı konularla ilgili konuşmaları katılmasına olanak sağlayan bir uygulama için benzersiz olan `ConversationRoom` adlı bir sınıf içerir. Bu örnek ayrıca bağlantılar için bir sınıf içerir. Bağlantı sınıfı, Grup üyeliğini izlemek için kesinlikle gerekli değildir, ancak kullanıcıları izlemeye yönelik genellikle güçlü çözümün bir parçasıdır.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

Ardından, hub 'da, Grup ve Kullanıcı bilgilerini veritabanından alabilir ve kullanıcıyı uygun gruplara el ile ekleyebilirsiniz. Örnek, Kullanıcı bağlantılarını izlemeye yönelik kodu içermez. Bu örnekte, bir ileti doğrudan grubun üyelerine gönderilmediğinden, `await` anahtar sözcüğü `Groups.Add` önce uygulanmaz. Yeni üye eklendikten hemen sonra grubun tüm üyelerine bir ileti göndermek istiyorsanız, zaman uyumsuz işlemin tamamlandığından emin olmak için `await` anahtar sözcüğünü uygulamak isteyebilirsiniz.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Azure Tablo Depolaması 'nda grup üyeliğini depolama

Grubu ve Kullanıcı bilgilerini depolamak için Azure Tablo depolama kullanmak, veritabanı kullanmaya benzer. Aşağıdaki örnek, Kullanıcı adını ve grup adını depolayan bir tablo varlığını gösterir.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

Hub 'da, Kullanıcı bağlanırken atanan grupları alırsınız.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>Yeniden bağlanırken grup üyeliği doğrulanıyor

Varsayılan olarak, SignalR, bağlantı zaman aşımına uğramadan önce bir bağlantının düşürülme ve yeniden oluşturulması gibi geçici bir kesintiden yeniden bağlanıldığında bir kullanıcıyı uygun gruplara otomatik olarak yeniden atar. Kullanıcının grup bilgileri yeniden bağlanıldığında bir belirtece geçirilir ve bu belirteç sunucuda doğrulanır. Kullanıcıların gruplara yeniden katılması için doğrulama süreci hakkında bilgi için bkz. [yeniden bağlanıldığında grupları yeniden birleştirme](index.md).

Genel olarak, yeniden bağlanma sırasında grupları otomatik olarak yeniden birleştirme varsayılan davranışını kullanmanız gerekir. SignalR grupları, gizli verilere erişimi kısıtlamak için bir güvenlik mekanizması olarak tasarlanmamıştır. Ancak, uygulamanızın yeniden bağlanırken bir kullanıcının grup üyeliğini iki kez denetlemesi gerekiyorsa, varsayılan davranışı geçersiz kılabilirsiniz. Varsayılan davranışı değiştirmek, bir kullanıcının grup üyeliğinin yalnızca Kullanıcı bağlantısı yerine her yeniden bağlantı için alınması gerektiğinden veritabanınıza bir yük ekleyebilir.

Yeniden bağlanma sırasında grup üyeliğini doğrulamanız gerekiyorsa, aşağıda gösterildiği gibi, atanmış grupların bir listesini döndüren yeni bir hub işlem hattı modülü oluşturun.

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

Ardından, aşağıda vurgulanan şekilde bu modülü hub işlem hattına ekleyin.

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]
