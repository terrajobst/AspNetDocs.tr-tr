---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: Web dağıtımına doğru yaklaşımı seçme | Microsoft Docs
author: jrjlee
description: Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) 2,0 veya sonraki sürümleriyle çalışırken, almak için kullanabileceğiniz üç ana yaklaşım vardır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13f784dd8e6404806104d56b026b3c41ca178892
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548484"
---
# <a name="choosing-the-right-approach-to-web-deployment"></a>Web Dağıtımı için Doğru Yaklaşımı Seçme

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) 2,0 veya sonraki sürümleriyle çalışırken, paketlenmiş Web uygulamalarınızı bir Web sunucusuna almak için kullanabileceğiniz üç ana yaklaşım vardır. Şunlardan birini yapabilirsiniz:
> 
> - Hedef sunucuda *Web Deployment Agent hizmetini* ("uzak Aracı" olarak da bilinir) hedefleyerek uygulamayı uzak bir konumdan dağıtın.
> - Uygulamayı Isteğe bağlı Web Dağıtımı ("geçici aracı" olarak da bilinir) kullanarak uzak bir konumdan dağıtın.
> - Hedef sunucuda *ııs Web dağıtımı işleyicisini* hedefleyerek, uzak bir konumdan uygulamayı dağıtın.
> - Web paketini hedef sunucuya el ile kopyalayarak ve IIS Yöneticisi aracılığıyla içeri aktararak uygulamayı dağıtın.
> 
> Hedef Web sunucularınızı nasıl yapılandırdığınız, kullanmak istediğiniz dağıtıma göre değişir. Bu konu, hangi dağıtıma yönelik hangi yaklaşımın sizin için doğru olduğuna karar vermenize yardımcı olur.

Bu tabloda her bir yaklaşım için en sık kullanılan senaryolarla birlikte her bir dağıtım yaklaşımının başlıca avantajları ve dezavantajları gösterilmektedir.

| Yaklaşım | Yararları | Dezavantajlar | Tipik senaryolar |
| --- | --- | --- | --- |
| Uzak Aracı | Kolayca ayarlanabilir. Web uygulamalarına ve içeriğine yönelik normal güncelleştirmeler için uygundur. | Kullanıcının hedef sunucuda yönetici olması gerekir. Kullanıcı alternatif kimlik bilgilerini sağlayamıyorum. | Geliştirme ortamları. Test ortamları. |
| Geçici aracı | Hedef bilgisayara Web Dağıtımı yüklemeye gerek yoktur. Web Dağıtımı en son sürümü otomatik olarak kullanılır. | Kullanıcının hedef sunucuda yönetici olması gerekir. Kullanıcı alternatif kimlik bilgilerini sağlayamıyorum. | Geliştirme ortamları. Test ortamları. |
| Web Dağıtımı Işleyicisi | Yönetici olmayan kullanıcılar, içerik dağıtabilir. Web uygulamalarına ve içeriğine yönelik normal güncelleştirmeler için uygundur. | Ayarlamanız çok daha karmaşıktır. | Hazırlama ortamları. Intranet üretim ortamları. Barındırılan ortamlar. |
| Çevrimdışı dağıtım | Kolayca ayarlanabilir. Yalıtılmış ortamlar için uygundur. | Sunucu Yöneticisi, Web paketini her seferinde el ile kopyalayıp içeri aktarmalıdır. | Internet 'e yönelik üretim ortamları. Yalıtılmış ağ ortamları. |

## <a name="using-the-remote-agent"></a>Uzak aracıyı kullanma

Bir hedef sunucuda varsayılan ayarları kullanarak Web Dağıtımı yüklediğinizde, Web Deployment Agent hizmeti ("uzak Aracı") otomatik olarak yüklenip başlatılır. Varsayılan olarak, uzak Aracı şu adreste bir HTTP uç noktası sunar:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]

> [!NOTE]
> [*Server*] yerine Web sunucunuzun makine adını, Web sunucunuzun IP adresini veya Web sunucunuza çözümlenen bir ana bilgisayar adını değiştirebilirsiniz.

Sunucu yöneticileri, bu uç nokta adresini belirterek bir geliştirici makinesi veya yapı sunucusu gibi uzak bir konumdan Web paketleri dağıtabilir. Örneğin, Fabrikam, Inc. adresinden Matt hink, geliştirici makinesinde ContactManager. Mvc Web uygulaması projesini oluşturduğunu varsayalım. Yapı işlemi, paketi yüklemek için gereken Web Dağıtımı komutlarını içeren *. deploy. cmd* dosyası ile birlikte bir Web paketi oluşturur. Matt, TESTWEB1 sunucusunda bir sunucu yöneticisiyseniz, geliştirici makinesinde bu komutu çalıştırarak Web uygulamasını test Web sunucusuna dağıtabilir:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]

Gerçek olguda, Web Dağıtımı yürütülebilir dosyası, makine adını sağlarsanız, uzak aracının uç nokta adresini çıkarabilir, bu nedenle yalnızca Matt yalnızca şunu yazmaları gerekir:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]

> [!NOTE]
> Web Dağıtımı komut satırı sözdizimi ve *. cmd dosyalarını dağıtma* hakkında daha fazla bilgi için bkz. [nasıl yapılır: dağıtım paketini Deploy. cmd dosyasını kullanarak oluşturma](https://msdn.microsoft.com/library/ff356104.aspx).

Uzak Aracı, uzak bir konumdan içerik dağıtmanın kolay bir yolunu sunar ve bu yaklaşım tek tıklamayla veya otomatik dağıtımla iyi çalışabilir. Ancak, dağıtım komutunu çalıştıran kullanıcının aynı zamanda bir etki alanı yöneticisi veya hedef sunucuda yerel Yöneticiler grubunun bir üyesi olması gerekir. Buna ek olarak, uzak Aracı temel kimlik doğrulamasını desteklemez, bu nedenle komut satırına alternatif kimlik bilgilerini geçiremezsiniz.

Uzak Aracı, geliştirme veya test senaryolarında dağıtıma faydalı bir yaklaşım sağlar. burada, geliştiricilerin bir test sunucusu ortamı üzerinde tam yönetici denetimine sahip olması ve uygulamaların genellikle yeniden oluşturulması ve yeniden dağıtılması çok seyrek değildir. karşılaşırsanız. Ancak, bu yaklaşım genellikle hazırlama veya üretim ortamları için daha az kabul edilebilir.

Uzak aracı yaklaşımını kullanan bir senaryoya uçtan uca bir örnek için bkz. [Senaryo: Web dağıtımı Için test ortamı yapılandırma](scenario-configuring-a-test-environment-for-web-deployment.md).

## <a name="using-the-temp-agent"></a>Geçici aracıyı kullanma

Dağıtım için geçici aracı yaklaşımı, uzak Aracı yaklaşımına benzer. Ancak, uzak Aracı yaklaşımını tersine, hedef Web sunucusuna Web Dağıtımı yüklemeniz gerekmez. Bunun yerine, dağıtımını gerçekleştirdiğinizde Web Dağıtımı hedef sunucuda Web Dağıtım Aracısı hizmetinin geçici bir sürümünü yükler ve bu işlemi kullanarak içeriğinizi IIS 'e dağıtabilirsiniz. Dağıtım tamamlandığında, tüm geçici dosyalar kaldırılır.

Geçici aracı sağlayıcısı ayarını kullanmak istiyorsanız, dağıtım Komutunuz için **/g** bayrağını ekleyin:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]

> [!NOTE]
> Hizmet çalışmıyor olsa bile, hedef bilgisayara Web Dağıtım Aracısı hizmeti yüklenmişse geçici aracıyı kullanamazsınız.

Bu yaklaşımın avantajı, hedef sunucularınızda Web Dağıtımı yüklemelerini sürdürmenize gerek kalmaz. Ayrıca, kaynak ve hedef bilgisayarların aynı Web Dağıtımı sürümünü çalıştırdığından emin olmanız gerekmez. Ancak, bu yaklaşım uzak Aracı yaklaşımıyla aynı asıl sınırlamalara sahiptir; Yani, içerik dağıtmak için hedef sunucuda yerel yönetici olmanız ve yalnızca NTLM kimlik doğrulamasının desteklenmesi gerekir. Geçici aracı yaklaşımı aynı zamanda hedef ortamın daha fazla bir başlangıç yapılandırmasını gerektirir.

Geçici aracıyı kullanma hakkında daha fazla bilgi için bkz. [nasıl yapılır: dağıtım paketini Deploy. cmd dosyasını kullanarak yüklemek](https://msdn.microsoft.com/library/ff356104.aspx) ve [isteğe bağlı Web dağıtımı](https://technet.microsoft.com/library/ee517345(WS.10).aspx).

## <a name="using-the-web-deploy-handler"></a>Web Dağıtımı Işleyicisini kullanma

IIS 7 ve sonraki sürümleri için Web Dağıtımı IIS Web Dağıtımı Işleyicisi aracılığıyla alternatif bir dağıtım yaklaşımı sunar. Web Dağıtımı Işleyicisi, kullanıcıların IIS Web sitelerini uzak konumlardan yönetmesine olanak tanımak için tasarlanan IIS Web yönetimi hizmeti (WMSvc) ile yakından tümleşiktir.

Varsayılan olarak, uzak Aracı şu adreste bir HTTP uç noktası sunar:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]

> [!NOTE]
> [*Server*] yerine Web sunucunuzun makine adını, Web sunucunuzun IP adresini veya Web sunucunuza çözümlenen bir ana bilgisayar adını değiştirebilirsiniz.

Uzak aracı ve geçici aracı üzerinde Web Dağıtımı Işleyicisinin büyük avantajı, yönetici olmayan kullanıcıların uygulamaları ve içeriği belirli IIS Web sitelerine dağıtmasını sağlayacak şekilde IIS 'yi yapılandırabilmeniz gerekir. Web Dağıtımı Işleyicisi temel kimlik doğrulamasını da destekler, böylece Web Dağıtımı komutlarınıza parametre olarak alternatif kimlik bilgileri sağlayabilirsiniz. Büyük dezavantajı, Web Dağıtımı Işleyicisinin ilk olarak ayarlanması ve yapılandırılması için çok daha karmaşıktır.

Yönetici olmayan kullanıcılar söz konusu olduğunda, Web yönetimi hizmeti (WMSvc) yalnızca kullanıcının sunucu düzeyindeki bir bağlantı yerine site düzeyinde bir bağlantı kullanarak IIS 'ye bağlanmasına izin verir. Belirli bir siteye erişmek için uç nokta adresine siteye özgü bir sorgu dizesi dahil edebilirsiniz:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]

Örneğin, her başarılı derlemeden sonra bir hazırlama ortamına otomatik olarak bir Web uygulaması dağıtmak üzere bir yapı işleminin yapılandırıldığını varsayalım. Uzak aracı yaklaşımını kullandıysanız, yapı işlem kimliğini hedef sunucularınızda yönetici yapmanız gerekir. Buna karşılık, Web dağıtımı işleyicisi yaklaşımını kullanarak yönetici olmayan&#x2014;**bir kullanıcıya yalnızca** belirli bir IIS Web sitesi için&#x2014;izin verebilir ve derleme işlemi, Web paketini dağıtmak için bu kimlik bilgilerini verebilir.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]

> [!NOTE]
> Web Dağıtımı komut satırı işlemleri ve sözdizimi hakkında daha fazla bilgi için bkz. [Web dağıtımı komut satırı başvurusu](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx). *. Deploy. cmd* dosyasını kullanma hakkında daha fazla bilgi için bkz. [nasıl yapılır: dağıtım paketini Deploy. cmd dosyasını kullanarak](https://msdn.microsoft.com/library/ff356104.aspx)kullanma.

Web Dağıtımı Işleyici, hazırlama ortamları, barındırılan ortamlar ve Intranet tabanlı üretim ortamlarında dağıtıma yönelik olarak, sunucuya uzaktan erişimin kullanılabildiği, ancak yönetici kimlik bilgilerinin olmadığı yararlı bir yaklaşım sağlar.

Web Dağıtımı Işleyicisi yaklaşımını kullanan bir senaryonun uçtan uca bir örneği için bkz. [Senaryo: Web dağıtımı Için hazırlama ortamı yapılandırma](scenario-configuring-a-staging-environment-for-web-deployment.md).

## <a name="using-offline-deployment"></a>Çevrimdışı dağıtım kullanma

Bazı durumlarda, uzak bir konumdan bir IIS Web sitesine uygulama ve içerik dağıtmak mümkün değildir veya pratik değildir. Örneğin, kaynak ve hedef bilgisayarlar yalıtılmış ağlarda veya ağ kesimlerinde olabilir veya güvenlik duvarı ilkesi uzaktan erişime izin vermeyebilir.

Bunlar gibi senaryolarda, Web Dağıtımı; paketleme ve yayımlama özelliklerini kullanmaya devam edebilirsiniz. yalnızca uzak bir konumdan kullanamazsınız. Bunun yerine, hedef sunucudaki bir yöneticinin Web paketini sunucuya kopyalaması ve IIS Yöneticisi aracılığıyla içeri aktarması gerekir.

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

Çevrimdışı dağıtım yaklaşımı genellikle Internet 'e yönelik üretim ortamlarında yararlı olur ve bir çevre ağındaki sunucular iç ağdaki bilgisayarlarla sınırlı bir bağlantı olabilir.

Çevrimdışı dağıtım yaklaşımını kullanan bir senaryoya uçtan uca bir örnek için bkz. [Senaryo: Web dağıtımı Için üretim ortamı yapılandırma](scenario-configuring-a-production-environment-for-web-deployment.md).

## <a name="further-reading"></a>Daha Fazla Bilgi

Web Dağıtımı komut satırı işlemleri ve sözdizimi hakkında daha fazla bilgi için bkz. [Web dağıtımı komut satırı başvurusu](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx). *. Deploy. cmd* dosyasını kullanma hakkında daha fazla bilgi için bkz. [nasıl yapılır: dağıtım paketini Deploy. cmd dosyasını kullanarak](https://msdn.microsoft.com/library/ff356104.aspx)kullanma.

Uzak bir bilgisayardan Web paketleri dağıtmak için kullanabileceğiniz farklı yollarla ilgili daha genel yönergeler için, bkz. [Web Dağıtımı uzaktan kullanma](https://technet.microsoft.com/library/ee461175(WS.10).aspx). Isteğe bağlı Web Dağıtımı kullanma hakkında daha fazla bilgi için bkz. [isteğe bağlı Web dağıtımı](https://technet.microsoft.com/library/ee517345(WS.10).aspx).

> [!div class="step-by-step"]
> [Önceki](configuring-server-environments-for-web-deployment.md)
> [İleri](scenario-configuring-a-test-environment-for-web-deployment.md)
