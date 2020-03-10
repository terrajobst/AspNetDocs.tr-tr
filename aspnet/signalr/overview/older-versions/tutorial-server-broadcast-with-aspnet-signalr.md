---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 'Öğretici: ASP.NET SignalR 1. x ile sunucu yayını | Microsoft Docs'
author: bradygaster
description: Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Sunucu yayını, communic...
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579410"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>Öğretici: ASP.NET SignalR 1x ile Sunucu Yayını

by [Patrick Fletu](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu öğreticide, sunucu yayını işlevselliği sağlamak için ASP.NET SignalR kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Sunucu yayını, istemcilere gönderilen iletişimin sunucu tarafından başlatılmasıdır. Bu senaryo, istemcilere gönderilen iletişimin bir veya daha fazla istemciden başlatıldığı sohbet uygulamaları gibi eşler arası senaryolardan farklı bir programlama yaklaşımı gerektirir.
> 
> Bu öğreticide oluşturacağınız uygulama, sunucu yayını işlevselliği için tipik bir senaryo olan bir stok Ticker benzetimini yapar.
> 
> Öğreticideki yorumlara hoş geldiniz. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com)'e gönderebilirsiniz.

## <a name="overview"></a>Genel bakış

[Microsoft. Aspnet. SignalR. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet paketi, bir Visual Studio projesinde örnek bir sanal stok şeridi uygulaması yüklüyor. Bu öğreticinin ilk bölümünde, bu uygulamanın basitleştirilmiş bir sürümünü sıfırdan oluşturacaksınız. Öğreticinin geri kalanında NuGet paketini yükleyecek ve oluşturduğu ek özellikleri ve kodu gözden geçireceğiz.

Hisse senedi bandı uygulaması, düzenli aralıklarla sunucudan tüm bağlı istemcilere "göndermek" veya yayımlamak istediğiniz bir tür gerçek zamanlı uygulamanın temsilcisidir.

Bu öğreticinin ilk bölümünde oluşturacağınız uygulama, hisse senedi verileri içeren bir kılavuz görüntüler.

![StockTicker ilk sürümü](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

Düzenli aralıklarla sunucu, stok fiyatlarını rastgele güncelleştirir ve güncelleştirmeleri tüm bağlı istemcilere iter. Tarayıcıda, **değişiklik** ve **%** sütunlarında bulunan sayılar ve semboller, sunucudan gelen bildirimlere yanıt olarak dinamik olarak değişir. Aynı URL 'ye ek tarayıcılar açarsanız, hepsi aynı verileri ve verilerde aynı değişiklikleri aynı anda gösterir.

Bu öğretici aşağıdaki bölümleri içerir:

- [Önkoşullar](#prerequisites)
- [Projeyi oluşturma](#createproject)
- [SignalR NuGet paketlerini ekleyin](#nugetpackages)
- [Sunucu kodunu ayarlama](#server)
- [İstemci kodunu ayarlama](#client)
- [Uygulamayı test etme](#test)
- [Günlüğü etkinleştirme](#enablelogging)
- [Tam StockTicker örneğini yükleyip gözden geçirin](#fullsample)
- [Sonraki adımlar](#nextsteps)

> [!NOTE]
> Uygulamayı oluşturma adımları boyunca çalışmak istemiyorsanız, SignalR. Sample paketini yeni bir **boş ASP.NET Web uygulaması** projesine yükleyebilir ve kodun açıklamalarını almak için bu adımları okuyabilirsiniz. Öğreticinin ilk bölümü, SignalR. Sample kodunun bir alt kümesini kapsamakta ve ikinci bölüm SignalR. Sample paketindeki ek işlevlerin temel özelliklerini açıklar.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Önkoşullar

Başlamadan önce, bilgisayarınızda Visual Studio 2012 veya 2010 SP1 yüklü olduğundan emin olun. Visual Studio yoksa, Web için ücretsiz Visual Studio 2012 Express 'i almak için bkz. [ASP.net İndirmeleri](https://www.asp.net/downloads) .

Visual Studio 2010 kullanıyorsanız, [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 'in yüklü olduğundan emin olun.

<a id="createproject"></a>

## <a name="create-the-project"></a>Projeyi oluşturma

1. **Dosya** menüsünde **Yeni proje**' ye tıklayın.
2. **Yeni proje** Iletişim kutusunda Şablonlar ' ı genişletin **C#** ve **Web**' i seçin.
3. **ASP.net boş Web uygulaması** şablonunu seçin, proje *SignalR. StockTicker*olarak adlandırın ve **Tamam**' a tıklayın.

    ![Yeni Proje iletişim kutusu](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>SignalR NuGet paketlerini ekleyin

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>SignalR ve JQuery NuGet paketlerini ekleyin

Bir NuGet paketi yükleyerek bir projeye SignalR işlevi ekleyebilirsiniz.

1. Araçlar 'ı tıklatın **| NuGet Paket Yöneticisi | Paket Yöneticisi konsolu**.
2. Paket Yöneticisi 'nde aşağıdaki komutu girin.

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    SignalR paketi, birkaç farklı NuGet paketini bağımlılıklar olarak yüklüyor. Yükleme tamamlandığında, bir ASP.NET uygulamasında SignalR 'yi kullanmak için gereken tüm sunucu ve istemci bileşenlerine sahip olursunuz.

<a id="server"></a>

## <a name="set-up-the-server-code"></a>Sunucu kodunu ayarlama

Bu bölümde, sunucuda çalışan kodu ayarlarsınız.

### <a name="create-the-stock-class"></a>Hisse senedi sınıfını oluşturma

Bir hisse senedi hakkındaki bilgileri depolamak ve aktarmak için kullanacağınız stok modeli sınıfını oluşturarak başlarsınız.

1. Proje klasöründe yeni bir sınıf dosyası oluşturun, *Stock.cs*olarak adlandırın ve ardından şablon kodunu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    Hisse senetleri oluştururken ayarlayacağımız iki özellik simgedir (örneğin, Microsoft için MSFT) ve fiyat. Diğer özellikler, fiyatı nasıl ve ne zaman ayarlayadiğinize bağlıdır. Fiyatı ilk kez ayarladığınızda, değer, Bayopen 'ya yayılır. Fiyatı ayarladığınızda, Change ve PercentChange özellik değerleri, Price ve kıyopen arasındaki farka göre hesaplanır.

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>StockTicker ve StockTickerHub sınıfları oluşturma

Sunucudan istemciye etkileşimi işlemek için SignalR hub API 'sini kullanırsınız. SignalR hub sınıfından türetilen bir StockTickerHub sınıfı, istemcilerden gelen bağlantıları ve Yöntem çağrılarını almayı işleymeyecektir. Ayrıca, istemci bağlantılarından bağımsız olarak fiyat güncelleştirmelerini düzenli olarak tetiklemek için stok verilerini korumanız ve bir Zamanlayıcı nesnesi çalıştırmanız gerekir. Hub örnekleri geçici olduğundan bu işlevleri bir hub sınıfına koyamazsınız. Hub üzerindeki her işlem için, istemciden sunucuya bağlantılar ve çağrılar gibi bir hub sınıfı örneği oluşturulur. Bu nedenle, stok verilerini tutan, fiyatları güncelleştiren ve fiyat güncelleştirmelerinin yayınlaması gereken mekanizmanın ayrı bir sınıfta çalışması gerekir, bu da StockTicker olarak adlandırın.

![StockTicker 'den yayımlama](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

Yalnızca bir StockTicker sınıfının bir örneğinin sunucuda çalıştırılmasını istiyorsunuz, bu nedenle her bir StockTickerHub örneğinden Singleton StockTicker örneğine bir başvuru ayarlamanız gerekir. StockTicker sınıfı, stok verilerini ve Tetikleyiciler güncelleştirmelerini içerdiğinden, ancak StockTicker bir hub sınıfı olmadığından istemcilere yayınlayamaz. Bu nedenle, StockTicker sınıfının SignalR hub bağlantı bağlamı nesnesine bir başvuru alması gerekir. Daha sonra, istemcilere yayımlamak için SignalR bağlantı bağlamı nesnesini kullanabilir.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **Yeni öğe Ekle**' ye tıklayın.
2. [ASP.NET and Web Tools 2012,2 güncelleştirmesiyle](https://go.microsoft.com/fwlink/?LinkId=279941)Visual Studio 2012 varsa,  **C# Visual** altında **Web** ' e tıklayın ve **SignalR hub sınıfı** öğe şablonunu seçin. Aksi takdirde, **sınıf** şablonunu seçin.
3. Yeni sınıfı *StockTickerHub.cs*olarak adlandırın ve ardından **Ekle**' ye tıklayın.

    ![StockTickerHub.cs Ekle](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. Şablon kodunu aşağıdaki kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    [Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx) sınıfı, istemcilerin sunucuda çağırabilirler yöntemleri tanımlamak için kullanılır. Bir yöntem tanımlanıyor: `GetAllStocks()`. Bir istemci sunucuya ilk kez bağlandığında, geçerli fiyatlarına sahip tüm hisse senetleri listesini almak için bu yöntemi çağırır. Yöntem zaman uyumlu olarak yürütebilir ve bellekten veri döndürdüğü için `IEnumerable<Stock>` döndürebilir. Bir veritabanı araması veya Web hizmeti çağrısı gibi, beklenerek, yöntemin verileri alması gerekiyorsa, zaman uyumsuz işlemeyi etkinleştirmek için dönüş değeri olarak `Task<IEnumerable<Stock>>` belirtmeniz gerekir. Daha fazla bilgi için bkz. [ASP.NET SignalR hub 'LARı API Kılavuzu-sunucu-zaman uyumsuz olarak yürütülecektir](index.md).

    HubName özniteliği, hub 'ın istemcideki JavaScript kodunda nasıl başvurduğunu belirtir. Bu özniteliği kullanmazsanız istemcideki varsayılan ad, sınıf adının bir Camel-cased sürümüdür ve bu durumda stockTickerHub olacaktır.

    Daha sonra StockTicker sınıfını oluştururken göreceğiniz gibi, bu sınıfın tek bir örneği statik örnek özelliğinde oluşturulur. Bu tek StockTicker örneği, kaç istemci bağlantı veya bağlantısı kesildiğine bakılmaksızın bellekte kalır ve bu örnek, geçerli stok bilgilerini döndürmek için Getallstock yönteminin kullandığı şeydir.
5. Proje klasöründe yeni bir sınıf dosyası oluşturun, *StockTicker.cs*olarak adlandırın ve ardından şablon kodunu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    Birden çok iş parçacığı aynı StockTicker Code örneğini çalıştırdığından, StockTicker sınıfının threadsafe olması gerekir.

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>Tek örneği statik bir alanda depolama

    Kod, örnek özelliğini bir sınıfının örneğiyle yedekleyen statik \_örneği alanını başlatır ve bu, Oluşturucu özel olarak işaretlendiğinden, oluşturulabilecek sınıfın tek örneğidir. [Yavaş başlatma](https://msdn.microsoft.com/library/dd997286.aspx) , performans nedenleriyle değil, örnek oluşturmanın threadsafe olduğundan emin olmak için \_örneği alanı için kullanılır.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    İstemci sunucuya her bağlanışında, ayrı bir iş parçacığında çalışan StockTickerHub sınıfının yeni bir örneği, StockTickerHub sınıfında daha önce gördüğünüz gibi StockTicker. Instance static özelliğinden StockTicker Singleton örneğini alır.

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>Bir ConcurrentDictionary içinde hisse senedi verilerini depolama

    Oluşturucu \_hisse senedi koleksiyonunu bazı örnek hisse senedi verileriyle başlatır ve Getallhisse senetleri, stokları geri döndürür. Daha önce gördüğünüz gibi, bu hisse senedi koleksiyonu, istemcilerin çağırabileceği hub sınıfında bir sunucu yöntemi olan StockTickerHub. Getallhisse öğeleri tarafından döndürülür.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    Hisse senetleri koleksiyonu, iş parçacığı güvenliği için bir [ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx) türü olarak tanımlanır. Alternatif olarak, bir [Sözlük](https://msdn.microsoft.com/library/xfhwa508.aspx) nesnesi kullanabilir ve üzerinde değişiklik yaptığınızda sözlüğü açıkça kilitleyemezsiniz.

    Bu örnek uygulama için, uygulama verilerini bellekte depolamak ve StockTicker örneği atıldığı zaman verileri kaybetmek Tamam ' dır. Gerçek bir uygulamada, veritabanı gibi bir arka uç veri deposuyla çalışırsınız.

    ### <a name="periodically-updating-stock-prices"></a>Stok fiyatlarını düzenli olarak güncelleştirme

    Oluşturucu, stok fiyatlarını rastgele olarak güncelleştiren yöntemleri düzenli aralıklarla çağıran bir Zamanlayıcı nesnesi başlatır.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices, durum parametresinde null değeri geçen Zamanlayıcı tarafından çağırılır. Fiyatları güncelleştirmeden önce \_updateStockPricesLock nesnesinde bir kilit alınır. Kod, başka bir iş parçacığının fiyatları zaten güncelleştirme olup olmadığını denetler ve ardından listedeki her bir stokta TryUpdateStockPrice öğesini çağırır. TryUpdateStockPrice yöntemi, stok fiyatının değiştirilip değişmeyeceğine ve ne kadarının değiştirileceğini belirler. Hisse senedi fiyatı değiştirilirse, stok fiyatı değişikliğini tüm bağlı istemcilere yayımlamak için BroadcastStockPrice çağırılır.

    \_updatingStockPrices bayrağı, erişimi threadsafe olduğundan emin olmak için [geçici](https://msdn.microsoft.com/library/x13ttww7.aspx) olarak işaretlenir.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    Gerçek bir uygulamada, TryUpdateStockPrice yöntemi fiyata bakmak için bir Web hizmeti çağırır; Bu kodda, değişiklikleri rastgele yapmak için rastgele bir sayı Oluşturucu kullanır.

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>StockTicker sınıfının istemcilere yayınlanabilmesi için SignalR bağlamı alma

    Fiyat değişiklikleri StockTicker nesnesinde yer aldığı için, bu, tüm bağlı istemcilerde bir updateStockPrice yöntemi çağırması gereken nesnedir. Bir hub sınıfında, istemci yöntemlerini çağırmak için bir API 'SI vardır, ancak StockTicker hub sınıfından türetilmez ve herhangi bir hub nesnesine bir başvuruya sahip değildir. Bu nedenle, bağlı istemcilere yayımlamak için StockTicker sınıfının, StockTickerHub sınıfı için SignalR bağlam örneğini alması ve istemciler üzerinde yöntemleri çağırmak için bunu kullanması gerekir.

    Kod, tek sınıf örneğini oluşturduğunda SignalR bağlamına bir başvuru alır, bu başvuruyu oluşturucuya geçirir ve Oluşturucu bunu Istemciler özelliğine koyar.

    Bağlamı tek bir kez almak istemeniz gereken iki neden vardır: bağlamı almak pahalı bir işlemdir ve bu işlemin bir kez alınması, istemcilere gönderilen iletilerin amaçlanan sırasının korunmasını sağlar.

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    İçeriğin Istemciler özelliğinin alınması ve StockTickerClient özelliğine yerleştirilmesi, bir hub sınıfında olduğu gibi görünen istemci yöntemlerini çağırmak için kod yazmanıza olanak tanır. Örneğin, tüm istemcilere yayımlamak için, Istemcileri yazabilirsiniz. ALL. updateStockPrice (hisse senedi).

    BroadcastStockPrice içinde aradığınız updateStockPrice yöntemi henüz yok; daha sonra, istemcide çalışan bir kod yazdığınızda eklersiniz. UpdateStockPrice adresine başvurabilirsiniz çünkü Istemciler. All dinamik olduğundan, ifade çalışma zamanında değerlendirilecek anlamına gelir. Bu yöntem çağrısı yürütüldüğünde, SignalR yöntem adını ve parametre değerini istemciye gönderir ve istemcinin updateStockPrice adlı bir yöntemi varsa, bu yöntem çağrılır ve parametre değeri bu değere geçirilir.

    İstemcileri. All tüm istemcilere gönder anlamına gelir. SignalR, hangi istemcileri veya istemci gruplarını gönderileceğini belirtmek için size diğer seçenekler sağlar. Daha fazla bilgi için bkz. [Hubconnectioncontext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx).

### <a name="register-the-signalr-route"></a>SignalR rotasını kaydetme

Sunucunun hangi URL 'yi ele geçirip SignalR 'ye yönlendireceğimizi bilmeleri gerekir. Bunu yapmak için *Global. asax* dosyasına bazı kodlar ekleyeceksiniz.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve ardından **Yeni öğe Ekle**' ye tıklayın.
2. **Genel uygulama sınıfı** öğe şablonunu seçin ve ardından **Ekle**' ye tıklayın.

    ![Global. asax Ekle](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. SignalR yol kayıt kodunu uygulama\_başlangıç yöntemine ekleyin:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    Varsayılan olarak, tüm SignalR trafiği için temel URL "/SignalR" ve "/SignalR/Hub", uygulamanızda sahip olduğunuz tüm Hub 'Lara yönelik proxy 'leri tanımlayan dinamik olarak oluşturulmuş bir JavaScript dosyası almak için kullanılır. MapHubs yöntemi, [Hubconfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx) sınıfının bir örneğinde farklı bır temel URL ve belirli bir SignalR seçeneği belirtmenize olanak tanıyan aşırı yüklemeleri içerir.
4. Dosyanın üst kısmına bir using ifadesini ekleyin:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. *Global. asax* dosyasını kaydedip kapatın ve projeyi derleyin.

Artık sunucu kodunu ayarlamayı tamamladınız. Sonraki bölümde, istemcisini ayarlayacaksınız.

<a id="client"></a>

## <a name="set-up-the-client-code"></a>İstemci kodunu ayarlama

1. Proje klasöründe yeni bir HTML dosyası oluşturun ve *StockTicker. html*olarak adlandırın.
2. Şablon kodunu aşağıdaki kodla değiştirin:

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    HTML, 5 sütun, başlık satırı ve tüm 5 sütuna yayılan tek hücreli bir veri satırı içeren bir tablo oluşturur. Veri satırında "yükleniyor..." görüntülenir ve yalnızca uygulama başlatıldığında anlık olarak gösterilir. JavaScript kodu, bu satırı kaldırır ve kendi yerleştirme satırlarına sunucudan alınan stok verilerini ekler.

    Komut dosyası etiketleri, jQuery betik dosyası, SignalR Core betik dosyası, SignalR proxy 'leri betik dosyası ve daha sonra oluşturacağınız bir StockTicker betik dosyası belirtir. "/SignalR/hub 'ları" URL 'sini belirten SignalR proxy 'leri betik dosyası dinamik olarak oluşturulur ve bu örnekte StockTickerHub. Getallhisse malarındaki yöntemler için proxy yöntemlerini tanımlar. İsterseniz, bu JavaScript dosyasını [SignalR yardımcı programlarını](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) kullanarak el ile oluşturabilir ve MapHubs Yöntem çağrısında dinamik dosya oluşturmayı devre dışı bırakabilirsiniz.
3. > [!IMPORTANT]
   > *StockTicker. html* içindeki JavaScript dosyası başvurularının doğru olduğundan emin olun. Diğer bir deyişle, komut dosyası etiketinizdeki jQuery sürümünün (örnekteki 1.8.2) projenizin *betikler* klasöründeki jQuery sürümü ile aynı olduğundan emin olun ve betik etiketinizdeki SignalR sürümünün projenizin *betikler* klasöründeki SignalR sürümü ile aynı olduğundan emin olun. Gerekirse, komut dosyası etiketlerindeki dosya adlarını değiştirin.
4. **Çözüm Gezgini**' de, *StockTicker. html*' ye sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' ya tıklayın.
5. Proje klasöründe yeni bir JavaScript dosyası oluşturun ve *StockTicker. js*olarak adlandırın.
6. Şablon kodunu aşağıdaki kodla değiştirin:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $. Connection, SignalR proxy 'leri anlamına gelir. Kod, StockTickerHub sınıfı için proxy 'ye bir başvuru alır ve bunu Ticker değişkenine koyar. Proxy adı [HubName] özniteliği tarafından ayarlanan addır:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    Tüm değişkenler ve işlevler tanımlandıktan sonra, dosyadaki kodun son satırı, SignalR start işlevini çağırarak SignalR bağlantısını başlatır. Start işlevi zaman uyumsuz olarak yürütülür ve bir [jQuery ertelenmiş nesnesi](http://api.jquery.com/category/deferred-object/)döndürür; bu, zaman uyumsuz işlem tamamlandığında çağrılacak işlevi belirtmek için Done işlevini çağırabilmeniz anlamına gelir.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    İnit işlevi sunucudaki Getallstock işlevini çağırır ve sunucunun stok tablosunu güncelleştirmek için döndürdüğü bilgileri kullanır. Varsayılan olarak, yöntem adı sunucuda Pascal-cased olmasına rağmen, istemci üzerinde ortası büyük harfleri kullanmanız gerektiğini unutmayın. Camel-büyük harf kuralı, nesneler için değil yalnızca metotlar için geçerlidir. Örneğin, stoğa başvurursunuz. Sembol ve hisse senedi. Fiyat, stok. sembol veya hisse senedi. fiyat.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    İstemcide Pascal büyük/küçük harf kullanmak istiyorsanız veya tamamen farklı bir yöntem adı kullanmak istiyorsanız, hub metodunu HubName özniteliğiyle birlikte yönettiğiniz şekilde, HubMethodName özniteliğiyle birlikte süslemek isteyebilirsiniz.

    İnit yönteminde, bir tablo satırı için HTML, stok nesnesinin özelliklerini biçimlendirmek üzere formatStock çağırarak ve sonra rowTemplate değişkeninde yer tutucuları ( *StockTicker. js*' nin üst kısmında tanımlanır) çağırarak, stok nesne özelliği değerleriyle birlikte RowTemplate değişkeninde bulunan her bir stok nesnesi için oluşturulur. Elde edilen HTML daha sonra hisse senedi tablosuna eklenir.

    Başlatma işlemini, zaman uyumsuz başlatma işlevi tamamlandıktan sonra yürütülen bir geri çağırma işlevi olarak geçirerek çağırın. Start çağrıldıktan sonra ayrı bir JavaScript ekstresi olarak init olarak çağrılırsa, başlatma işlevinin bağlantıyı kurmayı bitirmesini beklemeden hemen yürütülemediğinden işlev başarısız olur. Bu durumda, init işlevi sunucu bağlantısı oluşturulmadan önce Getallhisse senedi işlevini çağırmaya çalışır.

    Sunucu bir hisse senedi fiyatını değiştirdiğinde, bağlı istemcilerde updateStockPrice çağırır. İşlevi, stockTicker proxy 'sinin istemci özelliğine, sunucudan gelen çağrılar için kullanılabilir hale getirmek için eklenir.

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    UpdateStockPrice işlevi, sunucudan alınan bir hisse senedi nesnesini, init işleviyle aynı şekilde bir tablo satırına biçimlendirir. Ancak, satırı tabloya eklemek yerine, tablodaki geçerli satırını bulur ve bu satırı yeni bir satır ile değiştirir.

<a id="test"></a>

## <a name="test-the-application"></a>Uygulamayı test etme

1. Uygulamayı hata ayıklama modunda çalıştırmak için F5 tuşuna basın.

    Hisse senedi tablosu başlangıçta "yükleniyor..." satırı, ardından ilk stok verileri görüntülenirken kısa bir gecikmeden sonra Stok fiyatları değişmeden başlar.

    ![Yükleniyor](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![İlk stok tablosu](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![Sunucudan değişiklikleri alan stok tablosu](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. Tarayıcı adres çubuğundan URL 'YI kopyalayın ve bir veya daha fazla yeni tarayıcı penceresine yapıştırın.

    İlk stok görüntüsü ilk tarayıcıyla aynıdır ve değişiklikler aynı anda gerçekleşir.
3. Tüm tarayıcıları kapatın ve yeni bir tarayıcı açın ve ardından aynı URL 'ye gidin.

    StockTicker Singleton nesnesi sunucuda çalışmaya devam etti, bu nedenle hisse senedi tablosu görünümü hisse senedinin değişmeye devam ediyor olduğunu gösterir. (İlk tabloyu sıfır değişiklik rakamlarını görmezsiniz.)
4. Tarayıcıyı kapatın.

<a id="enablelogging"></a>

## <a name="enable-logging"></a>Günlüğü etkinleştirme

SignalR 'de, sorun gidermeye yardımcı olmak için istemcisinde etkinleştirebilmeniz gereken yerleşik bir günlüğe kaydetme işlevi vardır. Bu bölümde, günlüğe kaydetmeyi etkinleştirir ve günlüklerin, SignalR aşağıdaki taşıma yöntemlerinden hangisini kullandığını nasıl söyletiğini gösteren örneklere bakabilirsiniz:

- [WebSockets](http://en.wikipedia.org/wiki/WebSocket), IIS 8 ve geçerli tarayıcılar tarafından desteklenir.
- Internet Explorer dışındaki tarayıcılar tarafından desteklenen [sunucu tarafından gönderilen olaylar](http://en.wikipedia.org/wiki/Server-sent_events).
- Internet Explorer tarafından desteklenen [süresiz çerçeve](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe).
- Tüm tarayıcılar tarafından desteklenen [Ajax uzun yoklama](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling).

Verilen herhangi bir bağlantı için, SignalR hem sunucu hem de istemci tarafından desteklenen en iyi taşıma yöntemini seçer.

1. *StockTicker. js* dosyasını açın ve dosyanın sonunda bağlantıyı başlatan koddan hemen önce günlüğe kaydetmeyi etkinleştirmek için bir kod satırı ekleyin:

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. Projeyi çalıştırmak için F5 tuşuna basın.
3. Tarayıcınızın geliştirici araçları penceresini açın ve günlükleri görmek için konsolu seçin. Yeni bir bağlantı için taşıma yöntemiyle ilgili olarak, SignalR 'nin işlem için anlaşmasının günlüklerini görmek üzere sayfayı yenilemeniz gerekebilir.

    Windows 8 (IIS 8) üzerinde Internet Explorer 10 çalıştırıyorsanız, aktarım yöntemi WebSockets olur.

    ![IE 10 IIS 8 konsolu](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    Windows 7 ' de (IIS 7,5) Internet Explorer 10 çalıştırıyorsanız, taşıma yöntemi iframe 'dir.

    ![IE 10 konsolu, IIS 7,5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    Firefox 'ta, bir konsol penceresi almak için Firebug eklentisini yüklersiniz. Windows 8 (IIS 8) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi WebSockets olur.

    ![Firefox 19 IIS 8 WebSockets](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    Windows 7 (IIS 7,5) üzerinde Firefox 19 çalıştırıyorsanız, aktarım yöntemi sunucu tarafından gönderilen olaylardır.

    ![Firefox 19 IIS 7,5 konsolu](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>Tam StockTicker örneğini yükleyip gözden geçirin

[Microsoft. Aspnet. SignalR. Sample](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet paketi tarafından yüklenen StockTicker uygulaması, sıfırdan yeni oluşturduğunuz Basitleştirilmiş sürümden daha fazla özellik içerir. Öğreticinin bu bölümünde, NuGet paketini yükler ve yeni özellikleri ve bunları uygulayan kodu gözden geçirin.

### <a name="install-the-signalrsample-nuget-package"></a>SignalR. Sample NuGet paketini yükler

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **NuGet Paketlerini Yönet**' e tıklayın.
2. **NuGet Paketlerini Yönet** Iletişim kutusunda **çevrimiçi**' e tıklayın, **çevrimiçi ara** kutusuna *SignalR. Sample* girin ve ardından **SignalR. Sample** paketinde **Install (Kur** ) seçeneğine tıklayın.

    ![SignalR. Sample paketini yükler](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. *Global. asax* dosyasında, RouteTable. Routes. MapHubs (); öğesini açıklama olarak inceleyin. daha önce uygulama\_başlangıç yöntemine eklediğiniz satır.

    SignalR. Sample paketi, SignalR yolunu *App\_start/Registerhub. cs* dosyasına kaydettiği için *Global. asax* dosyasındaki koda artık gerek duyulmaz:

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    Derleme özniteliği tarafından başvurulan WebActivator sınıfı, SignalR. Sample paketinin bir bağımlılığı olarak yüklenen WebActivatorEx NuGet paketine dahildir.
4. **Çözüm Gezgini**, SignalR. Sample paketini yükleyerek oluşturulan *SignalR. Sample* klasörünü genişletin.
5. *SignalR. Sample* klasöründe, *StockTicker. html*' ye sağ tıklayın ve ardından **Başlangıç sayfası olarak ayarla**' ya tıklayın.

    > [!NOTE]
    > SignalR. Sample NuGet paketini yükleme, *Scripts* klasörünüzdeki jQuery sürümünü değiştirebilir. Paketin *SignalR. Sample* klasörüne yüklediği yeni *StockTicker. html* dosyası, paketin yüklediği jQuery sürümüyle eşitlenmiş olacaktır, ancak özgün *StockTicker. html* dosyanızı tekrar çalıştırmak Istiyorsanız, önce komut dosyası etiketinde jQuery başvurusunu güncelleştirmeniz gerekebilir.

### <a name="run-the-application"></a>Uygulamayı çalıştırma

1. Uygulamayı çalıştırmak için F5'e basın.

    Daha önce gördüğünüz kılavuza ek olarak, tam hisse senedi şeridi uygulaması aynı stok verilerini görüntüleyen yatay bir kaydırma penceresi gösterir. Uygulamayı ilk kez çalıştırdığınızda, "Pazar" "kapalı" olur ve bir statik kılavuz ve kaydırılmayan bir Ticker penceresi görürsünüz.

    ![StockTicker ekranı Başlat](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    **Pazara aç**' a tıkladığınızda, **canlı stok bandı** kutusu yatay olarak kaydırmaya başlar ve sunucu düzenli olarak stok fiyatı değişikliklerini rastgele bir şekilde yayınlar. Bir stok fiyatı her değiştiğinde, hem **canlı stok tablosu** Kılavuzu hem de **canlı hisse senedi bandı** kutusu güncelleştirilir. Bir hisse senedinin fiyat değişikliği pozitif olduğunda, stok yeşil bir arka plan ile gösterilir ve değişiklik negatif olduğunda, stok kırmızı bir arka plan ile gösterilir.

    ![StockTicker uygulaması, Pazar açık](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    **Pazara kapat** düğmesi değişiklikleri durduruyor ve Ticker kaydırmasını durduruyor ve **Sıfırla** düğmesi, fiyat değişiklikleri başlatılmadan önce tüm stok verilerini ilk duruma sıfırlar. Daha fazla tarayıcı penceresi açıp aynı URL 'ye giderseniz, her tarayıcıda aynı anda aynı verilerin dinamik olarak güncelleştirildiğini görürsünüz. Düğmelerden birine tıkladığınızda, tüm tarayıcılar aynı anda aynı şekilde yanıt verir.

### <a name="live-stock-ticker-display"></a>Canlı hisse şeridi görüntüleme

**Canlı hisse senedi bandı** EKRANı, CSS stilleriyle tek bir satıra biçimlendirilen bir div öğesinde sıralanmamış bir listesidir. Ticker başlatılır ve tabloyla aynı şekilde güncelleştirilir: &lt;li&gt; şablon dizesindeki yer tutucuları değiştirerek ve &lt;li&gt; öğelerini &lt;ul&gt; öğesine dinamik olarak ekleme. Kaydırma, div içindeki sıralanmamış listenin sol kenar boşluğunu değiştirmek için jQuery canlandır işlevi kullanılarak gerçekleştirilir.

Stock Ticker HTML:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

Hisse şeridi için CSS:

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

Kaydırma yapan jQuery kodu:

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>Sunucuda istemcinin çağıra, ek Yöntemler

StockTickerHub sınıfı, istemcinin çağırabileceğini dört ek yöntem tanımlar:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

OpenMarket, CloseMarket ve Reset, sayfanın en üstündeki düğmelere yanıt olarak çağırılır. Tek bir istemcinin, tüm istemcilere anında yayılmış durumdaki bir değişikliği tetikleyen bir istemcinin modelini gösterir. Bu yöntemlerin her biri, StockTicker sınıfındaki Pazar durumu değişikliğini etkileyen bir yöntemi çağırır ve sonra yeni durumu yayınlar.

StockTicker sınıfında, Pazar durumu bir Pazar durum numaralandırması değeri döndüren bir pazar durumu özelliği tarafından korunur:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

StockTicker sınıfının threadsafe olması gerektiğinden, Pazar durumunu değiştiren yöntemlerin her biri bir kilit bloğunun içinde olur:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

Bu kodun threadsafe olduğundan emin olmak için, MarketState özelliğini yedekleyen \_Pazar durumu alanı geçici olarak işaretlenir,

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

Yayınmarkette ve Yayınmarketi sıfırlama yöntemleri, zaten gördüğünüz BroadcastStockPrice yöntemine benzerdir, ancak istemcide tanımlı farklı Yöntemler çağırır:

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>İstemcinin çağıra, istemci üzerinde ek işlevler

UpdateStockPrice işlevi artık hem kılavuz hem de Ticker görüntüsünü işler ve kırmızı ve yeşil renkleri Flash için jQuery. Color kullanır.

*SignalR. StockTicker. js* ' deki yeni işlevler, Pazar durumuna göre düğmeleri etkinleştirir ve devre dışı bırakır ve Ticker pencere yatay kaydırmasını durdurur veya başlatır. Ticker. Client 'a birden çok işlev eklendiğinden, bu nesneleri eklemek için [jQuery genişletme işlevi](http://api.jquery.com/jQuery.extend/) kullanılır.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>Bağlantı kurulduktan sonra ek istemci kurulumu

İstemci bağlantıyı kurduktan sonra, başka bir iş yapması gerekir: uygun menkul değer veya pazar kapalı işlevini çağırmak için pazara açık veya kapalı olup olmadığını öğrenin ve sunucu yöntemi çağrılarını düğmelere ekleyin.

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

Sunucu yöntemleri, bağlantı kurulana kadar düğmelere bağlı değildir, böylece kod kullanılabilir olmadan önce sunucu yöntemlerini çağırmaya deneyemez.

<a id="nextsteps"></a>

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, sunucudan iletileri yayınlayan bir SignalR uygulamasının her ikisi de düzenli aralıklarla ve herhangi bir istemciden gelen bildirimlere yanıt olarak nasıl çalıştığını öğrendiniz. Sunucu durumunu korumak için çok iş parçacıklı tekil örnek kullanmanın bir deseninin aynı zamanda çok oyunculu çevrimiçi oyun senaryolarında de kullanılabilir. Bir örnek için bkz. [SignalR 'yi temel alan ShootR oyunu](https://github.com/NTaylorMullen/ShootR).

Eşler arası iletişim senaryolarını gösteren öğreticiler için bkz. [SignalR Ile çalışmaya](index.md) başlama ve [SignalR Ile gerçek zamanlı güncelleştirme](index.md).

Daha gelişmiş SignalR geliştirme kavramları hakkında daha fazla bilgi edinmek için, SignalR kaynak kodu ve kaynakları için aşağıdaki siteleri ziyaret edin:

- [ASP.NET SignalR](https://asp.net/signalr/)
- [SignalR projesi](http://signalr.net/)
- [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)
- [SignalR wiki](https://github.com/SignalR/SignalR/wiki)
