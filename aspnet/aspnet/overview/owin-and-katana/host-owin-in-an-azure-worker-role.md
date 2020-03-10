---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Azure çalışan rolünde ana bilgisayar | Microsoft Docs
author: MikeWasson
description: Bu öğreticide, Microsoft Azure çalışan rolünde nasıl bağımsız olarak OWIN barındırılacağını gösterilmektedir. .NET için açık Web arabirimi (OWıN), .NET Web sunucusu arasında bir soyutlama tanımlıyor...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584618"
---
# <a name="host-owin-in-an-azure-worker-role"></a>Azure Çalışan Rolünde OWIN Barındırma

, [Mike te son](https://github.com/MikeWasson)

> Bu öğreticide, Microsoft Azure çalışan rolünde nasıl bağımsız olarak OWIN barındırılacağını gösterilmektedir.
>
> [.Net Için açık Web arabirimi](http://owin.org/) (owın), .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar. OWIN, Web uygulamasını sunucudan ayırır, bu da bir Web uygulamasını kendi işleminizde, IIS dışında (örneğin, bir Azure çalışan rolü içinde) kendine barındırmak için ideal hale getirir.
>
> Bu öğreticide, bir OWIN uygulamasını Microsoft Azure çalışan rolünde nasıl barındıralabileceğinizi öğreneceksiniz. Çalışan rolleri hakkında daha fazla bilgi için bkz. [Azure yürütme modelleri](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [.NET 2,3 için Azure SDK](https://azure.microsoft.com/downloads/)
> - [Microsoft. Owin. Selfhost 2.1.0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a>Microsoft Azure projesi oluşturma

Visual Studio 'Yu yönetici ayrıcalıklarıyla başlatın. Azure işlem öykünücüsü kullanılarak uygulamanın yerel olarak hata ayıklaması için yönetici ayrıcalıkları gerekir.

**Dosya** menüsünde **Yeni**' ye ve ardından **Proje**' ye tıklayın. **Yüklü şablonlardan**, Visual C#altında **bulut** ' a ve ardından **Windows Azure bulut hizmeti**' ne tıklayın. Projeyi "AzureApp" olarak adlandırın ve **Tamam**' a tıklayın.

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

**Yeni Windows Azure bulut hizmeti** Iletişim kutusunda **çalışan rolü**' ne çift tıklayın. Varsayılan adı bırakın ("WorkerRole1"). Bu adım çözüme bir çalışan rolü ekler. **Tamam**’a tıklayın.

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

Oluşturulan Visual Studio çözümü iki proje içerir:

- &quot;AzureApp&quot;, Azure uygulamasının rollerini ve yapılandırmasını tanımlar.
- &quot;WorkerRole1&quot;, çalışan rolü için kodu içerir.

Genel olarak, bir Azure uygulaması birden çok rol içerebilir, ancak bu öğretici tek bir rol kullanıyor olabilir.

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>OWıN Self-Host paketlerini ekleme

**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.

Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>HTTP uç noktası ekleme

Çözüm Gezgini ' de, AzureApp projesini genişletin. Roller düğümünü genişletin, WorkerRole1 öğesine sağ tıklayın ve **Özellikler**' i seçin.

![](host-owin-in-an-azure-worker-role/_static/image6.png)

**Uç noktalar**' a ve ardından **uç nokta Ekle**' ye tıklayın.

**Protokol** açılan listesinde "http" öğesini seçin. **Genel bağlantı noktası** ve **özel bağlantı noktası**alanına 80 yazın. Bu bağlantı noktası numaraları farklı olabilir. Genel bağlantı noktası, istemcilerin role bir istek gönderdiklerinde kullandıkları şeydir.

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>OWıN başlangıç sınıfını oluşturma

Çözüm Gezgini ' de, WorkerRole1 projesine sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin. `Startup`sınıfı adlandırın.

Tüm ortak kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

`UseWelcomePage` uzantısı yöntemi, sitenizin çalıştığını doğrulamak için uygulamanıza basit bir HTML sayfası ekler.

## <a name="start-the-owin-host"></a>OWıN konağını başlatma

WorkerRole.cs dosyasını açın. Bu sınıf, çalışan rolü başlatıldığında ve durdurulduğunda çalışan kodu tanımlar.

Şu deyimi kullanarak aşağıdakileri ekleyin:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

`WorkerRole` sınıfına bir **IDisposable** üyesi ekleyin:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

`OnStart` yönteminde, ana bilgisayarı başlatmak için aşağıdaki kodu ekleyin:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

**WebApp. Start** yöntemi owın konağını başlatır. `Startup` sınıfının adı, yöntemin tür parametresidir. Kurala göre, ana bilgisayar bu sınıfın `Configure` yöntemini çağırır.

*\_uygulama* örneğinin atılırken `OnStop` geçersiz kılın:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

WorkerRole.cs için kodun tamamı aşağıda verilmiştir:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

Çözümü oluşturun ve F5 tuşuna basarak uygulamayı Azure Işlem öykünücüsünde yerel olarak çalıştırın. Güvenlik duvarınızın ayarlarına bağlı olarak, güvenlik duvarınız aracılığıyla öykünücüye izin vermeniz gerekebilir.

İşlem öykünücüsü uç noktaya bir yerel IP adresi atar. Işlem öykünücüsü Kullanıcı arabirimini görüntüleyerek IP adresini bulabilirsiniz. Görev çubuğu bildirim alanında öykünücü simgesine sağ tıklayın ve **Işlem öykünücüsü Kullanıcı arabirimini göster**' i seçin.

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

Hizmet dağıtımları, dağıtım [kimlik], hizmet ayrıntıları altındaki IP adresini bulun. Bir Web tarayıcısı açın ve http:\/\/*Address*adresine gidin; burada *Adres* , Işlem öykünücüsü tarafından atanan IP adresidir; Örneğin, `http://127.0.0.1:80`. OWıN karşılama sayfasını görmeniz gerekir:

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>Azure’a dağıtma

Bu adım için bir Azure hesabınızın olması gerekir. Henüz bir hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz. [ücretsiz deneme Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

Çözüm Gezgini, AzureApp projesine sağ tıklayın. **Yayımla**’yı seçin.

![](host-owin-in-an-azure-worker-role/_static/image12.png)

Azure hesabınızda oturum açmadıysanız **oturum aç**' a tıklayın.

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

Oturum açtıktan sonra bir abonelik seçin ve **İleri**' ye tıklayın.

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

Bulut hizmeti için bir ad girin ve bir bölge seçin. **Oluştur**'u tıklatın.

![](host-owin-in-an-azure-worker-role/_static/image17.png)

**Yayımla**’ta tıklayın.

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

Azure etkinlik günlüğü penceresinde dağıtım ilerleme durumu gösterilir. Uygulama dağıtıldığında `http://appname.cloudapp.net/`gidin; burada *appname* , bulut hizmetinizin adıdır.

## <a name="additional-resources"></a>Ek Kaynaklar

- [Project Katana’ya Genel Bakış](an-overview-of-project-katana.md)
- [GitHub üzerinde Katana proje](https://github.com/aspnet/AspNetKatana/)
