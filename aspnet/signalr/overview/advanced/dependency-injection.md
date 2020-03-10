---
uid: signalr/overview/advanced/dependency-injection
title: SignalR 'de bağımlılık ekleme | Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri hakkında bilgi Için bu konunun önceki sürümlerini Visual Studio 2013...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: a14121ae-02cf-4024-8af0-9dd0dc810690
msc.legacyurl: /signalr/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 52978b10b6c131ac8eff4535216cc60b43fdf3de
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537333"
---
# <a name="dependency-injection-in-signalr"></a>SignalR’da Bağımlılık Ekleme

, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a>Bu konuda kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR sürüm 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Bu konunun önceki sürümleri
>
> SignalR 'nin önceki sürümleri hakkında daha fazla bilgi için bkz. [SignalR daha eski sürümleri](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com/)'e gönderebilirsiniz.

Bağımlılık ekleme, nesneler arasında sabit kodlanmış bağımlılıkları kaldırmanın bir yoludur. bu sayede, bir nesnenin bağımlılıklarını test etmek için (sahte nesneleri kullanarak) veya çalışma zamanı davranışını değiştirmek kolaylaşır. Bu öğreticide, SignalR hub 'larda bağımlılık ekleme işlemlerinin nasıl gerçekleştirileceği gösterilmektedir. Ayrıca, SignalR ile IOC kapsayıcılarını nasıl kullanacağınızı gösterir. Bir IOC kapsayıcısı, bağımlılık ekleme için genel bir çerçevedir.

## <a name="what-is-dependency-injection"></a>Bağımlılık ekleme nedir?

Bağımlılık ekleme konusunda zaten bilgi sahibiyseniz bu bölümü atlayın.

*Bağımlılık ekleme* (dı), nesnelerin kendi bağımlılıklarını oluşturmadan sorumlu olmayan bir modeldir. İşte, bu, bir değer olarak motive etmek için basit bir örnektir. İletileri günlüğe kaydetmek için gereken bir nesneniz olduğunu varsayalım. Günlüğe kaydetme arabirimi tanımlayabilirsiniz:

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

Nesneniz, iletileri günlüğe kaydetmek için bir `ILogger` oluşturabilirsiniz:

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

Bu işe yarar, ancak en iyi tasarım değildir. `FileLogger` başka bir `ILogger` uygulamasıyla değiştirmek istiyorsanız `SomeComponent`değiştirmeniz gerekir. Birçok farklı nesnenin `FileLogger`kullanduymasını, bunların tümünü değiştirmeniz gerekir. Ya da tek bir `FileLogger` yapmaya karar verirseniz, uygulama genelinde de değişiklikler yapmanız gerekir.

Daha iyi bir yaklaşım, nesne içine bir `ILogger` eklemek — örneğin, bir Oluşturucu bağımsız değişkeni kullanarak:

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

Artık, hangi `ILogger` kullanacağınızı seçmeden nesne sorumlu değildir. Kendisine bağımlı nesneleri değiştirmeden `ILogger` uygulamaları geçebilirsiniz.

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

Bu düzene [Oluşturucu Ekleme](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection)adı verilir. Başka bir model, bir ayarlayıcı yöntemi veya özelliği aracılığıyla bağımlılığı ayarladığınız ayarlayıcı ekleme işlemi olur.

## <a name="simple-dependency-injection-in-signalr"></a>SignalR 'de basit bağımlılık ekleme

[SignalR Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr.md)başlama öğreticiden sohbet uygulamasını göz önünde bulundurun. Bu uygulamadaki Merkez sınıfı aşağıda verilmiştir:

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

Göndermeden önce sohbet iletilerini sunucuda depolamak istediğinizi varsayalım. Bu işlevi soyutlayan bir arabirim tanımlayabilir ve arabirimi `ChatHub` sınıfına eklemek için DI kullanabilirsiniz.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

Tek sorun, bir SignalR uygulamasının doğrudan hub oluşturmamalıdır; SignalR bunları sizin için oluşturur. Varsayılan olarak, SignalR bir hub sınıfının parametresiz bir oluşturucuya sahip olmasını bekler. Ancak, hub örnekleri oluşturmak için bir işlevi kolayca kaydedebilir ve bu işlevi, DI işlemini gerçekleştirmek için kullanabilirsiniz. **Globalhost. DependencyResolver. Register**çağırarak işlevi kaydedin.

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

Artık `ChatHub` bir örnek oluşturması gerektiğinde SignalR bu anonim işlevi çağıracaktır.

## <a name="ioc-containers"></a>IoC kapsayıcıları

Önceki kod, basit durumlar için uygundur. Ancak yine de şunu yazmanız gerekiyordu:

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

Birçok bağımlılığı olan karmaşık bir uygulamada, bu "kablolama" kodunun çoğunu yazmanız gerekebilir. Özellikle bağımlılıklar iç içe ise, bu kod bakımını yapmak zor olabilir. Ayrıca birim testi de zordur.

Bir çözüm bir IOC kapsayıcısı kullanmaktır. Bir IOC kapsayıcısı, bağımlılıkları yönetmekten sorumlu bir yazılım bileşenidir. Türleri kapsayıcıya kaydeder ve sonra nesneleri oluşturmak için kapsayıcıyı kullanın. Kapsayıcı, bağımlılık ilişkilerini otomatik olarak belirler. Birçok IOC kapsayıcısı ayrıca nesne ömrü ve kapsamı gibi şeyleri denetlemenize olanak tanır.

> [!NOTE]
> "IoC", bir çerçevenin uygulama koduna çağırdığı genel bir model olan "denetimin INVERSION" anlamına gelir. Bir IOC kapsayıcısı, nesnelerinizi sizin için oluşturur, bu da normal denetim akışını "tersine çevirir".

## <a name="using-ioc-containers-in-signalr"></a>SignalR 'de IOC kapsayıcıları kullanma

Sohbet uygulaması, bir IOC kapsayıcısından faydalanmak için büyük olasılıkla çok basittir. Bunun yerine [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) örneğine göz atalım.

StockTicker örneği iki ana sınıfı tanımlar:

- `StockTickerHub`: istemci bağlantılarını yöneten hub sınıfı.
- `StockTicker`: stok fiyatlarını tutan ve düzenli aralıklarla güncelleştiren bir tek.

`StockTickerHub`, `StockTicker` tekil öğesine bir başvuru tutar `StockTicker` ancak `StockTickerHub`için **IHV Ubconnectioncontext** 'e bir başvuru barındırır. `StockTickerHub` örneklerle iletişim kurmak için bu arabirimi kullanır. (Daha fazla bilgi için bkz. [ASP.NET SignalR Ile sunucu yayını](../getting-started/tutorial-server-broadcast-with-signalr.md).)

Bu bağımlılıklara bir bit eklemek için bir IOC kapsayıcısı kullanabiliriz. İlk olarak, `StockTickerHub` ve `StockTicker` sınıflarını basitleşelim. Aşağıdaki kodda, ihtiyaç duyduğumuz parçalar hakkında yorum yaptı.

Parametresiz oluşturucuyu `StockTickerHub`kaldırın. Bunun yerine, her zaman, hub 'ı oluşturmak için DI 'yi kullanacağız.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

StockTicker için Singleton örneğini kaldırın. Daha sonra, StockTicker ömrünü denetlemek için IoC kapsayıcısını kullanacağız. Ayrıca, oluşturucuyu genel hale getirin.

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

Daha sonra, `StockTicker`için bir arabirim oluşturarak kodu yeniden düzenleyebilirsiniz. Bu arabirimi, `StockTickerHub` `StockTicker` sınıfından ayırmak için kullanacağız.

Visual Studio bu tür yeniden düzenleme kolaylaştırır. StockTicker.cs dosyasını açın, `StockTicker` sınıfı bildirimine sağ tıklayın ve yeniden **Düzenle** ... seçeneğini belirleyin. **Arabirimi Ayıkla**.

![](dependency-injection/_static/image1.png)

**Arabirimi Ayıkla** Iletişim kutusunda **Tümünü Seç**' e tıklayın. Diğer varsayılan değerleri bırakın. **Tamam**’a tıklayın.

![](dependency-injection/_static/image2.png)

Visual Studio `IStockTicker`adlı yeni bir arabirim oluşturur ve ayrıca `IStockTicker`türetmeye `StockTicker` değişir.

IStockTicker.cs dosyasını açın ve arabirimi **genel**' e değiştirin.

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

`StockTickerHub` sınıfında, iki `StockTicker` örneğini `IStockTicker`olarak değiştirin:

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

`IStockTicker` arabirimi oluşturmak kesinlikle gerekli değildir, ancak uygulamanızın uygulamanızdaki bileşenler arasında Eşleneni azaltmaya nasıl yardımcı olduğunu göstermek istiyorum.

## <a name="add-the-ninject-library"></a>Nekleme kitaplığını ekleme

.NET için çok sayıda açık kaynaklı IFC kapsayıcısı vardır. Bu öğretici için [Nekleme](http://www.ninject.org/)'yi kullanacağız. (Diğer popüler kitaplıklar, [role](http://www.castleproject.org/) [Spring.net](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)ve [StructureMap](http://docs.structuremap.net)içerir.)

[Nekleme kitaplığını](https://nuget.org/packages/Ninject/3.0.1.10)yüklemek Için NuGet Paket Yöneticisi 'ni kullanın. Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>SignalR bağımlılık çözümleyicisini değiştirme

SignalR içinde Nekleme kullanmak için, **Defaultdependencyresolver**'dan türeyen bir sınıf oluşturun.

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

Bu sınıf, **Defaultdependencyresolver**'ın **GetService** ve **GetServices** yöntemlerini geçersiz kılar. SignalR, hub örnekleri ve ayrıca SignalR tarafından dahili olarak kullanılan çeşitli hizmetler dahil olmak üzere çalışma zamanında çeşitli nesneler oluşturmak için bu yöntemleri çağırır.

- **GetService** yöntemi bir türün tek bir örneğini oluşturur. Nekleme çekirdeğinin **TryGet** yöntemini çağırmak için bu yöntemi geçersiz kılın. Bu yöntem null döndürürse, varsayılan çözümleyiciye geri dönün.
- **GetServices** yöntemi, belirtilen türde nesnelerin bir koleksiyonunu oluşturur. Neklemesine ait sonuçları varsayılan çözümleyiciyle sonuçlarla birleştirmek için bu yöntemi geçersiz kılın.

## <a name="configure-ninject-bindings"></a>Nekleme bağlamalarını yapılandırma

Şimdi tür bağlamaları bildirmek için Nekleme kullanacağız.

Uygulamanızın Startup.cs sınıfını açın (`readme.txt`' deki paket yönergelerine göre el ile oluşturduğunuz veya projenize kimlik doğrulaması eklenerek oluşturulan). `Startup.Configuration` yönteminde Nekleme kapsayıcısını oluşturun ve Nekleme, *çekirdeği*çağırır.

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

Özel bağımlılık çözümleyicimizin bir örneğini oluşturun:

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

`IStockTicker` için aşağıdaki şekilde bir bağlama oluşturun:

[!code-csharp[Main](dependency-injection/samples/sample17.cs)]

Bu kod iki şeyi söyleyerek. İlk olarak, uygulama bir `IStockTicker`ihtiyaç duyduğunda, çekirdek bir `StockTicker`örneği oluşturacaktır. İkincisi, `StockTicker` sınıfı tek bir nesne olarak oluşturulmuş olmalıdır. Nekleme nesnenin bir örneğini oluşturur ve her istek için aynı örneği döndürür.

**Iubconnectioncontext** için aşağıdaki şekilde bir bağlama oluşturun:

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

Bu kod, bir **Ihubconnection**döndüren anonim bir işlev oluşturur. **Whenınjectedinto** yöntemi, neklemesine bu işlevi yalnızca `IStockTicker` örnekleri oluştururken kullanmasını söyler. Bunun nedeni, SignalR 'nin, dahili olarak **IHV Ubconnectioncontext** örnekleri oluşturduğunu ve SignalR 'nin bunları nasıl oluşturduğunu geçersiz kılmak istemedik. Bu işlev yalnızca `StockTicker` sınıfımız için geçerlidir.

Bir hub yapılandırması ekleyerek bağımlılık çözümleyicisini **Mapsignalr** yöntemine geçirin:

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

Örnek başlangıç sınıfındaki Startup. ConfigureSignalR yöntemini yeni parametresiyle güncelleştirin:

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

Şimdi SignalR, varsayılan çözümleyici yerine **Mapsignalr**içinde belirtilen çözümleyici 'yi kullanacaktır.

`Startup.Configuration`için kod listesinin tamamı aşağıda verilmiştir.

[!code-csharp[Main](dependency-injection/samples/sample21.cs)]

Visual Studio 'da StockTicker uygulamasını çalıştırmak için F5 'e basın. Tarayıcı penceresinde `http://localhost:*port*/SignalR.Sample/StockTicker.html`' a gidin.

![](dependency-injection/_static/image3.png)

Uygulama daha önce olduğu gibi tamamen aynı işlevselliğe sahiptir. (Bir açıklama için bkz. [ASP.NET SignalR Ile sunucu yayını](../getting-started/tutorial-server-broadcast-with-signalr.md).) Davranışı değiştirmedik; kodu test etmek, sürdürmek ve geliştirmek için daha kolay hale getirilir.
