---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
title: Bir Web sunucusunu Web Dağıtımı yayımlama için yapılandırma (uzak Aracı) | Microsoft Docs
author: jrjlee
description: Bu konu, IIS Web dağıtımı kullanarak Web yayımlaması ve dağıtımı desteklemek için bir Internet Information Services (IIS) Web sunucusunun nasıl yapılandırılacağını açıklamaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 239c7aa8-d09a-4d02-9c0e-6bd52be5f0d5
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent
msc.type: authoredcontent
ms.openlocfilehash: ce0d246afdfb65c2ea15a287064511e7d1d58622
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589046"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-remote-agent"></a>Bir Web Sunucusunu Web Dağıtımı Yayımlama için Yapılandırma (Uzak Aracı)

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konuda, IIS Web Dağıtım Aracı (Web Dağıtımı) uzak Aracı hizmeti kullanılarak Web yayımlaması ve dağıtımı desteklemek için bir Internet Information Services (IIS) Web sunucusunun nasıl yapılandırılacağı açıklanmaktadır.
> 
> Web Dağıtımı 2,0 veya sonraki bir sürümüyle çalışırken, uygulamalarınızı veya sitelerinizi bir Web sunucusuna almak için kullanabileceğiniz üç ana yaklaşım vardır. Şunları yapabilirsiniz:
> 
> - *Web dağıtımı uzak aracı hizmetini*kullanın. Bu yaklaşım, Web sunucusu için daha az yapılandırma gerektirir, ancak sunucuya her şeyi dağıtmak için bir yerel sunucu yöneticisinin kimlik bilgilerini sağlamanız gerekir.
> - *Web dağıtımı işleyicisini*kullanın. Bu yaklaşım çok daha karmaşıktır ve Web sunucusunu ayarlamak için daha fazla ilk çaba gerektirir. Ancak, bu yaklaşımı kullandığınızda, IIS 'yi yönetici olmayan kullanıcıların dağıtımı gerçekleştirmesine izin verecek şekilde yapılandırabilirsiniz. Web Dağıtımı Işleyicisi yalnızca IIS sürüm 7 veya üzeri sürümlerde kullanılabilir.
> - *Çevrimdışı dağıtım*kullanın. Bu yaklaşım, Web sunucusu için en az yapılandırmayı gerektirir, ancak bir sunucu yöneticisinin Web paketini sunucuya el ile kopyalaması ve IIS Yöneticisi aracılığıyla içeri aktarması gerekir.
> 
> Bu yaklaşımların temel özellikleri, avantajları ve dezavantajları hakkında daha fazla bilgi için, bkz. [Web dağıtımına doğru yaklaşımı seçme](choosing-the-right-approach-to-web-deployment.md).

## <a name="is-the-web-deploy-remote-agent-the-right-approach-for-you"></a>Web Dağıtımı uzak aracı sizin için doğru yaklaşımda mi?

Evet, içeriği dağıtan Kullanıcı hedef sunucuda bir yöneticinin kimlik bilgilerini sağlayabilir. Bu yaklaşım genellikle bu tür senaryolarda tercih edilir:

- Geliştirme veya test ortamları, geliştirici hedef Web sunucusu ve veritabanı sunucusu üzerinde tam denetime sahiptir.
- Tek bir kullanıcının veya küçük bir Kullanıcı grubunun tüm uygulama yaşam döngüsü üzerinde denetime sahip olduğu daha küçük kuruluşlar.

Çoğu daha büyük kuruluşta ve özellikle de hazırlama veya üretim ortamlarında, kullanıcılara Web sunucuları üzerinde yönetici hakları vermek gerçekçi değildir. Barındırılan Web sunucuları söz konusu olduğunda bu durum özellikle büyük olasılıkla düşüktür. Ayrıca, bir yapı sunucusundan dağıtımı otomatik hale getirmeyi planlıyorsanız, dağıtım işlemi için yönetici kimlik bilgilerini kullanmak istemeyebilirsiniz. Bu senaryolarda, Web sunucularınızı [Web dağıtımı işleyicisini](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md) kullanarak dağıtımı destekleyecek şekilde yapılandırmak, daha tatmin edici bir seçenek sağlayabilir.

## <a name="task-overview"></a>Göreve genel bakış

Bu konuda, Web Dağıtımı uzak Aracı yaklaşımını kullanarak uzak bir bilgisayardan Web paketlerini kabul etmek ve dağıtmak üzere bir Internet Information Services (IIS) 7,5 Web sunucusunun nasıl yapılandırılacağı açıklanmaktadır. Şunları yapmanız gerekir:

- IIS 7,5 ve IIS 7 önerilen yapılandırmayı yükler.
- Web Dağıtımı 2,1 veya üstünü yükler.
- Dağıtılan içeriği barındırmak için bir IIS Web sitesi oluşturun.
- Web Deployment Agent hizmetinin çalıştığından emin olun.

Örnek çözümü özellikle barındırmak için şunları yapmanız gerekir:

- 4,0 .NET Framework 'yi yükler.
- ASP.NET MVC 3 ' ü yükler.

Bu konu, bu yordamların her birini nasıl gerçekleştirekullanacağınızı gösterir. Bu konudaki görevler ve izlenecek yollar, Windows Server 2008 R2 çalıştıran bir temiz sunucu derlemesi ile başladığınızı varsayar. Devam etmeden önce aşağıdakileri doğrulayın:

- Windows Server 2008 R2 Service Pack 1 ve tüm kullanılabilir güncelleştirmeler yüklendi.
- Sunucu etki alanına katılmış.
- Sunucunun statik bir IP adresi vardır.

> [!NOTE]
> Bilgisayarları etki alanına katma hakkında daha fazla bilgi için bkz. [bilgisayarları etki alanına katma ve oturum açma](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Statik IP adreslerini yapılandırma hakkında daha fazla bilgi için bkz. [STATIK IP adresi yapılandırma](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx). Uzak Aracı hizmeti IIS 6 ' dan itibaren desteklenir ve bir etki alanına katılmaları gerekmez. Ancak, bu öğreticideki adımlar IIS 7,5 ' de geliştirilmiştir ve test edilmiştir ve diğer sürümlerin yordamları farklılık gösterebilir.

## <a name="install-products-and-components"></a>Ürün ve bileşenleri yükler

Bu bölüm, Web sunucusuna gerekli ürün ve bileşenleri yükleme konusunda size kılavuzluk eder. Başlamadan önce, sunucunuzun tamamen güncel olduğundan emin olmak için Windows Update çalıştırmak iyi bir uygulamadır.

Bu durumda, şunları yüklemeniz gerekir:

- **IIS 7 önerilen yapılandırma**. Bu, Web sunucunuzda **Web sunucusu (IIS)** rolünü sağlar ve bir ASP.NET uygulamasını barındırmak için IHTIYAç duyduğunuz IIS modülleri ve bileşenleri kümesini kurar.
- **.NET Framework 4,0**. Bu, .NET Framework bu sürümünde oluşturulan uygulamaları çalıştırmak için gereklidir.
- **Web dağıtımı aracı 2,1 veya sonraki bir sürümü**. Bu, sunucunuza Web Dağıtımı (ve temel alınan yürütülebilir dosyası, MSDeploy. exe) yüklenir. Bu işlemin bir parçası olarak Web Deployment Agent hizmetini yükleyip başlatır. Bu hizmet, uzak bir bilgisayardan Web paketleri dağıtmanızı sağlar.
- **ASP.NET MVC 3**. Bu, MVC 3 uygulamalarını çalıştırmak için gereken derlemeleri kurar.

> [!NOTE]
> Bu izlenecek yol, gerekli bileşenleri yüklemek ve yapılandırmak için Web Platformu Yükleyicisi 'nin kullanımını açıklar. Web platformu yükleyicisini kullanmanıza gerek olmasa da, bağımlılıkları otomatik olarak algılayarak ve en son ürün sürümlerini her zaman almanızı sağlayarak yükleme işlemini basitleştirir. Daha fazla bilgi için bkz. [Microsoft Web Platformu Yükleyicisi 3,0](https://go.microsoft.com/?linkid=9805118).

**Gerekli ürünleri ve bileşenleri yüklemek için**

1. [Web platformu yükleyicisini](https://go.microsoft.com/?linkid=9805118)indirip yükleyin.
2. Yükleme tamamlandığında, Web Platformu Yükleyicisi otomatik olarak başlatılır.

    > [!NOTE]
    > Artık **Başlangıç** menüsünden Web Platformu Yükleyicisi 'ni dilediğiniz zaman başlatabilirsiniz. Bunu yapmak için, **Başlat** menüsünde, **tüm programlar**' a ve ardından **Microsoft Web Platformu Yükleyicisi**' ye tıklayın.
3. **Web platformu yükleyicisi 3,0** penceresinin en üstünde, **Ürünler**' e tıklayın.
4. Pencerenin sol tarafında, gezinti bölmesinde, **çerçeveler**' e tıklayın.
5. **Microsoft .NET Framework 4** satırında, .NET Framework zaten yüklenmemişse **Ekle**' ye tıklayın.

    > [!NOTE]
    > .NET Framework 4,0 ' i Windows Update aracılığıyla zaten yüklemiş olabilirsiniz. Bir ürün veya bileşen zaten yüklüyse, Web Platformu Yükleyicisi, **Ekle** düğmesini **yüklü**olan metinle değiştirerek bunu gösterir.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image1.png)
6. **ASP.NET MVC 3 (Visual Studio 2010)** satırında **Ekle**' ye tıklayın.
7. Gezinti bölmesinde **sunucu**' ya tıklayın.
8. **IIS 7 önerilen yapılandırma** satırında **Ekle**' ye tıklayın.
9. **Web Dağıtım aracı 2,1** satırında **Ekle**' ye tıklayın.
10. **Yükle**'ye tıklatın. Web Platformu Yükleyicisi, yüklenecek ilişkili bağımlılıklarla&#x2014;&#x2014;birlikte ürünlerin bir listesini gösterir ve lisans koşullarını kabul etmenizi ister.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image2.png)
11. Lisans koşullarını gözden geçirin ve koşulları **onayladıysanız kabul ediyorum**' a tıklayın.
12. Yükleme tamamlandığında, **son**' a tıklayın ve ardından **Web Platformu Yükleyicisi 3,0** penceresini kapatın.

IIS 'yi yüklemeden önce 4,0 .NET Framework yüklediyseniz, en son ASP.NET sürümünü IIS ile kaydettirmek için [ASP.NET IIS kayıt aracı](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) 'nı (ASPNET\_regııs. exe) çalıştırmanız gerekir. Bunu yapmazsanız, IIS 'nin herhangi bir sorun olmadan statik içerik (HTML dosyaları gibi) sunacağını, ancak ASP.NET içeriğine gözatmaya çalıştığınızda, **http hatası 404,0 –** döndürülmeyeceğini göreceksiniz. Bu yordamı, ASP.NET 4,0 'in kaydedildiğinden emin olmak için kullanabilirsiniz.

**ASP.NET 4,0 'i IIS ile kaydetmek için**

1. **Başlat**' a tıklayın ve ardından **komut istemi**yazın.
2. Arama sonuçlarında **komut istemi**' ne sağ tıklayın ve ardından **yönetici olarak çalıştır**' a tıklayın.
3. Komut Istemi penceresinde **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** dizinine gidin.
4. Bu komutu yazın ve ENTER tuşuna basın:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample1.cmd)]
5. Herhangi bir noktada 64 bitlik Web uygulamalarını barındırmak istiyorsanız, ASP.NET 'in 64 bit sürümünü de IIS ile kaydetmeniz gerekir. Bunu yapmak için, komut Istemi penceresinde **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** dizinine gidin.
6. Bu komutu yazın ve ENTER tuşuna basın:

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-remote-agent/samples/sample2.cmd)]

İyi bir uygulama olarak, yüklediğiniz yeni ürün ve bileşenler için kullanılabilir güncelleştirmeleri indirmek ve yüklemek üzere bu noktada Windows Update yeniden kullanın.

## <a name="configure-the-iis-website"></a>IIS Web sitesini yapılandırma

Sunucunuza Web içeriği dağıtabilmeniz için önce içeriği barındırmak üzere bir IIS Web sitesi oluşturmanız ve yapılandırmanız gerekir. Web Dağıtımı, yalnızca mevcut bir IIS Web sitesine web paketleri dağıtabilir; sizin için Web sitesini oluşturamaz. Yüksek düzeyde, bu görevleri gerçekleştirmeniz gerekir:

- İçeriğinizi barındırmak için dosya sisteminde bir klasör oluşturun.
- İçeriği sunacak bir IIS Web sitesi oluşturun ve Yerel klasörle ilişkilendirin.
- Yerel klasördeki uygulama havuzu kimliği için okuma izinleri verin.

İçeriği IIS 'de varsayılan Web sitesine dağıtmaktan hiçbir şey yapmamaya rağmen, bu yaklaşım test veya tanıtım senaryolarından başka hiçbir şey için önerilmez. Bir üretim ortamının benzetimini yapmak için, uygulamanızın gereksinimlerine özel ayarlarla yeni bir IIS Web sitesi oluşturmanız gerekir.

**Bir IIS Web sitesi oluşturmak ve yapılandırmak için**

1. Yerel dosya sisteminde içeriğinizi depolamak için bir klasör oluşturun (örneğin, **C:\demosite**).
2. **Başlat** menüsünde, **Yönetim Araçları**' nın üzerine gelin ve ardından **Internet Information Services (IIS) Yöneticisi**' ne tıklayın.
3. IIS Yöneticisi 'nde, **Bağlantılar** bölmesinde, sunucu düğümünü genişletin (örneğin, **TESTWEB1**).

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image3.png)
4. **Siteler** düğümüne sağ tıklayın ve ardından **Web sitesi Ekle**' ye tıklayın.
5. **Site adı** kutusuna IIS Web sitesi için bir ad yazın (örneğin, **demosite**).
6. **Fiziksel yol** kutusunda, yerel klasörünüzün yolunu yazın (veya konumuna gidin) (örneğin, **c:\demosite**).
7. **Bağlantı noktası** kutusuna, Web sitesini barındırmak istediğiniz bağlantı noktası numarasını yazın (örneğin, **85**).

    > [!NOTE]
    > Standart bağlantı noktası numaraları HTTP için 80, HTTPS için 443 ' dir. Ancak, bu Web sitesini 80 numaralı bağlantı noktasında barındırdıysanız, sitenize erişebilmek için önce varsayılan Web sitesini durdurmanız gerekir.
8. Web sitesi için bir etki alanı adı sistemi (DNS) kaydı yapılandırmak istemediğiniz müddetçe, **ana bilgisayar adı** kutusunu boş bırakın ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image4.png)

    > [!NOTE]
    > Bir üretim ortamında, büyük ihtimalle Web sitenizi bağlantı noktası 80 ' de barındırmak ve eşleşen DNS kayıtlarıyla birlikte bir ana bilgisayar üst bilgisi yapılandırmak isteyeceksiniz. IIS 7 ' de konak üstbilgilerini yapılandırma hakkında daha fazla bilgi için bkz. [bir Web sitesi için bir konak üstbilgisi yapılandırma (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx). Windows Server 2008 R2 'deki DNS sunucusu rolü hakkında daha fazla bilgi için bkz. [DNS sunucusuna genel bakış](https://technet.microsoft.com/library/cc770392.aspx) ve [DNS sunucusu](https://technet.microsoft.com/windowsserver/dd448607).
9. **Eylemler** bölmesinde, **Site Düzenle**altında, **Bağlamalar**'ı tıklatın.
10. **Site bağlamaları** Iletişim kutusunda **Ekle**' ye tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image5.png)
11. **Site Bağlaması Ekle** iletişim kutusunda, **IP adresini** ve **bağlantı noktasını** mevcut site yapılandırmanızla eşleşecek şekilde ayarlayın.
12. **Ana bilgisayar adı** kutusuna Web sunucunuzun adını yazın (örneğin, **TESTWEB1**) ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image6.png)

    > [!NOTE]
    > İlk site bağlaması, IP adresini ve bağlantı noktasını veya `http://localhost:85`kullanarak siteye yerel olarak erişmenizi sağlar. İkinci site bağlaması, makine adını (örneğin, http://testweb1:85) kullanarak etki alanındaki diğer bilgisayarlardan siteye erişmenize olanak tanır.
13. **Site bağlamaları** Iletişim kutusunda **Kapat**' a tıklayın.
14. **Bağlantılar** bölmesinde, **uygulama havuzları**' na tıklayın.
15. **Uygulama havuzları** bölmesinde, uygulama havuzunuzun adına sağ tıklayın ve ardından **temel ayarlar**' a tıklayın. Varsayılan olarak, uygulama havuzunuzun adı, Web sitenizin adıyla (örneğin, **Demosite**) eşleşir.
16. **.NET Framework sürüm** listesinde **.NET Framework v 4.0.30319**' ı seçin ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image7.png)

    > [!NOTE]
    > Örnek çözüm .NET Framework 4,0 gerektirir. Bu, genel olarak Web Dağıtımı için bir gereklilik değildir.

Web sitenizin içeriğe içerik sunması için, uygulama havuzu kimliğinin içeriği depolayan yerel klasörde Okuma izinlerine sahip olması gerekir. IIS 7,5 ' de, uygulama havuzları varsayılan olarak benzersiz bir uygulama havuzu kimliğiyle çalışır (IIS 'nin önceki sürümlerinin aksine, uygulama havuzlarının genellikle ağ hizmeti hesabı kullanılarak çalıştığı). Uygulama havuzu kimliği gerçek bir kullanıcı hesabı değil ve bunun yerine hiçbir Kullanıcı veya grup&#x2014;listesinde gösterilmez, uygulama havuzu başlatıldığında dinamik olarak oluşturulur. Her uygulama havuzu kimliği, gizli bir öğe olarak yerel **ııs\_ıusrs** güvenlik grubuna eklenir.

Bir dosya veya klasördeki uygulama havuzu kimliğine izin vermek için iki seçeneğiniz vardır:

- <strong>IIS AppPool\</strong ><em>[uygulama havuzu adı]</em>biçimini kullanarak doğrudan uygulama havuzu kimliğine izin atayın (örneğin, <strong>IIS AppPool\DemoSite</strong>).
- **Iıs\_ıusrs** grubuna izinler atayın.

Bu yaklaşım, dosya sistemi izinlerini yeniden yapılandırmadan uygulama havuzlarını değiştirmenize olanak sağladığından, en yaygın yaklaşım, yerel **ııs\_ıusrs** grubuna izin atanmalıdır. Sonraki yordam bu grup tabanlı yaklaşımı kullanır.

> [!NOTE]
> IIS 7,5 ' deki uygulama havuzu kimlikleri hakkında daha fazla bilgi için bkz. [uygulama havuzu kimlikleri](https://go.microsoft.com/?linkid=9805123).

**Bir IIS Web sitesi için klasör izinlerini yapılandırmak için**

1. Windows Gezgini 'nde yerel klasörünüzün konumuna gidin.
2. Klasöre sağ tıklayın ve ardından **Özellikler**' e tıklayın.
3. **Güvenlik** sekmesinde, **Düzenle**' ye tıklayın ve ardından **Ekle**' ye tıklayın.
4. **Konumlar**' a tıklayın. **Konumlar** iletişim kutusunda yerel sunucuyu seçin ve ardından **Tamam**' a tıklayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image8.png)
5. **Kullanıcıları veya grupları seç** Iletişim kutusunda **IIS\_ıusrs**yazın, **adları denetle**' ye tıklayın ve ardından **Tamam**' a tıklayın.
6. <em>[Klasör adı]</em> <strong>izinleri</strong>iletişim kutusunda yeni gruba, varsayılan olarak <strong>okuma &amp; yürütme</strong>, <strong>klasör içeriğini listeleme</strong>ve <strong>okuma</strong> izinleri atandığını görürsünüz. Bunu değiştirmeden bırakın ve <strong>Tamam 'a</strong>tıklayın.
7. <em>[Klasör adı]</em><strong>özellikleri</strong> Iletişim kutusunu kapatmak için <strong>Tamam</strong> ' ı tıklatın.

Sunucunuza herhangi bir Web paketi dağıtmayı denemeden önce son bir görev olarak, Web Deployment Agent hizmetinin çalıştığından emin olmanız gerekir. Bir paketi uzak bir bilgisayardan dağıtırken, Web Deployment Agent hizmeti, paketin içeriğini ayıklamaktan ve yüklemekten sorumludur. Web Dağıtım aracını yüklediğinizde ve ağ hizmeti kimliği altında çalışırken hizmet varsayılan olarak başlatılır.

Çeşitli komut satırı yardımcı programları veya Windows PowerShell cmdlet 'leri kullanarak bir hizmetin birden çok farklı şekilde çalışıp çalışmadığını kontrol edebilirsiniz. Bu yordamda, basit bir UI tabanlı yaklaşım açıklanmaktadır.

**Web Deployment Agent hizmetinin çalıştığını denetlemek için**

1. **Başlat** menüsünde, **Yönetim Araçları**'na gelin ve ardından **Hizmetler**'e tıklayın.
2. **Web Deployment Agent hizmeti** satırını bulun ve **durumun** **başlatıldı**olarak ayarlandığını doğrulayın.

    ![](configuring-a-web-server-for-web-deploy-publishing-remote-agent/_static/image9.png)
3. Hizmet henüz başlatılmamışsa **Başlat**' a tıklayın.

## <a name="configure-firewall-exceptions"></a>Güvenlik Duvarı özel durumlarını yapılandırma

Varsayılan olarak, uzak Aracı hizmeti TCP bağlantı noktası 80 ' u Şu URL 'de dinler:

<http://servername.com/MSDEPLOYAGENTSERVICE>

Çoğu durumda, Web sunucuları genellikle bağlantı noktası 80 üzerinde HTTP isteklerini dinlerken, uzak Aracı hizmeti için ek güvenlik duvarı kuralları yapılandırmanız gerekmez. Yüklemeyi standart olmayan bir bağlantı noktasında dinlemek üzere özelleştirdiyseniz, güvenlik duvarı özel durumlarını gerektiği şekilde yapılandırmanız gerekir.

## <a name="conclusion"></a>Sonuç

Bu noktada, Web sunucunuz uzak bir bilgisayardan Web paketlerini kabul etmeye ve yüklemeye uygun olur. Bir Web uygulamasını sunucusuna dağıtmayı denemeden önce şu anahtar noktalarını denetlemek isteyebilirsiniz:

- ASP.NET 4,0 'i IIS ile kaydettiniz mi?
- Uygulama havuzu kimliği, Web sitenizin kaynak klasörüne okuma erişimine sahip mi?
- Web Deployment Agent hizmeti çalışıyor mu?

## <a name="further-reading"></a>Daha Fazla Bilgi

Web paketlerini uzak Aracı hizmetine dağıtmak üzere özel Microsoft Build Engine (MSBuild) proje dosyalarını yapılandırma hakkında yönergeler için bkz. [bir hedef ortam Için dağıtım özelliklerini yapılandırma](configuring-deployment-properties-for-a-target-environment.md).

> [!div class="step-by-step"]
> [Önceki](scenario-configuring-a-production-environment-for-web-deployment.md)
> [İleri](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
