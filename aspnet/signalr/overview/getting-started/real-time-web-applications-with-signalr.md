---
uid: signalr/overview/getting-started/real-time-web-applications-with-signalr
title: 'Uygulamalı laboratuvar: SignalR ile gerçek zamanlı web uygulamaları | Microsoft Docs'
author: bradygaster
description: Gerçek zamanlı web uygulamaları, bağlı istemcilere gerçek zamanlı olarak sunucu tarafı içeriği gönderme özelliğini sağlar. ASP.NET geliştiricileri için ASP...
ms.author: bradyg
ms.date: 07/16/2014
ms.assetid: ba07958c-42e1-4da0-81db-ba6925ed6db0
msc.legacyurl: /signalr/overview/getting-started/real-time-web-applications-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 9e39fd3f2fc9d4e791002450085215096c222fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537102"
---
# <a name="hands-on-lab-real-time-web-applications-with-signalr"></a>Uygulamalı Laboratuvar: SignalR ile Gerçek Zamanlı Web Uygulamaları

[Web 'de Camps ekibine](https://twitter.com/webcamps) göre

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[Web Camps eğitim paketini indirin, 2015 Ekim yayını](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)

> Gerçek zamanlı web uygulamaları, bağlı istemcilere gerçek zamanlı olarak sunucu tarafı içeriği gönderme özelliğini sağlar. ASP.NET geliştiricileri için **ASP.NET SignalR** , uygulamalarına gerçek zamanlı Web işlevselliği eklemek için bir kitaplıktır. İstemci ve sunucunun en iyi kullanılabilir taşıması verilen en iyi kullanılabilir aktarımı otomatik olarak seçerek birkaç aktarımdan yararlanır. Tarayıcı ve sunucu arasında çift yönlü iletişime izin veren bir HTML5 API 'SI olan **WebSocket**'ten faydalanır.
> 
> **SignalR** ayrıca, ASP.net uygulamanızda sunucu istemci RPC 'ye (Istemcilerinizdeki JavaScript işlevlerini çağırma) ve bağlantı yönetimi için, bağlanma/bağlantı kesme, gruplama bağlantıları ve yetkilendirme gibi faydalı kancalar ekleme için basit ve yüksek düzey bir API sağlar.
> 
> **SignalR** , istemci ve sunucu arasında gerçek zamanlı çalışma yapmak için gereken aktarımlara göre soyutlamadır. Bir **SignalR** bağlantısı http olarak başlar ve varsa bir **WebSocket** bağlantısına yükseltilir. **WebSocket** , **SignalR**için ideal bir aktarımdır, çünkü sunucu belleğinin en verimli şekilde kullanılmasını sağlar, en düşük gecikme süresine sahiptir ve en temel özelliklere sahiptir (istemci ve sunucu arasında tam çift yönlü iletişim gibi), ancak aynı zamanda en sıkı gereksinimlere sahiptir: **WebSocket** , sunucunun **Windows server 2012** veya **Windows 8**ile birlikte **.NET Framework 4,5**kullanmasını gerektirir. Bu gereksinimler karşılanmazsa, **SignalR** bağlantı yapmak için diğer aktarımları kullanmayı dener ( *Ajax uzun yoklama*gibi).
> 
> **SignalR** API 'si istemciler ve sunucular arasında iletişim kurmak için iki model Içerir: **kalıcı bağlantılar** ve **hub 'lar**. **Bağlantı** , tek alıcı, gruplandırılmış veya yayın iletileri göndermek için basit bir uç noktasını temsil eder. **Hub** , istemci ve sunucunuzun birbirlerine doğrudan Yöntemler çağırmasını sağlayan bağlantı API 'si üzerinde oluşturulmuş daha yüksek düzey bir işlem hattdır.
> 
> ![SignalR mimarisi](real-time-web-applications-with-signalr/_static/image1.png)
> 
> Tüm örnek kod ve kod parçacıkları [https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b](https://github.com/Microsoft-Web/WebCampTrainingKit/releases/tag/v2015.10.13b)adresinden erişilebilen Web Camps eğitim seti, 2015 Ekim sürümüne eklenmiştir.  Lütfen bu sayfadaki yükleyici bağlantısının artık çalışmadığını unutmayın; Bunun yerine varlıklar bölümünde bağlantılardan birini kullanın.

<a id="Overview"></a>
## <a name="overview"></a>Genel bakış

<a id="Objectives"></a>
### <a name="objectives"></a>Amaçlar

Bu uygulamalı laboratuvarda şunları nasıl yapacağınızı öğreneceksiniz:

- SignalR kullanarak sunucudan istemciye bildirim gönderin.
- **SQL Server**kullanarak SignalR uygulamanızı ölçeklendirin.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Önkoşullar

Bu uygulamalı laboratuvarın tamamlanabilmesi için aşağıdakiler gereklidir:

- Web veya daha büyük [için Visual Studio Express 2013](https://www.microsoft.com/visualstudio/)

<a id="Setup"></a>
### <a name="setup"></a>Kurulum

Bu uygulamalı laboratuvarda alýþtýrmalarý çalıştırmak için öncelikle ortamınızı ayarlamanız gerekecektir.

1. Bir Windows Explorer penceresi açın ve laboratuvarın **kaynak** klasörüne gidin.
2. Ortamınızı yapılandıracak ve bu laboratuvar için Visual Studio kod parçacıklarını yükleyecek kurulum işlemini başlatmak için **Setup. cmd** ' ye sağ tıklayın ve **yönetici olarak çalıştır** ' ı seçin.
3. Kullanıcı hesabı denetimi iletişim kutusu gösterilirse, devam etmek için eylemi onaylayın.

> [!NOTE]
> Kurulumu çalıştırmadan önce bu laboratuvarın tüm bağımlılıklarını denetlediğinizden emin olun.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Kod parçacıklarını kullanma

Laboratuvar belgesi boyunca kod blokları eklemeniz istenir. Kolaylık olması için, bu kodun çoğu Visual Studio Code kod parçacığı olarak sağlanır ve bu, el ile ekleme zorunluluğunu ortadan kaldırmak için Visual Studio 2013 içinden erişebilirsiniz.

> [!NOTE]
> Her alıştırma, her alıştırmanın bağımsız olarak her birini takip etmenizi sağlayan alıştırmanın **BEGIN** klasöründe bulunan bir başlangıç çözümüdür. Lütfen bir alıştırma sırasında eklenen kod parçacıklarının bu başlangıç çözümlerinde eksik olduğunu ve Alıştırmayı tamamlayana kadar çalışmadığının farkında olun. Bir alıştırmada kaynak kodun içinde, ilgili alıştırmada adımların tamamlanmasına neden olan koda sahip bir Visual Studio çözümü içeren bir **son** klasör de bulacaksınız. Bu uygulamalı laboratuvarda çalışırken daha fazla yardıma ihtiyacınız varsa bu çözümleri kılavuz olarak kullanabilirsiniz.

---

<a id="Exercises"></a>
## <a name="exercises"></a>Alıştırmalarda

Bu uygulamalı laboratuvar aşağıdaki alıştırmaları içerir:

1. [SignalR kullanarak gerçek zamanlı verilerle çalışma](#Exercise1)
2. [SQL Server kullanarak genişletme](#Exercise2)

Bu Laboratuvarı tamamlamaya yönelik tahmini süre: **60 dakika**

> [!NOTE]
> Visual Studio 'Yu ilk kez başlattığınızda, önceden tanımlanmış ayarlar koleksiyonundan birini seçmeniz gerekir. Her önceden tanımlı koleksiyon, belirli bir geliştirme stiliyle eşleşecek şekilde tasarlanmıştır ve pencere düzenlerini, düzenleyici davranışını, IntelliSense kod parçacıklarını ve iletişim kutusu seçeneklerini belirler. Bu laboratuvardaki yordamlarda, **genel geliştirme ayarları** koleksiyonu kullanılırken, Visual Studio 'da belirli bir görevi gerçekleştirmek için gereken eylemler açıklanır. Geliştirme ortamınız için farklı bir ayarlar koleksiyonu seçerseniz, adımlarda dikkate almanız gereken adımlarda farklılıklar olabilir.

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-real-time-data-using-signalr"></a>Alıştırma 1: SignalR kullanarak gerçek zamanlı verilerle çalışma

Sohbet genellikle örnek olarak kullanıldığında, gerçek zamanlı web işlevselliğiyle çok daha fazlasını yapabilirsiniz. Bir Kullanıcı yeni verileri görmek için bir Web sayfasını yenilediğinde veya yeni verileri almak için AJAX uzun yoklamayı uygularsa, SignalR kullanabilirsiniz.

SignalR, **sunucu gönderme** veya **yayınlama** işlevlerini destekler; bağlantı yönetimini otomatik olarak işler. İstemci-sunucu iletişimi için klasik HTTP bağlantılarında, her istek için bağlantı yeniden oluşturulur, ancak SignalR istemci ile sunucu arasında kalıcı bağlantı sağlar. SignalR 'de sunucu kodu, Bugün öğrendiğimiz istek-yanıt modeli yerine uzak yordam çağrılarını (RPC) kullanarak tarayıcıda istemci koduna çağrı yapılır.

Bu alıştırmada, tüm sayfayı yenilemeye gerek kalmadan, Istatistik panosunu güncelleştirilmiş ölçümlerle birlikte göstermek için **Geek test** uygulamasını bir SignalR kullanacak şekilde yapılandıracaksınız.

<a id="Ex1Task1"></a>
#### <a name="task-1--exploring-the-geek-quiz-statistics-page"></a>Görev 1 – Geek test Istatistikleri sayfasını keşfetme

Bu görevde, uygulamayı ilertirecek ve istatistik sayfasının nasıl görüntülendiğini ve bilgilerin güncelleştirilme şeklini nasıl geliştirebileceğinizi doğrulayacaksınız.

1. **Web için Visual Studio Express 2013** ' i açın ve **Source\Ex1-WorkingWithRealTimeData\Begin** klasöründe bulunan **geektest. sln** çözümünü açın.
2. Çözümü çalıştırmak için **F5** tuşuna basın. **Oturum açma** sayfası tarayıcıda görünmelidir.

    ![Çözümü çalıştırma](real-time-web-applications-with-signalr/_static/image2.png "Çözümü çalıştırma")

    *Çözümü çalıştırma*
3. Uygulamada yeni bir kullanıcı oluşturmak için sayfanın sağ üst köşesindeki **Kaydet** ' e tıklayın.

    ![Bağlantıyı Kaydet](real-time-web-applications-with-signalr/_static/image3.png "Bağlantıyı Kaydet")

    *Bağlantıyı Kaydet*
4. **Kaydet** sayfasında, bir **Kullanıcı adı** ve **parola**girin ve ardından **Kaydet**' e tıklayın.

    ![Kullanıcı kaydetme](real-time-web-applications-with-signalr/_static/image4.png "Kullanıcı kaydetme")

    *Kullanıcı kaydetme*
5. Uygulama yeni hesabı kaydeder ve kullanıcının kimliği doğrulanır ve ilk test sorusunu gösteren giriş sayfasına yeniden yönlendirilir.
6. **İstatistikler** sayfasını yeni bir pencerede açın ve **giriş** sayfası ve **İstatistikler** sayfasını yan yana yerleştirin.

    ![Yan yana Windows](real-time-web-applications-with-signalr/_static/image5.png "Yan yana pencereler")

    *Yan yana Windows*
7. **Giriş** sayfasında, seçeneklerden birine tıklayarak soruyu yanıtlayın.

    ![Soru yanıt verme](real-time-web-applications-with-signalr/_static/image6.png "Soru yanıt verme")

    *Soru yanıt verme*
8. Düğmelerden birine tıkladıktan sonra yanıt görüntülenmelidir.

    ![Soru yanıt doğru](real-time-web-applications-with-signalr/_static/image7.png "Soru yanıt doğru")

    *Soru doğru yanıtlandı*
9. Istatistikler sayfasında belirtilen bilgilerin güncel olmadığına dikkat edin. Güncelleştirilmiş sonuçları görmek için sayfayı yenileyin.

    ![İstatistikler sayfası](real-time-web-applications-with-signalr/_static/image8.png "İstatistikler sayfası")

    *İstatistikler sayfası*
10. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurun.

<a id="Ex1Task2"></a>
#### <a name="task-2--adding-signalr-to-geek-quiz-to-show-online-charts"></a>Görev 2 – çevrimiçi grafikleri göstermek için SignalR to Geek sınavını ekleme

Bu görevde, çözüme bir SignalR ekler ve sunucuya yeni bir yanıt gönderildiğinde güncelleştirmeleri otomatik olarak istemcilere gönderebilirsiniz.

1. Visual Studio 'daki **Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' na tıklayın.
2. **Paket Yöneticisi konsolu** penceresinde aşağıdaki komutu yürütün:

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample1.ps1)]

    ![SignalR paketi yüklemesi](real-time-web-applications-with-signalr/_static/image9.png "SignalR paketi yüklemesi")

    *SignalR paketi yüklemesi*

   > [!NOTE]
   > **SignalR** NuGet paketleri sürüm 2.0.2 'i yenı bir MVC 5 uygulamasından yüklerken, SignalR 'yi yüklemeden önce **owın** paketlerini (veya üzeri) sürüm 2.0.1'i el ile güncelleştirmeniz gerekir. Bunu yapmak için, **Paket Yöneticisi konsolunda**aşağıdaki betiği çalıştırabilirsiniz:
   > 
   > [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample2.ps1)]
   > 
   > SignalR 'nin gelecekteki bir sürümünde OWIN bağımlılıkları otomatik olarak güncelleştirilir.
3. **Çözüm Gezgini**, **betikler** klasörünü genişletin ve SignalR *js* dosyalarının çözüme eklendiğinden emin olun.

    ![SignalR JavaScript başvuruları](real-time-web-applications-with-signalr/_static/image10.png "SignalR JavaScript başvuruları")

    *SignalR JavaScript başvuruları*
4. **Çözüm Gezgini**, **geektest** projesine sağ tıklayın, | **Yeni klasör** **Ekle** ' yi seçin ve BT **hub**'ını adlandırın.
5. **Hub** klasörüne sağ tıklayın ve Ekle | ' yi seçin.  **Yeni öğe**.

    ![Yeni öğe Ekle](real-time-web-applications-with-signalr/_static/image11.png "Yeni öğe Ekle")

    *Yeni öğe Ekle*
6. **Yeni öğe Ekle** Iletişim kutusunda  **C# görseli seçin | Web | SignalR** düğümü sol bölmede, orta bölmeden **SignalR hub sınıfı (v2)** öğesini seçin, dosyayı **StatisticsHub.cs** olarak adlandırın ve **Ekle**' ye tıklayın.

    ![Yeni öğe Ekle iletişim kutusu](real-time-web-applications-with-signalr/_static/image12.png "Yeni öğe Ekle iletişim kutusu")

    *Yeni öğe Ekle iletişim kutusu*
7. **Statisticshub** sınıfındaki kodu aşağıdaki kodla değiştirin.

    (Kod parçacığı- *RealTimeSignalR-Ex1-StatisticsHubClass*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample3.cs)]
8. **Startup.cs** ' i açın ve **yapılandırma** yönteminin sonuna aşağıdaki satırı ekleyin.

    (Kod parçacığı- *RealTimeSignalR-Ex1-MapSignalR*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample4.cs)]
9. **Hizmetler** klasörünün içindeki **StatisticsService.cs** sayfasını açın ve aşağıdaki using yönergelerini ekleyin.

    (Kod parçacığı- *RealTimeSignalR-Ex1-Usingyönergeleri*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample5.cs)]
10. Güncelleştirmelerin bağlı istemcilerini bilgilendirmek için, önce geçerli bağlantı için bir **bağlam** nesnesi alırsınız. **Hub** nesnesi, tek bir istemciye ileti gönderme veya tüm bağlı istemcilere yayımlama yöntemlerini içerir. İstatistik verilerini yayınlamak için aşağıdaki yöntemi **Statisticsservice** sınıfına ekleyin.

    (Kod parçacığı- *RealTimeSignalR-Ex1-NotifyUpdatesMethod*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample6.cs)]

    > [!NOTE]
    > Yukarıdaki kodda, istemcideki bir işlevi çağırmak için rastgele bir yöntem adı kullanıyorsunuz (yani: *UpdateStatistics*). Belirttiğiniz Yöntem adı dinamik bir nesne olarak yorumlanır, yani bunun için IntelliSense veya derleme zamanı doğrulaması yoktur. İfade çalışma zamanında değerlendirilir. Yöntem çağrısı yürütüldüğünde, SignalR, yöntem adını ve parametre değerlerini istemciye gönderir. İstemcinin adıyla eşleşen bir yöntemi varsa, bu yöntem çağrılır ve parametre değerleri kendisine geçirilir. İstemcide eşleşen bir yöntem bulunamazsa, hiçbir hata oluşturulmaz. Daha fazla bilgi için [ASP.NET SignalR hub 'LARı API Kılavuzu](../guide-to-the-api/hubs-api-guide-server.md)' na bakın.
11. **Denetleyiciler** klasörünün içindeki **TriviaController.cs** sayfasını açın ve aşağıdaki using yönergelerini ekleyin.

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample7.cs)]
12. Aşağıdaki Vurgulanan kodu **Post** ACTION yöntemine ekleyin.

    (Kod parçacığı- *RealTimeSignalR-Ex1-NotifyUpdatesCall*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample8.cs)]
13. Görünümler içindeki **Statistics. cshtml** sayfasını açın **| Giriş** klasörü. **Betikler** bölümünü bulun ve bölümün başında aşağıdaki komut dosyası başvurularını ekleyin.

    (Kod parçacığı- *RealTimeSignalR-Ex1-SignalRScriptReferences*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample9.cshtml)]

    > [!NOTE]
    > Visual Studio projenize SignalR ve diğer betik kitaplıklarını eklediğinizde Paket Yöneticisi, bu konuda gösterilen sürümden daha yeni bir SignalR betik dosyası sürümü kurabilir. Kodunuzda betik başvurusunun projenizde yüklü olan betik kitaplığının sürümüyle eşleştiğinden emin olun.
14. İstemciyi SignalR hub 'ına bağlamak ve hub 'dan yeni bir ileti alındığında istatistik verilerini güncelleştirmek için aşağıdaki vurgulanmış kodu ekleyin.

    (Kod parçacığı- *RealTimeSignalR-Ex1-SignalRClientCode*)

    [!code-cshtml[Main](real-time-web-applications-with-signalr/samples/sample10.cshtml)]

    Bu kodda, bir hub proxy oluşturuyorsunuz ve sunucu tarafından gönderilen iletileri dinlemek için bir olay işleyicisi kaydediliyor. Bu durumda, *UpdateStatistics* yöntemiyle gönderilen iletileri dinler.

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>Görev 3 – çözümü çalıştırma

Bu görevde, yeni bir soru Yanıtlandıktan sonra istatistik görünümünün SignalR kullanılarak otomatik olarak güncelleştirildiğini doğrulamak için çözümü çalıştıracaksınız.

1. Çözümü çalıştırmak için **F5** tuşuna basın.

    > [!NOTE]
    > Zaten uygulamada oturum açmamışsa, görev 1 ' de oluşturduğunuz kullanıcıyla oturum açın.
2. **İstatistikler** sayfasını yeni bir pencerede açın ve **giriş** sayfası ve **İstatistikler** sayfasını görev 1 ' de yaptığınız gibi yan yana yerleştirin.
3. **Giriş** sayfasında, seçeneklerden birine tıklayarak soruyu yanıtlayın.

    ![Başka bir soruyu yanıtlama](real-time-web-applications-with-signalr/_static/image13.png "Başka bir soruyu yanıtlama")

    *Başka bir soruyu yanıtlama*
4. Düğmelerden birine tıkladıktan sonra yanıt görüntülenmelidir. Sayfadaki Istatistik bilgilerinin, tüm sayfayı yenilemeye gerek kalmadan, güncelleştirilmiş bilgilerle soru Yanıtlandıktan sonra otomatik olarak güncelleştirildiğini unutmayın.

    ![İstatistikler sayfası, yanıt sonrasında yenilendi](real-time-web-applications-with-signalr/_static/image14.png "İstatistikler sayfası, yanıt sonrasında yenilendi")

    *İstatistikler sayfası, yanıt sonrasında yenilendi*

<a id="Exercise2"></a>
### <a name="exercise-2-scaling-out-using-sql-server"></a>Alıştırma 2: SQL Server kullanarak genişletme

Bir Web uygulamasını ölçeklendirirken, genellikle *ölçeği artırma* ve *genişletme* seçenekleri arasından seçim yapabilirsiniz. *Ölçeği artırma* , daha fazla kaynak (CPU, RAM, vb.) ile daha büyük bir sunucu kullanarak yükü işlemek için daha fazla sunucu *ekleme anlamına gelir* . İkincisi ile ilgili sorun, istemcilerin farklı sunuculara yönlendirilmesidir. Bir sunucuya bağlı olan istemci, başka bir sunucudan gönderilen iletileri almaz.

Bu sorunları, iletileri sunucular arasında iletmek için *backdüzlemi*adlı bir bileşen kullanarak çözebilirsiniz. Bir sırt etkin olduğunda, her bir uygulama örneği geri düzleme iletiler gönderir ve geri düzlemi bunları diğer uygulama örneklerine iletir.

SignalR için şu anda üç tür arka düzlem vardır:

- **Windows Azure Service Bus**. Service Bus, bileşenlerin gevşek olarak bağlanmış iletiler göndermesini sağlayan bir mesajlaşma altyapısıdır.
- **SQL Server**. SQL Server arka düzlemi, iletileri SQL tablolarına yazar. Geri düzlemi verimli mesajlaşma için Hizmet Aracısı kullanır. Ancak, Hizmet Aracısı etkinleştirilmemişse da bu da işe yarar.
- **Redsıs**. Redsıs, bellek içi anahtar-değer deposudur. Redsıs, ileti göndermek için bir yayımla/abone ol ("pub/Sub") modelini destekler.

Her ileti bir ileti veri yolu aracılığıyla gönderilir. İleti veri yolu, yayımlama/abone olma soyutlaması sağlayan [IMessageBus](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.imessagebus(v=vs.100).aspx) arabirimini uygular. Arka düzlemler, varsayılan **IMessageBus 'ı** bu geri düzlemi için tasarlanan bir veri yolu ile değiştirerek çalışır.

Her sunucu örneği, veri yolu aracılığıyla geri düzleme bağlanır. Bir ileti gönderildiğinde, geri düzlemi ' ne gider ve geri düzlemi onu her sunucuya gönderir. Bir sunucu arkadüzleden bir ileti aldığında, iletiyi yerel önbelleğinde depolar. Sunucu daha sonra istemcilere yerel önbelleğinden iletiler gönderir.

SignalR geri düzlemi 'nin nasıl çalıştığı hakkında daha fazla bilgi için bu [makaleyi](../performance/scaleout-in-signalr.md)okuyun.

> [!NOTE]
> Bir geri düzlemin performans sorunlarına neden olduğu bazı senaryolar vardır. Tipik bir SignalR senaryosu aşağıda verilmiştir:
> 
> - [Sunucu yayını](tutorial-server-broadcast-with-signalr.md) (örneğin, hisse senedi bandı): sunucu iletilerin gönderilme hızını denetlemediğinden, bu senaryo Için geri düzler iyi çalışır.
> - [İstemciden istemciye](tutorial-getting-started-with-signalr.md) (ör. sohbet): Bu senaryoda, iletilerin sayısı istemci sayısıyla ölçeklenirken, arka uç bir performans sorunu olabilir; diğer bir deyişle, daha fazla istemci katılırken ileti hızının orantılı olarak büyümesi.
> - [Yüksek frekanslı gerçek zamanlı](tutorial-high-frequency-realtime-with-signalr.md) (örn. gerçek zamanlı Oyunlar): Bu senaryo için bir geri düzlem önerilmez.

Bu alıştırmada, iletileri **Geek test** uygulaması üzerinden dağıtmak için **SQL Server** kullanacaksınız. Yapılandırmayı ayarlamayı öğrenmek için bu görevleri tek bir test makinesinde çalıştıracaksınız, ancak tüm etkiyi almak için, SignalR uygulamasını iki veya daha fazla sunucuya dağıtmanız gerekir. Ayrıca, sunuculardan birine veya ayrı bir adanmış sunucuya SQL Server de yüklemelisiniz.

![SQL Server diyagramı kullanarak ölçeği genişletme](real-time-web-applications-with-signalr/_static/image15.png)

<a id="Ex2Task1"></a>
#### <a name="task-1---understanding-the-scenario"></a>Görev 1-senaryoyu anlama

Bu görevde, yerel makinenizde birden çok IIS örneğinin benzetimini yaparken, **Geek sınavın** 2 örneğini çalıştıracaksınız. Bu senaryoda, bir uygulamadaki sorular aracılığıyla yanıt verme sırasında, ikinci örneğin istatistik sayfasında güncelleştirmeye bildirilmez. Bu benzetim, uygulamanızın birden çok örneğe dağıtıldığı ve onlarla iletişim kurmak için bir yük dengeleyici kullanıldığı bir ortama benzer.

1. **Kaynak/EX2-ScalingOutWithSQLServer/Begin** klasöründe bulunan **BEGIN. sln** çözümünü açın. Yüklendikten sonra, çözümün aynı yapılar, ancak farklı adlara sahip iki proje olduğunu **Sunucu Gezgini** görürsünüz. Bu, yerel makinenizde aynı uygulamanın iki örneğini çalıştırmanın benzetimini yapar.

    ![Çözüme başla Geek sınavın 2 örnek benzetimi](real-time-web-applications-with-signalr/_static/image16.png "Çözüme başla Geek sınavın 2 örnek benzetimi")

    *Çözüme başla Geek sınavın 2 örnek benzetimi*
2. Çözüm düğümüne sağ tıklayıp **Özellikler**' i seçerek çözümün Özellikler sayfasını açın. **Başlangıç projesi**altında **birden çok başlangıç** projesi seçin ve her Iki proje Için de **eylem** değerini *başlatılacak*şekilde değiştirin.

    ![Birden çok proje başlatılıyor](real-time-web-applications-with-signalr/_static/image17.png "Birden çok proje başlatılıyor")

    *Birden çok proje başlatılıyor*
3. Çözümü çalıştırmak için **F5** tuşuna basın. Uygulama, farklı bağlantı noktalarında aynı uygulamanın birden fazla örneğini taklit eden iki **Geek test** örneğini başlatır. Sol taraftaki tarayıcıların birini ekranın sağ tarafında sabitleyin. Kimlik bilgilerinizle oturum açın veya yeni bir Kullanıcı kaydedin. Oturum açtıktan sonra, Üçlü sayfayı sola tutun ve sağdaki tarayıcıdaki **İstatistikler** sayfasına gidin.

    ![Yan yana Geek test](real-time-web-applications-with-signalr/_static/image18.png)

    *Yan yana Geek test*

    ![Farklı bağlantı noktalarında Geek test](real-time-web-applications-with-signalr/_static/image19.png)

    *Farklı bağlantı noktalarında Geek test*
4. Sol tarayıcıda sorularınızı yanıtlamayı başlatın ve doğru tarayıcıda **istatistik** sayfasının güncelleştirilmediğini fark edeceksiniz. Bunun nedeni, **SignalR** 'nin istemcilerine iletileri dağıtmak için yerel bir önbellek kullanması ve bu senaryonun birden çok örneği benzetiğinden, önbelleğin aralarında paylaşılmaması nedeniyle oluşur. Aynı adımları test ederek ve tek bir uygulama kullanarak **SignalR** 'nin çalıştığını doğrulayabilirsiniz. Aşağıdaki görevlerde, iletileri örnekler arasında çoğaltmak için bir arka düzlem yapılandıracaksınız.
5. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurun.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-sql-server-backplane"></a>Görev 2 – SQL Server arka düzlemi oluşturma

Bu görevde, **Geek test** uygulaması için bir arka düzlem olarak kullanılacak bir veritabanı oluşturacaksınız. **SQL Server Nesne Gezgini** kullanarak sunucunuza gözatıp veritabanını başlatabilirsiniz. Ayrıca, **Hizmet Aracısı**etkinleştirecektir.

1. **Visual Studio**'Da menü **görünümü** ' nü açın ve **SQL Server Nesne Gezgini**' yi seçin.
2. **SQL Server** düğümüne sağ tıklayıp **SQL Server Ekle...** seçeneğini belirleyerek LocalDB örneğinizi bağlayın.

    ![SQL Server örneği ekleme](real-time-web-applications-with-signalr/_static/image20.png "SQL Server örneği ekleme")

    *SQL Server Nesne Gezgini SQL Server örnek ekleme*
3. **Sunucu adını** *(LocalDB) \v11.0* olarak ayarlayın ve **Windows kimlik doğrulamasını** kimlik doğrulama modu olarak bırakın. Devam etmek için **Bağlan**’a tıklayın.

    ![LocalDB 'ye bağlanma](real-time-web-applications-with-signalr/_static/image21.png "LocalDB 'ye bağlanma")

    *LocalDB 'ye bağlanma*
4. LocalDB örneğinize bağlı olduğunuza göre, SignalR için SQL Server geri düzlemi temsil edecek bir veritabanı oluşturmanız gerekir. Bunu yapmak için **veritabanları** düğümüne sağ tıklayın ve **Yeni veritabanı Ekle**' yi seçin.

    ![Yeni veritabanı ekleme](real-time-web-applications-with-signalr/_static/image22.png "Yeni veritabanı ekleme")

    *Yeni veritabanı ekleme*
5. Veritabanı adını *SignalR* olarak ayarlayın ve **Tamam** ' a tıklayarak oluşturun.

    ![SignalR veritabanı oluşturma](real-time-web-applications-with-signalr/_static/image23.png "SignalR veritabanı oluşturma")

    *SignalR veritabanı oluşturma*

    > [!NOTE]
    > Veritabanı için herhangi bir ad seçebilirsiniz.
6. Güncelleştirmeleri geri düzlemden daha verimli bir şekilde almak için, veritabanı için Hizmet Aracısı etkinleştirmeniz önerilir. Hizmet Aracısı, SQL Server mesajlaşma ve kuyruğa alma için yerel destek sağlar. Arka düzlem Hizmet Aracısı olmadan da kullanılabilir. Veritabanına sağ tıklayıp **Yeni sorgu**' yı seçerek yeni bir sorgu açın.

    ![Yeni bir sorgu açılıyor](real-time-web-applications-with-signalr/_static/image24.png "Yeni bir sorgu açılıyor")

    *Yeni bir sorgu açılıyor*
7. Hizmet Aracısı etkinleştirilip etkinleştirilmediğini denetlemek için **sys. databases** katalog görünümündeki **\_Broker\_etkin** sütununu sorgulayın. Son açılan sorgu penceresinde aşağıdaki betiği yürütün.

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample11.sql)]

    ![Hizmet Aracısı durumu sorgulanıyor](real-time-web-applications-with-signalr/_static/image25.png "Hizmet Aracısı durumu sorgulanıyor")

    *Hizmet Aracısı durumu sorgulanıyor*
8. Veritabanınızdaki **\_broker\_etkin** sütununun değeri &quot;0&quot;ise, etkinleştirmek için aşağıdaki komutu kullanın. Veritabanı **&gt;&lt;** , veritabanını oluştururken ayarladığınız adla değiştirin (örn. SignalR).

    [!code-sql[Main](real-time-web-applications-with-signalr/samples/sample12.sql)]

    ![Hizmet Aracısı etkinleştiriliyor](real-time-web-applications-with-signalr/_static/image26.png "Hizmet Aracısı etkinleştiriliyor")

    *Hizmet Aracısı etkinleştiriliyor*

    > [!NOTE]
    > Bu sorgu kilitlenme olarak görünüyorsa, VERITABANıNA bağlı bir uygulama olmadığından emin olun.

<a id="Ex2Task3"></a>
#### <a name="task-3--configuring-the-signalr-application"></a>Görev 3 – SignalR uygulamasını yapılandırma

Bu görevde, **Geek sınavını** SQL Server arka düzleme bağlanacak şekilde yapılandıracaksınız. Önce **SignalR. SqlServer** NuGet paketini ekleyecek ve bağlantı dizesini arka düzlem veritabanınıza ayarlayacaksınız.

1. **NuGet paket yöneticisi** > **Araçlar** ' dan **Paket Yöneticisi konsolunu** açın. **Varsayılan proje** açılan listesinde **geektest** projesinin seçildiğinden emin olun. **Microsoft. Aspnet. SignalR. SqlServer** NuGet paketini yüklemek için aşağıdaki komutu yazın.

    [!code-powershell[Main](real-time-web-applications-with-signalr/samples/sample13.ps1)]
2. Project **GeekQuiz2**için önceki adımı, ancak bu kez tekrarlayın.
3. SQL Server geri düzlemi yapılandırmak için, **Geektest** projesinin **Startup.cs** dosyasını açın ve **Configure** yöntemine aşağıdaki kodu ekleyin. **&lt;-veritabanı&gt;** , SQL Server geri düzlemi oluştururken kullandığınız veritabanı adınızla değiştirin. **GeekQuiz2** projesi için bu adımı tekrarlayın.

    (Kod parçacığı- *RealTimeSignalR-EX2-StartupConfiguration*)

    [!code-csharp[Main](real-time-web-applications-with-signalr/samples/sample14.cs)]
4. Her iki proje de SQL Server arkadüzlemi kullanacak şekilde yapılandırıldığına göre, bunları aynı anda çalıştırmak için **F5** tuşuna basın.
5. **Visual Studio** , farklı bağlantı noktalarında **Geek sınavın** iki örneğini başlatır. Sol taraftaki tarayıcılardan birini ekranın sağ tarafında sabitleyin ve kimlik bilgilerinizle oturum açın. Sol taraftaki sayfayı sola tutun ve sağ tarayıcıda **İstatistikler** sayfasına gidin.
6. Sol tarayıcıda sorularınızı yanıtlamayı başlatın. Bu kez, **istatistik** sayfası, geri düzlemi için teşekkürler. Uygulamalar arasında geçiş yapın (**İstatistikler** artık sol **tarafta bulunur ve en sağda** bulunur) ve her iki örnek için çalıştığını doğrulamak için test yinelenir. Biriktirme listesi, her bağlı sunucu için paylaşılan bir ileti *önbelleği* görevi görür ve her sunucu, bağlı istemcilere dağıtmak üzere iletileri kendi yerel önbelleğinde depolar.
7. Visual Studio 'ya geri dönün ve hata ayıklamayı durdurun.
8. SQL Server backdüzlemi bileşeni, belirtilen veritabanında gerekli tabloları otomatik olarak oluşturur. **SQL Server Nesne Gezgini** panelinde, geri düzlemi (ör. SignalR) için oluşturduğunuz veritabanını açın ve tabloları genişletin. Aşağıdaki tabloları görmeniz gerekir:

    ![Arka düzlem tarafından oluşturulan tablolar](real-time-web-applications-with-signalr/_static/image27.png)

    *Arka düzlem tarafından oluşturulan tablolar*
9. **SignalR. Messages\_0** tablosuna sağ tıklayın ve **verileri görüntüle**' yi seçin.

    ![SignalR geri düzlemi Iletileri tablosunu görüntüle](real-time-web-applications-with-signalr/_static/image28.png)

    *SignalR geri düzlemi Iletileri tablosunu görüntüle*
10. Gidiş ile soruları yanıtlarken **hub** 'a gönderilen farklı iletileri görebilirsiniz. Geri düzlemi, bu iletileri herhangi bir bağlı örneğe dağıtır.

    ![Backuçak Iletileri tablosu](real-time-web-applications-with-signalr/_static/image29.png)

    *Backuçak Iletileri tablosu*

---

<a id="Summary"></a>
## <a name="summary"></a>Özet

Bu uygulamalı laboratuvarda, uygulamanıza **SignalR** ekleme ve **hub 'ları**kullanarak sunucudan bağlı istemcilerinize bildirim gönderme hakkında bilgiler edindiniz. Ayrıca, uygulamanız birden fazla IIS örneğine dağıtıldığında bir *backdüzlemi* bileşeni kullanarak uygulamanızı nasıl ölçeklendirebilirsiniz.
