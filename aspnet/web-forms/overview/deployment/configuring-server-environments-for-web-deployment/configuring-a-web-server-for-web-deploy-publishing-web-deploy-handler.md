---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: Bir Web sunucusunu Web Dağıtımı yayımlama için yapılandırma (Web Dağıtımı Işleyicisi) | Microsoft Docs
author: jrjlee
description: Bu konu, IIS Web Dağıtımı Han kullanarak Web yayımlaması ve dağıtımı desteklemek için bir Internet Information Services (IIS) Web sunucusunun nasıl yapılandırılacağını açıklamaktadır...
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: baaebd32f08d3c6b861572c5c5a16ec0fb70aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568567"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a>Bir Web Sunucusunu Web Dağıtımı Yayımlama için Yapılandırma (Web Dağıtımı İşleyicisi)

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, IIS Web Dağıtımı Işleyicisini kullanarak Web yayımlaması ve dağıtımı desteklemek için bir Internet Information Services (IIS) Web sunucusunun nasıl yapılandırılacağı açıklanmaktadır.
> 
> Web Dağıtımı 2,0 veya sonraki bir sürümüyle çalışırken, uygulamalarınızı veya sitelerinizi bir Web sunucusuna almak için kullanabileceğiniz üç ana yaklaşım vardır. Şunları yapabilirsiniz:
> 
> - *Web dağıtımı uzak aracı hizmetini*kullanın. Bu yaklaşım, Web sunucusu için daha az yapılandırma gerektirir, ancak sunucuya her şeyi dağıtmak için bir yerel sunucu yöneticisinin kimlik bilgilerini sağlamanız gerekir.
> - *Web dağıtımı işleyicisini*kullanın. Bu yaklaşım çok daha karmaşıktır ve Web sunucusunu ayarlamak için daha fazla ilk çaba gerektirir. Ancak, bu yaklaşımı kullandığınızda, IIS 'yi yönetici olmayan kullanıcıların dağıtımı gerçekleştirmesine izin verecek şekilde yapılandırabilirsiniz. Web Dağıtımı Işleyicisi yalnızca IIS sürüm 7 veya üzeri sürümlerde kullanılabilir.
> - *Çevrimdışı dağıtım*kullanın. Bu yaklaşım, Web sunucusu için en az yapılandırmayı gerektirir, ancak bir sunucu yöneticisinin Web paketini sunucuya el ile kopyalaması ve IIS Yöneticisi aracılığıyla içeri aktarması gerekir.
> 
> Bu yaklaşımların temel özellikleri, avantajları ve dezavantajları hakkında daha fazla bilgi için, bkz. [Web dağıtımına doğru yaklaşımı seçme](choosing-the-right-approach-to-web-deployment.md).

Evet, yönetici olmayan kullanıcıların belirli IIS Web sitelerine içerik dağıtmasını sağlamak istiyorsanız. Bu yaklaşım genellikle bu tür senaryolarda tercih edilir:

- Hazırlama veya üretim ortamları, uzak dağıtımı tetikleyen kişi veya hizmet hesabının, bir sunucu yöneticisinin kimlik bilgilerine erişimi olması olası değildir.
- Uzak kullanıcılara, web sunucularınız üzerinde tam denetim (veya başkalarının web sitelerine erişim) vermeden Web sitelerini güncelleştirme yeteneği vermek istediğiniz barındırılan ortamlar.

Geliştirme veya test senaryolarında ya da daha küçük kuruluşlarda, Sunucu Yöneticisi kimlik bilgilerini kullanarak içerik dağıtımı genellikle daha az çaba olur. Bu senaryolarda, Web sunucularınızı [Web dağıtımı uzak Aracı hizmeti](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) kullanılarak dağıtımı destekleyecek şekilde yapılandırmak daha kolay bir yaklaşım sunar.

## <a name="task-overview"></a>Göreve genel bakış

Web sunucusunu, Web Dağıtımı Işleyicisi yaklaşımını kullanarak uzak bir bilgisayardan Web paketlerini kabul edecek ve dağıtmaya yönelik olarak yapılandırmak için şunları yapmanız gerekir:

- Kimlik bilgilerini dağıtım gerçekleştirmek için kullanacağınız bir etki alanı kullanıcı hesabı ("yönetici olmayan Kullanıcı") oluşturun veya seçin.
- Web yönetimi hizmeti ve temel kimlik doğrulama modülü dahil olmak üzere IIS 7,5 ' ü yükler.
- Web Dağıtımı 2,1 veya üstünü yükler.
- Web yönetimi hizmetini uzak bağlantılara izin verecek şekilde yapılandırın ve hizmeti başlatın.
- Dağıtılan içeriği barındırmak için bir IIS Web sitesi oluşturun.
- IIS Yöneticisi 'nde Web sitenizde yönetici olmayan kullanıcı izinleri verin.
- Web yönetimi hizmeti temsili kurallarının yönetici olmayan kullanıcı hesabınızı kullanarak Web sitesi içeriği eklemesini ve değiştirmesini sağlayın.
- 8172 numaralı bağlantı noktasında gelen bağlantılara izin vermek için tüm güvenlik duvarlarını yapılandırın.

ContactManager örnek çözümünü özellikle barındırmak için şunları yapmanız gerekir:

- 4,0 .NET Framework 'yi yükler.
- ASP.NET MVC 3 ' ü yükler.

Bu konu, bu yordamların her birini nasıl gerçekleştirekullanacağınızı gösterir. Bu konudaki görevler ve izlenecek yollar, Windows Server 2016 çalıştıran bir temiz sunucu derlemesi ile başladığınızı varsayar. Devam etmeden önce aşağıdakileri doğrulayın:

- Windows Server 2016
- Sunucu etki alanına katılmış.
- Sunucunun statik bir IP adresi vardır.

> [!NOTE]
> Bilgisayarları etki alanına katma hakkında daha fazla bilgi için bkz. [bilgisayarları etki alanına katma ve oturum açma](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Statik IP adreslerini yapılandırma hakkında daha fazla bilgi için bkz. [STATIK IP adresi yapılandırma](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).

## <a name="install-products-and-components"></a>Ürün ve bileşenleri yükler

Bu bölüm, Web sunucusuna gerekli ürün ve bileşenleri yükleme konusunda size kılavuzluk eder. Başlamadan önce, sunucunuzun tamamen güncel olduğundan emin olmak için Windows Update çalıştırmak iyi bir uygulamadır.

Bu durumda, şunları yüklemeniz gerekir:

- **IIS 7 önerilen yapılandırma**. Bu, Web sunucunuzda **Web sunucusu (IIS)** rolünü sağlar ve bir ASP.NET uygulamasını barındırmak için IHTIYAç duyduğunuz IIS modülleri ve bileşenleri kümesini kurar.
- **IIS: Yönetim hizmeti**. Bu, Web yönetimi hizmetini (WMSvc) IIS 'ye yüklenir. Bu hizmet, IIS Web sitelerinin uzaktan yönetilmesini sağlar ve Web Dağıtımı Işleyici uç noktasını istemcilere sunar.
- **IIS: temel kimlik doğrulaması**. Bu, IIS temel kimlik doğrulama modülünü yüklenir. Bu, Web yönetimi hizmeti 'nin (WMSvc) sağladığınız kimlik bilgileriyle kimlik doğrulamasını sağlar.
- **Web dağıtımı aracı 2,1 veya sonraki bir sürümü**. Bu, sunucunuza Web Dağıtımı (ve temel alınan yürütülebilir dosyası, MSDeploy. exe) yüklenir. Bu işlemin bir parçası olarak, Web Dağıtımı Işleyicisini yükleyip Web yönetimi hizmetiyle tümleştirir.
- **.NET Framework 4,0**. Bu, .NET Framework bu sürümünde oluşturulan uygulamaları çalıştırmak için gereklidir.
- **ASP.NET MVC 3**. Bu, MVC 3 uygulamalarını çalıştırmak için gereken derlemeleri kurar.

> [!NOTE]
> Bu izlenecek yol, çeşitli bileşenleri yüklemek ve yapılandırmak için Web Platformu Yükleyicisi 'nin kullanımını açıklar. Web platformu yükleyicisini kullanmanıza gerek olmasa da, bağımlılıkları otomatik olarak algılayarak ve en son ürün sürümlerini her zaman almanızı sağlayarak yükleme işlemini basitleştirir. Daha fazla bilgi için bkz. [Microsoft Web Platformu Yükleyicisi](https://go.microsoft.com/?linkid=9805118).

**Gerekli ürünleri ve bileşenleri yüklemek için**

1. [Web platformu yükleyicisini](https://go.microsoft.com/?linkid=9805118)indirip yükleyin.
2. Yükleme tamamlandığında, Web Platformu Yükleyicisi otomatik olarak başlatılır.

    > [!NOTE]
    > Artık **Başlangıç** menüsünden Web Platformu Yükleyicisi 'ni dilediğiniz zaman başlatabilirsiniz. Bunu yapmak için, **Başlat** menüsünde, **tüm programlar**' a ve ardından **Microsoft Web Platformu Yükleyicisi**' ye tıklayın.
3. **Web Platformu Yükleyicisi** penceresinin en üstünde **Ürünler**'e tıklayın.
4. Pencerenin sol tarafında, gezinti bölmesinde, **çerçeveler**' e tıklayın.
5. **Microsoft .NET Framework 4** satırında, .NET Framework zaten yüklenmemişse **Ekle**' ye tıklayın.

    > [!NOTE]
    > .NET Framework 4,0 ' i Windows Update aracılığıyla zaten yüklemiş olabilirsiniz. Bir ürün veya bileşen zaten yüklüyse, Web Platformu Yükleyicisi, **Ekle** düğmesini **yüklü**olan metinle değiştirerek bunu gösterir.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. **ASP.NET MVC 3 (Visual Studio 2010)** satırında **Ekle**' ye tıklayın.
7. Gezinti bölmesinde **sunucu**' ya tıklayın.
8. **IIS 7 önerilen yapılandırma** satırında **Ekle**' ye tıklayın.
9. **Web Dağıtım aracı 2,1** satırında **Ekle**' ye tıklayın.
10. **IIS: temel kimlik doğrulaması** satırında **Ekle**' ye tıklayın.
11. **IIS: Yönetim hizmeti** satırında **Ekle**' ye tıklayın.
12. **Yükle**'ye tıklatın. Web Platformu yükleyicisi ürünleri &#x2014; herhangi bir ilişkili bağımlılıkları &#x2014; yüklenecek birlikte listesini gösterir ve lisans koşullarını kabul isteyip istemediğinizi sorar.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. Lisans koşullarını gözden geçirin ve koşulları **onayladıysanız kabul ediyorum**' a tıklayın.
14. Yükleme tamamlandığında, **son**' a tıklayın ve ardından **Web Platformu Yükleyicisi** penceresini kapatın.

IIS 'yi yüklemeden önce 4,0 .NET Framework yüklediyseniz, en son ASP.NET sürümünü IIS ile kaydettirmek için [ASP.NET IIS kayıt aracı](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) 'nı (ASPNET\_regııs. exe) çalıştırmanız gerekir. Bunu yapmazsanız, IIS 'nin herhangi bir sorun olmadan statik içerik (HTML dosyaları gibi) sunacağını, ancak ASP.NET içeriğine gözatmaya çalıştığınızda, **http hatası 404,0 –** döndürülmeyeceğini göreceksiniz. ASP.NET 4,0 ' nin kaydedildiğinden emin olmak için bir sonraki yordamı kullanabilirsiniz.

**ASP.NET 4,0 'i IIS ile kaydetmek için**

1. **Başlat**' a tıklayın ve ardından **komut istemi**yazın.
2. Arama sonuçlarında **komut istemi**' ne sağ tıklayın ve ardından **yönetici olarak çalıştır**' a tıklayın.
3. Komut Istemi penceresinde **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** dizinine gidin.
4. Bu komutu yazın ve ENTER tuşuna basın:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. Herhangi bir noktada 64 bitlik Web uygulamalarını barındırmak istiyorsanız, ASP.NET 'in 64 bit sürümünü de IIS ile kaydetmeniz gerekir. Bunu yapmak için, komut Istemi penceresinde **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** dizinine gidin.
6. Bu komutu yazın ve ENTER tuşuna basın:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

İyi bir uygulama olarak, yüklediğiniz yeni ürün ve bileşenler için kullanılabilir güncelleştirmeleri indirmek ve yüklemek üzere bu noktada Windows Update yeniden kullanın.

## <a name="configure-the-web-management-service"></a>Web yönetimi hizmetini yapılandırma

İhtiyacınız olan her şeyi yüklemişseniz, sonraki adım IIS 'de Web yönetimi hizmetini yapılandırmaktır. Yüksek düzeyde, bu görevleri gerçekleştirmeniz gerekir:

- Sunucu düzeyinde temel kimlik doğrulamasını etkinleştirin.
- Web yönetimi hizmetini uzak bağlantıları kabul edecek şekilde yapılandırın.
- Web yönetimi hizmetini başlatın.
- Gerekli Web yönetimi hizmeti temsili kurallarının yerinde olduğundan emin olun.

**Web yönetimi hizmetini yapılandırmak için**

1. **Başlat** menüsünde, **Yönetim Araçları**' nın üzerine gelin ve ardından **Internet Information Services (IIS) Yöneticisi**' ne tıklayın.
2. IIS Yöneticisi 'nde, **Bağlantılar** bölmesinde, sunucu düğümüne tıklayın (örneğin, **STAGEWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. Orta bölmede, **IIS**altında **kimlik doğrulama**' ya çift tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. **Temel kimlik doğrulaması**' na sağ tıklayın ve ardından **Etkinleştir**' e tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. **Bağlantılar** bölmesinde, en üst düzey ayarlara dönmek için sunucu düğümüne tekrar tıklayın.
6. Orta bölmede, **Yönetim**altında, **Yönetim hizmeti**' ne çift tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. Orta bölmede, **uzak bağlantıları etkinleştir**' i seçin.

    > [!NOTE]
    > Web yönetimi hizmeti zaten çalışıyorsa, önce bunu durdurmanız gerekir.
8. Web yönetimi hizmetini başlatmak için **Eylemler** bölmesinde **Başlat** ' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. Ayarlarınızı kaydetmeniz istenirse, **Evet**' e tıklayın.

    > [!NOTE]
    > Ayrıca hizmeti otomatik olarak başlayacak şekilde yapılandırmak isteyebilirsiniz. Bunu yapmak için, Hizmetler konsolunu açın, **Web yönetimi hizmeti**' ne sağ tıklayın ve ardından **Özellikler**' e tıklayın. **Başlangıç türü** açılan listesinde, **Otomatik**' i seçin ve ardından **Tamam**' a tıklayın.
10. **Bağlantılar** bölmesinde, en üst düzey ayarlara dönmek için sunucu düğümüne tekrar tıklayın.
11. Orta bölmede, **Yönetim**altında, **Yönetim hizmeti temsili**' ne çift tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. Orta bölmenin bir kural kümesi içerdiğini doğrulayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    Bu kurallar yetkili Web yönetimi hizmeti kullanıcılarının çeşitli Web Dağıtımı sağlayıcıları kullanmasına izin verir. Örneğin, Web Dağıtımı Işleyicisi aracılığıyla IIS 'ye Web uygulamaları ve içerik dağıtmak için, tüm kimliği doğrulanmış Web yönetimi hizmeti kullanıcılarının **contentPath** ve **iisApp** sağlayıcılarını kullanmasına izin veren bir yetkilendirme kuralı olmalıdır (ekran görüntüsünde görebileceğiniz son kural).

    Ürün ve bileşenleri bu konuda açıklanan sıraya göre yüklediyseniz, Web Dağıtımı en son sürümü, gerekli tüm yetkilendirme kurallarını Web Yönetim hizmetine otomatik olarak eklemektir. Yönetim hizmeti temsili sayfasında herhangi bir kural gösterilmezse, bunları kendiniz oluşturmanız gerekir. Bunun nasıl yapılacağı hakkında yönergeler için bkz. [Web Dağıtım Işleyicisini yapılandırma](https://go.microsoft.com/?linkid=9805124).
13. **Bağlantılar** bölmesinde, en üst düzey ayarlara dönmek için sunucu düğümüne tekrar tıklayın.

## <a name="create-and-configure-an-iis-website"></a>IIS Web sitesi oluşturma ve yapılandırma

Sunucunuza Web içeriği dağıtabilmeniz için önce içeriği barındırmak üzere bir IIS Web sitesi oluşturmanız ve yapılandırmanız gerekir. Web Dağıtımı, yalnızca mevcut bir IIS Web sitesine web paketleri dağıtabilir; sizin için Web sitesini oluşturamaz. Yönetici olmayan hesabınızın içeriği uzaktan dağıtmasını sağlamak için de çok fazla yapılandırma yapmanız gerekir. Yüksek düzeyde, bu görevleri gerçekleştirmeniz gerekir:

- İçeriğinizi barındırmak için dosya sisteminde bir klasör oluşturun.
- İçeriği sunacak bir IIS Web sitesi oluşturun ve Yerel klasörle ilişkilendirin.
- Yerel klasördeki uygulama havuzu kimliği için okuma izinleri verin.
- Web uygulamanızı dağıtacak etki alanı hesabına gerekli IIS izinlerini verin.

İçeriği IIS 'de varsayılan Web sitesine dağıtmaktan hiçbir şey yapmamaya rağmen, bu yaklaşım test veya tanıtım senaryolarından başka hiçbir şey için önerilmez. Bir üretim ortamının benzetimini yapmak için, uygulamanızın gereksinimlerine özel ayarlarla yeni bir IIS Web sitesi oluşturmanız gerekir.

**Bir IIS Web sitesi oluşturmak için**

1. Yerel dosya sisteminde içeriğinizi depolamak için bir klasör oluşturun (örneğin, **C:\demosite**).
2. **Başlat** menüsünde, **Yönetim Araçları**' nın üzerine gelin ve ardından **Internet Information Services (IIS) Yöneticisi**' ne tıklayın.
3. IIS Yöneticisi 'nde, **Bağlantılar** bölmesinde, sunucu düğümünü genişletin (örneğin, **STAGEWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. **Siteler** düğümüne sağ tıklayın ve ardından **Web sitesi Ekle**' ye tıklayın.
5. **Site adı** kutusuna IIS Web sitesi için bir ad yazın (örneğin, **demosite**).
6. **Fiziksel yol** kutusunda, yerel klasörünüzün yolunu yazın (veya konumuna gidin) (örneğin, **c:\demosite**).
7. **Bağlantı noktası** kutusuna, Web sitesini barındırmak istediğiniz bağlantı noktası numarasını yazın (örneğin, **85**).

    > [!NOTE]
    > Standart bağlantı noktası numaraları HTTP için 80, HTTPS için 443 ' dir. Ancak, bu Web sitesini 80 numaralı bağlantı noktasında barındırdıysanız, sitenize erişebilmek için önce varsayılan Web sitesini durdurmanız gerekir.
8. Web sitesi için bir etki alanı adı sistemi (DNS) kaydı yapılandırmak istemediğiniz müddetçe, **ana bilgisayar adı** kutusunu boş bırakın ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > Bir üretim ortamında, büyük ihtimalle Web sitenizi bağlantı noktası 80 ' de barındırmak ve eşleşen DNS kayıtlarıyla birlikte bir ana bilgisayar üst bilgisi yapılandırmak isteyeceksiniz. IIS 7 ' de konak üstbilgilerini yapılandırma hakkında daha fazla bilgi için bkz. [bir Web sitesi için bir konak üstbilgisi yapılandırma (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx). Windows Server 'daki DNS sunucusu rolü hakkında daha fazla bilgi için bkz. [DNS sunucusuna genel bakış](https://technet.microsoft.com/library/cc770392.aspx) ve [DNS sunucusu](https://technet.microsoft.com/windowsserver/dd448607).
9. **Eylemler** bölmesinde, **Site Düzenle**altında, **Bağlamalar**'ı tıklatın.
10. **Site Bağlamaları** iletişim kutusunda **Ekle**’ye tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. **Site Bağlaması Ekle** iletişim kutusunda, **IP adresini** ve **bağlantı noktasını** mevcut site yapılandırmanızla eşleşecek şekilde ayarlayın.
12. **Ana bilgisayar adı** kutusuna Web sunucunuzun adını yazın (örneğin, **STAGEWEB1**) ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > İlk site bağlaması, IP adresini ve bağlantı noktasını veya `http://localhost:85`kullanarak siteye yerel olarak erişmenizi sağlar. İkinci site bağlaması, makine adını (örneğin, http://stageweb1:85)kullanarak etki alanındaki diğer bilgisayarlardan siteye erişmenize olanak tanır.
13. **Site Bağlamaları** iletişim kutusunda **Kapat**’a tıklayın.
14. **Bağlantılar** bölmesinde, **uygulama havuzları**' na tıklayın.
15. **Uygulama havuzları** bölmesinde, uygulama havuzunuzun adına sağ tıklayın ve ardından **temel ayarlar**' a tıklayın. Varsayılan olarak, uygulama havuzunuzun adı, Web sitenizin adıyla (örneğin, **Demosite**) eşleşir.
16. **.NET CLR sürüm** LISTESINDE **.NET CLR v 4.0.30319**' ı seçin ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > Örnek çözüm .NET Framework 4,0 gerektirir. Bu, genel olarak Web Dağıtımı için bir gereklilik değildir.

Web sitenizin içeriğe içerik sunması için, uygulama havuzu kimliğinin içeriği depolayan yerel klasörde Okuma izinlerine sahip olması gerekir. IIS 7,5 ' de, uygulama havuzları varsayılan olarak benzersiz bir uygulama havuzu kimliğiyle çalışır (IIS 'nin önceki sürümlerinin aksine, uygulama havuzlarının genellikle ağ hizmeti hesabı kullanılarak çalıştığı). Uygulama havuzu kimliği gerçek kullanıcı hesabı değil ve tüm kullanıcılar veya gruplar &#x2014 listelerde görünmüyor; uygulama havuzunu başlatıldığında, bunun yerine, bunu dinamik olarak oluşturulur. Her uygulama havuzu kimliği, gizli bir öğe olarak yerel **ııs\_ıusrs** güvenlik grubuna eklenir.

Bir dosya veya klasördeki uygulama havuzu kimliğine izin vermek için iki seçeneğiniz vardır:

- <strong>IIS AppPool\</strong ><em>[uygulama havuzu adı]</em>biçimini kullanarak doğrudan uygulama havuzu kimliğine izin atayın (örneğin, <strong>IIS AppPool\DemoSite</strong>).
- **Iıs\_ıusrs** grubuna izinler atayın.

Bu yaklaşım, dosya sistemi izinlerini yeniden yapılandırmadan uygulama havuzlarını değiştirmenize olanak sağladığından, en yaygın yaklaşım, yerel **ııs\_IUSRS** grubuna izin atanamalarıdır. Sonraki yordam bu grup tabanlı yaklaşımı kullanır.

> [!NOTE]
> IIS 7,5 ' deki uygulama havuzu kimlikleri hakkında daha fazla bilgi için bkz. [uygulama havuzu kimlikleri](https://go.microsoft.com/?linkid=9805123).

**Bir IIS Web sitesi için klasör izinlerini yapılandırmak için**

1. Windows Gezgini 'nde yerel klasörünüzün konumuna gidin.
2. Klasöre sağ tıklayın ve ardından **Özellikler**' e tıklayın.
3. **Güvenlik** sekmesinde, **Düzenle**' ye tıklayın ve ardından **Ekle**' ye tıklayın.
4. **Konumlar**' a tıklayın. **Konumlar** iletişim kutusunda yerel sunucuyu seçin ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. **Kullanıcıları veya grupları seç** Iletişim kutusunda **IIS\_ıusrs**yazın, **adları denetle**' ye tıklayın ve ardından **Tamam**' a tıklayın.
6. <em>[Klasör adı]</em> <strong>izinleri</strong>iletişim kutusunda yeni gruba, varsayılan olarak <strong>okuma &amp; yürütme</strong>, <strong>klasör içeriğini listeleme</strong>ve <strong>okuma</strong> izinleri atandığını görürsünüz. Bunu değiştirmeden bırakın ve <strong>Tamam 'a</strong>tıklayın.
7. <em>[Klasör adı]</em><strong>özellikleri</strong> Iletişim kutusunu kapatmak için <strong>Tamam</strong> ' ı tıklatın.

Son bir görev olarak, kimlik bilgilerini içerik dağıtmak için kullanacağınız yönetici olmayan kullanıcıya uygun izinleri vermeniz gerekir. Bu Kullanıcı, Web sitenize uzaktan içerik dağıtma izinleri gerektirir.

**Yönetici olmayan bir etki alanı kullanıcısı için IIS Web sitesi izinlerini yapılandırmak için**

1. IIS Yöneticisi 'nde, **Bağlantılar** bölmesinde, Web sitesi düğümünüz (örneğin, **demosite**) sağ tıklayın, **Dağıt**' ın üzerine gelin ve ardından **Web dağıtımı yayımlamayı Yapılandır**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. **Web dağıtımı yayımlamayı Yapılandır** iletişim kutusunda, **Yayımlama izinleri vermek için Kullanıcı Seç** listesinin sağında, üç nokta düğmesine tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. **Kullanıcıya Izin ver** iletişim kutusunda, içerik dağıtmak için kullanmak istediğiniz hesabın etki alanını ve Kullanıcı adını yazın ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. **Web dağıtımı yayımlamayı Yapılandır** Iletişim kutusunda **Kurulum**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > Bu işlem bir adımda iki temel işlev gerçekleştirir. İlk olarak, kullanıcıya Web yönetim hizmeti aracılığıyla Web sitesini uzaktan değiştirme izni verir ve bu, önceki bölümde incelenen yetkilendirme kurallarına göre yapılır. İkincisi, kullanıcıya Web sitesinin kaynak klasörü için tam denetim verir, bu da kullanıcının Web sitesi içeriğine ekleme, değiştirme ve izinleri ayarlama izni verir.
5. **Web dağıtımı yayımlamayı Yapılandır** Iletişim kutusunda **Kapat**' a tıklayın.

## <a name="configure-firewall-exceptions"></a>Güvenlik Duvarı özel durumlarını yapılandırma

Varsayılan olarak, IIS Web yönetimi hizmeti TCP bağlantı noktası 8172 ' i dinler. Web sunucunuzda Windows Güvenlik Duvarı etkinse, bağlantı noktası 8172 üzerinde TCP trafiğine izin vermek için yeni bir gelen kuralı oluşturmanız gerekir (tüm giden trafiğe Windows güvenlik duvarında varsayılan olarak izin verilir). Üçüncü taraf güvenlik duvarı kullanıyorsanız trafiğe izin vermek için kurallar oluşturmanız gerekir.

| Yön | Bağlantı noktasından | Bağlantı noktası | Bağlantı noktası türü |
| --- | --- | --- | --- |
| Gelen | Herhangi biri | 8172 | TCP |
| Giden | 8172 | Herhangi biri | TCP |

Windows güvenlik duvarında kuralları yapılandırma hakkında daha fazla bilgi için bkz. [güvenlik duvarı kurallarını yapılandırma](https://technet.microsoft.com/library/dd448559(WS.10).aspx). Üçüncü taraf güvenlik duvarları için lütfen ürün belgelerinize bakın.

## <a name="conclusion"></a>Sonuç

Web sunucunuz artık Web yönetim hizmeti aracılığıyla Web Dağıtımı Işleyicisine uzak dağıtımları kabul etmeye hazır olmalıdır. Bir Web uygulamasını sunucusuna dağıtmayı denemeden önce şu anahtar noktalarını denetlemek isteyebilirsiniz:

- IIS 'de sunucu düzeyinde temel kimlik doğrulamasını etkinleştirdiniz mi?
- Web yönetimi hizmetine uzak bağlantıları etkinleştirdiniz mi?
- Web yönetimi hizmetini başlatmış musunuz?
- Yönetim hizmeti temsili kuralları var mı?
- Uygulama havuzu kimliği, Web sitenizin kaynak klasörüne okuma erişimine sahip mi?
- Yönetici olmayan kullanıcı hesabı IIS 'de site düzeyi izinlere sahip mi?
- Güvenlik duvarınız 8172 numaralı TCP bağlantı noktasındaki sunucuya gelen bağlantılara izin veriyor mu?

## <a name="further-reading"></a>Daha Fazla Bilgi

Web paketlerini Web Dağıtımı Işleyicisine dağıtmak üzere özel Microsoft Build Engine (MSBuild) proje dosyalarını yapılandırma hakkında yönergeler için bkz. [bir hedef ortam Için dağıtım özelliklerini yapılandırma](configuring-deployment-properties-for-a-target-environment.md).

> [!div class="step-by-step"]
> [Önceki](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [İleri](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
