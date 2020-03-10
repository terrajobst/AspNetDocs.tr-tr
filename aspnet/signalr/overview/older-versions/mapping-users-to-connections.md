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
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a>SignalR 1.x Sürümünde SignalR Kullanıcılarını Bağlantılarla Eşleme

, [Patrick Fleti](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu konuda kullanıcılar ve bağlantılarıyla ilgili bilgilerin nasıl saklanacağı gösterilmektedir.

## <a name="introduction"></a>Giriş

Bir hub 'a bağlanan her istemci, benzersiz bir bağlantı kimliği geçirir. Hub bağlamının `Context.ConnectionId` özelliğindeki bu değeri alabilirsiniz. Uygulamanız bir kullanıcıyı bağlantı kimliğiyle eşlemek ve bu eşlemeyi kalıcı hale getirmek için aşağıdakilerden birini kullanabilirsiniz:

- Sözlük gibi [bellek içi depolama](#inmemory)
- [Her Kullanıcı için SignalR grubu](#groups)
- Veritabanı tablosu veya Azure Tablo depolaması gibi [kalıcı, dış depolama](#database)

Bu uygulamaların her biri, bu konuda gösterilmektedir. Kullanıcı bağlantı durumunu izlemek için `Hub` sınıfının `OnConnected`, `OnDisconnected`ve `OnReconnected` yöntemlerini kullanın.

Uygulamanız için en iyi yaklaşım şunlara bağlıdır:

- Uygulamanızı barındıran Web sunucularının sayısı.
- Şu anda bağlı olan kullanıcıların listesini almanız gerekip gerekmediğini belirtir.
- Uygulama veya sunucu yeniden başlatıldığında Grup ve Kullanıcı bilgilerini kalıcı yapmanız gerekip gerekmediğini belirtir.
- Dış sunucu çağırma gecikmesinin bir sorun olup olmadığı.

Aşağıdaki tabloda bu noktalar için hangi yaklaşımın çalıştığı gösterilmektedir.

|  | Birden çok sunucu | Şu anda bağlı olan kullanıcıların listesini al | Yeniden başlatıldıktan sonra bilgileri kalıcı yap | En iyi performans |
| --- | --- | --- | --- | --- |
| Bellek içi |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| Tek Kullanıcı grupları | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| Kalıcı, dış | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>Bellek içi depolama

Aşağıdaki örneklerde, bağlantı ve Kullanıcı bilgilerinin bellekte depolanan bir sözlükte nasıl saklanacağı gösterilmektedir. Sözlük, bağlantı kimliğini depolamak için bir `HashSet` kullanır. Herhangi bir kullanıcının SignalR uygulamasına birden fazla bağlantısı olabilir. Örneğin, birden çok cihaz veya birden çok tarayıcı sekmesinden bağlanmış bir kullanıcının birden fazla bağlantı kimliği vardır.

Uygulama kapatılırsa tüm bilgiler kaybolur, ancak kullanıcılar bağlantılarını yeniden kurduğundan, yeniden doldurulur. Her sunucunun ayrı bir bağlantı koleksiyonu olması nedeniyle, ortamınız birden fazla Web sunucusu içeriyorsa, bellek içi depolama çalışmaz.

İlk örnek, kullanıcıların bağlantılardaki eşlemesini yöneten bir sınıfı gösterir. HashSet için anahtar, kullanıcının adı olacaktır.

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

Sonraki örnekte, bağlantı eşleme sınıfının bir hub 'dan nasıl kullanılacağı gösterilmektedir. Sınıfının örneği `_connections`değişken adında depolanır.

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Tek Kullanıcı grupları

Her Kullanıcı için bir grup oluşturabilir ve yalnızca bu kullanıcıya erişmek istediğinizde bu gruba bir ileti gönderebilirsiniz. Her grubun adı kullanıcının adıdır. Kullanıcının birden fazla bağlantısı varsa, her bağlantı kimliği kullanıcının grubuna eklenir.

Kullanıcının bağlantısı kesildiğinde kullanıcıyı gruptan el ile kaldırmayın. Bu eylem, SignalR çerçevesi tarafından otomatik olarak gerçekleştirilir.

Aşağıdaki örnek, tek kullanıcılı grupların nasıl uygulanacağını gösterir.

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Kalıcı, dış depolama

Bu konuda, bağlantı bilgilerini depolamak için bir veritabanının veya Azure Tablo depolamanın nasıl kullanılacağı gösterilmektedir. Her Web sunucusu aynı veri deposuyla etkileşime girebildiğinden, bu yaklaşım birden çok Web sunucunuz olduğunda işe yarar. Web sunucularınız çalışmayı durdurmuş veya uygulama yeniden başlatılırsa `OnDisconnected` yöntemi çağrılmaz. Bu nedenle, veri deponuzda artık geçerli olmayan bağlantı kimlikleri için kayıtlar olabilir. Bu yalnız bırakılmış kayıtları temizlemek için, uygulamanız için uygun bir zaman çerçevesi dışında oluşturulmuş herhangi bir bağlantıyı geçersiz kılmak isteyebilirsiniz. Bu bölümdeki örneklerde, bağlantının oluşturulduğu sırada izleme için bir değer yer alır, ancak bunu arka plan işlemi olarak yapmak isteyebileceğiniz için eski kayıtların nasıl temizleyeceğini göstermeyin.

### <a name="database"></a>Veritabanı

Aşağıdaki örneklerde, bağlantı ve Kullanıcı bilgilerinin bir veritabanında nasıl saklanacağı gösterilmektedir. Herhangi bir veri erişim teknolojisini kullanabilirsiniz; Ancak, aşağıdaki örnekte Entity Framework kullanarak modellerin nasıl tanımlanacağı gösterilmektedir. Bu varlık modelleri veritabanı tablolarına ve alanlarına karşılık gelir. Veri yapınız, uygulamanızın gereksinimlerine bağlı olarak önemli ölçüde farklılık gösterebilir.

İlk örnek, birçok bağlantı varlığı ile ilişkilendirilebilen bir Kullanıcı varlığının nasıl tanımlanacağını gösterir.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

Ardından, hub 'dan her bağlantının durumunu aşağıda gösterilen kodla izleyebilirsiniz.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a>Azure tablo depolama

Aşağıdaki Azure Tablo depolama örneği, veritabanı örneğine benzer. Azure Tablo Depolama hizmetini kullanmaya başlamak için ihtiyacınız olan tüm bilgileri içermez. Bilgi için bkz. [.net 'Ten Tablo Depolamayı kullanma](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).

Aşağıdaki örnek, bağlantı bilgilerini depolamak için bir tablo varlığı gösterir. Verileri Kullanıcı adına göre bölümlendirir ve her bir varlığı bağlantı kimliğiyle tanımlar, böylece Kullanıcı istedikleri zaman birden çok bağlantıya sahip olabilir.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

Hub 'da, her kullanıcının bağlantısının durumunu izlersiniz.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]
