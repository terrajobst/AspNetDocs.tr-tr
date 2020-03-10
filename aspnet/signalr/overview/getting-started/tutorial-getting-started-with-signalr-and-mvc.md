---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 'Öğretici: SignalR 2 ve MVC 5 ile gerçek zamanlı sohbet | Microsoft Docs'
author: bradygaster
description: Bu öğreticide, gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR 2 ' nin nasıl kullanılacağı gösterilmektedir. SignalR 'yi MVC 5 uygulamasına eklersiniz.
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537046"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a>Öğretici: SignalR 2 ve MVC 5 ile gerçek zamanlı sohbet

Bu öğreticide, gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR 2 ' nin nasıl kullanılacağı gösterilmektedir. Bir MVC 5 uygulamasına SignalR ekleyin ve ileti göndermek ve görüntülemek için bir sohbet görünümü oluşturun.

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Projeyi ayarlama
> * Örneği çalıştırma
> * Kodu inceleme

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Önkoşullar

* [ASP.NET ve web geliştirme](https://visualstudio.microsoft.com/downloads/) iş yüküyle **Visual Studio 2017**.

## <a name="set-up-the-project"></a>Projeyi ayarlama

Bu bölümde, Visual Studio 2017 ve SignalR 2 kullanarak boş bir ASP.NET MVC 5 uygulaması oluşturma, SignalR kitaplığını ekleme ve sohbet uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.

1. Visual Studio 'da .NET Framework 4,5 ' C# i hedefleyen bir ASP.NET uygulaması oluşturun, bunu SignalRChat olarak adlandırın ve Tamam ' a tıklayın.

    ![Web oluştur](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. **Yeni ASP.NET Web uygulaması-SignalRMvcChat**' de **MVC** ' yi ve ardından **kimlik doğrulamasını Değiştir**' i seçin.

1. **Kimlik doğrulamasını Değiştir**' de **kimlik doğrulaması yok** ' u ve **Tamam**' ı tıklatın

    ![Kimlik doğrulaması yok seçin](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. **Yeni ASP.NET Web uygulaması-SignalRMvcChat**' de **Tamam**' ı seçin.

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin.

1. **Yeni öğe Ekle-signalrchat**' te, **yüklü** > **Visual C#**  > **Web** > **SignalR** ' i seçin ve ardından **SignalR hub sınıfı (v2)** öğesini seçin.

1. Sınıfı *ChatHub* olarak adlandırın ve projeye ekleyin.

    Bu adım, *ChatHub.cs* sınıf dosyasını oluşturur ve proje Için SignalR 'yi destekleyen bir betik dosyaları ve derleme başvuruları kümesi ekler.

1. Yeni *ChatHub.cs* Class dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. **Çözüm Gezgini**, projeye sağ tıklayın ve > **sınıfı** **Ekle** ' yi seçin.

1. Yeni sınıf *başlangıcını* adlandırın ve projeye ekleyin.

1. *Startup.cs* Class dosyasındaki kodu şu kodla değiştirin:

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. **Çözüm Gezgini**, **denetleyiciler** > **HomeController.cs**' ı seçin.

1. Bu yöntemi *HomeController.cs*ekleyin.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    Bu yöntem, daha sonraki bir adımda oluşturduğunuz **sohbet** görünümünü döndürür.

1. **Çözüm Gezgini**' de, **Görünümler** > **giriş**' e sağ tıklayın ve >  **Görünüm** **Ekle** ' yi seçin.

1. **Görünüm Ekle**' de, yeni görünüm **sohbeti** ' nı adlandırın ve **Ekle**' yi seçin.

1. **Chat. cshtml** içeriğini şu kodla değiştirin:

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. **Çözüm Gezgini**' de **betikler**' ı genişletin.

    JQuery ve SignalR için betik kitaplıkları projede görülebilir.

    > [!IMPORTANT]
    > Paket Yöneticisi, SignalR betiklerinin daha yeni bir sürümünü yüklemiş olabilir.

1. Kod bloğundaki betik başvurularının projedeki betik dosyalarının sürümlerine karşılık geldiğinden emin olun.

    Özgün kod bloğundan gelen betik başvuruları:

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. Eşleşmiyorsa, *. cshtml* dosyasını güncelleştirin.

1. Menü çubuğundan **dosya** > **Tümünü Kaydet**' i seçin.

## <a name="run-the-sample"></a>Örneği çalıştırın

1. Araç çubuğunda, **betik hata ayıklamayı** açın ve ardından yürütme düğmesini seçerek örneği hata ayıklama modunda çalıştırın.

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. Tarayıcı açıldığında, sohbet Kimliğiniz için bir ad girin.

1. Tarayıcıdan URL 'YI kopyalayın, iki farklı tarayıcı açın ve adres çubuklarına URL 'Leri yapıştırın.

1. Her tarayıcıda benzersiz bir ad girin.

1. Şimdi bir açıklama ekleyin ve **Gönder**' i seçin. Bunu diğer tarayıcılarda yineleyin. Açıklamalar gerçek zamanlı olarak görünür.

    > [!NOTE]
    > Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz. Merkez tüm geçerli kullanıcılara yorum yayınlar. Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.

    Sohbet uygulamasının üç farklı tarayıcıda nasıl çalıştığını görün. Tom, anve, ve Çiğdem iletileri gönderirken tüm tarayıcıların gerçek zamanlı olarak güncelleştirilmesi:

    ![Üç tarayıcıda da aynı sohbet geçmişi görüntülenir](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. **Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin. SignalR kitaplığının çalışma zamanında oluşturduğu *Hublar* adlı bir betik dosyası vardır. Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir.

    ![Betik belgeleri düğümünde otomatik olarak oluşturulan hub betiği](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a>Kodu inceleyin

SignalR sohbet uygulaması iki temel SignalR geliştirme görevi gösterir. Bir hub oluşturmayı gösterir. Sunucu, ana düzenleme nesnesi olarak bu hub 'ı kullanır. Hub, ileti göndermek ve almak için SignalR jQuery kitaplığını kullanır.

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs 'de SignalR hub 'Ları

Kod örneğinde, `ChatHub` sınıfı `Microsoft.AspNet.SignalR.Hub` sınıfından türetilir. `Hub` sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur. Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve ardından bunları bir Web sayfasındaki betiklerden çağırarak bu yöntemlere erişebilirsiniz.

Sohbet kodunda, istemciler yeni bir ileti göndermek için `ChatHub.Send` yöntemini çağırır. İçindeki hub, `Clients.All.addNewMessageToPage`çağırarak iletiyi tüm istemcilere gönderir.

`Send` yöntemi çeşitli Merkez kavramlarını gösterir:

* İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.

* Bu hub 'a bağlı tüm istemcilerle iletişim kurmak için `Microsoft.AspNet.SignalR.Hub.Clients` Dynamic özelliğini kullanın.

* İstemcileri güncelleştirmek için istemcide bir işlev (`addNewMessageToPage` işlevi gibi) çağırın.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a>SignalR ve jQuery sohbeti. cshtml

Kod örneğindeki *chat. cshtml* görünüm dosyası bir SignalR hub 'ı ile iletişim kurmak Için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir.  Kod birçok önemli görevi gerçekleştirir. Hub için otomatik olarak oluşturulan ara sunucuya bir başvuru oluşturur, sunucunun istemcilere içerik göndermek için çağıradığına yönelik bir işlev bildirir ve hub 'a ileti göndermek için bir bağlantı başlatır.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> JavaScript 'te, sunucu sınıfına ve üyelerine yönelik başvuru camelCase ' de bulunur. Kod örneği, JavaScript 'teki C# `ChatHub` sınıfına `chatHub`olarak başvurur.

Bu kod bloğunda, betikte bir geri çağırma işlevi oluşturursunuz.

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır. `htmlEncode` işlevine yönelik isteğe bağlı çağrı, sayfada görüntülemeden önce ileti içeriğini HTML olarak kodlamak için bir yol gösterir. Betik ekleme işlemini önlemenin bir yoludur.

Bu kod, hub ile bir bağlantı açar.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> Bu yaklaşım, olay işleyicisi yürütmeden önce bir bağlantı oluşturmanızı sağlar.

Kod bağlantıyı başlatır ve ardından sohbet sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.

## <a name="get-the-code"></a>Kodu alma

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a>Ek kaynaklar

SignalR hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

* [SignalR projesi](http://signalr.net)

* [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)

* [SignalR wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide şunları yaptınız:

> [!div class="checklist"]
> * Projeyi ayarlama
> * Örneği çalıştırdı
> * Kod incelendi

Yüksek frekanslı mesajlaşma işlevselliği sağlamak için ASP.NET SignalR 2 kullanan bir Web uygulamasının nasıl oluşturulacağını öğrenmek için sonraki makaleye ilerleyin.
> [!div class="nextstepaction"]
> [Yüksek frekanslı mesajlaşma ile Web uygulaması](tutorial-high-frequency-realtime-with-signalr.md)