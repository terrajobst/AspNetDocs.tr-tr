---
uid: signalr/overview/performance/scaleout-with-sql-server
title: SignalR ölçeği SQL Server | Microsoft Docs
author: bradygaster
description: Bu konuda kullanılan yazılım sürümleri, .NET 4,5 SignalR sürüm 2 ' nin önceki sürümleri hakkında bilgi Için bu konunun önceki sürümlerini Visual Studio 2013...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579186"
---
# <a name="signalr-scaleout-with-sql-server"></a>SQL Server ile SignalR Ölçeğini Genişletme

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

Bu öğreticide, iki ayrı IIS örneğine dağıtılan bir SignalR uygulamasına ileti dağıtmak için SQL Server kullanacaksınız. Bu öğreticiyi tek bir test makinesinde da çalıştırabilirsiniz, ancak tüm etkiyi almak için, SignalR uygulamasını iki veya daha fazla sunucuya dağıtmanız gerekir. Ayrıca, sunuculardan birine veya ayrı bir adanmış sunucuya SQL Server de yüklemelisiniz. Diğer bir seçenek ise Azure 'da VM 'Leri kullanarak öğreticiyi çalıştıradır.

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a>Önkoşullar

Microsoft SQL Server 2005 veya üzeri. Arka düzlem SQL Server hem masaüstü hem de sunucu sürümlerini destekler. SQL Server Compact Edition veya Azure SQL veritabanı 'nı desteklemez. (Uygulamanız Azure üzerinde barındırılıyorsa, bunun yerine Service Bus geri düzlemi göz önünde bulundurun.)

## <a name="overview"></a>Genel bakış

Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.

1. Yeni boş bir veritabanı oluşturun. Geri düzlemi bu veritabanında gerekli tabloları oluşturacaktır.
2. Bu NuGet paketlerini uygulamanıza ekleyin:

    - [Microsoft. AspNet. SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. AspNet. SignalR. SqlServer](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. Bir SignalR uygulaması oluşturun.
4. Geri düzlemi yapılandırmak için Startup.cs 'e aşağıdaki kodu ekleyin:

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   Bu kod, geri düzlemi [Tablecount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) ve [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)için varsayılan değerlerle yapılandırır. Bu değerleri değiştirme hakkında daha fazla bilgi için bkz. [SignalR performansı: genişleme ölçümleri](signalr-performance.md#scaleout_metrics).

## <a name="configure-the-database"></a>Veritabanını yapılandırma

Uygulamanın, veritabanına erişmek için Windows kimlik doğrulaması veya SQL Server kimlik doğrulaması kullanıp kullanmayacağını belirleyin. Ne olursa olsun, veritabanı kullanıcısının oturum açma, şema oluşturma ve tablo oluşturma izinlerine sahip olduğundan emin olun.

Kullanılacak geri düzlemi için yeni bir veritabanı oluşturun. Veritabanına bir ad verebilirsiniz. Veritabanında herhangi bir tablo oluşturmanız gerekmez; geri düzlemi gerekli tabloları oluşturacaktır.

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a>Hizmet Aracısı etkinleştir

Arka düzme veritabanı için Hizmet Aracısı etkinleştirilmesi önerilir. Hizmet Aracısı, arka düzlemi güncelleştirmeleri daha verimli bir şekilde almasına olanak sağlayan SQL Server ileti ve kuyruğa alma için yerel destek sağlar. (Ancak, geri düzlem Hizmet Aracısı olmadan da kullanılabilir.)

Hizmet Aracısı etkinleştirilip etkinleştirilmediğini denetlemek için **sys. databases** katalog görünümündeki **\_Broker\_etkin** sütununu sorgulayın.

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

Hizmet Aracısı etkinleştirmek için aşağıdaki SQL sorgusunu kullanın:

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> Bu sorgu kilitlenme olarak görünüyorsa, VERITABANıNA bağlı bir uygulama olmadığından emin olun.

İzlemeyi etkinleştirdiyseniz, izlemeler Hizmet Aracısı etkinleştirilip etkinleştirilmediğini de gösterir.

## <a name="create-a-signalr-application"></a>SignalR uygulaması oluşturma

Bu öğreticilerden birini izleyerek bir SignalR uygulaması oluşturun:

- [SignalR 2,0 ile çalışmaya başlama](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR 2,0 ve MVC 5 ile çalışmaya başlama](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

Daha sonra, SQL Server ile ölçeği desteklemek için sohbet uygulamasını değiştireceksiniz. İlk olarak, SignalR. SqlServer NuGet paketini projenize ekleyin. Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

Sonra, Startup.cs dosyasını açın. **Yapılandırma** yöntemine aşağıdaki kodu ekleyin:

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a>Uygulamayı dağıtma ve çalıştırma

SignalR uygulamasını dağıtmak için Windows Server örneklerinizi hazırlayın.

IIS rolünü ekleyin. WebSocket protokolü de dahil olmak üzere "uygulama geliştirme" özellikleri ekleyin.

![](scaleout-with-sql-server/_static/image4.png)

Ayrıca yönetim hizmetini de ("Yönetim Araçları" altında listelenmiştir) içerir.

![](scaleout-with-sql-server/_static/image5.png)

**Web Dağıtımı 3,0 ' ü yükler.** IIS Yöneticisi 'Ni çalıştırdığınızda, Microsoft Web platformu yüklemenizi ister veya [yükleyiciyi indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=255386). Platform yükleyicisinde Web Dağıtımı arayın ve Web Dağıtımı 3,0 ' i yükleme

![](scaleout-with-sql-server/_static/image6.png)

Web yönetimi hizmetinin çalıştığından emin olun. Aksi takdirde, hizmeti başlatın. (Windows hizmetleri listesinde Web yönetimi hizmetini görmüyorsanız, IIS rolünü eklediğinizde Yönetim hizmetini yüklediğinizden emin olun.)

Son olarak, TCP için 8172 numaralı bağlantı noktasını açın. Bu, Web Dağıtımı aracının kullandığı bağlantı noktasıdır.

Artık Visual Studio projesini geliştirme makinenizden sunucuya dağıtmaya hazırsınız. Çözüm Gezgini, çözüme sağ tıklayın ve **Yayımla**' ya tıklayın.

Web dağıtımı hakkında daha ayrıntılı belgeler için bkz. [Visual Studio Için Web dağıtımı Içerik Haritası ve ASP.net](../../../whitepapers/aspnet-web-deployment-content-map.md).

Uygulamayı iki sunucuya dağıtırsanız, her bir örneği ayrı bir tarayıcı penceresinde açabilir ve bunların her birinin birinden SignalR iletileri aldıklarından emin olabilirsiniz. (Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına ait olacaktır.)

![](scaleout-with-sql-server/_static/image7.png)

Uygulamayı çalıştırdıktan sonra, SignalR 'nin veritabanında otomatik olarak tablo oluşturduğunu görebilirsiniz:

![](scaleout-with-sql-server/_static/image8.png)

SignalR tabloları yönetir. Uygulamanız dağıtıldığı sürece satırları silmeyin, tabloyu değiştirmez ve benzeri.
