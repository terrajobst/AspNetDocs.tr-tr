---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
title: Web grubu çerçevesi ile sunucu grubu oluşturma | Microsoft Docs
author: jrjlee
description: Bu konu başlığı altında, bir Web sunucusu grubunu sunucu koleksiyonundan oluşturmak ve yapılandırmak için Web grubu çerçevesi 'nin (WFF) 2,0 nasıl kullanılacağı açıklanmaktadır.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 656dd06d-806c-467c-863d-9fc45e5ba3ab
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework
msc.type: authoredcontent
ms.openlocfilehash: 204996514bed336e60ab77f184a923f04e7e2bba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637251"
---
# <a name="creating-a-server-farm-with-the-web-farm-framework"></a>Web Farm Framework ile Sunucu Grubu Oluşturma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu başlığı altında, bir Web sunucusu grubunu sunucu koleksiyonundan oluşturmak ve yapılandırmak için Web grubu çerçevesi 'nin (WFF) 2,0 nasıl kullanılacağı açıklanmaktadır.

WFF, Web platformu ürünlerini ve bileşenlerini, Web uygulamalarını, Web sitelerini ve yapılandırma ayarlarını birden çok yük dengeli Web sunucusu arasında eşitlemenize olanak tanır. Hazırlama ve üretim ortamları gibi birden fazla Web sunucusuna ihtiyacınız olan senaryolarda, bu, dağıtım ve yapılandırma işleminizi büyük ölçüde kolaylaştırabilir. Bir Web uygulamasını tek bir sunucuya&#x2014;dağıtabilmeniz için *birincil sunucu*&#x2014;ve wff, bu Web uygulamasını sunucu grubundaki diğer tüm Web sunucularında otomatik olarak çoğaltır.

## <a name="understanding-the-web-farm-framework"></a>Web grubu çerçevesini anlama

Bir Web sunucuları grubuna içerik sağlamak, yönetmek ve dağıtmak için WFF 2,0 kullanabilirsiniz. WFF dağıtımı üç temel sunucu rolünden oluşur:

- *Denetleyici sunucusu*. WFF sunucu grupları oluşturmak ve yapılandırmak için bu sunucuyu kullanırsınız. Denetleyici sunucusu, Web platformu bileşenlerinin, yapılandırma ayarlarının ve sunucu grubundaki Web sunucuları arasındaki uygulamaların eşitlemesini yönetir. WFF 2,0 ' i denetleyici sunucusuna yüklersiniz ve denetleyici sunucusu bir sunucu grubundaki sunucuların her birine WFF Aracısı 'nı yükler. Denetleyici sunucusu, herhangi bir WFF sunucu grubuna kavramsal değildir ve tek bir denetleyici sunucusu birden çok sunucu grubunu yönetebilir. Bu senaryoda, hazırlama sunucusu grubunu ve üretim sunucusu grubunu oluşturmak ve yönetmek için tek bir WFF denetleyici sunucusu kullanırsınız.
- *Birincil sunucu*. Her WFF sunucu grubu tek bir birincil sunucu içerir. Web Platformu bileşenlerini yüklediğinizde veya birincil sunucuya uygulamalar dağıttığınızda WFF, değişikliklerinizi sunucu grubundaki diğer tüm sunucularda eşitler.
- *İkincil sunucu*. Her WFF sunucu grubu bir veya daha fazla ikincil sunucu içerir. Birincil sunucuda yaptığınız tüm değişiklikler sunucu grubu içindeki her ikincil sunucuya çoğaltılır.

Bu, bu sunucu rollerinin Fabrikam, Inc. hazırlama ve üretim ortamları ile ilişkisini gösterir:

![](creating-a-server-farm-with-the-web-farm-framework/_static/image1.png)

Bu senaryoda, hazırlama ortamı ve üretim ortamının her ikisi de WFF sunucu grupları olarak yapılandırılır. Tek bir WFF denetleyici sunucusu her iki grubu da yönetir. Her bir sunucu grubunda, birincil sunucuda yapılan tüm değişiklikler tüm ikincil sunucuya çoğaltılır.

Hazırlama ve üretim ortamlarınızı yapılandırmaya başlamadan önce, WFF 2,0 'nin temel kavramlarını tanımak için bu makaleleri okumanızı öneririz:

- [IIS 7 için Web grubu çerçevesi 2,0 'ye Genel Bakış](https://go.microsoft.com/?linkid=9805126)
- [IIS 7 için Web grubu çerçevesi 2,0 ile sunucu grubu ayarlama](https://go.microsoft.com/?linkid=9805127)
- [IIS 7 için Web grubu çerçevesi 2,0 için sistem ve platform gereksinimleri](https://go.microsoft.com/?linkid=9805128)

## <a name="task-overview"></a>Göreve genel bakış

Bu konudaki görevleri ve izlenecek yolları tamamlayabilmeniz için, en az üç sunucu&#x2014;bir wff denetleyicisine, sunucu grubu için bir birincil web sunucusuna ve sunucu grubu için bir veya daha fazla ikincil Web sunucusuna ihtiyacınız vardır. İstediğiniz zaman WFF sunucu grubuna daha fazla ikincil sunucu ekleyebilirsiniz. Yüksek düzeyde, hazırlama veya üretim ortamınız için bir WFF sunucu grubu oluşturup yapılandırmak üzere şunları yapmanız gerekir:

- Internet Information Services (IIS) 7,5 ve WFF 2,0 ' i yükleyerek bir denetleyici sunucusu oluşturun.
- Ortak bir yönetici hesabı oluşturarak ve güvenlik duvarı özel durumlarını yapılandırarak birincil ve ikincil sunucuları hazırlayın.
- Denetleyici sunucusunda IIS Yöneticisi 'Ni kullanarak sunucu grubunu yapılandırın.
- IIS uygulama Isteği yönlendirme (ARR) veya alternatif bir yük dengeleme teknolojisini kullanarak yük dengelemeyi yapılandırın.

Bu konudaki görevler ve izlenecek yollar, Windows Server 2008 R2 çalıştıran temiz sunucu Derlemeleriyle başladığınızı varsayar. Başlamadan önce, her sunucu için şunları doğrulayın:

- Windows Server 2008 R2 Service Pack 1 ve tüm kullanılabilir güncelleştirmeler yüklendi.
- Sunucu etki alanına katılmış.
- Sunucunun statik bir IP adresi vardır.

> [!NOTE]
> Bilgisayarları etki alanına katma hakkında daha fazla bilgi için bkz. [bilgisayarları etki alanına katma ve oturum açma](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx). Statik IP adreslerini yapılandırma hakkında daha fazla bilgi için bkz. [STATIK IP adresi yapılandırma](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).

## <a name="create-the-wff-controller-server"></a>WFF denetleyici sunucusunu oluşturma

WFF denetleyici sunucusu oluşturmak için hem IIS 7, hem de WFF 2,0 veya üstünü yüklemeniz gerekir. Kapakların altında WFF, grubunuzdaki sunucuları senkronize etmek için IIS Web Dağıtım aracı 'nı (Web Dağıtımı) 2. x kullanır. WFF 'yi yüklemek için Web Platformu Yükleyicisi 'ni kullanırsanız, yükleyici sizin için Web Dağıtımı otomatik olarak indirip yükler.

**WFF denetleyici sunucusunu oluşturmak için**

1. [Web platformu yükleyicisini](https://go.microsoft.com/?linkid=9739157)indirip yükleyin.
2. **Web platformu yükleyicisi 3,0** penceresinin en üstünde, **Ürünler**' e tıklayın.
3. Pencerenin sol tarafında, gezinti bölmesinde, **sunucu**' ya tıklayın.
4. **IIS 7 önerilen yapılandırma** satırında **Ekle**' ye tıklayın.
5. <strong>Web grubu Framework 2.</strong> <em>x</em> satırı, <strong>Ekle</strong>' ye tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image2.png)
6. **Yükle**'ye tıklatın. Web platformu yükleyicisinin Web Dağıtım aracını, diğer diğer bağımlılıklarla birlikte yükleme listesine eklediğine dikkat edin.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image3.png)
7. Lisans koşullarını gözden geçirin ve koşulları **onayladıysanız kabul ediyorum**' a tıklayın.
8. Yükleme tamamlandığında, **son**' a tıklayın ve ardından **Web Platformu Yükleyicisi 3,0** penceresini kapatın.

## <a name="configure-the-primary-and-secondary-servers"></a>Birincil ve Ikincil sunucuları yapılandırma

Bir WFF sunucu grubu oluşturmadan önce, grubu oluşturacak Web sunucularındaki bazı hazırlık görevlerini gerçekleştirmeniz gerekir:

- **Çekirdek ağ**, **Uzaktan Yönetim**ve **dosya ve yazıcı paylaşım** özelliklerinin wff denetleyici sunucusuyla iletişim kurmasına izin vermek için güvenlik duvarı özel durumları ekleyin.
- Active Directory bir etki alanı hesabı oluşturun (örneğin, **FABRIKAM\stagingfarm**) ve her bir sunucuda yerel Yöneticiler grubuna ekleyin. Sunucu grubunu oluştururken bu hesabı sunucu grubu yönetici hesabı olarak kullanacaksınız.

Windows Güvenlik Duvarı 'nda bu güvenlik duvarı özel durumlarını yapılandırma hakkında daha fazla bilgi için bkz. [IIS Için Web grubu çerçevesi 2,0 Için sistem ve platform gereksinimleri](https://go.microsoft.com/?linkid=9805128). Diğer güvenlik duvarı sistemleri için ürün belgelerinize bakın.

Windows Server 2008 R2 'de yerel Yöneticiler grubuna bir etki alanı hesabı eklemek için sonraki yordamı kullanabilirsiniz. Diğer bir deyişle sunucu grubuna&#x2014;eklemek istediğiniz her sunucuda bu yordamı gerçekleştirmeniz gerekir, aynı etki alanı hesabını birincil sunucuda ve her ikincil sunucuda yerel Yöneticiler grubuna ekleyin.

**Yerel Yöneticiler grubuna bir etki alanı hesabı eklemek için**

1. **Başlat** menüsünde, **Yönetim Araçları**' nın üzerine gelin ve **Sunucu Yöneticisi**' ye tıklayın.
2. **Sunucu Yöneticisi** penceresinde, ağaç görünümü bölmesinde, **yapılandırma**, **yerel kullanıcılar ve gruplar**' ı genişletin ve ardından **gruplar**' a tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image4.png)
3. **Gruplar** bölmesinde **Yöneticiler**' e çift tıklayın.
4. **Yöneticiler özellikleri** Iletişim kutusunda **Ekle**' ye tıklayın.
5. **Kullanıcıları, bilgisayarları, hizmet hesaplarını veya grupları seç** iletişim kutusunda, etki alanı hesabınıza (örneğin, **FABRIKAM\stagingfarm**) yazın (veya tarayın) ve ardından **Tamam**' a tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image5.png)
6. **Yöneticiler özellikleri** Iletişim kutusunda **Tamam**' a tıklayın.

Sunucularınız artık bir sunucu grubuna eklenmek için hazırdır. Birincil sunucu söz konusu olduğunda, sunucuyu her iki durumda da sunucu grubunu&#x2014;oluşturmadan önce veya sonra, uygulama gereksinimlerinizi karşılayacak şekilde yapılandırabilirsiniz. wff, ikincil sunucularınıza aynı ürünleri, bileşenleri veya yapılandırmayı dağıtarak sunucuları eşitler. Kolaylık sağlaması için, bu öğreticide, sunucu grubunu oluşturmayı bitirdiğinizde birincil sunucuyu yapılandıracaksınız.

## <a name="create-the-wff-server-farm"></a>WFF sunucu grubu oluşturma

Bu noktada, tüm sunucularınız bir WFF sunucu grubuna eklenmek üzere hazırlanmalıdır:

- Denetleyici sunucusuna WFF yüklediniz.
- Birincil ve ikincil web sunucularınızda güvenlik duvarı özel durumları yapılandırdınız.
- Birincil ve ikincil web sunucularınızda yerel Yöneticiler grubuna bir etki alanı hesabı eklediniz.

Sonraki adım, sunucu grubunu WFF içinde oluşturmaktır. Bunu, WFF denetleyicisi sunucusunda IIS Yöneticisi 'nden yapabilirsiniz.

**WFF sunucu grubu oluşturmak için**

1. WFF denetleyicisi sunucusunda, **Başlat** menüsünde, **Yönetim Araçları**' nın üzerine gelin ve ardından **Internet Information Services (IIS) Yöneticisi**' ne tıklayın.
2. **Bağlantılar** bölmesinde, yerel sunucu düğümünü genişletin, **sunucu grupları**' na sağ tıklayın ve ardından **sunucu grubu oluştur**' a tıklayın.
3. **Sunucu grubu oluştur** iletişim kutusunda, sunucu grubu için anlamlı bir ad yazın (örneğin, **hazırlama grubu**) ve ardından **sunucu grubu sağla**' yı seçin.
4. Her bir sunucuda yerel Yöneticiler grubuna eklediğiniz etki alanı hesabının kullanıcı adını ve parolasını yazın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image6.png)
5. **İleri**'ye tıklayın.
6. **Sunucu Ekle** sayfasında, birincil sunucunun tam etki alanı adını (FQDN) yazın, **birincil sunucu**' yı seçin ve ardından **Ekle**' ye tıklayın.
7. Bu noktada WFF, verdiğiniz kimlik bilgilerini kullanarak birincil sunucuyla iletişim kurmayı dener. Bağlantı başarılı olursa, birincil sunucu sunucu **Ekle** sayfasındaki tabloya eklenecektir.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image7.png)

    > [!NOTE]
    > **Sunucunun, yük dengeleme için** varsayılan olarak kullanılabildiğini fark etmiş olabilirsiniz. WFF, yük dengelemeyi uygulamak için IIS ARR modülünü kullanır ve bu sayede istekleri sunucu grubunuzdaki Web sunucuları arasında dağıtır. Çoğu senaryoda, yalnızca bir üçüncü taraf yük dengeleme çözümü kullanmak isterseniz, **Yük Dengeleme seçeneği Için sunucu 'nun kullanılabilir olduğunu** temizlemelisiniz.
8. **Sunucu Ekle** sayfasında, ilk IKINCIL sunucunuzun FQDN 'sini yazın ve ardından **Ekle**' ye tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image8.png)
9. Grubunuzdaki diğer ikincil sunucular için 7. adımı tekrarlayın ve ardından **son**' a tıklayın.

WFF sunucu grubunuz artık çalışıyor ve çalışıyor. Birincil sunucuya yüklediğiniz tüm Web platformu ürünleri veya bileşenleri ve birincil sunucuya dağıttığınız tüm Web uygulamaları veya içerikler, tüm ikincil sunucularınızda otomatik olarak sağlanır.

WFF, geniş ve karmaşık bir konudur ve BT hakkında daha fazla bilgi edinmek için bkz. [IIS 7 Web sitesi Için Microsoft Web grubu çerçevesi 2,0](https://go.microsoft.com/?linkid=9805129) . Ancak, şu anda bilmeniz gereken iki özellik alanı vardır:

- *Uygulama sağlama* , Web uygulamaları ve yapılandırma ayarları gibi birincil sunucudan, sunucu grubundaki tüm ikincil sunucular üzerinde içerik çoğaltılan bir işlemdir. Örneğin, birincil hazırlama sunucunuza Contact Manager örnek çözümünü dağıtırsanız, WFF uygulama sağlama işlemi bu çözümü tüm ikincil hazırlama sunucularınıza dağıtır. Varsayılan olarak, uygulama sağlama işlemi her 30 saniyede bir çalışır.
- *Platform sağlama* , Web platformu ürünlerini ve bileşenlerini birincil sunucudan sunucu grubundaki tüm ikincil sunucularla eşitleyen işlemdir. Örneğin, birincil hazırlama sunucunuza ASP.NET MVC 3 ' ü yüklerseniz, platform sağlama işlemi, tüm ikincil hazırlama sunucularınızda ASP.NET MVC 3 ' ü yüklemek için Web Platformu Yükleyicisi ' ni kullanacaktır. Varsayılan olarak, platform sağlama işlemi her beş dakikada bir çalışır.

WFF denetleyicisi sunucunuzdaki IIS Yöneticisi 'nden temel uygulama ve platform sağlama ayarlarını yönetebilirsiniz.

**Uygulama ve platform sağlama ayarlarını keşfet**

1. IIS Yöneticisi 'nde, **Bağlantılar** bölmesinde, sunucu grubunuzu seçin.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image9.png)
2. **Sunucu grubu** bölmesinde, **uygulama sağlama**' ya çift tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image10.png)
3. Gördüğünüz gibi, sunucu grubu şu anda, birincil sunucu ve ikincil sunucular arasında her 30 saniyede Web içeriğini ve yapılandırma ayarlarını eşitleyecek şekilde yapılandırılmıştır.
4. **Geri**' ye tıklayın ve ardından **Platform sağlama**' ya çift tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image11.png)
5. Gördüğünüz gibi, sunucu grubu şu anda her beş dakikada bir birincil sunucu ve ikincil sunucular arasındaki web platformu ürünlerini ve bileşenlerini eşitleyecek şekilde yapılandırılmıştır.
6. **Geri**'yi tıklatın.
7. Sunucu grubunu web platformu ürünlerini hemen eşitlemeye zorlamak için, **Eylemler** bölmesinde, **Platform sağla**' ya tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image12.png)

    > [!NOTE]
    > Platform sağlama biraz zaman alabilir. Yükleyici işlemi, sunucu grubunuzdaki ikincil sunucular üzerinde arka planda çalışır.
8. Sağlama işleminin tamamlanabilmesi için yeterli zaman size izin verildiğinde, birincil sunucuya eklediğiniz ürünlerin ve bileşenlerin artık ikincil sunucularda çoğaltıldığını doğrulayabilirsiniz. Örneğin, bir ikincil sunucuda oturum açabilir ve **Sunucu Yöneticisi** penceresini kullanarak Web sunucusu rolünün yüklü olduğunu doğrulayabilirsiniz.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image13.png)
9. Ayrıca, çeşitli web platformu bileşenlerinin eklendiğini doğrulamak için yüklü programlar listesini de denetleyebilirsiniz.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image14.png)

## <a name="configure-load-balancing"></a>Yük dengelemeyi yapılandırma

Bir Web grubu oluşturduğunuzda, web sunucularınız arasında HTTP istekleri dağıtmak için bir yük dengeleme formu ayarlamanız gerekir. Bu, Windows Server 2008 Ağ Yükü Dengeleme, IIS ARR veya üçüncü taraf yazılım tabanlı ya da donanım tabanlı yük dengeleme çözümü olabilir.

WFF, IIS ARR ile yakından tümleştirilecek şekilde tasarlanmıştır. Bu tümleştirmeden faydalanmak için, WFF denetleyici sunucusuna ARR modülünü yüklemeniz gerekir. Böylece, genellikle etki alanı adı sistemi (DNS) kayıtlarını yapılandırarak tüm Web trafiğinizi denetleyici sunucusuna yönlendirebilirsiniz. Denetleyici sunucusu daha sonra sunucu kullanılabilirliğine ve çeşitli diğer ölçütlere bağlı olarak, gelen istekleri grubunuzdaki sunucular arasında dağıtır.

> [!NOTE]
> ARR 'yi WFF ile kullanmanız gerekmez; WFF 'yi, üçüncü taraf yük dengeleme çözümleriyle çalışacak şekilde yapılandırabilirsiniz. Daha fazla bilgi için bkz. [IIS 7 Için Web grubu çerçevesi 2,0 'ye genel bakış](https://go.microsoft.com/?linkid=9805126).

ARR kullanarak yük dengeleme, çoğu Bu öğreticinin kapsamı ötesinde karmaşık bir konudur. Ancak, ARR modülünü yüklemek ve yük dengelemeye başlamak için bir sonraki yordamı kullanabilirsiniz.

**WFF denetleyici sunucusunda yük dengelemeyi ayarlamak için**

1. WFF denetleyicisi sunucusunda Web Platformu Yükleyicisi ' ni başlatın.
2. **Web platformu yükleyicisi 3,0** penceresinin en üstünde, **Ürünler**' e tıklayın.
3. Pencerenin sol tarafında, gezinti bölmesinde, **sunucu**' ya tıklayın.
4. **Uygulama Isteği yönlendirme 2,5** satırında **Ekle**' ye tıklayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image15.png)
5. **Yükleme**' ye tıklayın ve ardından **Web platformu yükleme** penceresindeki yönergeleri izleyin.
6. Yükleme tamamlandığında, IIS Yöneticisi 'ni başlatın ve **Bağlantılar** bölmesinde sunucu grubu düğümünüz ' ı tıklatın. **Sunucu grubu** bölmesine birkaç yeni simge eklendiğini unutmayın.

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image16.png)
7. **Sunucu Grubu** bölmesinde **Yük Dengeleme**'ye çift tıklayın.
8. **Yük Dengeleme** bölmesinde, bir yük dengeleme algoritması seçin (örneğin, **en az geçerli istek**).

    > [!NOTE]
    > Yük Dengeleme algoritmaları ve diğer yapılandırma ayarları hakkında daha fazla bilgi için bkz. [uygulama Isteği yönlendirme modülü](https://go.microsoft.com/?linkid=9805130).

    ![](creating-a-server-farm-with-the-web-farm-framework/_static/image17.png)
9. **Eylemler** bölmesinde **Uygula**' ya tıklayın.

Artık sunucu grubunuzdaki sunucular için temel yük dengelemeyi yapılandırdınız. Tüm Web grubu trafiğinizi denetleyici sunucusuna yönlendirirsiniz, istekler kullanılabilirliğe ve seçtiğiniz Yük Dengeleme algoritmasına göre grubunuzdaki sunucular arasında dağıtılır.

ARR ile yük dengelemeyi yapılandırma hakkında daha fazla bilgi için bkz. [uygulama Isteği yönlendirme modülü](https://go.microsoft.com/?linkid=9805130).

## <a name="monitor-the-server-farm"></a>Sunucu grubunu izleme

Sunucu grubunuzun sistem durumunu, denetleyici sunucusundaki IIS Yöneticisi aracılığıyla istediğiniz zaman izleyebilirsiniz. **Bağlantılar** bölmesinde, sunucu grubunuzu genişletin ve ardından **sunucular**' a tıklayın. Orta bölmede, son etkinliğin izleme günlüğü ile birlikte gruptaki her bir sunucunun özeti gösterilir.

![](creating-a-server-farm-with-the-web-farm-framework/_static/image18.png)

## <a name="conclusion"></a>Sonuç

WFF sunucu grubunuz artık çalışır durumda olmalıdır. Birincil sunucuyu, hangi dağıtım yaklaşımını tercih&#x2014;ettiğiniz, Ayrıntılar&#x2014;için daha fazla okuma bölümünü görmek üzere yapılandırabilirsiniz ve yapılandırmanız sunucu grubundaki her ikincil sunucuda çoğaltılır.

## <a name="further-reading"></a>Daha Fazla Bilgi

WFF 'yi yapılandırmanın ve kullanmanın tüm yönleri hakkında daha fazla bilgi için bkz. [IIS 7 Için Microsoft Web grubu çerçevesi 2,0](https://go.microsoft.com/?linkid=9805129) Web sitesi.

> [!div class="step-by-step"]
> [Önceki](configuring-a-database-server-for-web-deploy-publishing.md)
> [İleri](configuring-deployment-properties-for-a-target-environment.md)
