---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Azure App Service Web Apps ile SignalR kullanma | Microsoft Docs
author: bradygaster
description: Bu belgede, Microsoft Azure üzerinde çalışan bir SignalR uygulamasının nasıl yapılandırılacağı açıklanmaktadır. Öğreticide kullanılan yazılım sürümleri Visual Studio 2013 veya VIS...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558704"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a>Azure App Service'te Web Apps ile SignalR Kullanma

, [Patrick Fleti](https://github.com/pfletcher) tarafından

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Bu belgede, Microsoft Azure üzerinde çalışan bir SignalR uygulamasının nasıl yapılandırılacağı açıklanmaktadır.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) veya Visual Studio 2012
> - .NET 4.5
> - SignalR sürüm 2
> - Visual Studio 2013 veya 2012 için Azure SDK 2,3
>
>
>
> ## <a name="questions-and-comments"></a>Sorular ve açıklamalar
>
> Lütfen bu öğreticiyi nasıl beğentireceğiniz ve sayfanın en altındaki açıklamalarda İyileştiğimiz hakkında geri bildirimde bulunun. Öğreticiyle doğrudan ilgili olmayan sorularınız varsa, bunları [ASP.NET SignalR forumuna](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/)veya [Microsoft Azure forumlarına](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform)gönderebilirsiniz.

## <a name="table-of-contents"></a>İçindekiler

- [Giriş](#introduction)
- [Azure App Service için bir SignalR Web uygulaması dağıtma](#deploying)
- [Azure App Service üzerinde WebSockets etkinleştiriliyor](#websocket)
- [Azure Redis Cache Arkadüzlemi kullanma](#backplane)
- [Sonraki adımlar](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>Giriş

ASP.NET SignalR, sunucular ve Web veya .NET istemcileri arasında yeni bir etkileşim düzeyi getirmek için kullanılabilir. Azure 'da barındırıldığında, SignalR uygulamaları, bulutta çalışan yüksek oranda kullanılabilir, ölçeklenebilir ve performanslı ortamlarından faydalanabilir.

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>Azure App Service için bir SignalR Web uygulaması dağıtma

SignalR, bir uygulamayı Azure 'a dağıtmaya ve şirket içi bir sunucuya dağıtmaya yönelik belirli bir karmaşıklıklar eklemez. SignalR kullanan bir uygulama, yapılandırmada veya diğer ayarlarda herhangi bir değişiklik yapılmadan Azure 'da barındırılabilir (ancak WebSockets desteği için, aşağıdaki Azure App Service için bkz. [etkinleştirme WebSockets](#websocket) .) Bu öğreticide, Başlangıç [öğreticisinde](../getting-started/tutorial-getting-started-with-signalr.md) oluşturulan uygulamayı Azure 'a dağıtırsınız.

**Önkoşullar**

- Visual Studio 2013. Visual Studio yoksa, Azure SDK yüklemesine Web için Visual Studio 2013 Express eklenmiştir.
- [Visual Studio 2013 Için Azure sdk 2,3](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) veya [Visual Studio 2012 için Azure SDK 2,3](https://go.microsoft.com/fwlink/p/?linkid=323511).
- Bu öğreticiyi tamamlayabilmeniz için bir Azure aboneliğine ihtiyacınız olacaktır. [MSDN abonesi avantajlarınızı etkinleştirebilir](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)veya [deneme aboneliği için kaydolabilirsiniz](https://azure.microsoft.com/pricing/free-trial/).

### <a name="deploying-a-signalr-web-app-to-azure"></a>Azure 'a bir SignalR Web uygulaması dağıtma

1. Başlangıç [öğreticisini](../getting-started/tutorial-getting-started-with-signalr.md)doldurun veya [kod galerisinden](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)tamamlanmış projeyi indirin.
2. Visual Studio 'da **Build**, **SignalR sohbeti Yayımla**' yı seçin.
3. "Web 'i Yayımla" iletişim kutusunda "Windows Azure Web siteleri" ni seçin.

    ![Azure Web siteleri seçin](using-signalr-with-azure-web-sites/_static/image1.png)
4. Microsoft hesabı oturum açmadıysanız, "var olan Web sitesini Seç" iletişim kutusunda **oturum aç...** öğesine tıklayın ve oturum açın.

    ![Mevcut Web sitesini seçin](using-signalr-with-azure-web-sites/_static/image2.png)    ![Azure'da oturum açma](using-signalr-with-azure-web-sites/_static/image3.png)
5. "Varolan Web sitesini Seç" iletişim kutusunda **Yeni**' ye tıklayın.

    ![Yeni Web sitesi](using-signalr-with-azure-web-sites/_static/image4.png)
6. "Windows Azure 'da site oluştur" iletişim kutusunda benzersiz bir uygulama adı girin. Bölge açılan kutusunda size en yakın bölgeyi seçin. **Oluştur**'u tıklatın.

    ![Azure 'da site oluşturma](using-signalr-with-azure-web-sites/_static/image5.png)
7. "Web 'i Yayımla" iletişim kutusunda **Yayımla**' ya tıklayın.

    ![Siteyi Yayımla](using-signalr-with-azure-web-sites/_static/image6.png)
8. Uygulamanın yayımlanması tamamlandığında, Azure App Service Web Apps barındırılan SignalR sohbet uygulaması bir tarayıcıda açılır.

    ![Tarayıcıda açılan site](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>Azure App Service Web Apps üzerinde WebSockets etkinleştiriliyor

WebSockets 'in bir SignalR uygulamasında kullanılabilmesi için Web uygulamanızda açık bir şekilde etkinleştirilmesi gerekir; Aksi takdirde, diğer protokoller kullanılacaktır (Ayrıntılar için bkz. [taşımalar ve Fallyedekler](../getting-started/introduction-to-signalr.md#transports) ).

WebSockets Azure App Service Web Apps kullanmak için, Web uygulamasının yapılandırma bölümünde etkinleştirin. Bunu yapmak için, Web uygulamanızı [Azure yönetim portalı](https://manage.windowsazure.com/)açın ve Yapılandır ' ı seçin.

![Yapılandır sekmesi](using-signalr-with-azure-web-sites/_static/image8.png)

Yapılandırma sayfasının en üstünde, .NET 4,5 ' in Web uygulamanız için kullanıldığından emin olun.

![.NET Framework sürüm 4,5 ayarı](using-signalr-with-azure-web-sites/_static/image9.png)

Yapılandırma sayfasında, **WebSockets** ayarında **Açık**' ı seçin.

![WebSockets ayarı: açık](using-signalr-with-azure-web-sites/_static/image10.png)

Değişikliklerinizi kaydetmek için yapılandırma sayfasının alt kısmındaki **Kaydet** ' i seçin.

![Ayarları Kaydet](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>Azure Redis Cache Arkadüzlemi kullanma

Web uygulamanız için birden çok örnek kullanıyorsanız ve bu örneklerin kullanıcılarının birbirleriyle etkileşime ihtiyacı varsa (örneğin, bir örnekte oluşturulan sohbet iletileri diğer örneklere bağlı olan kullanıcılara ulaşabilmesi için), [Azure Redis Cache backdüzlemi](../performance/scaleout-with-redis.md) uygulamanızda uygulanmalıdır.

<a id="nextsteps"></a>
## <a name="next-steps"></a>Sonraki Adımlar

Azure App Service Web Apps hakkında daha fazla bilgi için bkz. [Web Apps genel bakış](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).
