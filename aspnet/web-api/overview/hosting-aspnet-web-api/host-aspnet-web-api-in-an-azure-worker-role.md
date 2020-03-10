---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure çalışan rolünde Host ASP.NET Web API 2-ASP.NET 4. x
author: MikeWasson
description: "Öğretici: Web API çerçevesini Self barındırmak için OWıN kullanarak bir Azure çalışan rolünde ASP.NET Web API 'SI barındırın."
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556632"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>Azure çalışan rolünde Host ASP.NET Web API 2

, [Mike te son](https://github.com/MikeWasson)

> Bu öğreticide, Web API çerçevesini Self barındırmak için OWIN kullanılarak Azure çalışan rolünde ASP.NET Web API 'sinin nasıl barındıralınacağını gösterilmektedir.
>
> [.Net Için açık Web arabirimi](http://owin.org/) (owın), .NET Web sunucuları ile Web uygulamaları arasında bir soyutlama tanımlar. OWIN, Web uygulamasını sunucudan ayırır, bu da bir Web uygulamasını kendi işleminizde, IIS dışında (örneğin, bir Azure çalışan rolü içinde) kendine barındırmak için ideal hale getirir.
>
> Bu öğreticide, kendi kendini barındırmak için kullanılan bir HTTP sunucusu sağlayan Microsoft. Owin. Host. HttpListener paketini kullanacaksınız.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Web API 2
> - [.NET 2,3 için Azure SDK](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a>Microsoft Azure projesi oluşturma

Visual Studio 'Yu yönetici ayrıcalıklarıyla başlatın. Azure işlem öykünücüsü kullanılarak uygulamanın yerel olarak hata ayıklaması için yönetici ayrıcalıkları gerekir.

**Dosya** menüsünde **Yeni**' ye ve ardından **Proje**' ye tıklayın. **Yüklü şablonlardan**, Visual C#altında **bulut** ' a ve ardından **Windows Azure bulut hizmeti**' ne tıklayın. Projeyi "AzureApp" olarak adlandırın ve **Tamam**' a tıklayın.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

**Yeni Windows Azure bulut hizmeti** Iletişim kutusunda **çalışan rolü**' ne çift tıklayın. Varsayılan adı bırakın ("WorkerRole1"). Bu adım çözüme bir çalışan rolü ekler. **Tamam**’a tıklayın.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

Oluşturulan Visual Studio çözümü iki proje içerir:

- &quot;AzureApp&quot;, Azure uygulamasının rollerini ve yapılandırmasını tanımlar.
- &quot;WorkerRole1&quot;, çalışan rolü için kodu içerir.

Genel olarak, bir Azure uygulaması birden çok rol içerebilir, ancak bu öğretici tek bir rol kullanıyor olabilir.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>Web API 'sini ve OWIN paketlerini ekleyin

**Araçlar** menüsünde **NuGet Paket Yöneticisi**' ne ve ardından **Paket Yöneticisi konsolu**' na tıklayın.

Paket Yöneticisi konsolu penceresinde, aşağıdaki komutu girin:

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>HTTP uç noktası ekleme

Çözüm Gezgini ' de, AzureApp projesini genişletin. Roller düğümünü genişletin, WorkerRole1 öğesine sağ tıklayın ve **Özellikler**' i seçin.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

**Uç noktalar**' a ve ardından **uç nokta Ekle**' ye tıklayın.

**Protokol** açılan listesinde "http" öğesini seçin. **Genel bağlantı noktası** ve **özel bağlantı noktası**alanına 80 yazın. Bu bağlantı noktası numaraları farklı olabilir. Genel bağlantı noktası, istemcilerin role bir istek gönderdiklerinde kullandıkları şeydir.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>Self-Host için Web API 'YI yapılandırma

Çözüm Gezgini ' de, WorkerRole1 projesine sağ tıklayın ve yeni bir sınıf eklemek için / **sınıfı** **Ekle** ' yi seçin. `Startup`sınıfı adlandırın.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>Web API denetleyicisi ekleme

Sonra, bir Web API denetleyici sınıfı ekleyin. WorkerRole1 projesine sağ tıklayın ve / **sınıfı** **Ekle** ' yi seçin. Test denetleyicisi sınıfını adlandırın. Bu dosyadaki tüm ortak kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

Kolaylık olması için bu denetleyici yalnızca düz metin döndüren iki GET yöntemi tanımlar.

## <a name="start-the-owin-host"></a>OWıN konağını başlatma

WorkerRole.cs dosyasını açın. Bu sınıf, çalışan rolü başlatıldığında ve durdurulduğunda çalışan kodu tanımlar.

Şu deyimi kullanarak aşağıdakileri ekleyin:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

`WorkerRole` sınıfına bir **IDisposable** üyesi ekleyin:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

`OnStart` yönteminde, ana bilgisayarı başlatmak için aşağıdaki kodu ekleyin:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

**WebApp. Start** yöntemi owın konağını başlatır. `Startup` sınıfının adı, yöntemin tür parametresidir. Kurala göre, ana bilgisayar bu sınıfın `Configure` yöntemini çağırır.

*\_uygulama* örneğinin atılırken `OnStop` geçersiz kılın:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

WorkerRole.cs için kodun tamamı aşağıda verilmiştir:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

Çözümü oluşturun ve F5 tuşuna basarak uygulamayı Azure Işlem öykünücüsünde yerel olarak çalıştırın. Güvenlik duvarınızın ayarlarına bağlı olarak, güvenlik duvarınız aracılığıyla öykünücüye izin vermeniz gerekebilir.

> [!NOTE]
> Aşağıdakiler gibi bir özel durum alırsanız, geçici çözüm için lütfen [Bu blog gönderisine](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) bakın. "Dosya veya derleme ' Microsoft. Owin, Version = 2.0.2.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' veya bağımlılıklarından biri yüklenemedi. Konumlandırılan derlemenin bildirim tanımı derleme başvurusuyla eşleşmiyor. (HRESULT özel durumu: 0x80131040) "

İşlem öykünücüsü uç noktaya bir yerel IP adresi atar. Işlem öykünücüsü Kullanıcı arabirimini görüntüleyerek IP adresini bulabilirsiniz. Görev çubuğu bildirim alanında öykünücü simgesine sağ tıklayın ve **Işlem öykünücüsü Kullanıcı arabirimini göster**' i seçin.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

Hizmet dağıtımları, dağıtım [kimlik], hizmet ayrıntıları altındaki IP adresini bulun. Bir Web tarayıcısı açın ve http://<em>Address</em>/test/1 adresine gidin; burada <em>Adres</em> , Işlem öykünücüsü tarafından atanan IP adresidir; Örneğin, `http://127.0.0.1:80/test/1`. Web API denetleyicisinden yanıtı görmeniz gerekir:

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>Azure’a dağıtma

Bu adım için bir Azure hesabınızın olması gerekir. Henüz bir hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılar için bkz. [ücretsiz deneme Microsoft Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

Çözüm Gezgini, AzureApp projesine sağ tıklayın. **Yayımla**’yı seçin.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

Azure hesabınızda oturum açmadıysanız **oturum aç**' a tıklayın.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

Oturum açtıktan sonra bir abonelik seçin ve **İleri**' ye tıklayın.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

Bulut hizmeti için bir ad girin ve bir bölge seçin. **Oluştur**'u tıklatın.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

**Yayımla**’ta tıklayın.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

Azure etkinlik günlüğü penceresinde dağıtım ilerleme durumu gösterilir. Uygulama dağıtıldığında http://appname.cloudapp.net/test/1gidin.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>Ek Kaynaklar

- [Project Katana’ya Genel Bakış](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [GitHub üzerinde Katana proje](https://github.com/aspnet/AspNetKatana)
