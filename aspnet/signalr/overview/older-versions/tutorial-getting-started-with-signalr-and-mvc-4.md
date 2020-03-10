---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 'Öğretici: SignalR 1. x ve MVC 4 ile çalışmaya başlama | Microsoft Docs'
author: bradygaster
description: Gerçek zamanlı bir sohbet uygulaması derlemek için ASP.NET SignalR ve ASP.NET MVC 4 kullanın.
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579571"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a>Öğretici: SignalR 1.x ve MVC 4 ile Çalışmaya Başlama

, [Patrick Fleti](https://github.com/pfletcher), [Tim teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu öğreticide, gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR 'nin nasıl kullanılacağı gösterilmektedir. Bir MVC 4 uygulamasına SignalR ekleyeceksiniz ve ileti göndermek ve görüntülemek için bir sohbet görünümü oluşturmanız gerekir.

## <a name="overview"></a>Genel bakış

Bu öğretici, ASP.NET SignalR ve ASP.NET MVC 4 ile gerçek zamanlı web uygulaması geliştirmeyi sağlar. Öğretici, [SignalR kullanmaya başlama öğreticisi](tutorial-getting-started-with-signalr.md)ile aynı sohbet uygulama kodunu kullanır, ancak bunu Internet şablonuna DAYALı bir MVC 4 uygulamasına eklemeyi gösterir.

Bu konu başlığında aşağıdaki SignalR geliştirme görevlerini öğreneceksiniz:

- SignalR kitaplığı bir MVC 4 uygulamasına ekleniyor.
- İstemcilere içerik göndermek için bir hub sınıfı oluşturma.
- Bir Web sayfasında, iletileri göndermek ve merkezi 'nden güncelleştirme göstermek için SignalR jQuery kitaplığını kullanma.

Aşağıdaki ekran görüntüsünde, bir tarayıcıda çalışan tamamlanmış sohbet uygulaması gösterilmektedir.

![Sohbet örnekleri](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

Başlıklı

- [Projeyi ayarlama](#setup)
- [Örneği çalıştırın](#run)
- [Kodu inceleyin](#code)
- [Sonraki adımlar](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>Projeyi ayarlama

Ön koşullar:

- Visual Studio 2010 SP1, Visual Studio 2012 veya Visual Studio 2012 Express. Visual Studio yoksa, ücretsiz Visual Studio 2012 Express geliştirme aracını almak için [ASP.net İndirmeleri](https://www.asp.net/downloads) bölümüne bakın.
- Visual Studio 2010 için [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)' ü yüklemelisiniz.

Bu bölümde, ASP.NET MVC 4 uygulamasının nasıl oluşturulacağı, SignalR kitaplığının nasıl ekleneceği ve sohbet uygulamasının nasıl oluşturulacağı gösterilmektedir.

1. 1. Visual Studio 'da bir ASP.NET MVC 4 uygulaması oluşturun, SignalRChat olarak adlandırın ve Tamam ' a tıklayın.

        > [!NOTE]
        > VS 2010 ' de çerçeve sürümü açılan denetiminde **.NET Framework 4** ' ü seçin. SignalR kodu 4 ve 4,5 .NET Framework sürümler üzerinde çalışır.

        ![MVC web oluştur](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. Internet uygulaması şablonunu seçin, **birim testi projesi oluşturma**seçeneğini temizleyin ve Tamam ' a tıklayın.

         ![MVC internet sitesi oluştur](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. **Araçlar > NuGet paket yöneticisi > Paket Yöneticisi konsolu** ' nu açın ve aşağıdaki komutu çalıştırın. Bu adım, bir dizi betik dosyası ve SignalR işlevselliğini etkinleştiren derleme başvuruları projesine ekler.

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. **Çözüm Gezgini** betikler klasörünü genişletin. SignalR için betik kitaplıklarının projeye eklendiğini unutmayın.

         ![Kitaplık başvuruları](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. **Çözüm Gezgini**, projeye sağ tıklayın, Ekle ' yi seçin **| Yeni klasör**ve **hub**adlı yeni bir klasör ekleyin.
      6. **Hub** klasörüne sağ tıklayın, Ekle ' ye tıklayın.  **Sınıfını**ve C# **ChatHub.cs**adlı yeni bir sınıf oluşturun. Bu sınıfı, tüm istemcilere ileti gönderen bir SignalR sunucu hub 'ı olarak kullanacaksınız.

> [!NOTE]
> Visual Studio 2012 kullanıyorsanız ve [ASP.NET and Web Tools 2012,2 güncelleştirmesini](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)yüklediyseniz, hub sınıfını oluşturmak Için yeni SignalR öğe şablonunu kullanabilirsiniz. Bunu yapmak için, **hub** klasörüne sağ tıklayın, Ekle ' ye tıklayın.  **Yeni öğe**, **SignalR hub sınıfı (v1)** öğesini seçin ve sınıfı **ChatHub.cs**olarak adlandırın.

1. **ChatHub** sınıfındaki kodu aşağıdaki kodla değiştirin.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. Projenin **Global. asax** dosyasını açın ve `Application_Start` yönteminde kodun ilk satırı olarak `RouteTable.Routes.MapHubs();` yöntemine bir çağrı ekleyin. Bu kod, SignalR hub 'ları için varsayılan yolu kaydeder ve başka yollar kaydedilmeden önce çağrılmalıdır. Tamamlanan `Application_Start` yöntemi aşağıdaki örneğe benzer şekilde görünür.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. **Controllers/HomeController. cs** dosyasında bulunan `HomeController` sınıfını düzenleyin ve aşağıdaki yöntemi sınıfına ekleyin. Bu yöntem, daha sonraki bir adımda oluşturacağınız **sohbet** görünümünü döndürür.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. Yeni oluşturduğunuz `Chat` yönteminin içine sağ tıklayın ve yeni bir görünüm dosyası oluşturmak için **Görünüm Ekle** ' ye tıklayın.
5. **Görünüm Ekle** iletişim kutusunda, **Düzen veya ana sayfa** (diğer onay kutularını temizleyin) kullanmak için onay kutusunun seçili olduğundan emin olun ve ardından **Ekle**' ye tıklayın.

    ![Görünüm ekleme](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. **Chat. cshtml**adlı yeni görünüm dosyasını düzenleyin. &lt;H2&gt; etiketinden sonra, aşağıdaki &lt;div&gt; bölümünü ve `@section scripts` kod bloğunu sayfaya yapıştırın. Bu betik, sayfanın sohbet iletileri göndermesini ve sunucudan ileti görüntülemesini sağlar. Sohbet görünümü için kodun tamamı aşağıdaki kod bloğunda görüntülenir.

    > [!IMPORTANT]
    > Visual Studio projenize SignalR ve diğer betik kitaplıklarını eklediğinizde, Paket Yöneticisi bu konuda gösterilen sürümlerden daha yeni olan betiklerin sürümlerini yükleyebilirsiniz. Kodunuzda betik başvurularının projenizde yüklü olan betik kitaplıklarının sürümleriyle eşleştiğinden emin olun.

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. Projenin **Tümünü kaydedin** .

<a id="run"></a>

## <a name="run-the-sample"></a>Örneği çalıştırın

1. Projeyi hata ayıklama modunda çalıştırmak için F5 tuşuna basın.
2. Tarayıcı adres satırında, **/Home/chat** ' i proje için varsayılan sayfanın URL 'sine ekleyin. Sohbet sayfası bir tarayıcı örneğinde yüklenir ve Kullanıcı adı ister.

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. Bir kullanıcı adı girin.
4. Tarayıcının adres satırındaki URL 'YI kopyalayın ve bu iki tarayıcı örneği açmak için kullanın. Her tarayıcı örneğinde benzersiz bir Kullanıcı adı girin.
5. Her tarayıcı örneğinde bir açıklama ekleyin ve **Gönder**' e tıklayın. Yorumlar Tüm tarayıcı örneklerinde görüntülenmelidir.

    > [!NOTE]
    > Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz. Merkez tüm geçerli kullanıcılara yorum yayınlar. Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.
6. Aşağıdaki ekran görüntüsünde, bir tarayıcıda çalışan sohbet uygulaması gösterilmektedir.

    ![Sohbet tarayıcıları](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. **Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin. Tarayıcınız olarak Internet Explorer kullanıyorsanız, bu düğüm hata ayıklama modunda görünür. SignalR kitaplığının çalışma zamanında dinamik olarak oluşturduğu **Hublar** adlı bir betik dosyası vardır. Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir. Internet Explorer dışında bir tarayıcı kullanıyorsanız, dinamik **hub** dosyasına doğrudan göz atarak da erişebilirsiniz. örneğin, http://mywebsite/signalr/hubs.

    ![Oluşturulan Merkez betiği](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a>Kodu inceleyin

SignalR sohbet uygulaması iki temel SignalR geliştirme görevini gösterir: sunucuda ana düzenleme nesnesi olarak bir hub oluşturma ve ileti göndermek ve almak için SignalR jQuery kitaplığı kullanma.

### <a name="signalr-hubs"></a>SignalR hub 'Ları

Kod örneğinde, **ChatHub** sınıfı **Microsoft. Aspnet. SignalR. hub** sınıfından türetilir. **Hub** sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur. Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve ardından bunları bir Web sayfasındaki jQuery komut dosyalarından çağırarak bu yöntemlere erişebilirsiniz.

Sohbet kodunda, istemciler yeni bir ileti göndermek için **ChatHub. Send** yöntemini çağırır. İçindeki hub, iletileri **istemcileri. ALL. addNewMessageToPage**çağırarak tüm istemcilere gönderir.

**Send** yöntemi çeşitli Merkez kavramlarını gösterir:

- İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.
- Bu hub 'a bağlı tüm istemcilere erişmek için **Microsoft. Aspnet. SignalR. hub. clients** özelliğini kullanın.
- İstemcileri güncelleştirmek için istemcide jQuery işlevini (`addNewMessageToPage` işlevi gibi) çağırın.

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR ve jQuery

Kod örneğindeki **chat. cshtml** görünüm dosyası bir SignalR hub 'ı ile iletişim kurmak Için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir. Koddaki temel görevler, Hub için otomatik olarak oluşturulan ara sunucuya bir başvuru oluşturuyor ve sunucunun istemcilere içerik göndermek için çağırabilir bir işlev bildirmek ve hub 'a ileti göndermek için bir bağlantı başlatmak.

Aşağıdaki kod bir hub için proxy bildirir.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> JQuery içinde, sunucu sınıfına ve üyelerine yönelik başvuru ortası durumunda. Kod örneği, jQuery içindeki C# **ChatHub** sınıfına **ChatHub**olarak başvurur. JQuery 'teki `ChatHub` sınıfına, içinde C#olduğu gibi geleneksel Pascal büyük küçük harf başvurmak istiyorsanız, ChatHub.cs sınıf dosyasını düzenleyin. `Microsoft.AspNet.SignalR.Hubs` ad alanına başvurmak için `using` bir ifade ekleyin. Ardından `HubName` özniteliğini `ChatHub` sınıfına ekleyin, örneğin `[HubName("ChatHub")]`. Son olarak, jQuery başvurunuz `ChatHub` sınıfına güncelleştirin.

Aşağıdaki kod, betikte bir geri çağırma işlevinin nasıl oluşturulacağını gösterir. Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır. `htmlEncode` işlevine yönelik isteğe bağlı çağrı, komut dosyası ekleme işlemini önlemenin bir yolu olarak, ileti içeriğini sayfada görüntülemeden önce, HTML 'ye kodlama yolunu gösterir.

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

Aşağıdaki kod, hub ile bir bağlantının nasıl açılacağını gösterir. Kod bağlantıyı başlatır ve ardından sohbet sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.

> [!NOTE]
> Bu yaklaşım, olay işleyicisi yürütmeden önce bağlantının kurulabilmesini sağlar.

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>Sonraki Adımlar

SignalR 'nin gerçek zamanlı web uygulamaları oluşturmak için bir çerçevede olduğunu öğrendiniz. Ayrıca birkaç SignalR geliştirme görevi öğrendiniz: bir ASP.NET uygulamasına SignalR ekleme, hub sınıfı oluşturma ve hub 'dan ileti gönderme ve alma.

Daha gelişmiş bir SignalR gelişmeleri kavramı hakkında daha fazla bilgi edinmek için, SignalR kaynak kodu ve kaynakları için aşağıdaki siteleri ziyaret edin:

- [SignalR projesi](http://signalr.net)
- [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)
- [SignalR wiki](https://github.com/SignalR/SignalR/wiki)
