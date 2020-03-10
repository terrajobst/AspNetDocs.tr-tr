---
uid: signalr/overview/older-versions/scaleout-with-redis
title: Redsıs ile SignalR ölçeğini genişletme (SignalR 1. x) | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536563"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a>Redis ile SignalR Ölçeğini Genişletme (SignalR 1.x)

, [Mike Ison](https://github.com/MikeWasson), [Patrick fleti](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Bu öğreticide, iki ayrı IIS örneğine dağıtılan bir SignalR uygulamasına ileti dağıtmak için [redsıs](http://redis.io/) ' i kullanacaksınız.

Redsıs, bellek içi anahtar-değer deposudur. Ayrıca, Yayımla/abone ol modeliyle bir mesajlaşma sistemini destekler. SignalR redin backdüzlemi, iletileri diğer sunuculara iletmek için pub/Sub özelliğini kullanır.

![](scaleout-with-redis/_static/image1.png)

Bu öğretici için üç sunucu kullanacaksınız:

- Bir SignalR uygulamasını dağıtmak için kullanacağınız Windows çalıştıran iki sunucu.
- Redo 'u çalıştırmak için kullanacağınız Linux çalıştıran bir sunucu. Bu öğreticideki ekran görüntüleri için Ubuntu 12,04 TLS kullandım.

Kullanabileceğiniz üç fiziksel sunucunuz yoksa, Hyper-V ' d e sanal makineler oluşturabilirsiniz. Diğer bir seçenek de Azure 'da VM oluşturmaktır.

Bu öğretici resmi redin uygulamasını kullanmasına karşın, MSOpenTech ' [ın bir Windows bağlantı noktası](https://github.com/MSOpenTech/redis) da vardır. Kurulum ve yapılandırma farklıdır, ancak başka bir adım aynı şekilde yapılır.

> [!NOTE] 
> 
> Redsıs ile SignalR ölçeği, Redsıs kümelerini desteklemez.

## <a name="overview"></a>Genel bakış

Ayrıntılı öğreticiye girmeden önce, ne yapabileceğinize ilişkin hızlı bir genel bakış sunulmaktadır.

1. Redsıs 'i yükleyip Redsıs sunucusunu başlatın.
2. Bu NuGet paketlerini uygulamanıza ekleyin: 

    - [Microsoft. AspNet. SignalR](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [Microsoft. AspNet. SignalR. Redsıs](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. Bir SignalR uygulaması oluşturun.
4. Geri düzlemi yapılandırmak için aşağıdaki kodu Global. asax öğesine ekleyin: 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a>Hyper-V üzerinde Ubuntu

Windows Hyper-V ' d i kullanarak Windows Server 'da kolayca bir Ubuntu VM oluşturabilirsiniz.

[http://www.ubuntu.com](http://www.ubuntu.com/)'Den Ubuntu ISO dosyasını indirin.

Hyper-V ' d a yeni bir VM ekleyin. **Sanal sabit diski bağla** adımında, **sanal sabit disk oluştur**' u seçin.

![](scaleout-with-redis/_static/image2.png)

**Yükleme seçenekleri** adımında, **görüntü dosyası (. iso)** seçeneğini belirleyin, **Araştır**' a tıklayın ve Ubuntu yükleme ISO dosyasına gidin.

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a>Redsıs 'yi Install

Redsıs 'yi indirmek ve derlemek için [http://redis.io/download](http://redis.io/download) bölümündeki adımları izleyin.

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

Bu, `src` dizininde Redsıs ikililerini oluşturur.

Varsayılan olarak redin parola gerektirmez. Bir parola ayarlamak için, kaynak kodun kök dizininde bulunan `redis.conf` dosyasını düzenleyin. (Düzenlemeden önce dosyanın yedek kopyasını oluşturun!) `redis.conf`için aşağıdaki yönergeyi ekleyin:

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

Şimdi Redsıs sunucusunu başlatın:

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

Redin dinlediği varsayılan bağlantı noktası olan 6379 numaralı bağlantı noktasını açın. (Yapılandırma dosyasındaki bağlantı noktası numarasını değiştirebilirsiniz.)

## <a name="create-the-signalr-application"></a>SignalR uygulamasını oluşturma

Bu öğreticilerden birini izleyerek bir SignalR uygulaması oluşturun:

- [SignalR ile çalışmaya başlama](../getting-started/tutorial-getting-started-with-signalr.md)
- [SignalR ve MVC 4 ile çalışmaya başlama](tutorial-getting-started-with-signalr-and-mvc-4.md)

Daha sonra, sohbet uygulamasını Redsıs ile ölçeği destekleyecek şekilde değiştireceksiniz. İlk olarak, projenize SignalR. Redsıs NuGet paketini ekleyin. Visual Studio 'da, **Araçlar** menüsünden **NuGet Paket Yöneticisi**' ni ve ardından **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

Ardından, Global. asax dosyasını açın. Aşağıdaki kodu **uygulama\_başlangıç** yöntemine ekleyin:

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- "sunucu" Reddir çalıştıran sunucunun adıdır.
- *bağlantı* noktası numarası bağlantı noktasıdır
- "Password" redsıs. conf dosyasında tanımladığınız paroladır.
- "AppName" herhangi bir dizedir. SignalR, bu adla bir Redsıs pub/Sub kanalı oluşturur.

Örneğin:

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a>Uygulamayı dağıtma ve çalıştırma

SignalR uygulamasını dağıtmak için Windows Server örneklerinizi hazırlayın.

IIS rolünü ekleyin. WebSocket protokolü de dahil olmak üzere "uygulama geliştirme" özellikleri ekleyin.

![](scaleout-with-redis/_static/image5.png)

Ayrıca yönetim hizmetini de ("Yönetim Araçları" altında listelenmiştir) içerir.

![](scaleout-with-redis/_static/image6.png)

**Web Dağıtımı 3,0 ' ü yükler.** IIS Yöneticisi 'Ni çalıştırdığınızda, Microsoft Web platformu yüklemenizi ister veya [yükleyiciyi indirebilirsiniz](https://go.microsoft.com/fwlink/?LinkId=255386). Platform yükleyicisinde Web Dağıtımı arayın ve Web Dağıtımı 3,0 ' i yükleme

![](scaleout-with-redis/_static/image7.png)

Web yönetimi hizmetinin çalıştığından emin olun. Aksi takdirde, hizmeti başlatın. (Windows hizmetleri listesinde Web yönetimi hizmetini görmüyorsanız, IIS rolünü eklediğinizde Yönetim hizmetini yüklediğinizden emin olun.)

Varsayılan olarak, Web yönetimi hizmeti TCP bağlantı noktası 8172 ' i dinler. Windows Güvenlik Duvarı 'nda 8172 numaralı bağlantı noktasında TCP trafiğine izin vermek için yeni bir gelen kuralı oluşturun. Daha fazla bilgi için bkz. [güvenlik duvarı kurallarını yapılandırma](https://technet.microsoft.com/library/dd448559(WS.10).aspx). (VM 'Leri Azure 'da barındırıyorsanız, bunu doğrudan Azure portal yapabilirsiniz. Bkz. [sanal makineye uç noktaları ayarlama](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)

Artık Visual Studio projesini geliştirme makinenizden sunucuya dağıtmaya hazırsınız. Çözüm Gezgini, çözüme sağ tıklayın ve **Yayımla**' ya tıklayın.

Web dağıtımı hakkında daha ayrıntılı belgeler için bkz. [Visual Studio Için Web dağıtımı Içerik Haritası ve ASP.net](../../../whitepapers/aspnet-web-deployment-content-map.md).

Uygulamayı iki sunucuya dağıtırsanız, her bir örneği ayrı bir tarayıcı penceresinde açabilir ve bunların her birinin birinden SignalR iletileri aldıklarından emin olabilirsiniz. (Kuşkusuz, bir üretim ortamında, iki sunucu bir yük dengeleyicinin arkasına ait olacaktır.)

![](scaleout-with-redis/_static/image8.png)

Redsıs 'e gönderilen iletileri görmeyi merak ediyorsanız redsıs ile yüklenen **redsıs-CLI** istemcisini kullanabilirsiniz.

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
