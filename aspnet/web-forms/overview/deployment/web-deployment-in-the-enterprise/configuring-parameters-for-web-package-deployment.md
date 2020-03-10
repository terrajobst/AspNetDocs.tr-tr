---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: Web paketi dağıtımı için parametreleri yapılandırma | Microsoft Docs
author: jrjlee
description: Bu konuda Internet Information Services (IIS) Web uygulaması adları, bağlantı dizeleri ve hizmet uç noktaları gibi parametre değerlerinin nasıl ayarlanacağı açıklanmaktadır,...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: f04ace98d81a33053b10cab7e40dbd75a6c0992c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544956"
---
# <a name="configuring-parameters-for-web-package-deployment"></a>Web Paketi Dağıtımı için Parametreleri Yapılandırma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, bir Web paketini uzak bir IIS Web sunucusuna dağıtırken Internet Information Services (IIS) Web uygulaması adları, bağlantı dizeleri ve hizmet uç noktaları gibi parametre değerlerinin nasıl ayarlanacağını açıklar.

Bir Web uygulaması projesi oluşturduğunuzda, derleme ve paketleme işlemi üç anahtar dosyası üretir:

- *[Proje adı]. zip* dosyası. Bu, Web uygulaması projeniz için Web Dağıtım paketidir. Bu paket, Web uygulamanızı uzak bir IIS Web sunucusunda yeniden oluşturmak için gereken tüm derlemeleri, dosyaları, veritabanı betiklerini ve kaynakları içerir.
- *[Proje adı]. deploy. cmd* dosyası. Bu, Web Dağıtım paketinizi uzak bir IIS Web sunucusuna yayımlamanızı sağlayan parametreli Web Dağıtımı (MSDeploy. exe) komutlarının bir kümesini içerir.
- A *[proje adı]. SetParameters. xml* dosyası. Bu, MSDeploy. exe komutuna parametre değerleri kümesi sağlar. Bu dosyadaki değerleri güncelleştirebilir ve Web paketinizi dağıtırken komut satırı parametresi olarak Web Dağıtımı geçirebilirsiniz.

> [!NOTE]
> Derleme ve paketleme süreci hakkında daha fazla bilgi için bkz. [Web uygulaması projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md).

*SetParameters. xml* dosyası, Web uygulaması proje dosyanızdaki ve projenizdeki tüm yapılandırma dosyalarından dinamik olarak oluşturulur. Projenizi derleyip paketlemeyi yaparken, Web yayımlama işlem hattı (WPP), hedef IIS Web uygulaması ve herhangi bir veritabanı bağlantı dizesi gibi, dağıtım ortamları arasında değişen değişkenlerin büyük bir kısmını otomatik olarak algılar. Bu değerler, Web dağıtım paketinde otomatik olarak parametreleştirilenir ve *SetParameters. xml* dosyasına eklenir. Örneğin, Web uygulaması projenizdeki *Web. config* dosyasına bir bağlantı dizesi eklerseniz, derleme işlemi bu değişikliği algılar ve *SetParameters. xml* dosyasına uygun olarak bir giriş ekler.

Birçok durumda, bu otomatik Parametreleştirme yeterli olacaktır. Ancak, kullanıcılarınızın uygulama ayarları veya hizmet uç noktası URL 'Leri gibi dağıtım ortamları arasındaki diğer ayarları değiştirmek gerekiyorsa, bu değerleri dağıtım paketinde parametreleştirmek ve *SetParameters. xml* dosyasına karşılık gelen girdileri eklemek için WPP 'ye söylemeniz gerekir. Aşağıdaki bölümlerde bunun nasıl yapılacağı açıklanmaktadır.

### <a name="automatic-parameterization"></a>Otomatik Parametreleştirme

Bir Web uygulaması oluşturup paketlemeyi yaparken, WPP otomatik olarak bu işlemleri parametreleştirilecektir:

- Hedef IIS Web uygulaması yolu ve adı.
- *Web. config* dosyanızdaki herhangi bir bağlantı dizesi.
- Proje özellik sayfalarındaki **Package/PUBLISH SQL** sekmesine eklediğiniz tüm veritabanları için bağlantı dizeleri.

Örneğin, [Ilgili kişi Yöneticisi](the-contact-manager-solution.md) örnek çözümünü herhangi bir şekilde Parametreleştirme işlemine dokunmadan derleyip paketlemeyi SEÇTIYSENIZ, WPP bu *ContactManager. Mvc. SetParameters. xml* dosyasını oluşturur:

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]

Bu durumda:

- **IIS Web uygulaması adı** parametresi, Web uygulamasını DAĞıTMAK istediğiniz IIS yoludur. Varsayılan değer, proje özellik sayfalarındaki **Package/Publish Web** sayfasından alınır.
- **ApplicationServices-Web. config bağlantı dizesi** parametresi, *Web. config* dosyasındaki bir **connectionStrings/Add** öğesinden oluşturulmuştur. Uygulamanın, üyelik veritabanıyla iletişim kurmak için kullanması gereken bağlantı dizesini temsil eder. Burada sağladığınız değer dağıtılan *Web. config* dosyasının yerini alacak. Varsayılan değer dağıtım öncesi *Web. config* dosyasından alınır.

WPP, oluşturduğu dağıtım paketindeki bu özellikleri de parametreleştirir. Dağıtım paketini yüklerken bu özellikler için değerler sağlayabilirsiniz. Paketi IIS Manager aracılığıyla el ile yüklerseniz, [Web paketlerinin el Ile yüklenmesi](manually-installing-web-packages.md)bölümünde açıklandığı gibi, Yükleme Sihirbazı herhangi bir parametre için değer vermenizi ister. [Web paketlerini dağıtma](deploying-web-packages.md)bölümünde açıklandığı gibi, paketi *. deploy. cmd* dosyasını kullanarak uzaktan yüklerseniz, Web dağıtımı parametre değerlerini sağlamak için bu *SetParameters. xml* dosyasına bakar. *SetParameters. xml* dosyasındaki değerleri el ile düzenleyebilir veya dosyayı otomatik derleme ve dağıtım sürecinin bir parçası olarak özelleştirebilirsiniz. Bu işlem, bu konunun ilerleyen bölümlerinde daha ayrıntılı açıklanmıştır.

### <a name="custom-parameterization"></a>Özel Parametreleştirme

Daha karmaşık dağıtım senaryolarında, projenizi dağıtmadan önce genellikle ek özellikler parametreleştirmek isteyeceksiniz. Genellikle, hedef ortamlar arasında değişiklik olacak özellikleri ve ayarları parametreleştiriyor olmanız gerekir. Bunlar şunlar olabilir:

- *Web. config* dosyasındaki hizmet uç noktaları.
- *Web. config* dosyasındaki uygulama ayarları.
- Kullanıcılara belirtmesini istemek istediğiniz diğer bildirim temelli Özellikler.

Bu özellikleri parametreleştirmek için en kolay yol, Web uygulaması projenizin kök klasörüne *Parameters. xml* dosyası eklemektir. Örneğin, Contact Manager çözümünde, ContactManager. Mvc projesi kök klasörde *Parameters. xml* dosyasını içerir.

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

Bu dosyayı açarsanız, tek bir **parametre** girişi içerdiğini görürsünüz. Giriş, *Web. config* dosyasındaki contactservice WINDOWS COMMUNICATION FOUNDATION (WCF) hizmetinin uç nokta URL 'sini bulmak ve parametreleştirmek IÇIN bir XML yol dili (XPath) sorgusu kullanır.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]

Dağıtım paketindeki uç nokta URL 'sini parametreleştirmenin yanı sıra, WPP, dağıtım paketiyle birlikte oluşturulan *SetParameters. xml* dosyasına karşılık gelen bir giriş de ekler.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]

Dağıtım paketini el ile yüklerseniz, IIS Yöneticisi tarafından otomatik olarak parametreleştirilen özelliklerle birlikte hizmet uç noktası adresini istenir. Dağıtım paketini *. deploy. cmd* dosyasını çalıştırarak yüklerseniz, otomatik olarak parametreleştirilen özelliklerin değerleriyle birlikte hizmet uç noktası adresi için bir değer sağlamak üzere *SetParameters. xml* dosyasını düzenleyebilirsiniz.

*Parameters. xml* dosyasının nasıl oluşturulacağı hakkında tam Ayrıntılar için bkz. [nasıl yapılır: paket yüklendiğinde dağıtım ayarlarını yapılandırmak için parametreleri kullanma](https://msdn.microsoft.com/library/ff398068.aspx). **Web. config dosyası ayarları dağıtım parametrelerini kullanmak için** adlı yordam, adım adım yönergeler sağlar.

## <a name="modifying-the-setparametersxml-file"></a>SetParameters. xml dosyasını değiştirme

Web uygulaması paketini *. deploy. cmd* dosyasını çalıştırarak veya&#x2014;komut satırından&#x2014;MSDeploy. exe ' yi çalıştırarak El Ile dağıtmayı planlıyorsanız, dağıtımdan önce *SetParameters. xml* dosyasını el ile düzenleyebilirsiniz. Ancak, kurumsal ölçekte bir çözümde çalışıyorsanız, bir Web uygulaması paketini daha büyük, otomatik derleme ve dağıtım sürecinin bir parçası olarak dağıtmanız gerekebilir. Bu senaryoda, sizin için *SetParameters. xml* dosyasını değiştirmek için Microsoft Build Engine (MSBuild) gerekir. Bunu, MSBuild **XmlPoke** görevini kullanarak yapabilirsiniz.

[Ilgili kişi Yöneticisi örnek çözümü](the-contact-manager-solution.md) bu süreci göstermektedir. Aşağıdaki kod örnekleri, yalnızca bu örnekle ilgili ayrıntıları gösterecek şekilde düzenlendi.

> [!NOTE]
> Örnek çözümde proje dosya modeline daha geniş bir genel bakış ve genel olarak özel proje dosyalarına giriş için, bkz. [Proje dosyasını anlama](understanding-the-project-file.md) ve [derleme sürecini anlama](understanding-the-build-process.md).

İlk olarak, ilgilendiğiniz parametre değerleri ortama özgü proje dosyasında özellik olarak tanımlanır (örneğin, *env-dev. proj*).

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]

> [!NOTE]
> Kendi sunucu ortamlarınız için ortama özgü proje dosyalarını özelleştirmeye ilişkin yönergeler için bkz. [hedef ortam Için dağıtım özelliklerini yapılandırma](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

Daha sonra *Publish. proj* dosyası bu özellikleri içeri aktarır. Her *SetParameters. xml* dosyası bir *. deploy. cmd* dosyası ile ilişkilendirildiği ve son olarak proje dosyasının her *. deploy. cmd* dosyasını çağırmasını istiyorduk, proje dosyası her *. deploy. cmd* dosyası için bir MSBuild *öğesi* oluşturur ve ilgilendiğiniz özellikleri *öğe meta verileri*olarak tanımlar.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]

Bu durumda:

- **Parametersxml** meta veri değeri *SetParameters. xml* dosyasının konumunu gösterir.
- **Iıswebappname** değeri, Web uygulamasını DAĞıTMAK istediğiniz IIS yoludur.
- **Membershipdbconnectionstring** değeri, üyelik veritabanının bağlantı dizesidir ve **Membershipdbconnectionname** değeri *SetParameters. xml* dosyasında karşılık gelen parametrenin **ad** özniteliğidir.
- **Serviceendpointvalue** değeri, hedef sunucudaki WCF hizmeti için uç nokta adresidir ve **Serviceendpointparamname** değeri *SetParameters. xml* dosyasında karşılık gelen parametrenin ad özniteliğidir.

Son olarak, *Publish. proj* dosyasında, **publishwebpackages** hedefi, bu değerleri *SetParameters. xml* dosyasında değiştirmek için **XmlPoke** görevini kullanır.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]

Her bir **XmlPoke** görevinin dört öznitelik değeri belirttiğinden emin olun:

- **Xmlinputpath** özniteliği, göreve değiştirmek istediğiniz dosyayı nerede bulacağını söyler.
- **Sorgu** özniteliği, DEğIşTIRMEk istediğiniz XML düğümünü tanımlayan bir XPath sorgusudur.
- **Değer** özniteliği, seçili XML düğümüne eklemek istediğiniz yeni değerdir.
- **Condition** özniteliği, görevin çalıştırılacağı veya çalıştırılmayan ölçütünüz. Bu durumlarda koşul, *SetParameters. xml* dosyasına null veya boş değer eklemeye çalışmamanızı sağlar.

## <a name="conclusion"></a>Sonuç

Bu konuda, *SetParameters. xml* dosyasının rolü açıklanmış ve bir Web uygulaması projesi oluşturduğunuzda nasıl oluşturulduğu açıklanmaktadır. Projenize *Parameters. xml* dosyası ekleyerek ek ayarları nasıl parametreleştirileyebilirsiniz. Ayrıca, proje dosyalarınızda **XmlPoke** görevi kullanılarak *SetParameters. xml* dosyasını daha büyük ve otomatikleştirilmiş bir yapı sürecinin bir parçası olarak nasıl değiştirebileceğiniz açıklanmıştır.

[Web paketlerini dağıtmaya](deploying-web-packages.md)yönelik bir sonraki konu, *. deploy. cmd* dosyasını çalıştırarak veya doğrudan MSDeploy. exe komutlarını kullanarak bir Web paketini nasıl dağıtabileceğinizi açıklar. Her iki durumda da *SetParameters. xml* dosyanızı bir dağıtım parametresi olarak belirtebilirsiniz.

## <a name="further-reading"></a>Daha Fazla Bilgi

Web paketleri oluşturma hakkında daha fazla bilgi için bkz. [Web uygulaması projeleri oluşturma ve paketleme](building-and-packaging-web-application-projects.md). Web paketinin dağıtımı hakkında yönergeler için bkz. [Web paketleri dağıtma](deploying-web-packages.md). *Parameters. xml* dosyasının nasıl oluşturulacağı hakkında adım adım yönergeler için bkz. [nasıl yapılır: paket yüklendiğinde dağıtım ayarlarını yapılandırmak için parametreleri kullanma](https://msdn.microsoft.com/library/ff398068.aspx).

Web Dağıtımı Parametreleştirme hakkında daha fazla genel bilgi için, bkz. [eylem içinde Web dağıtımı Parametreleştirme](https://go.microsoft.com/?linkid=9805119) (blog gönderisi).

> [!div class="step-by-step"]
> [Önceki](building-and-packaging-web-application-projects.md)
> [İleri](deploying-web-packages.md)
