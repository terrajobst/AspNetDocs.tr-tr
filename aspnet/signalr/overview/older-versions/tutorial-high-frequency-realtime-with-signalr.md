---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: SignalR 1. x ile yüksek frekanslı gerçek zamanlı Microsoft Docs
author: bradygaster
description: Bu öğreticide, yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Üzerinde yüksek frekanslı mesajlaşma...
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623503"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a>SignalR 1.x ile Yüksek Sıklıkta Gerçek Zamanlı

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu öğreticide, yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Bu durumda yüksek frekanslı mesajlaşma, sabit bir hızda gönderilen güncelleştirmeler anlamına gelir; Bu uygulama söz konusu olduğunda, saniyede en fazla 10 ileti.
> 
> Bu öğreticide oluşturacağınız uygulama, kullanıcıların sürükleyebilmesi için bir şekil görüntüler. Diğer tüm bağlı tarayıcılardaki şeklin konumu, zamanlanmış güncelleştirmeler kullanılarak sürüklenen şeklin konumuyla eşleşecek şekilde güncelleştirilecektir.
> 
> Bu öğreticide tanıtılan kavramların gerçek zamanlı oyun ve diğer simülasyon uygulamalarına yönelik uygulamaları vardır.
> 
> Öğreticideki yorumlara hoş geldiniz. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) veya [StackOverflow.com](http://stackoverflow.com)'e gönderebilirsiniz.

## <a name="overview"></a>Genel bakış

Bu öğretici, bir nesnenin durumunu gerçek zamanlı olarak diğer tarayıcılarla paylaşan bir uygulamanın nasıl oluşturulacağını gösterir. Oluşturduğumuz uygulama MoveShape olarak adlandırılır. MoveShape sayfasında kullanıcının sürükleyebilmesi için bir HTML div öğesi görüntülenir; Kullanıcı div öğesini sürüklediğinde, yeni konumu sunucusuna gönderilir. Bu, diğer tüm bağlı istemcilerin şeklin konumunu eşleşecek şekilde güncelleştirmesini söylemiş olur.

![Uygulama penceresi](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

Bu öğreticide oluşturulan uygulama, Davmian edinin bir tanıtımı temel alır. Bu tanıtımı içeren bir video [burada](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)görünebilirler.

Bu öğretici, şekil sürüklenirken harekete geçirerek her bir olaydan SignalR iletilerinin nasıl gönderileceğini gösteren bir başlayacaktır. Her bağlı istemci, her ileti alındığında şeklin yerel sürümünün konumunu güncelleştirir.

Uygulama bu yöntemi kullanarak işlev yaparken, bu, önerilen bir programlama modeli değildir, çünkü gönderilen ileti sayısı üst sınırı yoktur, bu nedenle istemciler ve sunucu iletilerle daha fazla bulunabilir ve performans düşebilir . Şekil her bir yeni konuma düzgün şekilde taşınmaktansa, istemci üzerindeki görüntülenmiş animasyon de kopuk olur. Öğreticinin sonraki bölümlerinde, iletilerin istemci veya sunucu tarafından gönderilme maksimum hızını kısıtlayan bir Zamanlayıcı işlevinin nasıl oluşturulacağı ve şekillerin konumlar arasında sorunsuzca nasıl taşınacağı gösterilmektedir. Bu öğreticide oluşturulan uygulamanın son sürümü [kod galerisinden](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)indirilebilir.

Bu öğretici aşağıdaki bölümleri içerir:

- [Önkoşullar](#prerequisites)
- [Projeyi oluşturma](#createtheproject)
- [ASP.NET SignalR ve JQuery. UI NuGet paketlerini ekleyin](#nugetpackages)
- [Temel uygulamayı oluşturma](#baseapp)
- [İstemci döngüsünü ekleme](#clientloop)
- [Sunucu döngüsünü ekleyin](#serverloop)
- [İstemciye sorunsuz animasyon ekleme](#animation)
- [Diğer adımlar](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Önkoşullar

Bu öğretici, Visual Studio 2012 veya Visual Studio 2010 gerektirir. Visual Studio 2010 kullanılıyorsa, proje .NET Framework 4,5 yerine .NET Framework 4 ' ü kullanacaktır.

Visual Studio 2012 kullanıyorsanız, [ASP.NET and Web Tools 2012,2 güncelleştirmesini](https://go.microsoft.com/fwlink/?LinkId=282650)yüklemenizi öneririz. Bu güncelleştirme yayımlama, yeni işlevsellik ve yeni şablonlar geliştirmeleri gibi yeni özellikler içerir.

Visual Studio 2010 kullanıyorsanız, [NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 'in yüklü olduğundan emin olun.

<a id="createtheproject"></a>

## <a name="create-the-project"></a>Projeyi oluşturma

Bu bölümde, projeyi Visual Studio 'da oluşturacağız.

1. **Dosya** menüsünde **Yeni proje**' ye tıklayın.
2. **Yeni proje** Iletişim kutusunda Şablonlar ' ı genişletin **C#** ve **Web**' i seçin.
3. **ASP.net boş Web uygulaması** şablonunu seçin, projeyi *Moveshaayaklı Mo*olarak adlandırın ve **Tamam**' a tıklayın.

    ![Yeni proje oluşturuluyor](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a>SignalR ve JQuery. UI NuGet paketlerini ekleyin

Bir NuGet paketi yükleyerek bir projeye SignalR işlevi ekleyebilirsiniz. Bu öğretici, şeklin sürüklenip taşınmalarına izin vermek için JQuery. UI paketini de kullanacaktır.

1. Araçlar 'ı tıklatın **| NuGet Paket Yöneticisi | Paket Yöneticisi konsolu**.
2. Paket Yöneticisi 'nde aşağıdaki komutu girin.

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    SignalR paketi, birkaç farklı NuGet paketini bağımlılıklar olarak yüklüyor. Yükleme tamamlandığında, bir ASP.NET uygulamasında SignalR 'yi kullanmak için gereken tüm sunucu ve istemci bileşenlerine sahip olursunuz.
3. JQuery ve JQuery. UI paketlerini yüklemek için Paket Yöneticisi konsoluna aşağıdaki komutu girin.

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>Temel uygulamayı oluşturma

Bu bölümde, her fare taşıma olayı sırasında şeklin konumunu sunucuya gönderen bir tarayıcı uygulaması oluşturacağız. Sunucu daha sonra bu bilgileri, alındığı gibi diğer tüm bağlı istemcilere yayınlar. Daha sonraki bölümlerde bu uygulamada geniştireceğiz.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve **Ekle**, **sınıf..** . öğesini seçin. Sınıfı **Moveshapehub** olarak adlandırın ve **Ekle**' ye tıklayın.
2. Yeni **Moveshapehub** sınıfındaki kodu aşağıdaki kodla değiştirin.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    Yukarıdaki `MoveShapeHub` sınıfı, bir SignalR hub 'ının uygulamasıdır. [SignalR Ile çalışmaya](index.md) başlama öğreticisinde olduğu gibi, hub 'da istemcilerin doğrudan çağıracağız bir yöntemi vardır. Bu durumda, istemci, şeklin yeni X ve Y koordinatlarını içeren bir nesneyi sunucuya gönderir ve bu, daha sonra diğer tüm bağlı istemciler tarafından yayınlanacaktır. SignalR, JSON kullanarak bu nesneyi otomatik olarak serileştirilir.

    İstemciye gönderilecek nesne (`ShapeModel`) şeklin konumunu depolayacak Üyeler içerir. Sunucu üzerindeki nesnenin sürümü Ayrıca, belirli bir istemcinin kendi verilerini göndermemesi için, hangi istemci verilerinin depolanmakta olduğunu izlemek için bir üye içerir. Bu üye, serileştirilmesi ve istemciye gönderilmesini önlemek için `JsonIgnore` özniteliğini kullanır.
3. Daha sonra, uygulama başladığında hub 'ı ayarlayacağız. **Çözüm Gezgini**, projeye sağ tıklayın ve ardından Ekle ' ye tıklayın **| Genel uygulama sınıfı**. *Genel* varsayılan adını kabul edip **Tamam**' a tıklayın.

    ![Genel uygulama sınıfı Ekle](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. Global.asax.cs sınıfında, belirtilen **using deyimlerini kullanarak** aşağıdaki `using` deyimini ekleyin.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. SignalR için varsayılan yolu kaydetmek üzere genel sınıfın `Application_Start` yöntemine aşağıdaki kod satırını ekleyin.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    Global. asax dosyanız aşağıdaki gibi görünmelidir:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. Ardından, istemcisini ekleyeceğiz. **Çözüm Gezgini**, projeye sağ tıklayın ve ardından Ekle ' ye tıklayın **| Yeni öğe**. **Yeni öğe Ekle** Iletişim kutusunda **HTML sayfası**' nı seçin. Sayfaya uygun bir ad verin ( **default. html**gibi) ve **Ekle**' ye tıklayın.
7. **Çözüm Gezgini**, yeni oluşturduğunuz sayfaya sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' ya tıklayın.
8. HTML sayfasındaki varsayılan kodu aşağıdaki kod parçacığı ile değiştirin.

    > [!NOTE]
    > Aşağıdaki betik başvurularının, komut dosyaları klasöründe projenize eklenen paketlerle eşleştiğini doğrulayın. Visual Studio 2010 ' de, projeye eklenen JQuery ve SignalR sürümü aşağıdaki sürüm numaralarıyla eşleşmeyebilir.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    Yukarıdaki HTML ve JavaScript kodu, şekil adlı kırmızı bir div oluşturur ve şeklin konumunu sunucuya göndermek için şeklin `drag` olayını kullanır.
9. F5 tuşuna basarak uygulamayı başlatın. Sayfanın URL 'sini kopyalayın ve ikinci bir tarayıcı penceresine yapıştırın. Şekli tarayıcı pencerelerinin birine sürükleyin; diğer tarayıcı penceresindeki şekil hareket etmelidir.

    ![Uygulama penceresi](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>İstemci döngüsünü ekleme

Her fare taşıma olayında şekil konumunun gönderilmesi gereksiz miktarda ağ trafiği oluşturacak olduğundan, istemciden gelen iletilerin kısıtlanacak olması gerekir. Yeni konum bilgilerini sunucuya sabit bir hızda gönderen bir döngü ayarlamak için JavaScript `setInterval` işlevini kullanacağız. Bu döngü, bir oyunun veya başka bir simülasyonu 'nin tüm işlevselliğini destekleyen bir kez daha sürekli çağrılan işlev olan "oyun döngüsünün" çok basit bir gösterimidir.

1. HTML sayfasındaki istemci kodunu aşağıdaki kod parçacığı ile eşleşecek şekilde güncelleştirin.

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    Yukarıdaki güncelleştirme, sabit bir sıklıkta çağrılan `updateServerModel` işlevini ekler. Bu işlev, `moved` bayrağı gönderilecek yeni konum verilerinin olduğunu gösterdiğinde, konum verilerini sunucuya gönderir.
2. F5 tuşuna basarak uygulamayı başlatın. Sayfanın URL 'sini kopyalayın ve ikinci bir tarayıcı penceresine yapıştırın. Şekli tarayıcı pencerelerinin birine sürükleyin; diğer tarayıcı penceresindeki şekil hareket etmelidir. Sunucuya gönderilen ileti sayısı kısıtlandığından, animasyon önceki bölümde olduğu kadar düzgün görünmez.

    ![Uygulama penceresi](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>Sunucu döngüsünü ekleyin

Geçerli uygulamada, sunucudan istemciye gönderilen iletiler, alındıkları sıklıkta zaman aşımına uğrar. Bu, istemcide görülen benzer bir sorunu gösterir; iletiler gereksiniminden daha sık gönderilebilir ve bağlantı sonuç olarak taşabilir. Bu bölümde, giden iletilerin oranını hedefleyen bir Zamanlayıcı uygulamak için sunucunun nasıl güncelleştirileceğini açıklanmaktadır.

1. `MoveShapeHub.cs` içeriğini aşağıdaki kod parçacığı ile değiştirin.

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    Yukarıdaki kod, istemciyi .NET Framework 'te `Timer` sınıfını kullanarak giden iletileri belirleyen `Broadcaster` sınıfını eklemek üzere genişletir.

    Hub 'ın kendisi geçişli olduğundan (her gerektiğinde oluşturulur), `Broadcaster` tek bir olarak oluşturulur. Yavaş başlatma (.NET 4 ' te tanıtılan), oluşturma işlemi tamamlanana kadar ertelenmesi için kullanılır ve ilk Merkez örneği Zamanlayıcı başlatılmadan önce tamamen oluşturulduğundan emin olur.

    İstemciler ' `UpdateShape` işlevine yapılan çağrı bundan sonra hub 'ın `UpdateModel` yönteminden taşınır, böylece gelen iletiler alındığında hemen çağrılmaz. Bunun yerine, istemcilere gönderilen iletiler, `Broadcaster` sınıfının içinden `_broadcastLoop` Zamanlayıcı tarafından yönetilen, saniyede 25 çağrı hızında gönderilir.

    Son olarak, doğrudan hub 'dan istemci yöntemi çağırmak yerine, `Broadcaster` sınıfın, `GlobalHost`kullanarak şu anda işletim merkezine (`_hubContext`) bir başvuru alması gerekir.
2. F5 tuşuna basarak uygulamayı başlatın. Sayfanın URL 'sini kopyalayın ve ikinci bir tarayıcı penceresine yapıştırın. Şekli tarayıcı pencerelerinin birine sürükleyin; diğer tarayıcı penceresindeki şekil hareket etmelidir. Önceki bölümden tarayıcıda görünür bir fark olmayacaktır, ancak istemciye gönderilen ileti sayısı kısıtlanacaktır.

    ![Uygulama penceresi](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>İstemciye sorunsuz animasyon ekleme

Uygulama neredeyse tamamlanmıştır, ancak sunucu iletilerine yanıt olarak taşındığı için şeklin hareket halinde daha fazla geliştirme yapabiliriz. Şeklin konumunu sunucu tarafından verilen yeni konuma ayarlamak yerine, şekli geçerli ve yeni konumuna düzgün bir şekilde taşımak için JQuery Kullanıcı arabirimi kitaplığının `animate` işlevini kullanacağız.

1. Aşağıdaki Vurgulanan koda bakmak için istemcinin `updateShape` yöntemini güncelleştirin:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    Yukarıdaki kod, şekli eski konumdan, animasyon aralığı (Bu durumda 100 milisaniye) sırasında sunucu tarafından verilen yeni bir konuma taşır. Şekil üzerinde çalışan herhangi bir önceki animasyon, yeni animasyon başlamadan önce temizlenir.
2. F5 tuşuna basarak uygulamayı başlatın. Sayfanın URL 'sini kopyalayın ve ikinci bir tarayıcı penceresine yapıştırın. Şekli tarayıcı pencerelerinin birine sürükleyin; diğer tarayıcı penceresindeki şekil hareket etmelidir. Diğer penceredeki şeklin hareketi, her gelen ileti için bir kez ayarlanmaması yerine zamana göre enterpolasyonla daha az bir şekilde görünmelidir.

    ![Uygulama penceresi](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>Diğer adımlar

Bu öğreticide, istemciler ve sunucular arasında yüksek frekanslı iletiler gönderen bir SignalR uygulamasını nasıl programlayabilirsiniz. Bu iletişim paradigması, [SignalR ile oluşturulan ShootR oyunu](http://shootr.signalr.net)gibi çevrimiçi oyunları ve diğer benzetimleri geliştirmek için yararlıdır.

Bu öğreticide oluşturulan tüm uygulama [kod galerisinden](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)indirilebilir.

SignalR geliştirme kavramları hakkında daha fazla bilgi edinmek için, SignalR kaynak kodu ve kaynakları için aşağıdaki siteleri ziyaret edin:

- [SignalR projesi](http://signalr.net)
- [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)
- [SignalR wiki](https://github.com/SignalR/SignalR/wiki)
