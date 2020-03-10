---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 'Öğretici: SignalR 2 ile sunucu yayını | Microsoft Docs'
author: tdykstra
description: Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir.
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536605"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>Öğretici: SignalR 2 ile sunucu yayını

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Sunucu yayını, sunucunun istemcilere gönderilen iletişimleri başlattığı anlamına gelir.

Bu öğreticide oluşturacağınız uygulama, sunucu yayını işlevselliği için tipik bir senaryo olan bir stok Ticker benzetimini yapar. Düzenli aralıklarla, sunucu stok fiyatlarını rastgele güncelleştirir ve güncelleştirmeleri tüm bağlı istemcilere yayınlar. Tarayıcıda, **değişiklik** ve **%** sütunlarında bulunan sayılar ve semboller, sunucudan gelen bildirimlere yanıt olarak dinamik olarak değişir. Aynı URL 'ye ek tarayıcılar açarsanız, hepsi aynı verileri ve verilerde aynı değişiklikleri aynı anda gösterir.

![Web oluştur](tutorial-server-broadcast-with-signalr/_static/image1.png)

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Projeyi oluşturma
> * Sunucu kodunu ayarlama
> * Sunucu kodunu inceleyin
> * İstemci kodunu ayarlama
> * İstemci kodunu inceleme
> * Uygulamayı test etme
> * Günlüğü etkinleştirme

> [!IMPORTANT]
> Uygulamayı oluşturma adımları boyunca çalışmak istemiyorsanız, SignalR. Sample paketini yeni bir boş ASP.NET Web uygulaması projesine yükleyebilirsiniz. NuGet paketini bu öğreticideki adımları uygulamadan yüklerseniz, *README. txt* dosyasındaki yönergeleri izlemeniz gerekir. Paketi çalıştırmak için, yüklü paketteki `ConfigureSignalR` yöntemini çağıran bir OWıN başlangıç sınıfı eklemeniz gerekir. OWıN başlangıç sınıfını eklememanız durumunda bir hata alırsınız. Bu makalenin [StockTicker örneğini Install](#install-the-stockticker-sample) bölümüne bakın.

## <a name="prerequisites"></a>Önkoşullar

* [ASP.NET ve web geliştirme](https://visualstudio.microsoft.com/downloads/) iş yüküyle **Visual Studio 2017**.

## <a name="create-the-project"></a>Projeyi oluşturma

Bu bölümde, Visual Studio 2017 ' ın boş bir ASP.NET Web uygulaması oluşturmak için nasıl kullanılacağı gösterilmektedir.

1. Visual Studio 'da bir ASP.NET Web uygulaması oluşturun.

    ![Web oluştur](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. **Yeni ASP.NET Web uygulaması-SignalR. StockTicker** penceresinde **boş** bırakın ve **Tamam**' ı seçin.

## <a name="set-up-the-server-code"></a>Sunucu kodunu ayarlama

Bu bölümde, sunucuda çalışan kodu ayarlarsınız.

### <a name="create-the-stock-class"></a>Hisse senedi sınıfını oluşturma

Bir hisse senedi hakkındaki bilgileri depolamak ve aktarmak için kullanacağınız *Stok* modeli sınıfını oluşturarak başlarsınız.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **sınıfı** **Ekle** ' yi seçin.

1. Sınıfı *stoğa* adlandırın ve projeye ekleyin.

1. *Stock.cs* dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    Hisse senetleri oluştururken ayarlayacağımız iki özellik `Symbol` (örneğin, Microsoft için MSFT) ve `Price`. Diğer özellikler `Price`nasıl ve ne zaman ayarlandığınıza bağlıdır. `Price`ilk kez ayarlandığında, değer `DayOpen`yayılır. Bundan sonra, `Price`ayarladığınızda, uygulama `Change` ve `PercentChange` özellik değerlerini `Price` ve `DayOpen`arasındaki farka göre hesaplar.

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>StockTickerHub ve StockTicker sınıfları oluşturma

Sunucudan istemciye etkileşimi işlemek için SignalR hub API 'sini kullanırsınız. SignalR `Hub` sınıfından türetilen `StockTickerHub` bir sınıf, istemcilerden gelen bağlantıları ve Yöntem çağrılarını almayı işleyecek. Ayrıca, stok verilerini korumanız ve bir `Timer` nesnesi çalıştırmanız gerekir. `Timer` nesnesi, Fiyat güncelleştirmelerini düzenli olarak istemci bağlantılarından bağımsız olarak tetikleyecektir. Hub 'Lar geçici olduğundan, bu işlevleri bir `Hub` sınıfına koyamazsınız. Uygulama, hub üzerindeki her görev için, istemcilerden sunucuya bağlantılar ve çağrılar gibi bir `Hub` sınıf örneği oluşturur. Bu nedenle, stok verilerini tutan, fiyatları güncelleştiren ve fiyat güncelleştirmelerinin yayınlarından oluşan mekanizmanın ayrı bir sınıfta çalışması gerekir. `StockTicker`sınıfı adını değiştireceksiniz.

![StockTicker 'den yayımlama](tutorial-server-broadcast-with-signalr/_static/image3.png)

Yalnızca bir `StockTicker` sınıfının bir örneğinin sunucuda çalıştırılmasını istiyorsunuz, bu nedenle her bir `StockTickerHub` örneğinden Singleton `StockTicker` örneğine bir başvuru ayarlamanız gerekir. `StockTicker` sınıfı, stok verilerini ve Tetikleyiciler güncelleştirmelerini içerdiğinden, ancak `StockTicker` bir `Hub` sınıfı olmadığından istemcilere yayınlayacak. `StockTicker` sınıfı, SignalR hub bağlantı bağlamı nesnesine bir başvuru almak için sahiptir. Daha sonra, istemcilere yayımlamak için SignalR bağlantı bağlamı nesnesini kullanabilir.

#### <a name="create-stocktickerhubcs"></a>StockTickerHub.cs oluştur

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.

1. **Yeni öğe Ekle-SignalR. StockTicker**' da, **yüklü** > **Visual C#**  > **Web** > **SignalR** ' i seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.

1. Sınıfı *StockTickerHub* olarak adlandırın ve projeye ekleyin.

    Bu adım *StockTickerHub.cs* sınıf dosyasını oluşturur. Aynı anda, bir dizi betik dosyası ve proje için SignalR 'yi destekleyen derleme başvuruları ekler.

1. *StockTickerHub.cs* dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. Dosyayı kaydedin.

Uygulama, istemcilerin sunucuda çağırabilmesine yönelik yöntemleri tanımlamak için [hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) sınıfını kullanır. Bir yöntem tanımlanıyor: `GetAllStocks()`. Bir istemci sunucuya ilk kez bağlandığında, geçerli fiyatlarına sahip tüm hisse senetleri listesini almak için bu yöntemi çağırır. Yöntem zaman uyumlu olarak çalışabilir ve bellekten veri döndürdüğü için `IEnumerable<Stock>` döndürebilir.

Bir veritabanı araması veya Web hizmeti çağrısı gibi, beklenmek üzere, yöntemin verileri alması gerekiyorsa, zaman uyumsuz işlemeyi etkinleştirmek için dönüş değeri olarak `Task<IEnumerable<Stock>>` belirtmeniz gerekir. Daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-zaman uyumsuz olarak yürütülecektir](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods).

`HubName` özniteliği, uygulamanın, istemcideki JavaScript kodunda hub 'A nasıl başvurulacağını belirtir. İstemci üzerindeki varsayılan ad bu özniteliği kullanmıyorsanız, sınıf adının bir camelCase sürümüdür, bu durumda `stockTickerHub`.

`StockTicker` sınıfını oluştururken daha sonra göreceğiniz gibi, uygulama, statik `Instance` özelliğinde bu sınıfın tek bir örneğini oluşturur. Bu `StockTicker` tekil örneği, kaç istemcinin bağlanıp bağlantısı kesildiğine bakılmaksızın bellekte bulunur. Bu örnek, `GetAllStocks()` yönteminin geçerli stok bilgilerini döndürmek için kullandığı şeydir.

#### <a name="create-stocktickercs"></a>StockTicker.cs oluştur

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **sınıfı** **Ekle** ' yi seçin.

1. Sınıfı *StockTicker* olarak adlandırın ve projeye ekleyin.

1. *StockTicker.cs* dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

Tüm iş parçacıkları StockTicker Code 'un aynı örneğini çalıştırdığından, StockTicker sınıfının iş parçacığı açısından güvenli olması gerekir.

### <a name="examine-the-server-code"></a>Sunucu kodunu inceleyin

Sunucu kodunu incelerseniz, uygulamanın nasıl çalıştığını anlamanıza yardımcı olur.

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>Tek örneği statik bir alanda depolama

Kod, `Instance` özelliğini bir sınıfının örneğiyle yedekleyen statik `_instance` alanını başlatır. Oluşturucu özel olduğundan, sınıfın, uygulamanın oluşturabileceğinden tek örneğidir. Uygulama, `_instance` alanı için [yavaş başlatma](/dotnet/framework/performance/lazy-initialization) kullanır. Performans nedenleriyle bu değildir. Örnek oluşturmanın iş parçacığı açısından güvenli olduğundan emin olmak.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

İstemci sunucuya her bağlanışında, ayrı bir iş parçacığında çalışan StockTickerHub sınıfının yeni bir örneği, `StockTickerHub` sınıfında daha önce gördüğünüz gibi `StockTicker.Instance` static özelliğinden StockTicker Singleton örneğini alır.

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Bir ConcurrentDictionary içinde hisse senedi verilerini depolama

Oluşturucu `_stocks` koleksiyonunu bazı örnek hisse senedi verileriyle başlatır ve `GetAllStocks` hisse senetleri döndürür. Daha önce gördüğünüz gibi, bu hisse senedi koleksiyonu, istemcilerin çağırabileceği `Hub` sınıfında bir sunucu yöntemi olan `StockTickerHub.GetAllStocks`tarafından döndürülür.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

Hisse senetleri koleksiyonu, iş parçacığı güvenliği için bir [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) türü olarak tanımlanır. Alternatif olarak, bir [Sözlük](https://msdn.microsoft.com/library/xfhwa508.aspx) nesnesi kullanabilir ve üzerinde değişiklik yaptığınızda sözlüğü açıkça kilitleyemezsiniz.

Bu örnek uygulama için uygulama verilerini bellekte depolamak ve uygulama `StockTicker` örneği olmadığında verileri kaybetmek için Tamam. Gerçek bir uygulamada, veritabanı gibi bir arka uç veri deposuyla çalışırsınız.

#### <a name="periodically-updating-stock-prices"></a>Stok fiyatlarını düzenli olarak güncelleştirme

Oluşturucu, stok fiyatlarını rastgele olarak güncelleştiren yöntemleri düzenli aralıklarla çağıran bir `Timer` nesnesi başlatır.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer`, durum parametresinde null değeri geçen `UpdateStockPrices`çağırır. Uygulama, fiyatları güncelleştirmeden önce `_updateStockPricesLock` nesnesinde bir kilit alır. Kod, başka bir iş parçacığının fiyatları zaten güncelleştirme olup olmadığını denetler ve ardından listedeki her stokta `TryUpdateStockPrice` çağırır. `TryUpdateStockPrice` yöntemi, stok fiyatının değiştirilip değişmeyeceğine ve ne kadarının değiştirileceğini belirler. Stok fiyatı değişirse, uygulama, stok fiyatı değişikliğini tüm bağlı istemcilere yayınlamak için `BroadcastStockPrice` çağırır.

`_updatingStockPrices` bayrağı, iş parçacığı açısından güvenli olduğundan emin olmak için [geçici](https://msdn.microsoft.com/library/x13ttww7.aspx) olarak belirlenmiş.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

Gerçek bir uygulamada `TryUpdateStockPrice` yöntemi, fiyatı aramak için bir Web hizmeti çağırır. Bu kodda, uygulama, değişiklikleri rastgele yapmak için rastgele bir sayı Oluşturucu kullanır.

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker sınıfının istemcilere yayınlanabilmesi için SignalR bağlamı alma

Fiyat değişiklikleri `StockTicker` nesnesinde yer aldığı için, tüm bağlı istemcilerde bir `updateStockPrice` yöntemi çağırması gereken nesnedir. `Hub` sınıfında, istemci yöntemlerini çağırmak için bir API 'SI vardır, ancak `StockTicker` `Hub` sınıfından türemez ve herhangi bir `Hub` nesnesine bir başvuruya sahip olmaz. Bağlı istemcilere yayımlamak için `StockTicker` sınıfı, `StockTickerHub` sınıfının SignalR bağlam örneğini almak ve bu işlemi istemcilerdeki yöntemleri çağırmak için kullanır.

Kod, tek sınıf örneğini oluşturduğunda SignalR bağlamına bir başvuru alır, bu başvuruyu oluşturucuya geçirir ve Oluşturucu onu `Clients` özelliğine koyar.

Bağlamı yalnızca bir kez almak istediğiniz iki neden vardır: bağlamı almak pahalı bir görevdir ve bir kez alınması, uygulamanın istemcilere gönderilen iletilerin amaçlanan sırasını koruyabilmesine olanak sağlar.

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

Bağlam `Clients` özelliğinin alınması ve `StockTickerClient` özelliğine yerleştirilmesi, bir `Hub` sınıfında olduğu gibi görünen istemci yöntemlerini çağırmak için kod yazmanıza olanak tanır. Örneğin, tüm istemcilere yayımlamak için `Clients.All.updateStockPrice(stock)`yazabilirsiniz.

`BroadcastStockPrice` içinde aradığınız `updateStockPrice` yöntemi henüz yok. Daha sonra, istemcide çalışan bir kod yazdığınızda eklersiniz. `Clients.All` dinamik olduğu için `updateStockPrice` buraya başvurabilirsiniz. Bu, uygulamanın çalışma zamanında ifadeyi değerlendirmesi anlamına gelir. Bu yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerini istemciye gönderir ve istemcinin `updateStockPrice`adlı bir yöntemi varsa, uygulama bu yöntemi çağırır ve parametre değerini bu yönteme iletir.

`Clients.All` tüm istemcilere gönderme anlamına gelir. SignalR, hangi istemcileri veya istemci gruplarını gönderileceğini belirtmek için size diğer seçenekler sağlar. Daha fazla bilgi için bkz. [Hubconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>SignalR rotasını kaydetme

Sunucunun hangi URL 'yi ele geçirip SignalR 'ye yönlendireceğimizi bilmeleri gerekir. Bunu yapmak için bir OWıN başlangıç sınıfı ekleyin:

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.

1. **Yeni öğe Ekle-SignalR. StockTicker** **yüklü** > **Visual C#**  > **Web** ' i seçin ve ardından **owın başlangıç sınıfı**' nı seçin.

1. Sınıfın *başlangıcını* adlandırın ve **Tamam**' ı seçin.

1. *Startup.cs* dosyasındaki varsayılan kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

Artık sunucu kodunu ayarlamayı tamamladınız. Sonraki bölümde, istemcisini ayarlayacaksınız.

## <a name="set-up-the-client-code"></a>İstemci kodunu ayarlama

Bu bölümde, istemcisinde çalışan kodu ayarlarsınız.

### <a name="create-the-html-page-and-javascript-file"></a>HTML sayfası ve JavaScript dosyası oluşturma

HTML sayfasında veriler görüntülenir ve JavaScript dosyası verileri düzenler.

#### <a name="create-stocktickerhtml"></a>StockTicker. HTML oluşturma

İlk olarak, HTML istemcisini eklersiniz.

1. **Çözüm Gezgini**' de projeye sağ tıklayın ve > **HTML sayfası** **Ekle** ' yi seçin.

1. Dosyayı *StockTicker* olarak adlandırın ve **Tamam**' ı seçin.

1. *StockTicker. html* dosyasındaki varsayılan kodu şu kodla değiştirin:

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML, beş sütun, üst bilgi satırı ve beş sütuna yayılan tek bir hücre içeren bir veri satırı içeren bir tablo oluşturur. Veri satırında "yükleniyor..." görüntülenir uygulama başladığında anlık olarak. JavaScript kodu, bu satırı kaldırır ve kendi yerleştirme satırlarına sunucudan alınan stok verilerini ekler.

    Komut dosyası etiketleri şunları belirtir:

    * JQuery betik dosyası.

    * SignalR çekirdek betik dosyası.

    * SignalR proxy 'leri betik dosyası.

    * Daha sonra oluşturacağınız bir StockTicker betik dosyası.

    Uygulama, SignalR proxy 'leri betik dosyasını dinamik olarak oluşturur. "/SignalR/hub 'ları" URL 'sini belirtir ve bu durumda `StockTickerHub.GetAllStocks`için, hub sınıfında yöntemler için proxy yöntemlerini tanımlar. İsterseniz, [SignalR yardımcı programlarını](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)kullanarak bu JavaScript dosyasını el ile oluşturabilirsiniz. `MapHubs` yöntemi çağrısında dinamik dosya oluşturmayı devre dışı bırakmayı unutmayın.

1. **Çözüm Gezgini**' de **betikler**' ı genişletin.

    JQuery ve SignalR için betik kitaplıkları projede görülebilir.

    > [!IMPORTANT]
    > Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yükler.

1. Kod bloğundaki betik başvurularını projedeki betik dosyalarının sürümlerine karşılık gelecek şekilde güncelleştirin.

1. **Çözüm Gezgini**' de, *StockTicker. html*' ye sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' yı seçin.

#### <a name="create-stocktickerjs"></a>StockTicker. js oluştur

Şimdi JavaScript dosyasını oluşturun.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **JavaScript dosyası** **Ekle** ' yi seçin.

1. Dosyayı *StockTicker* olarak adlandırın ve **Tamam**' ı seçin.

1. Bu kodu *StockTicker. js* dosyasına ekleyin:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>İstemci kodunu inceleme

İstemci kodunu incelerseniz, istemci kodunun, uygulamayı çalışır hale getirmek için sunucu koduyla nasıl etkileşime gireceğini öğrenirsiniz.

#### <a name="starting-the-connection"></a>Bağlantı başlatılıyor

`$.connection`, SignalR proxy 'leri anlamına gelir. Kod, `StockTickerHub` sınıfı için proxy 'ye bir başvuru alır ve `ticker` değişkenine koyar. Proxy adı, `HubName` özniteliği tarafından ayarlanan addır:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

Tüm değişkenleri ve işlevleri tanımladıktan sonra, dosyadaki kodun son satırı, SignalR `start` işlevini çağırarak SignalR bağlantısını başlatır. `start` işlevi zaman uyumsuz olarak yürütülür ve [jQuery ertelenmiş nesnesini](http://api.jquery.com/category/deferred-object/)döndürür. Uygulama zaman uyumsuz eylemi bitirdiğinde çağrılacak işlevi belirtmek için bitti işlevini çağırabilirsiniz.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>Tüm stokları alma

`init` işlevi, sunucuda `getAllStocks` işlevini çağırır ve sunucunun stok tablosunu güncelleştirmek için döndürdüğü bilgileri kullanır. Varsayılan olarak, yöntem adı sunucuda Pascal-cased olsa da, istemci üzerinde Camelbüyük harfleri kullanmanız gerektiğini unutmayın. Camelphı kuralı yalnızca yöntemlere uygulanır, nesneleri değil. Örneğin, `stock.symbol` veya `stock.price`değil, `stock.Symbol` ve `stock.Price`başvurursunuz.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

`init` yönteminde, uygulama, `stock` nesnenin özelliklerini biçimlendirmek için `formatStock` çağırarak ve sonra `supplant` çağırarak `rowTemplate` nesne özellik değerleriyle birlikte çağırarak, sunucudan alınan her bir stok nesnesi için bir tablo satırı için HTML oluşturur.`stock` Elde edilen HTML daha sonra hisse senedi tablosuna eklenir.

> [!NOTE]
> `init`, zaman uyumsuz `start` işlevi bittikten sonra yürüten bir `callback` işlevi olarak geçirerek çağırın. `start`çağrıldıktan sonra ayrı bir JavaScript açıklaması olarak `init` çağrılırsa, başlatma işlevinin bağlantıyı kurmayı tamamlaması beklenmeden hemen çalıştırılacağından işlev başarısız olur. Bu durumda `init` işlevi, uygulama bir sunucu bağlantısı kurmadan önce `getAllStocks` işlevini çağırmayı dener.

#### <a name="getting-updated-stock-prices"></a>Güncelleştirilmiş Stok fiyatları alma

Sunucu bir hisse senedi fiyatını değiştirdiğinde, bağlı istemcilerde `updateStockPrice` çağırır. Uygulama, sunucudan çağrılarla kullanılabilmesini sağlamak için işlevi `stockTicker` proxy 'sinin istemci özelliğine ekler.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

`updateStockPrice` işlevi, sunucudan alınan bir hisse senedi nesnesini, `init` işlevi ile aynı şekilde tablo satırına biçimlendirir. Satırı tabloya eklemek yerine, stoktaki geçerli satırını bulur ve bu satırı yeni bir satır ile değiştirir.

## <a name="test-the-application"></a>Uygulamayı test etme

Çalıştığından emin olmak için uygulamayı test edebilirsiniz. Tüm tarayıcı pencerelerinin, hisse senedi fiyatları dalgalanarak canlı hisse senedi tablosunu görüntülemesini görürsünüz.

1. Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından uygulamayı hata ayıklama modunda çalıştırmak için Yürüt düğmesini seçin.

    ![Kullanıcı hata ayıklama modunu açıp oynat 'ı seçen kullanıcının ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image4.png)

    **Canlı hisse senedi tablosunu**görüntüleyen bir tarayıcı penceresi açılacaktır. Hisse senedi tablosu başlangıçta "yükleniyor..." ardından, kısa bir süre sonra, uygulama ilk stok verilerini gösterir ve stok fiyatları değişme başlar.

1. Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.

    İlk stok görüntüsü ilk tarayıcıyla aynıdır ve değişiklikler aynı anda gerçekleşir.

1. Tüm tarayıcıları kapatın, yeni bir tarayıcı açın ve aynı URL 'ye gidin.

    StockTicker Singleton nesnesi sunucuda çalışmaya devam ediyor. **Canlı hisse senedi tablosu** , hisse senedinin değişmeye devam etseyi gösterir. Sıfır değişiklik rakamlarını içeren ilk tabloyu görmezsiniz.

1. Tarayıcıyı kapatın.

## <a name="enable-logging"></a>Günlüğü etkinleştirme

SignalR 'de, sorun gidermeye yardımcı olmak için istemcisinde etkinleştirebilmeniz gereken yerleşik bir günlüğe kaydetme işlevi vardır. Bu bölümde, günlüğe kaydetmeyi etkinleştirir ve günlüklerin, SignalR aşağıdaki taşıma yöntemlerinden hangisini kullandığını nasıl söyletiğini gösteren örneklere bakabilirsiniz:

* [WebSockets](http://en.wikipedia.org/wiki/WebSocket), IIS 8 ve geçerli tarayıcılar tarafından desteklenir.

* Internet Explorer dışındaki tarayıcılar tarafından desteklenen [sunucu tarafından gönderilen olaylar](http://en.wikipedia.org/wiki/Server-sent_events).

* Internet Explorer tarafından desteklenen [süresiz çerçeve](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe).

* Tüm tarayıcılar tarafından desteklenen [Ajax uzun yoklama](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).

Verilen herhangi bir bağlantı için, SignalR hem sunucu hem de istemci tarafından desteklenen en iyi taşıma yöntemini seçer.

1. *StockTicker. js*' ye açın.

1. Dosyanın sonunda bağlantıyı başlatan koddan hemen önce günlüğe kaydetmeyi etkinleştirmek için bu vurgulanmış kod satırını ekleyin:

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. Projeyi çalıştırmak için **F5** tuşuna basın.

1. Tarayıcınızın geliştirici araçları penceresini açın ve günlükleri görmek için konsolu seçin. Yeni bir bağlantı için taşıma yöntemiyle ilgili olarak, SignalR 'nin işlem için anlaşmasının günlüklerini görmek üzere sayfayı yenilemeniz gerekebilir.

    * Windows 8 (IIS 8) üzerinde Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi **WebSockets**olur.

    * Windows 7 ' de (IIS 7,5) Internet Explorer 10 çalıştırıyorsanız, taşıma yöntemi **iframe**'dir.

    * Windows 8 (IIS 8) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi **WebSockets**olur.

        > [!TIP]
        > Firefox 'ta, bir konsol penceresi almak için Firebug eklentisini yüklersiniz.

    * Windows 7 (IIS 7,5) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi **sunucu tarafından gönderilen** olaylardır.

## <a name="install-the-stockticker-sample"></a>StockTicker örneğini yükler

[Microsoft. Aspnet. SignalR. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) , StockTicker uygulamasını yüklüyor. NuGet paketi sıfırdan oluşturduğunuz Basitleştirilmiş sürümden daha fazla özellik içerir. Öğreticinin bu bölümünde, NuGet paketini yükler ve yeni özellikleri ve bunları uygulayan kodu gözden geçirin.

> [!IMPORTANT]
> Bu öğreticinin önceki adımlarını gerçekleştirmeden paketi yüklerseniz, projenize bir OWıN başlangıç sınıfı eklemeniz gerekir. NuGet paketi için bu Benioku. txt dosyasında bu adım açıklanmaktadır.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR. Sample NuGet paketini yükler

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin.

1. **NuGet Paket Yöneticisi: SignalR. StockTicker**' de, **Araştır**' ı seçin.

1. **Paket kaynağından** **NuGet.org**öğesini seçin.

1. Arama kutusuna *SignalR. Sample* girin ve **Microsoft. Aspnet. signalr. Sample** > **Install**' u seçin.

1. **Çözüm Gezgini**, *SignalR. Sample* klasörünü genişletin.

    SignalR. Sample paketini yükleme, klasörü ve içeriğini oluşturdu.

1. *SignalR. Sample* klasöründe, *StockTicker. html*' ye sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' yı seçin.

    > [!NOTE]
    > SignalR. Sample NuGet paketini yükleme, *Scripts* klasörünüzdeki jQuery sürümünü değiştirebilir. Paketin *SignalR. Sample* klasörüne yüklediği yeni *StockTicker. html* dosyası, paketin yüklediği jQuery sürümüyle eşitlenmiş olacaktır, ancak özgün *StockTicker. html* dosyanızı tekrar çalıştırmak Istiyorsanız, önce komut dosyası etiketinde jQuery başvurusunu güncelleştirmeniz gerekebilir.

### <a name="run-the-application"></a>Uygulamayı çalıştırma

 İlk uygulamada gördüğünüz tablo yararlı özelliklere sahipti. Tam hisse senedi oluşturma uygulaması yeni özellikleri gösterir: bir yatay kaydırma penceresi, renkleri arttığında ve düşecek şekilde değişen hisse senedi verilerini ve stokları gösterir.

1. Uygulamayı çalıştırmak için **F5** tuşuna basın.

     Uygulamayı ilk kez çalıştırdığınızda, "Pazar" "kapalı" olur ve kaydırılmayan bir statik tablo ve bir Ticker penceresi görürsünüz.

1. **Açık Pazar**' ı seçin.

    ![Canlı Ticker 'ın ekran görüntüsü.](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * **Canlı hisse senedi bandı** , yatay olarak kaydırmaya başlar ve sunucu düzenli olarak stok fiyatı değişikliklerini rastgele bir şekilde yayınlar.

    * Bir stok fiyatı her değiştiğinde uygulama hem **canlı hisse senedi tablosunu** hem de **canlı hisse senedi bandı**' ni güncelleştirir.

    * Bir hisse senedinin fiyat değişikliği pozitif olduğunda, uygulama stoku yeşil bir arka plana gösterir.

    * Değişiklik negatifse, uygulama, stoku kırmızı bir arka plana gösterir.

1. **Pazara kapat**' ı seçin.

    * Tablo güncelleştirmeleri durdu.

    * Ticker, kaydırmayı durduruyor.

1. **Sıfırla**' yı seçin.

    * Tüm hisse senedi verileri sıfırlanır.

    * Uygulama, Fiyat değişikliklerinin başlatılmasından önce ilk durumu geri yükler.

1. Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.

1. Aynı verileri her bir tarayıcıda dinamik olarak güncelleştirilmiş şekilde görürsünüz.

1. Denetimlerden herhangi birini seçtiğinizde, tüm tarayıcılar aynı anda aynı şekilde yanıt verir.

### <a name="live-stock-ticker-display"></a>Canlı hisse şeridi görüntüleme

**Canlı hisse senedi bandı** EKRANı, CSS stilleriyle tek bir satırda biçimlendirilen bir `<div>` öğesinde sıralanmamış bir listesidir. Uygulama başlatılır ve Ticker 'ı tabloyla aynı şekilde güncelleştirir: bir `<li>` şablon dizesindeki yer tutucuları değiştirerek ve `<li>` öğelerini `<ul>` öğesine dinamik olarak ekleme. Uygulama, `<div>`içinde sıralanmamış listenin sol kenar boşluğunu değiştirmek için jQuery `animate` işlevini kullanarak kaydırma içerir.

#### <a name="signalrsample-stocktickerhtml"></a>SignalR. Sample StockTicker. html

Stock Ticker HTML kodu:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR. Sample StockTicker. css

Hisse senedi bandı CSS kodu:

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR. örnek SignalR. StockTicker. js

Kaydırma yapan jQuery kodu:

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Sunucuda istemcinin çağıra, ek Yöntemler

Uygulamaya esneklik eklemek için, uygulamanın çağırabilmesine ek yöntemler vardır.

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR. Sample StockTickerHub.cs

`StockTickerHub` sınıfı, istemcinin çağırabileceğini dört ek yöntemi tanımlar:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

Uygulama, sayfanın üst kısmındaki düğmelere yanıt olarak `OpenMarket`, `CloseMarket`ve `Reset` çağırır. Tüm istemcilere anında yayılmış durumdaki bir değişikliği tetikleyen bir istemcinin modelini gösterir. Bu yöntemlerin her biri, piyasa durumunun değişmesine neden olan `StockTicker` sınıfında bir yöntemi çağırır ve sonra yeni durumu yayınlar.

#### <a name="signalrsample-stocktickercs"></a>SignalR. Sample StockTicker.cs

`StockTicker` sınıfında, uygulama, bir `MarketState` Enum değeri döndüren bir `MarketState` özelliği ile Pazar durumunu korur:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

`StockTicker` sınıfın iş parçacığı açısından güvenli olması gerektiğinden, Pazar durumunu değiştiren yöntemlerin her biri bir kilit bloğunun içinde olur:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

Bu kodun iş parçacığı açısından güvenli olduğundan emin olmak için, `volatile`belirtilen `MarketState` özelliğini yedekleyen `_marketState` alanı:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange` ve `BroadcastMarketReset` yöntemleri, zaten gördüğünüz BroadcastStockPrice yöntemine benzerdir, ancak istemcide tanımlı farklı Yöntemler çağırır:

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>İstemcinin çağıra, istemci üzerinde ek işlevler

`updateStockPrice` işlevi artık hem tabloyu hem de Ticker görüntüsünü işler ve kırmızı ve yeşil renkleri Flash 'ta `jQuery.Color` kullanır.

*SignalR. StockTicker. js* ' deki yeni işlevler, Pazar durumuna göre düğmeleri etkinleştirir ve devre dışı bırakır. Ayrıca **canlı hisse senedi bandı** yatay kaydırmayı da durdurur veya başlatır. `ticker.client`çok sayıda işlev eklendiğinden, uygulama bunları eklemek için [jQuery genişletme işlevini](http://api.jquery.com/jQuery.extend/) kullanır.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Bağlantı kurulduktan sonra ek istemci kurulumu

İstemci bağlantıyı belirledikten sonra, yapılacak bazı ek işler de vardır:

* Uygun `marketOpened` veya `marketClosed` işlevini çağırmak için pazara açık veya kapalı olup olmadığını öğrenin.

* Düğmelerine sunucu yöntemi çağrılarını ekleyin.

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

Sunucu yöntemleri, uygulama bağlantıyı yapana kadar düğmelere bağlı değildir. Bu, kodun kullanılabilir hale gelmeden önce sunucu yöntemlerine çağrı yapamıyor.

## <a name="additional-resources"></a>Ek kaynaklar

Bu öğreticide, sunucudan bağlı olan tüm istemcilere ileti veren bir SignalR uygulamasını nasıl programlayabilirsiniz. Artık iletileri düzenli aralıklarla ve herhangi bir istemciden gelen bildirimlere yanıt olarak yayınlayabilirsiniz. Çoklu iş parçacıklı tekil örnek kavramını kullanarak, çok oyunculu çevrimiçi oyun senaryolarında sunucu durumunu koruyabilirsiniz. Bir örnek için bkz. [SignalR tabanlı ShootR oyunu](https://github.com/NTaylorMullen/ShootR).

Eşler arası iletişim senaryolarını gösteren öğreticiler için bkz. [SignalR Ile çalışmaya](introduction-to-signalr.md) başlama ve [SignalR Ile gerçek zamanlı güncelleştirme](tutorial-high-frequency-realtime-with-signalr.md).

SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [ASP.NET SignalR](../../index.md)
* [SignalR projesi](http://signalr.net/)
* [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)
* [SignalR wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Proje oluşturuldu
> * Sunucu kodunu ayarlama
> * Sunucu kodu incelendi
> * İstemci kodunu ayarlama
> * İstemci kodu incelendi
> * Uygulamayı test etme
> * Etkin günlük kaydı

ASP.NET SignalR 2 kullanan gerçek zamanlı bir Web uygulamasının nasıl oluşturulacağını öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [SignalR ile gerçek zamanlı web uygulaması oluşturma](real-time-web-applications-with-signalr.md)
