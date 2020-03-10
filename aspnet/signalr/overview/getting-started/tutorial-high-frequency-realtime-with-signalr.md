---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 'Öğretici: SignalR 2 ile yüksek frekanslı gerçek zamanlı uygulama oluşturma | Microsoft Docs'
author: bradygaster
description: Bu öğreticide, yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558627"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a>Öğretici: SignalR 2 ile yüksek frekanslı gerçek zamanlı uygulama oluşturma

Bu öğreticide, yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağı gösterilmektedir. Bu durumda, "yüksek frekanslı mesajlaşma", sunucunun güncelleştirmeleri sabit bir hızda göndermesi anlamına gelir. Saniyede en fazla 10 ileti gönderirsiniz.

Oluşturduğunuz uygulama, kullanıcıların sürükleyebilmesi için bir şekil görüntüler. Sunucu, bağlı olan tüm tarayıcılarda şeklin konumunu, zamanlanmış güncelleştirmeleri kullanarak sürüklenen şeklin konumuyla eşleşecek şekilde güncelleştirir.

Bu öğreticide tanıtılan kavramların gerçek zamanlı oyun ve diğer simülasyon uygulamalarına yönelik uygulamaları vardır.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Projeyi ayarlama
> * Temel uygulamayı oluşturma
> * Uygulama başlatıldığında hub 'a eşle
> * İstemciyi ekleme
> * Uygulamayı çalıştırma
> * İstemci döngüsünü ekleme
> * Sunucu döngüsünü ekleyin
> * Kesintisiz animasyon ekle

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Önkoşullar

* [ASP.NET ve web geliştirme](https://visualstudio.microsoft.com/downloads/) iş yüküyle **Visual Studio 2017**.

## <a name="set-up-the-project"></a>Projeyi ayarlama

Bu bölümde, projeyi Visual Studio 2017 ' de oluşturursunuz.

Bu bölümde, Visual Studio 2017 kullanarak boş bir ASP.NET Web uygulaması oluşturma ve SignalR ve jQuery. UI kitaplıklarını ekleme gösterilmektedir.

1. Visual Studio 'da bir ASP.NET Web uygulaması oluşturun.

    ![Web oluştur](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. **Yeni ASP.NET Web uygulaması-Moveshaayaklı Mo** penceresinde **boş** bırakın ve **Tamam**' ı seçin.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.

1. **Yeni öğe Ekle-moveshaayaklı Mo**'da, **yüklü** > **Visual C#**  > **Web** > **SignalR** ' i seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.

1. Sınıfı *Moveshapehub* olarak adlandırın ve projeye ekleyin.

    Bu adım *MoveShapeHub.cs* sınıf dosyasını oluşturur. Aynı anda, bir dizi betik dosyası ve proje için SignalR 'yi destekleyen derleme başvuruları ekler.

1. **Araçlar** > **NuGet Paket Yöneticisi** > **Paket Yöneticisi konsolu**' nu seçin.

1. **Paket Yöneticisi konsolu**'nda şu komutu çalıştırın:

    ```console
    Install-Package jQuery.UI.Combined
    ```

    Komutu jQuery kullanıcı arabirimi kitaplığını yükleme. Şekle animasyon eklemek için bunu kullanırsınız.

1. **Çözüm Gezgini**' de betikler düğümünü genişletin.

    ![Betik kitaplığı başvuruları](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    JQuery, jQueryUI ve SignalR için betik kitaplıkları projede görünür.

## <a name="create-the-base-application"></a>Temel uygulamayı oluşturma

Bu bölümde, bir tarayıcı uygulaması oluşturacaksınız. Uygulama, her fare taşıma olayı sırasında şeklin konumunu sunucuya gönderir. Sunucu, bu bilgileri tüm bağlı istemcilere gerçek zamanlı olarak yayınlar. Daha sonraki bölümlerde bu uygulama hakkında daha fazla bilgi edinebilirsiniz.

1. *MoveShapeHub.cs* dosyasını açın.

1. *MoveShapeHub.cs* dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. Dosyayı kaydedin.

`MoveShapeHub` sınıfı, bir SignalR hub 'ının uygulamasıdır. [SignalR Ile çalışmaya](tutorial-getting-started-with-signalr.md) başlama öğreticisinde olduğu gibi, hub 'ın istemcilerin doğrudan çağırdığına yönelik bir yöntemi vardır. Bu durumda, istemci, şeklin yeni X ve Y koordinatlarıyla sunucuya bir nesne gönderir. Bu koordinatlar, diğer tüm bağlı istemcilere göre yapılır. SignalR, JSON kullanarak bu nesneyi otomatik olarak serileştirir.

Uygulama `ShapeModel` nesnesini istemciye gönderir. Şeklin konumunu depolayan üyelere sahiptir. Sunucu üzerindeki nesnenin sürümü, hangi istemci verilerinin depolanmakta olduğunu izlemek için bir üyeye de sahiptir. Bu nesne, sunucunun istemciye ait verileri geri göndermesini önler. Bu üye, uygulamanın verileri serileştirmesini ve istemciye geri göndermesini önlemek için `JsonIgnore` özniteliğini kullanır.

## <a name="map-to-the-hub-when-app-starts"></a>Uygulama başlatıldığında hub 'a eşle

Daha sonra, uygulama başladığında hub ile eşlemeyi ayarlarsınız. SignalR 2 ' de, bir OWıN başlangıç sınıfı eklendiğinde eşleme oluşturulur.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.

1. **Yeni öğe Ekle-moveshaayaklı Mo** ' da **yüklü** > **Visual C#**  > **Web** ' i seçin ve ardından **owın başlangıç sınıfı**' nı seçin.

1. Sınıfın *başlangıcını* adlandırın ve **Tamam**' ı seçin.

1. *Startup.cs* dosyasındaki varsayılan kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

OWıN başlangıç sınıfı, uygulama `Configuration` yöntemini yürüttüğünde `MapSignalR` çağırır. Uygulama, `OwinStartup` derleme özniteliğini kullanarak sınıfı OWıN başlangıç işlemine ekler.

## <a name="add-the-client"></a>İstemciyi ekleme

İstemci için HTML sayfasını ekleyin.

1. **Çözüm Gezgini**' de projeye sağ tıklayın ve > **HTML sayfası** **Ekle** ' yi seçin.

1. Sayfa **varsayılanını** adlandırın ve **Tamam**' ı seçin.

1. **Çözüm Gezgini**' de, *default. html* ' ye sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.

1. *Default. html* dosyasındaki varsayılan kodu şu kodla değiştirin:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. **Çözüm Gezgini**' de **betikler**' ı genişletin.

    JQuery ve SignalR için betik kitaplıkları projede görülebilir.

    > [!IMPORTANT]
    > Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yüklüyor.

1. Kod bloğundaki betik başvurularını projedeki betik dosyalarının sürümlerine karşılık gelecek şekilde güncelleştirin.

Bu HTML ve JavaScript kodu `shape`adlı kırmızı bir `div` oluşturur. Şeklin, jQuery kitaplığını kullanarak sürükleme davranışını sağlar ve şeklin konumunu sunucuya göndermek için `drag` olayını kullanır.

## <a name="run-the-app"></a>Uygulamayı çalıştırma

Uygulamayı çalıştırmak için kullanabilirsiniz. Şekli bir tarayıcı penceresi etrafında sürüklediğinizde, şekil diğer tarayıcılarda da hareket eder.

1. Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından uygulamayı hata ayıklama modunda çalıştırmak için Yürüt düğmesini seçin.

    ![Kullanıcı hata ayıklama modunu açıp oynat 'ı seçen kullanıcının ekran görüntüsü.](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    Sağ üst köşedeki kırmızı şekille bir tarayıcı penceresi açılır.

1. Sayfanın URL 'sini kopyalayın.

1. Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.

1. Şekli tarayıcı pencerelerinin birine sürükleyin. Diğer tarayıcı penceresindeki şekil aşağıda verilmiştir.

Uygulama bu yöntemi kullanırken çalışır, ancak önerilen bir programlama modeli değildir. Gönderilen ileti sayısı üst sınırı yoktur. Sonuç olarak, istemciler ve sunucu iletileri ve performansı düşürür. Ayrıca, uygulama istemcide kopuk bir animasyon görüntüler. Bu düzensiz animasyon, şekil her yöntem tarafından anında taşınabileceğinden oluşur. Şekil her yeni konuma düzgün şekilde taşınırsa daha iyidir. Ardından, bu sorunları nasıl düzelteceğinizi öğrenirsiniz.

## <a name="add-the-client-loop"></a>İstemci döngüsünü ekleme

Her fare taşıma olayında şeklin konumunu göndermek gereksiz miktarda ağ trafiği oluşturur. Uygulamanın, istemciden gelen iletileri azaltması gerekiyor.

Yeni konum bilgilerini sunucuya sabit bir hızda gönderen bir döngü ayarlamak için JavaScript `setInterval` işlevini kullanın. Bu döngü, "oyun döngüsünün" temel bir gösterimidir. Bu, bir oyunun tüm işlevselliğini destekleyen, tekrar tekrar çağrılan bir işlevdir.

1. *Default. html* dosyasındaki istemci kodunu şu kodla değiştirin:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > Betik başvurularını yeniden değiştirmeniz gerekir. Projenin, projedeki betiklerin sürümleriyle eşleşmesi gerekir.

    Bu yeni kod `updateServerModel` işlevini ekler. Sabit bir sıklıkta çağrılır. İşlevi, `moved` bayrağı gönderilecek yeni konum verilerinin olduğunu gösterdiğinde, konum verilerini sunucuya gönderir.

1. Uygulamayı başlatmak için Oynat düğmesini seçin

1. Sayfanın URL 'sini kopyalayın.

1. Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.

1. Şekli tarayıcı pencerelerinin birine sürükleyin. Diğer tarayıcı penceresindeki şekil aşağıda verilmiştir.

Uygulama, sunucuya gönderilen ileti sayısını kısıtladığından, animasyon ilk olarak düzgün bir şekilde görünmez.

## <a name="add-the-server-loop"></a>Sunucu döngüsünü ekleyin

Geçerli uygulamada, sunucudan istemciye gönderilen iletiler, alındıkları sıklıkta zaman aşımına uğrar. Bu ağ trafiği, istemcide görtiğimiz gibi benzer bir sorun gösterir.

Uygulama, gerekli olduklarından daha sık ileti gönderebilir. Bağlantı sonuç olarak taşabilir. Bu bölümde, giden iletilerin oranını hedefleyen bir Zamanlayıcı eklemek için sunucunun nasıl güncelleştirileceğini açıklanmaktadır.

1. `MoveShapeHub.cs` içeriğini şu kodla değiştirin:

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. Uygulamayı başlatmak için Oynat düğmesini seçin.

1. Sayfanın URL 'sini kopyalayın.

1. Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.

1. Şekli tarayıcı pencerelerinin birine sürükleyin.

Bu kod, `Broadcaster` sınıfını eklemek için istemciyi genişletir. Yeni sınıf, .NET Framework 'teki `Timer` sınıfını kullanarak giden iletileri kısıtlar.

Hub 'ın geçişli olduğunu öğrenmek iyi bir yoldur. Her gerektiğinde oluşturulur. Bu nedenle uygulama, `Broadcaster` tek bir olarak oluşturur. `Broadcaster`oluşturma işlemi, gerekene kadar ertelenmesi için yavaş başlatma kullanır. Bu, uygulamanın süreölçeri başlatmadan önce ilk hub örneğini tamamen oluşturduğunu garanti eder.

İstemciler ' `UpdateShape` işlevine yapılan çağrı daha sonra hub 'ın `UpdateModel` yönteminden çıkarılır. Uygulama gelen iletileri aldığında artık hemen çağrılmaz. Bunun yerine, uygulama iletileri istemcilere saniyede 25 çağrı hızında gönderir. İşlem, `Broadcaster` sınıfının içinden `_broadcastLoop` Zamanlayıcı tarafından yönetilir.

Son olarak, doğrudan hub 'dan istemci yöntemini çağırmak yerine, `Broadcaster` sınıfın şu anda çalışan `_hubContext` hub 'ına bir başvuru alması gerekir. `GlobalHost`başvurusunu alır.

## <a name="add-smooth-animation"></a>Kesintisiz animasyon ekle

Uygulama neredeyse tamamlandı, ancak bir geliştirme yapabiliriz. Uygulama, istemci üzerindeki şekli sunucu iletilerine yanıt olarak kaydırır. Şeklin konumunu sunucu tarafından verilen yeni konuma ayarlamak yerine, JQuery Kullanıcı arabirimi kitaplığının `animate` işlevini kullanın. Şekli geçerli ve yeni konumu arasında sorunsuzca hareket edebilir.

1. *Varsayılan. html* dosyasındaki istemcinin `updateShape` yöntemini vurgulanan kodla aynı şekilde güncelleştirin:

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. Uygulamayı başlatmak için Oynat düğmesini seçin.

1. Sayfanın URL 'sini kopyalayın.

1. Başka bir tarayıcı açın ve URL 'YI adres çubuğuna yapıştırın.

1. Şekli tarayıcı pencerelerinin birine sürükleyin.

Şeklin diğer penceredeki hareketi daha az jerbir şekilde görünür. Uygulama, gelen ileti başına bir kez ayarlanmaktansa hareketini zamana göre enterpolasyonlar.

Bu kod, şekli eski konumdan yeni bir konuma taşır. Sunucu, animasyon aralığı boyunca şeklin konumunu verir. Bu durumda, 100 milisaniyedir. Uygulama, yeni animasyon başlamadan önce şekil üzerinde çalışan önceki animasyonu temizler.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a>Ek kaynaklar

Yeni öğrendiğiniz iletişim paradigması, [SignalR ile oluşturulan ShootR oyunu](https://shootr.azurewebsites.net/)gibi çevrimiçi oyunları ve diğer benzetimleri geliştirmek için yararlıdır.

SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [SignalR projesi](http://signalr.net)

* [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)

* [SignalR wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Projeyi ayarlama
> * Temel uygulama oluşturuldu
> * Uygulama başlatıldığında hub 'a eşlendi
> * İstemci eklendi
> * Uygulamayı çalıştırdım
> * İstemci döngüsü eklendi
> * Sunucu döngüsü eklendi
> * Kesintisiz animasyon eklendi

Sunucu yayını işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağını öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [SignalR 2 ve sunucu yayını](tutorial-server-broadcast-with-signalr.md)