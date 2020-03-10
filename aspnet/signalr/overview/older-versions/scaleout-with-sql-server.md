---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: SignalR ölçeği SQL Server (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536472"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a>SQL Server ile SignalR Ölçeğini Genişletme (SignalR 1.x)

, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

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
4. Geri düzlemi yapılandırmak için aşağıdaki kodu Global. asax öğesine ekleyin: 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

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

- [SignalR ile çalışmaya başlama](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR ve MVC 4 ile çalışmaya başlama](tutorial-getting-started-with-signalr-and-mvc-4.md)

Daha sonra, SQL Server ile ölçeği desteklemek için sohbet uygulamasını değiştireceksiniz. İlk olarak, SignalR. SqlServer NuGet paketini projenize ekleyin. Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

Ardından, Global. asax dosyasını açın. Aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:

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
