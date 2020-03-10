---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 'Öğretici: SignalR 1. x ile çalışmaya başlama | Microsoft Docs'
author: bradygaster
description: Bir HTML sayfasında gerçek zamanlı bir sohbet uygulaması oluşturmak için ASP.NET SignalR kullanın.
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623545"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a>Öğretici: SignalR 1.x ile Çalışmaya Başlama

, [Patrick Fleti](https://github.com/pfletcher), [Tim teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu öğreticide SignalR kullanarak gerçek zamanlı bir sohbet uygulaması oluşturma işlemi gösterilir. SignalR 'i boş bir ASP.NET Web uygulamasına ekleyecek ve ileti göndermek ve göstermek için bir HTML sayfası oluşturmanız gerekir.

## <a name="overview"></a>Genel bakış

Bu öğretici, basit bir tarayıcı tabanlı sohbet uygulamasının nasıl oluşturulduğunu göstererek SignalR geliştirmeyi tanıtır. SignalR kitaplığını boş bir ASP.NET Web uygulamasına ekleyecek, istemcilere ileti göndermek için bir hub sınıfı oluşturacak ve kullanıcıların sohbet iletilerini göndermesini ve almasına imkan tanıyan bir HTML sayfası oluşturmanız gerekir. MVC 4 ' te MVC görünümü kullanarak bir sohbet uygulamasının nasıl oluşturulduğunu gösteren benzer bir öğretici için bkz. [SignalR ve MVC 4 Ile çalışmaya](index.md)başlama.

> [!NOTE]
> Bu öğretici, SignalR 'nin sürüm (1. x) sürümünü kullanır. SignalR 1. x ve 2,0 arasındaki değişikliklerle ilgili ayrıntılar için bkz. [SignalR 1. x projelerini yükseltme](../releases/upgrading-signalr-1x-projects-to-20.md).

SignalR, canlı Kullanıcı etkileşimi veya gerçek zamanlı veri güncelleştirmeleri gerektiren Web uygulamaları oluşturmaya yönelik açık kaynaklı bir .NET kitaplığıdır. Sosyal uygulamalar, çok kullanıcılı Oyunlar, iş birliği ve Haberler, hava durumu veya finans güncelleştirme uygulamaları buna örnek olarak verilebilir. Bunlar genellikle gerçek zamanlı uygulamalar olarak adlandırılır.

SignalR gerçek zamanlı uygulamalar oluşturma sürecini basitleştirir. İstemci-sunucu bağlantılarını yönetmeyi kolaylaştırmak ve istemcilere içerik güncelleştirmelerini göndermek için bir ASP.NET sunucu kitaplığı ve bir JavaScript istemci kitaplığı içerir. SignalR kitaplığını mevcut bir ASP.NET uygulamasına ekleyerek gerçek zamanlı işlevselliği elde edebilirsiniz.

Öğreticide aşağıdaki SignalR geliştirme görevleri gösterilmektedir:

- SignalR kitaplığını bir ASP.NET Web uygulamasına ekleme.
- İstemcilere içerik göndermek için bir hub sınıfı oluşturma.
- Bir Web sayfasında, iletileri göndermek ve merkezi 'nden güncelleştirme göstermek için SignalR jQuery kitaplığını kullanma.

Aşağıdaki ekran görüntüsünde, bir tarayıcıda çalışan sohbet uygulaması gösterilmektedir. Her yeni kullanıcı yorum gönderebilir ve Kullanıcı sohbete katıldıktan sonra eklenen açıklamaları görebilir.

![Sohbet örnekleri](tutorial-getting-started-with-signalr/_static/image1.png)

Başlıklı

- [Projeyi ayarlama](#setup)
- [Örneği çalıştırın](#run)
- [Kodu inceleyin](#code)
- [Sonraki adımlar](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>Projeyi ayarlama

Bu bölümde, boş bir ASP.NET Web uygulaması oluşturma, SignalR ekleme ve sohbet uygulaması oluşturma işlemlerinin nasıl yapılacağı gösterilmektedir.

Ön koşullar:

- Visual Studio 2010 SP1 veya 2012. Visual Studio yoksa, ücretsiz Visual Studio 2012 Express geliştirme aracını almak için [ASP.net İndirmeleri](https://www.asp.net/downloads) bölümüne bakın.
- [Microsoft ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=279941). Visual Studio 2012 için, bu yükleyici, SignalR şablonları dahil olmak üzere Visual Studio 'ya yeni ASP.NET özellikleri ekler. Visual Studio 2010 SP1 için bir yükleyici yoktur, ancak kurulum adımlarında açıklandığı gibi SignalR NuGet paketini yükleyerek öğreticiyi tamamlayabilirsiniz.

Aşağıdaki adımlarda, ASP.NET boş bir Web uygulaması oluşturmak ve SignalR kitaplığını eklemek için Visual Studio 2012 kullanılır:

1. Visual Studio 'da ASP.NET boş bir Web uygulaması oluşturun.

    ![Boş Web oluştur](tutorial-getting-started-with-signalr/_static/image2.png)
2. Araçlar 'ı seçerek **Paket Yöneticisi konsolunu** açın **| NuGet Paket Yöneticisi | Paket Yöneticisi konsolu**. Konsol penceresine aşağıdaki komutu girin:

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    Bu komut, SignalR 1. x ' in en son sürümünü yüklenir.
3. **Çözüm Gezgini**, projeye sağ tıklayın, Ekle ' yi seçin **| Sınıf**. Yeni sınıfı **ChatHub**olarak adlandırın.
4. **Çözüm Gezgini** betikler düğümünü genişletin. JQuery ve SignalR için betik kitaplıkları projede görülebilir.

    ![Kitaplık başvuruları](tutorial-getting-started-with-signalr/_static/image3.png)
5. **ChatHub** sınıfındaki kodu aşağıdaki kodla değiştirin.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. **Çözüm Gezgini**, projeye sağ tıklayın ve ardından Ekle ' ye tıklayın **| Yeni öğe**. **Yeni öğe Ekle** Iletişim kutusunda **genel uygulama sınıfı** ' nı seçin ve **Ekle**' ye tıklayın.

    ![Genel Ekle](tutorial-getting-started-with-signalr/_static/image4.png)
7. Global.asax.cs sınıfında, belirtilen `using` deyimlerden sonra aşağıdaki `using` deyimlerini ekleyin.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. SignalR hub 'larının varsayılan yolunu kaydetmek için genel sınıfın `Application_Start` metoduna aşağıdaki kod satırını ekleyin.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. **Çözüm Gezgini**, projeye sağ tıklayın ve ardından Ekle ' ye tıklayın **| Yeni öğe**. **Yeni öğe Ekle** Iletişim kutusunda HTML sayfası ' nı seçin ve **Ekle**' ye tıklayın.
10. **Çözüm Gezgini**' de, yenı oluşturduğunuz HTML sayfasına sağ tıklayın ve **Başlangıç sayfası olarak ayarla**' ya tıklayın.
11. HTML sayfasındaki varsayılan kodu aşağıdaki kodla değiştirin.

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. Projenin **Tümünü kaydedin** .

<a id="run"></a>

## <a name="run-the-sample"></a>Örneği çalıştırın

1. Projeyi hata ayıklama modunda çalıştırmak için F5 tuşuna basın. HTML sayfası bir tarayıcı örneğinde yüklenir ve Kullanıcı adı ister.

    ![Kullanıcı adını girin](tutorial-getting-started-with-signalr/_static/image5.png)
2. Bir kullanıcı adı girin.
3. Tarayıcının adres satırındaki URL 'YI kopyalayın ve bu iki tarayıcı örneği açmak için kullanın. Her tarayıcı örneğinde benzersiz bir Kullanıcı adı girin.
4. Her tarayıcı örneğinde bir açıklama ekleyin ve **Gönder**' e tıklayın. Yorumlar Tüm tarayıcı örneklerinde görüntülenmelidir.

    > [!NOTE]
    > Bu basit sohbet uygulaması, sunucuda tartışma bağlamını korumaz. Merkez tüm geçerli kullanıcılara yorum yayınlar. Daha sonra sohbete katılması olan kullanıcılar, bu kişilerin eklendiği zamandan eklenen iletileri görür.

    Aşağıdaki ekran görüntüsünde, hepsi bir örnek ileti gönderdiğinde güncellenen üç tarayıcı örneğinde çalışan sohbet uygulaması gösterilmektedir:

    ![Sohbet tarayıcıları](tutorial-getting-started-with-signalr/_static/image6.png)
5. **Çözüm Gezgini**, çalışan uygulamanın **komut dosyası belgeleri** düğümünü inceleyin. SignalR kitaplığının çalışma zamanında dinamik olarak oluşturduğu **Hublar** adlı bir betik dosyası vardır. Bu dosya jQuery betiği ile sunucu tarafı kodu arasındaki iletişimi yönetir.

    ![Oluşturulan Merkez betiği](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a>Kodu inceleyin

SignalR sohbet uygulaması iki temel SignalR geliştirme görevini gösterir: sunucuda ana düzenleme nesnesi olarak bir hub oluşturma ve ileti göndermek ve almak için SignalR jQuery kitaplığı kullanma.

### <a name="signalr-hubs"></a>SignalR hub 'Ları

Kod örneğinde, **ChatHub** sınıfı **Microsoft. Aspnet. SignalR. hub** sınıfından türetilir. **Hub** sınıfından türetmek, bir SignalR uygulaması oluşturmanın kullanışlı bir yoludur. Hub sınıfınız üzerinde ortak Yöntemler oluşturabilir ve ardından bunları bir Web sayfasındaki jQuery komut dosyalarından çağırarak bu yöntemlere erişebilirsiniz.

Sohbet kodunda, istemciler yeni bir ileti göndermek için **ChatHub. Send** yöntemini çağırır. İçindeki hub, iletileri **istemciler. ALL. Yayıniletisi**çağırarak tüm istemcilere gönderir.

**Send** yöntemi çeşitli Merkez kavramlarını gösterir:

- İstemcilerin bunları çağırabilmesi için ortak yöntemleri bir hub üzerinde bildirin.
- Bu hub 'a bağlı tüm istemcilere erişmek için **Microsoft. Aspnet. SignalR. hub. clients** dinamik özelliğini kullanın.
- İstemcileri güncelleştirmek için istemcide jQuery işlevini (`broadcastMessage` işlevi gibi) çağırın.

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR ve jQuery

Kod örneğindeki HTML sayfası, SignalR hub 'ı ile iletişim kurmak için SignalR jQuery kitaplığını nasıl kullanacağınızı gösterir. Koddaki temel görevler, hub 'a başvurmak için bir proxy bildiriyor, sunucunun istemcilere içerik göndermek için çağırabilir bir işlev bildiriyor ve hub 'a ileti gönderecek bir bağlantı başlatıyor.

Aşağıdaki kod bir hub için proxy bildirir.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> JQuery içinde, sunucu sınıfına ve üyelerine yönelik başvuru ortası durumunda. Kod örneği, jQuery içindeki C# **ChatHub** sınıfına **ChatHub**olarak başvurur.

Aşağıdaki kod, komut dosyasında bir geri çağırma işlevi oluşturma işlemi. Sunucu üzerindeki hub sınıfı, içerik güncelleştirmelerini her bir istemciye göndermek için bu işlevi çağırır. HTML 'nin içeriği görüntülemeden önce kodladığı iki satır isteğe bağlıdır ve betik ekleme işlemini önlemenin basit bir yolunu gösterir.

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

Aşağıdaki kod, hub ile bir bağlantının nasıl açılacağını gösterir. Kod bağlantıyı başlatır ve sonra HTML sayfasındaki **Gönder** düğmesine tıklama olayını işlemek için bir işlev geçirir.

> [!NOTE]
> Bu yaklaşım, bağlantının olay işleyicisi yürütmeden önce yöntem.

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>Sonraki Adımlar

SignalR 'nin gerçek zamanlı web uygulamaları oluşturmak için bir çerçevede olduğunu öğrendiniz. Ayrıca birkaç SignalR geliştirme görevi öğrendiniz: bir ASP.NET uygulamasına SignalR ekleme, hub sınıfı oluşturma ve hub 'dan ileti gönderme ve alma.

Bu öğreticide veya diğer SignalR uygulamalarında örnek uygulamayı bir barındırma sağlayıcısına dağıtarak Internet üzerinden kullanılabilir hale getirebilirsiniz. Microsoft, ücretsiz bir [Windows Azure deneme hesabında](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)en fazla 10 Web sitesi için ücretsiz web barındırma hizmeti sunar. Örnek SignalR uygulamasını dağıtma hakkında yönergeler için bkz. [SignalR Başlarken örneğini bir Windows Azure Web sitesi olarak yayımlama](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx). Bir Visual Studio Web projesinin bir Windows Azure Web sitesine nasıl dağıtılacağı hakkında ayrıntılı bilgi için, bkz. [Windows Azure Web sitesine bir ASP.NET uygulaması dağıtma](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet). (Not: WebSocket aktarımı Şu anda Microsoft Azure Web siteleri için desteklenmiyor. WebSocket taşıması kullanılabilir olmadığında, SignalR, [SignalR 'ye Giriş konusunun](index.md)aktarımlar bölümünde açıklandığı gibi diğer kullanılabilir taşımaları kullanır.)

Daha gelişmiş bir SignalR gelişmeleri kavramı hakkında daha fazla bilgi edinmek için, SignalR kaynak kodu ve kaynakları için aşağıdaki siteleri ziyaret edin:

- [SignalR projesi](http://signalr.net)
- [SignalR GitHub ve örnekleri](https://github.com/SignalR/SignalR)
- [SignalR wiki](https://github.com/SignalR/SignalR/wiki)
