---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 'Öğretici: SignalR 2 ile gerçek zamanlı sohbet | Microsoft Docs'
author: bradygaster
description: Bu öğreticide SignalR kullanarak gerçek zamanlı bir sohbet uygulaması oluşturma işlemi gösterilir. SignalR 'yi boş bir ASP.NET Web uygulamasına eklersiniz.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536983"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>Öğretici: SignalR 2 ile gerçek zamanlı sohbet

Bu öğreticide, SignalR kullanarak gerçek zamanlı bir sohbet uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir. SignalR 'i boş bir ASP.NET Web uygulamasına eklersiniz ve ileti göndermek ve göstermek için bir HTML sayfası oluşturmanız gerekir.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Projeyi ayarlama
> * Örneği çalıştırma
> * Kodu inceleme

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Önkoşullar

* [ASP.NET ve web geliştirme](https://visualstudio.microsoft.com/downloads/) iş yüküyle **Visual Studio 2017**.

## <a name="set-up-the-project"></a>Projeyi ayarlama

Bu bölümde, boş bir ASP.NET Web uygulaması oluşturmak, SignalR eklemek ve sohbet uygulaması oluşturmak için Visual Studio 2017 ve SignalR 2 ' nin nasıl kullanılacağı gösterilmektedir.

1. Visual Studio 'da bir ASP.NET Web uygulaması oluşturun.

    ![Web oluştur](tutorial-getting-started-with-signalr/_static/image2.png)

1. **New ASP.NET Project-SignalRChat** penceresinde **boş** bırakın ve **Tamam**' ı seçin.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.

1. **Yeni öğe Ekle-signalrchat**' te, **yüklü** > **Visual C#**  > **Web** > **SignalR** ' i seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.

1. Sınıfı *ChatHub* olarak adlandırın ve projeye ekleyin.

    Bu adım, *ChatHub.cs* sınıf dosyasını oluşturur ve proje Için SignalR 'yi destekleyen bir betik dosyaları ve derleme başvuruları kümesi ekler.

1. Yeni *ChatHub.cs* Class dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.

1. **Yeni öğe Ekle-signalrchat** ' in **yüklü** > **Visual C#**  > **Web** ' i seçip **owın başlangıç sınıfı**' nı seçin.

1. Sınıfın *başlangıcını* adlandırın ve projeye ekleyin.

1. *Başlangıç* sınıfındaki varsayılan kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. **Çözüm Gezgini**' de projeye sağ tıklayın ve > **HTML sayfası** **Ekle** ' yi seçin.

1. Yeni sayfa *dizinini* adlandırın ve **Tamam**' ı seçin.

1. **Çözüm Gezgini**, oluşturduğunuz HTML sayfasına sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' yı seçin.

1. HTML sayfasındaki varsayılan kodu şu kodla değiştirin:

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. **Çözüm Gezgini**' de **betikler**' ı genişletin.

    JQuery ve SignalR için betik kitaplıkları projede görülebilir.

    > [!IMPORTANT]
    > Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yüklemiş olabilir.

1. Kod bloğundaki betik başvurularının projedeki betik dosyalarının sürümlerine karşılık geldiğinden emin olun.

    Özgün kod bloğundan gelen betik başvuruları:

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. Eşleşiyorlarsa, *. html* dosyasını güncelleştirin.

1. Menü çubuğundan **dosya** > **Tümünü Kaydet**' i seçin.

## <a name="run-the-sample"></a>Örneği çalıştırın

1. Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından yürütme düğmesini seçerek örneği hata ayıklama modunda çalıştırın.

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr/_static/image3.png)

1. Tarayıcı açıldığında, sohbet Kimliğiniz için bir ad girin.

1. Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.

1. Her tarayıcıda benzersiz bir ad girin.

1. Şimdi bir açıklama ekleyin ve **Gönder**' i seçin. Bunu diğer tarayıcılarda yineleyin. Açıklamalar gerçek zamanlı olarak görünür.

    > [!NOTE]
    > Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz. Merkez tüm geçerli kullanıcılara yorum yayınlar. Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.

    Sohbet uygulamasının üç farklı tarayıcıda nasıl çalıştığını görün. Tom, anve, ve Çiğdem iletileri gönderirken tüm tarayıcıların gerçek zamanlı olarak güncelleştirilmesi:

    ![Üç tarayıcıda da aynı sohbet geçmişi görüntülenir](tutorial-getting-started-with-signalr/_static/image4.png)

1. **Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin. SignalR kitaplığının çalışma zamanında oluşturduğu *Hublar* adlı bir betik dosyası vardır. Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir.

    ![Betik belgeleri düğümünde otomatik olarak oluşturulan hub betiği](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>Kodu inceleyin

SignalRChat uygulaması iki temel SignalR geliştirme görevi gösterir. Bir hub oluşturmayı gösterir. Sunucu, ana düzenleme nesnesi olarak bu hub 'ı kullanır. Hub, ileti göndermek ve almak için SignalR jQuery kitaplığını kullanır.

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs 'de SignalR hub 'Ları

Yukarıdaki kod örneğinde, `ChatHub` sınıfı `Microsoft.AspNet.SignalR.Hub` sınıfından türetilir. `Hub` sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur. Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve sonra bu yöntemleri bir Web sayfasındaki betiklerden çağırarak kullanabilirsiniz.

Sohbet kodunda, istemciler yeni bir ileti göndermek için `ChatHub.Send` yöntemini çağırır. Merkez daha sonra `Clients.All.broadcastMessage`çağırarak iletiyi tüm istemcilere gönderir.

`Send` yöntemi çeşitli Merkez kavramlarını gösterir:

* İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.

* Bu hub 'a bağlı tüm istemcilerle iletişim kurmak için `Microsoft.AspNet.SignalR.Hub.Clients` Dynamic özelliğini kullanın.

* İstemcileri güncelleştirmek için istemcide bir işlev (`broadcastMessage` işlevi gibi) çağırın.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>Dizin. html dosyasındaki SignalR ve jQuery

Kod örneğindeki *index. html* sayfası, bir SignalR hub 'ı ile iletişim kurmak Için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir. Kod birçok önemli görevi gerçekleştirir. Hub 'a başvurmak için bir proxy bildirir, sunucunun istemcilere içerik göndermek için çağıradığına yönelik bir işlev bildirir ve hub 'a ileti göndermeye yönelik bir bağlantı başlatır.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> JavaScript 'te, sunucu sınıfına ve üyelerine yönelik başvurunun camelCase olması gerekmez. Kod örneği, JavaScript 'teki C# *ChatHub* sınıfına `chatHub`olarak başvurur.

Bu kod bloğunda, betikte bir geri çağırma işlevi oluşturursunuz.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır. HTML-içeriği görüntülemeden önce kodlayan iki satır isteğe bağlıdır ve betik ekleme işlemini önlemenin iyi bir yolunu gösterir.

Bu kod, hub ile bir bağlantı açar.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> Bu yaklaşım, olay işleyicisi yürütmeden önce kodun bir bağlantı kurmasını sağlar.

Kod bağlantıyı başlatır ve sonra HTML sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a>Ek kaynaklar

SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [SignalR projesi](http://signalr.net)

* [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)

* [SignalR wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yapabilirsiniz:

> [!div class="checklist"]
> * Projeyi ayarlama
> * Örneği çalıştırdı
> * Kod incelendi

SignalR ve MVC 5 ' i nasıl kullanacağınızı öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [SignalR 2 ve MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)