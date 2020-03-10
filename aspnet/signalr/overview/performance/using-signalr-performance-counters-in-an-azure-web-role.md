---
uid: signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
title: Azure Web rolünde SignalR performans sayaçlarını kullanma | Microsoft Docs
author: guardrex
description: Azure Web rolünde SignalR performans sayaçlarını yüklemek ve kullanmak.
keywords: ASP. NET, SignalR, performans sayacı, Azure Web rolü
ms.author: bradyg
ms.date: 10/03/2018
ms.assetid: 2a127d3b-21ed-4cc9-bec0-cdab4e742a25
msc.legacyurl: /signalr/overview/performance/using-signalr-performance-counters-in-an-azure-web-role
msc.type: authoredcontent
ms.openlocfilehash: 969a2ce43a7cb8d649555daf282f900401c0c914
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578983"
---
# <a name="using-signalr-performance-counters-in-an-azure-web-role"></a>Azure Web rolünde SignalR performans sayaçlarını kullanma

[Luke Latham](https://github.com/guardrex) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

SignalR performans sayaçları, uygulamanızın performansını bir Azure Web rolünde izlemek için kullanılır. Sayaçlar Microsoft Azure Tanılama tarafından yakalanır. Azure 'da SignalR performans sayaçlarını, tek başına veya şirket içi uygulamalar için kullanılan aynı araç olan *SignalR. exe*ile birlikte yüklersiniz. Azure rolleri geçici olduğundan, bir uygulamayı başlangıçtan sonra SignalR performans sayaçlarını yükleyecek ve kaydedecek şekilde yapılandırırsınız.

## <a name="prerequisites"></a>Önkoşullar

* Visual Studio 2015 veya [2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
* [Visual Studio için MICROSOFT Azure SDK](https://azure.microsoft.com/downloads/) 'sı **: SDK 'yı yükledikten sonra makinenizi yeniden başlatın.**
* Microsoft Azure abonelik: ücretsiz bir Azure deneme hesabına kaydolmak Için bkz. [Azure Ücretsiz deneme](https://azure.microsoft.com/free/).

## <a name="creating-an-azure-web-role-application-that-exposes-signalr-performance-counters"></a>SignalR performans sayaçlarını kullanıma sunan bir Azure Web rolü uygulaması oluşturma

1. Visual Studio'yu açın.

2. Visual Studio 'da **dosya** > **Yeni** > **Proje**' yi seçin.

3. **Yeni proje** iletişim kutusunda, sol taraftaki **Visual C#**  > **bulut** kategorisini seçin ve ardından **Azure bulut hizmeti** şablonunu seçin. Uygulamayı **Signalrperfcounters** olarak adlandırın ve **Tamam**' ı seçin.

   ![Yeni bulut uygulaması](using-signalr-performance-counters-in-an-azure-web-role/_static/image1.png)

   > [!NOTE]
   > **Bulut** şablonu kategorisini veya **Azure bulut hizmeti** şablonunu görmüyorsanız, Visual Studio 2017 için **Azure geliştirme** iş yükünü yüklemeniz gerekir. Visual Studio Yükleyicisi açmak için **Yeni proje** iletişim kutusunun sol alt tarafındaki **Visual Studio yükleyicisi aç** bağlantısını seçin. **Azure geliştirme** iş yükünü seçin ve sonra iş yükünü yüklemeye başlamak için **Değiştir** ' i seçin.
   >
   > ![Visual Studio Yükleyicisi Azure geliştirme iş yükü](using-signalr-performance-counters-in-an-azure-web-role/_static/azure-development-workload.png)

4. **Yeni Microsoft Azure bulut hizmeti** iletişim kutusunda **ASP.NET Web rolü** ' nü seçin ve rolü projeye eklemek için > düğmesini seçin. **Tamam**’ı seçin.

   ![ASP.NET Web rolü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image2.png)

5. **Yeni ASP.NET Web uygulaması-WebRole1** Iletişim kutusunda **MVC** şablonunu seçin ve ardından **Tamam**' ı seçin.

   ![MVC ve Web API 'SI ekleme](using-signalr-performance-counters-in-an-azure-web-role/_static/image3.png)

6. **Çözüm Gezgini**' de, **WebRole1**altında *Diagnostics. wadcfgx* dosyasını açın.

   ![Çözüm Gezgini Diagnostics. wadcfgx](using-signalr-performance-counters-in-an-azure-web-role/_static/image4.png)

7. Dosyanın içeriğini aşağıdaki yapılandırmayla değiştirin ve dosyayı kaydedin:

   [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample1.xml)]

8. **NuGet paket yöneticisi** > **Araçlar** ' dan **Paket Yöneticisi konsolunu** açın. SignalR 'nin en son sürümünü ve SignalR yardımcı programları paketini yüklemek için aşağıdaki komutları girin:

   [!code-powershell[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample2.ps1)]

9. Uygulamayı başlatıldığında veya geri dönüştürüldüğünde, SignalR performans sayaçlarını rol örneğine yükleyecek şekilde yapılandırın. **Çözüm Gezgini**, **WebRole1** projesine sağ tıklayın ve > **Yeni klasör** **Ekle** ' yi seçin. Yeni klasör *başlangıcını*adlandırın.

   ![Başlangıç klasörü Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image5.png)

10. *SignalR. exe* dosyasını ( **Microsoft. Aspnet. SignalR. utils** paketi ile eklendi) \<projesi klasöründen kopyalayın >/SignalRPerfCounters/Packages/Microsoft.Aspnet.SignalR.utils. önceki adımda oluşturduğunuz *Başlangıç* klasörü için sürüm >/tools\<.

11. **Çözüm Gezgini**, *Başlangıç* klasörüne sağ tıklayın ve > **var olan öğeyi** **Ekle** ' yi seçin. Görüntülenen iletişim kutusunda *SignalR. exe* ' yi seçin ve **Ekle**' yi seçin.

    ![SignalR. exe ' yi projeye Ekle](using-signalr-performance-counters-in-an-azure-web-role/_static/image6.png)

12. Oluşturduğunuz *Başlangıç* klasörüne sağ tıklayın.  > **Yeni öğe** **Ekle** ' yi seçin. **Genel** düğümünü seçin, **metin dosyası**' nı seçin ve yeni öğe *signalrperfcounterınstall. cmd*olarak adlandırın. Bu komut dosyası, SignalR performans sayaçlarını Web rolüne yükler.

    ![SignalR performans sayacı yüklemesi toplu iş dosyası oluşturma](using-signalr-performance-counters-in-an-azure-web-role/_static/image7.png)

13. Visual Studio, *Signalrperfcounterınstall. cmd* dosyasını oluşturduğunda ana pencerede otomatik olarak açılır. Dosyanın içeriğini aşağıdaki komut dosyasıyla değiştirin, sonra dosyayı kaydedip kapatın. Bu betik, SignalR performans sayaçlarını rol örneğine ekleyen *SignalR. exe*' yi yürütür.

    [!code-console[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample3.cmd)]

14. **Çözüm Gezgini**'da *SignalR. exe* dosyasını seçin. Dosyanın **özelliklerinde**, **her zaman kopyalamak**için **Çıkış Dizinine Kopyala** ' yı ayarlayın.

    ![Her zaman kopyalamak için çıkış dizinine Kopyala ayarla](using-signalr-performance-counters-in-an-azure-web-role/_static/image8.png)

15. *Signalrperfcounterınstall. cmd* dosyası için önceki adımı tekrarlayın.

16. *Signalrperfcounterınstall. cmd* dosyasına sağ tıklayın ve **birlikte Aç**' ı seçin. Görüntülenen iletişim kutusunda **Ikili düzenleyici** ' yi seçin ve **Tamam**' ı seçin.

    ![Ikili düzenleyiciyle aç](using-signalr-performance-counters-in-an-azure-web-role/_static/image9.png)

17. İkili düzenleyicide, dosyadaki önde gelen baytları seçin ve silin. Dosyayı kaydedin ve kapatın.

    ![Baştaki baytları Sil](using-signalr-performance-counters-in-an-azure-web-role/_static/image10.png)

18. *ServiceDefinition. csdef* ' i açın ve hizmet başlatıldığında *Signalrperfcounterınstall. cmd* dosyasını yürüten bir başlangıç görevi ekleyin:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample4.xml?highlight=4-7)]

19. `Views/Shared/_Layout.cshtml` açın ve dosya sonundan jQuery paket betiğini kaldırın.

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample5.cshtml)]

20. Sunucuda `increment` yöntemi sürekli çağıran bir JavaScript istemcisi ekleyin. `Views/Home/Index.cshtml` açın ve içeriği şu kodla değiştirin:

    [!code-cshtml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample6.cshtml)]

21. **WebRole1** projesinde *hub 'lar*adlı yeni bir klasör oluşturun. **Çözüm Gezgini** *hub* klasörüne sağ tıklayın ve > **Yeni öğe** **Ekle** ' yi seçin. **Yeni öğe Ekle** iletişim kutusunda, **Web** > **SignalR** kategorisini seçin ve ardından **SignalR hub sınıfı (v2)** öğe şablonunu seçin. Yeni hub *MyHub.cs* ' ı adlandırın ve **Ekle**' yi seçin.

    ![SignalR hub sınıfı yeni öğe Ekle iletişim kutusunda hub klasörüne ekleniyor](using-signalr-performance-counters-in-an-azure-web-role/_static/image13.png)

22. *MyHub.cs* , ana pencerede otomatik olarak açılır. İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample7.cs)]

23. *[Crank. exe](signalr-connection-density-testing-with-crank.md)* , SignalR kod temeli ile birlikte sunulan bir bağlantı yoğunluğu test aracıdır. Crank kalıcı bir bağlantı gerektirdiğinden, test ederken kullanmak için sitenize bir tane ekleyin. **WebRole1** projesine *Persistentconnections*adlı yeni bir klasör ekleyin. Bu klasöre sağ tıklayın ve > sınıfı **Ekle** 'yi seçin. Yeni sınıf dosyasını *MyPersistentConnections.cs* olarak adlandırın ve **Ekle**' yi seçin.

24. Visual Studio, *MyPersistentConnections.cs* dosyasını ana pencerede açar. İçeriği aşağıdaki kodla değiştirin, sonra dosyayı kaydedip kapatın:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample8.cs)]

25. `Startup` sınıfını kullanarak, OWıN başlatıldığında SignalR nesneleri başlatılır. *Startup.cs* açın veya oluşturun ve içeriğini şu kodla değiştirin:

    [!code-csharp[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample9.cs)]

    Yukarıdaki kodda `OwinStartup` özniteliği, OWıN 'u başlatmak için bu sınıfı işaretler. `Configuration` yöntemi SignalR 'yi başlatır.

26. **F5**tuşuna basarak Microsoft Azure öykünücüsü uygulamanızı test edin.

    > [!NOTE]
    > **Mapsignalr**'de bir **FileLoadException** ile karşılaşırsanız, *Web. config* dosyasındaki bağlama yeniden yönlendirmelerini aşağıdaki şekilde değiştirin:

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample12.xml?highlight=3,7)]

27. Bir dakika bekleyin. Visual Studio 'da Cloud Explorer araç penceresini açın ( > **bulut Gezginini** **görüntüleyin** ) ve yolu `(Local)/Storage Accounts/(Development)/Tables`genişletin. **WADPerformanceCountersTable**çift tıklayın. Tablo verilerinde SignalR sayaçlarını görmeniz gerekir. Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir. Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.

    ![Visual Studio Cloud Explorer 'da WAD performans sayaçları tablosunu seçme](using-signalr-performance-counters-in-an-azure-web-role/_static/image11.png)

    ![WAD performans sayaçları tablosunda toplanan sayaçları gösterme](using-signalr-performance-counters-in-an-azure-web-role/_static/image12.png)

28. Uygulamanızı bulutta test etmek için, **ServiceConfiguration. Cloud. cscfg** dosyasını güncelleştirin ve `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` geçerli bir Azure depolama hesabı bağlantı dizesi olarak ayarlayın.

    [!code-xml[Main](using-signalr-performance-counters-in-an-azure-web-role/samples/sample10.xml)]

29. Uygulamayı Azure aboneliğinize dağıtın. Bir uygulamayı Azure 'a dağıtma hakkında ayrıntılı bilgi için bkz. [bulut hizmeti oluşturma ve dağıtma](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).

30. Birkaç dakika bekleyin. **Cloud Explorer**'da, yukarıda yapılandırdığınız depolama hesabını bulun ve içinde `WADPerformanceCountersTable` tablosunu bulun. Tablo verilerinde SignalR sayaçlarını görmeniz gerekir. Tabloyu görmüyorsanız, Azure depolama kimlik bilgilerinizi yeniden girmeniz gerekebilir. Tabloyu **Cloud Explorer** 'da görmek için **Yenile** düğmesini seçmeniz veya tablodaki verileri görmek Için tablo aç penceresindeki **Yenile** düğmesini seçmeniz gerekebilir.

Bu öğreticide kullanılan özgün içerik için özel [Marrichard](https://social.msdn.microsoft.com/profile/Martin+Richard) 'e teşekkür ederiz.
