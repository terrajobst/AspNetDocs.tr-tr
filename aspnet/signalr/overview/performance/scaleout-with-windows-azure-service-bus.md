---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: SignalR ölçeği Azure Service Bus | Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, bu konunun SignalR 1. x sürümü Için .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri Visual Studio 2013,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579179"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a>Azure Service Bus ile SignalR Ölçeğini Genişletme

, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Bu öğreticide, her rol örneğine ileti dağıtmak için Service Bus arka düzlemi kullanarak bir SignalR uygulamasını bir Windows Azure Web rolüne dağıtacaksınız. ( [Azure App Service Web Apps](https://docs.microsoft.com/azure/app-service-web/)ile Service Bus arka düzlemi de kullanabilirsiniz.)

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

Ön koşullar:

- Bir Windows Azure hesabı.
- [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).
- Visual Studio 2012 veya 2013.

Service Bus geri düzlemi, [Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), sürüm 1,1 Service Bus ile de uyumludur. Ancak, Windows Server için Service Bus sürüm 1,0 ile uyumlu değildir.

## <a name="pricing"></a>Fiyatlandırma

Service Bus arkadüzlemi ileti göndermek için konuları kullanır. En son fiyatlandırma bilgileri için bkz. [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/). Bu yazma sırasında, $1 ' den küçük bir ayda 1.000.000 ileti gönderebilirsiniz. Backdüzlemi, bir SignalR hub yöntemi çağrısı için bir Service Bus iletisi gönderir. Bağlantılar için bazı denetim mesajları de vardır, bağlantıları geri bırakabilir, grupların katılımını ve bu şekilde devam eder. Çoğu uygulamada, ileti trafiğinin büyük bölümü hub yöntemi etkinleştirmeleri olacaktır.

## <a name="overview"></a>Genel bakış

Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.

1. Yeni bir Service Bus ad alanı oluşturmak için Windows Azure portal kullanın.
2. Bu NuGet paketlerini uygulamanıza ekleyin: 

    - [Microsoft. AspNet. SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. Aspnet. SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) veya [Microsoft. Aspnet. SignalR. ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)
3. Bir SignalR uygulaması oluşturun.
4. Geri düzlemi yapılandırmak için Startup.cs 'e aşağıdaki kodu ekleyin: 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

Bu kod, [Topiccount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) ve [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)için varsayılan değerlerle birlikte geri düzlemi yapılandırır. Bu değerleri değiştirme hakkında daha fazla bilgi için bkz. [SignalR performansı: genişleme ölçümleri](signalr-performance.md#scaleout_metrics).

Her uygulama için, "YourAppName" için farklı bir değer seçin. Birden çok uygulama arasında aynı değeri kullanmayın.

## <a name="create-the-azure-services"></a>Azure hizmetlerini oluşturma

[Bulut hizmeti oluşturma ve dağıtma](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)bölümünde açıklandığı gibi bir bulut hizmeti oluşturun. "Nasıl yapılır: hızlı oluşturma kullanarak bulut hizmeti oluşturma" bölümündeki adımları izleyin. Bu öğreticide, bir sertifikayı karşıya yüklemeniz gerekmez.

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

[Service Bus konu/abonelik kullanma](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)bölümünde açıklandığı gibi yeni bir Service Bus ad alanı oluşturun. "Hizmet ad alanı oluşturma" bölümündeki adımları izleyin.

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> Bulut hizmeti ve Service Bus ad alanı için aynı bölgeyi seçtiğinizden emin olun.

## <a name="create-the-visual-studio-project"></a>Visual Studio projesi oluşturma

Visual Studio’yu çalıştırın. **Dosya** menüsünden **Yeni Proje**’ye tıklayın.

**Yeni proje** iletişim kutusunda, **görsel C#** ' i genişletin. **Yüklü şablonlar**altında **bulut** ' u ve ardından **Windows Azure bulut hizmeti**' ni seçin. Varsayılan .NET Framework 4,5 ' i tutun. Uygulamayı ChatService olarak adlandırın ve **Tamam**' a tıklayın.

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

**Yeni Windows Azure bulut hizmeti** iletişim kutusunda ASP.NET Web rolü ' nü seçin. Rolü çözümünüze eklemek için sağ ok düğmesine ( **&gt;** ) tıklayın.

Fareyi yeni rolün üzerine getirin, bu nedenle kurşun kalem simgesi görünür. Rolü yeniden adlandırmak için bu simgeye tıklayın. Rolü "SignalRChat" olarak adlandırın ve **Tamam**' a tıklayın.

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

**Yeni ASP.NET projesi** Iletişim kutusunda **MVC**' yi seçin ve Tamam ' ı tıklatın.

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

Proje Sihirbazı iki proje oluşturur:

- ChatService: Bu proje Windows Azure uygulamasıdır. Azure rollerini ve diğer yapılandırma seçeneklerini tanımlar.
- SignalRChat: Bu proje ASP.NET MVC 5 projem.

## <a name="create-the-signalr-chat-application"></a>SignalR sohbet uygulaması oluşturma

Sohbet uygulamasını oluşturmak için, [SignalR ve MVC 5 Ile çalışmaya](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)başlama öğreticisindeki adımları izleyin.

Gerekli kitaplıkları yüklemek için NuGet kullanın. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. **Paket Yöneticisi konsolu** penceresinde aşağıdaki komutları girin:

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

Paketleri Windows Azure projesi yerine ASP.NET MVC projesine yüklemek için `-ProjectName` seçeneğini kullanın.

## <a name="configure-the-backplane"></a>Arka düzlemi yapılandırma

Uygulamanızın Startup.cs dosyasında aşağıdaki kodu ekleyin:

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

Artık Service Bus Bağlantı dizenizi almanız gerekir. Azure portal, oluşturduğunuz Service Bus ad alanını seçin ve erişim anahtarı simgesine tıklayın.

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

Bağlantı dizesini panoya kopyalayın, ardından *ConnectionString* değişkenine yapıştırın.

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a>Azure’a dağıtma

Çözüm Gezgini ' de, ChatService projesinin içindeki **Roller** klasörünü genişletin.

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

SignalRChat rolüne sağ tıklayın ve **Özellikler**' i seçin. **Yapılandırma** sekmesini seçin. **Örnekler** altında 2 ' yi seçin. VM boyutunu **çok küçük**olarak da ayarlayabilirsiniz.

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

Değişiklikleri kaydedin.

Çözüm Gezgini, ChatService projesine sağ tıklayın. **Yayımla**’yı seçin.

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

Windows Azure 'a ilk kez yayımladıysanız, kimlik bilgilerinizi indirmeniz gerekir. **Yayımla** sihirbazında, "kimlik bilgilerini Indirmek Için oturum aç" a tıklayın. Bu, Windows Azure portal oturum açmanızı ve bir yayımlama ayarları dosyası indirmeyi ister.

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

**Içeri aktar** ' a tıklayın ve indirdiğiniz yayınlama ayarları dosyasını seçin.

**İleri**'ye tıklayın. **Yayımlama ayarları** iletişim kutusunda, **bulut hizmeti**altında, daha önce oluşturduğunuz bulut hizmetini seçin.

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

**Yayımla**’ta tıklayın. Uygulamanın dağıtılması ve VM 'Lerin başlatılması birkaç dakika sürebilir.

Artık sohbet uygulamasını çalıştırdığınızda, rol örnekleri Service Bus bir konu kullanarak Azure Service Bus üzerinden iletişim kurar. Konu başlığı, birden çok aboneye izin veren bir ileti kuyruğu.

Geri düzlemi, konuyu ve abonelikleri otomatik olarak oluşturur. Abonelikler ve ileti etkinliğini görmek için Azure portal açın, Service Bus ad alanını seçin ve "konular" a tıklayın.

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

İleti etkinliğinin panoda gösterilmesi birkaç dakika sürer.

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

SignalR, konu ömrünü yönetir. Uygulamanız dağıtıldığı sürece konuları el ile silmeye veya konudaki ayarları değiştirmeye çalışmayın.

## <a name="troubleshooting"></a>Sorun giderme

**System. InvalidOperationException "desteklenen tek IsolationLevel ' IsolationLevel. Serializable '."**

Bu hata, bir işlemin işlem düzeyi `Serializable`dışında bir değere ayarlanmışsa ortaya çıkabilir. Diğer işlem düzeyleriyle hiçbir işlem gerçekleştirilmediğini doğrulayın.
