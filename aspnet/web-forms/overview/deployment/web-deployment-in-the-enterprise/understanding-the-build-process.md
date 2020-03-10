---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: Derleme Işlemini anlama | Microsoft Docs
author: jrjlee
description: Bu konu, kurumsal ölçekte bir derleme ve dağıtım sürecine yönelik bir anlatım sağlar. Bu konuda açıklanan yaklaşım özel Microsoft Build engin kullanır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 802d93f7ca987d018967275bae68b8c56d883a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641143"
---
# <a name="understanding-the-build-process"></a>Derleme İşlemini Anlama

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, kurumsal ölçekte bir derleme ve dağıtım sürecine yönelik bir anlatım sağlar. Bu konuda açıklanan yaklaşım, işlemin her yönüyle ayrıntılı denetim sağlamak için özel Microsoft Build Engine (MSBuild) proje dosyalarını kullanır. Proje dosyaları içinde, özel MSBuild hedefleri, Internet Information Services (IIS) Web Dağıtım Aracı (MSDeploy. exe) ve veritabanı dağıtımı yardımcı programı VSDBCMD. exe gibi dağıtım yardımcı programlarını çalıştırmak için kullanılır.
> 
> > [!NOTE]
> > Bir MSBuild proje dosyasının anahtar bileşenleri açıklanarak ve birden çok hedef ortama dağıtımı desteklemek için bölünmüş proje dosyaları kavramı tanıtılan [Proje dosyasını anlamak](understanding-the-project-file.md)için önceki konu. Bu kavramları zaten bilmiyorsanız, bu konu başlığı altında çalışmadan önce [Proje dosyasını anlamak için](understanding-the-project-file.md) gözden geçirmeniz gerekir.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="build-and-deployment-overview"></a>Derleme ve Dağıtım genel bakış

[Ilgili kişi Yöneticisi çözümünde](the-contact-manager-solution.md), derleme ve dağıtım sürecini üç dosya denetler:

- *Evrensel proje dosyası* (*Publish. proj*). Bu, hedef ortamlar arasında değişmemelidir derleme ve dağıtım yönergelerini içerir.
- *Ortama özgü bir proje dosyası* (*env-dev. proj*). Bu, belirli bir hedef ortama özgü derleme ve dağıtım ayarlarını içerir. Örneğin, bir geliştirici veya test ortamı için ayarlar sağlamak üzere *env-dev. proj* dosyasını kullanabilir ve bir hazırlama ortamının ayarlarını sağlamak için *env-Stage. proj* adlı alternatif bir dosya oluşturabilirsiniz.
- Bir *komut dosyası* (*Publish-dev. cmd*). Bu, hangi proje dosyalarını yürütmek istediğinizi belirten bir MSBuild. exe komutu içerir. Her bir dosyanın, ortama özgü farklı bir proje dosyası belirten bir MSBuild. exe komutu içerdiği her hedef ortam için bir komut dosyası oluşturabilirsiniz. Bu, geliştiricinin yalnızca uygun komut dosyasını çalıştırarak farklı ortamlara dağıtmasını sağlar.

Örnek çözümde, bu üç dosyayı Yayımla çözüm klasöründe bulabilirsiniz.

![](understanding-the-build-process/_static/image1.png)

Bu dosyalara daha ayrıntılı bir şekilde bakmadan önce, bu yaklaşımı kullandığınızda genel derleme sürecinin nasıl çalıştığına göz atalım. Yüksek düzeyde, derleme ve dağıtım işlemi şöyle görünür:

![](understanding-the-build-process/_static/image2.png)

Meydana gelen ilk şey, evrensel derleme ve dağıtım yönergelerinden&#x2014;oluşan iki proje dosyası ve ortama özgü ayarların&#x2014;bulunduğu bir tek proje dosyasında birleştirilmesidir. MSBuild sonra proje dosyasındaki yönergeler aracılığıyla işe yarar. Her proje için proje dosyasını kullanarak çözümdeki projelerin her birini oluşturur. Daha sonra, Web içeriğinizi ve veritabanlarınızı hedef ortama dağıtmak için Web Dağıtımı (MSDeploy. exe) ve VSDBCMD yardımcı programı gibi diğer araçlara çağrı yapılır.

Başlangıçtan sonuna kadar, derleme ve dağıtım işlemi şu görevleri gerçekleştirir:

1. Yeni bir derleme hazırlığı sırasında çıkış dizininin içeriğini siler.
2. Çözümdeki her bir projeyi oluşturur:

    1. Bu durumda Web&#x2014;projeleri için, BIR ASP.NET MVC web uygulaması ve bir WCF Web hizmeti&#x2014;yapı işlemi her proje için bir Web dağıtım paketi oluşturur.
    2. Veritabanı projeleri için, yapı işlemi her proje için bir dağıtım bildirimi (. DeployManifest dosyası) oluşturur.
3. Bu, projedeki her bir veritabanı projesini dağıtmak için VSDBCMD. exe yardımcı programını kullanır, proje dosyaları&#x2014;bir hedef bağlantı dizesi ve bir veritabanı adı&#x2014;. DeployManifest dosyası ile birlikte kullanılır.
4. Dağıtım işlemini denetlemek için proje dosyalarından çeşitli özellikleri kullanarak her bir Web projesini çözüme dağıtmak üzere MSDeploy. exe yardımcı programını kullanır.

Bu işlemi daha ayrıntılı izlemek için örnek çözümü kullanabilirsiniz.

> [!NOTE]
> Kendi sunucu ortamlarınız için ortama özgü proje dosyalarını özelleştirmeye ilişkin yönergeler için bkz. [hedef ortam Için dağıtım özelliklerini yapılandırma](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

## <a name="invoking-the-build-and-deployment-process"></a>Derleme ve Dağıtım Işlemi çağrılıyor

Geliştirici sınama ortamına Contact Manager çözümünü dağıtmak için, Geliştirici *Publish-dev. cmd* komut dosyasını çalıştırır. Bu, yürütülecek proje dosyası olarak *Publish. proj* ve bir parametre değeri olarak *env-dev. proj* belirterek MSBuild. exe ' yi çağırır.

[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]

> [!NOTE]
> **/Fl** anahtarı ( **/filegünlükçü**için Short), derleme çıkışını geçerli dizinde *MSBuild. log* adlı bir dosyaya kaydeder. Daha fazla bilgi için bkz. [MSBuild komut satırı başvurusu](https://msdn.microsoft.com/library/ms164311.aspx).

Bu noktada MSBuild çalışmaya başlar, *Publish. proj* dosyasını yükler ve içindeki yönergeleri işlemeye başlar. İlk yönerge MSBuild 'e **Targetenvpropsfile** parametresinin belirttiği proje dosyasını içeri aktarmaya bildirir.

[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]

**Targetenvpropsfile** parametresi, *env-dev. proj* dosyasını belirtir, bu nedenle MSBuild, *env-dev. proj* dosyasının içeriğini *Publish. proj* dosyasına birleştirir.

MSBuild 'in birleştirilmiş proje dosyasında karşılaştığı sonraki öğeler Özellik gruplarıdır. Özellikler dosyada göründükleri sırada işlenir. MSBuild, her bir özellik için, belirtilen koşulların karşılanmasını sağlayarak bir anahtar-değer çifti oluşturur. Dosyasında daha sonra tanımlanan özellikler, dosyasında daha önce tanımlanan aynı ada sahip tüm özelliklerin üzerine yazar. Örneğin, **Outputroot** özelliklerini göz önünde bulundurun.

[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]

MSBuild ilk **Outputroot** öğesini işlediğinde benzer şekilde adlandırılmış bir parametre sağlanmadıysa, **outputroot** özelliğinin değerini olarak ayarlar **. \Publish\Out**. İkinci **outputroot** öğesiyle karşılaştığında, koşul **true**olarak değerlendirilirse, **Outputroot** özelliğinin değeri **OutDir** parametresinin değeri ile geçersiz kılınır.

MSBuild 'in karşılaştığı sonraki öğe, **ProjectsToBuild**adlı bir öğe içeren tek bir öğe grubudur.

[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]

MSBuild, bu yönergeyi **ProjectsToBuild**adlı bir öğe listesi oluşturarak işler. Bu durumda, öğe listesi çözüm dosyasının yolunu ve dosya adını&#x2014;tek bir değer içerir.

Bu noktada, kalan öğeler hedeflerdir. Hedefler, özelliklerden ve öğelerden&#x2014;farklı şekilde işlenir, ancak kullanıcı tarafından açıkça belirtilmedikçe veya proje dosyasındaki başka bir yapı tarafından çağrılmadıkça hedefler işlenmez. Açılış **projesi** etiketinin bir **DefaultTargets** özniteliği içerdiğini hatırlayın.

[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]

Bu, MSBuild. exe çağrıldığında hedefler belirtilmemişse, **Fullpublish** hedefini çağırmak için MSBuild 'e söyler. **Fullpublish** hedefi herhangi bir görev içermiyor; Bunun yerine, yalnızca bağımlılıkların bir listesini belirtir.

[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]

Bu bağımlılık, **Fullpublish** hedefini yürütmek için MSBuild 'e, bu hedeflerin listesini belirtilen sırada çağırması gerektiğini bildirir:

1. **Temizleme** hedefini çağırmalıdır.
2. **Buildprojects** hedefini çağırmalıdır.
3. Bu, **Gatherpackagesforpublishing** hedefini çağırmalıdır.
4. **Publishdbpackages** hedefini çağırmalıdır.
5. **Publishwebpackages** hedefini çağırmalıdır.

### <a name="the-clean-target"></a>Temizleme hedefi

**Temizleme** hedefi, yeni bir derleme için hazırlık olarak çıkış dizinini ve tüm içeriğini temelde siler.

[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]

Hedefin bir **ItemGroup** öğesi içerdiğine dikkat edin. Bir **hedef** öğe içindeki özellikleri veya öğeleri tanımlarken, *dinamik* Özellikler ve öğeler oluşturuyorsunuz. Diğer bir deyişle, hedef yürütülene kadar Özellikler veya öğeler işlenmez. Çıkış dizini mevcut olmayabilir veya derleme işlemi başlamadan önce herhangi bir dosya içeremez, bu nedenle **\_FilesToDelete** listesini statik öğe olarak derleyemiyorum; yürütme devam edene kadar beklemeniz gerekir. Bu nedenle, listeyi hedef içinde dinamik bir öğe olarak oluşturursunuz.

> [!NOTE]
> Bu durumda, **Temizleme** hedefi ilk yürütülecek olan olduğundan, dinamik bir öğe grubu kullanmak için gerçek bir gereksinim yoktur. Ancak, belirli bir noktada hedefleri farklı bir sırada yürütmek isteyebileceğiniz için, bu tür bir senaryoda dinamik özellikleri ve öğeleri kullanmak iyi bir uygulamadır.  
> Ayrıca, asla kullanılmayacak öğeleri bildirmemeyi de hedeflemelidir. Yalnızca belirli bir hedef tarafından kullanılacak öğeleriniz varsa, yapı sürecinde gereksiz ek yükü kaldırmak için bunları hedefin içine yerleştirmeyi göz önünde bulundurun.

Dinamik öğeler, **Temizleme** hedefi oldukça basittir ve yerleşik **ileti**, **silme**ve **RemoveDir** görevlerinin kullanımını sağlar:

1. Günlükçü 'ye bir ileti gönderin.
2. Silinecek dosyaların bir listesini oluşturun.
3. Dosyaları silin.
4. Çıkış dizinini kaldırın.

### <a name="the-buildprojects-target"></a>BuildProjects hedefi

**Buildprojects** hedefi, örnek Çözümdeki tüm projeleri temel olarak oluşturur.

[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]

Bu hedef, görevlerin ve hedeflerin referans özelliklerini ve öğelerini göstermek için [, önceki](understanding-the-project-file.md)konudaki bazı konularda açıklanmıştı. Bu noktada, temel olarak **MSBuild** göreviyle ilgileniyorsunuz. Bu görevi, birden çok proje oluşturmak için kullanabilirsiniz. Görev, MSBuild. exe ' nin yeni bir örneğini oluşturmaz; her projeyi derlemek için geçerli çalışan örneği kullanır. Bu örnekte ilgilendiğiniz önemli noktaları, dağıtım özellikleridir:

- **Deployonbuild** özelliği MSBuild 'e, her projenin derlemesi tamamlandığında proje ayarlarında herhangi bir dağıtım yönergesi çalıştırmasını söyler.
- **Deploytarget** özelliği, proje derlendikten sonra çağırmak istediğiniz hedefi tanımlar. Bu durumda, **paket** hedefi, proje çıkışını dağıtılabilir bir Web paketinde oluşturur.

> [!NOTE]
> **Paket** hedefi, MSBuild ve Web dağıtımı arasında tümleştirme sağlayan Web yayımlama ardışık DÜZENINI (WPP) çağırır. WPP 'nin sağladığı yerleşik hedeflere göz atmak isterseniz,% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web klasöründeki *Microsoft. Web. Publishing. targets* dosyasını gözden geçirin.

### <a name="the-gatherpackagesforpublishing-target"></a>GatherPackagesForPublishing hedefi

**Gatherpackagesforpublishing** hedefini inceliyorsanız, aslında hiçbir görevi içermediğini fark edeceksiniz. Bunun yerine, üç dinamik öğeyi tanımlayan tek bir öğe grubu içerir.

[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]

Bu öğeler, **Buildprojects** hedefi yürütüldüğünde oluşturulan dağıtım paketlerine başvurur. Bu öğeleri proje dosyasında statik olarak tanımlamadığınız için, **Buildprojects** hedefi yürütülene kadar öğelerin başvurduğu dosyalar yok. Bunun yerine,, **Buildprojects** hedefi yürütülene kadar çağrılmayan bir hedef içinde öğelerin dinamik olarak tanımlanması gerekir.

Öğeler bu hedef&#x2014;içinde kullanılmıyor bu hedef, öğeleri ve her öğe değeri ile ilişkili meta verileri oluşturur. Bu öğeler işlendikten sonra, **Publishpackages** öğesi iki değer Içerir, *ContactManager. Mvc. deploy. cmd* dosyasının yolu ve *ContactManager. Service. deploy. cmd* dosyasının yolu. Web Dağıtımı, bu dosyaları her proje için Web paketinin bir parçası olarak oluşturur ve paketleri dağıtmak için hedef sunucuda çağırmanız gereken dosyalardır. Bu dosyalardan birini açarsanız, temel olarak derleme özgü çeşitli parametre değerleriyle bir MSDeploy. exe komutu görürsünüz.

**Dbpublishpackages** öğesi, *ContactManager. Database. DeployManifest* dosyasının yolunu tek bir değere sahip olacaktır.

> [!NOTE]
> Bir. DeployManifest dosyası, bir veritabanı projesi oluşturduğunuzda oluşturulur ve MSBuild proje dosyası ile aynı şemayı kullanır. Veritabanı şemasının (. dbschema) konumu ve dağıtım öncesi ve dağıtım sonrası betiklerin ayrıntıları dahil olmak üzere bir veritabanını dağıtmak için gereken tüm bilgileri içerir. Daha fazla bilgi için bkz. [veritabanı derleme ve dağıtım genel bakış](https://msdn.microsoft.com/library/aa833165.aspx).

Dağıtım paketleri ve veritabanı dağıtım bildirimlerinin, [Web uygulaması projelerini oluşturma ve paketleme](building-and-packaging-web-application-projects.md) ve [veritabanı projelerini dağıtma](deploying-database-projects.md)hakkında daha fazla bilgi edineceksiniz.

### <a name="the-publishdbpackages-target"></a>PublishDbPackages hedefi

Kısaca, **Publishdbpackages** hedefi, **ContactManager** veritabanını bir hedef ortama dağıtmak için VSDBCMD yardımcı programını çağırır. Veritabanı dağıtımını yapılandırmak çok sayıda kararlar ve nutlar içerir ve bu, [veritabanı projelerini dağıtma](deploying-database-projects.md) ve [birden çok ortam Için veritabanı dağıtımlarını özelleştirme](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)konusunda daha fazla bilgi edineceksiniz. Bu konu başlığında, bu hedefin gerçekten nasıl çalıştığı hakkında odaklanacağız.

İlk olarak, açılış etiketinin bir **çıktılar** özniteliği içerdiğine dikkat edin.

[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]

Bu, *hedef toplu işleme*örneğidir. MSBuild proje dosyalarında, toplu işleme koleksiyonlar üzerinde yineleme için bir tekniktir. **"% (Dbpublishpackages. Identity)"** **Çıkış** özniteliğinin değeri, **Dbpublishpackages** öğe listesinin **kimlik** meta verileri özelliğine başvurur. Bu gösterim, **çıktılar =% * * * (ItemList. ItemMetaDataName)* , şöyle çevrilir:

- **Dbpublishpackages** içindeki öğeleri aynı **kimlik** meta verisi değerini içeren öğelerin toplu işlemlerine ayırın.
- Hedefi toplu iş başına bir kez yürütün.

> [!NOTE]
> **Kimlik** , oluşturma sırasında her öğeye atanan [yerleşik meta veri değerlerinden](https://msdn.microsoft.com/library/ms164313.aspx) biridir. Diğer sözcükteki **item** öğesi&#x2014;içindeki **Include** özniteliğinin değerini, öğenin yolunu ve dosya adını belirtir.

Bu durumda, aynı yol ve dosya adına sahip birden fazla öğe olmaması gerektiğinden, aslında tek bir toplu iş boyutlarıyla çalışıyoruz. Hedef her veritabanı paketi için bir kez yürütülür.

**\_cmd** özelliğinde benzer bir gösterimi görebilirsiniz. Bu, uygun anahtarlarla bir VSDBCMD komutu oluşturur.

[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]

Bu durumda, **% (Dbpublishpackages. DatabaseConnectionString)** , **% (Dbpublishpackages. TargetDatabase)** ve **% (Dbpublishpackages. FullPath)** hepsi **dbpublishpackages** öğe koleksiyonunun meta veri değerlerine başvurur. **\_cmd** özelliği, komutunu çağıran **Exec** görevi tarafından kullanılır.

[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]

Bu NOTATION 'un bir sonucu olarak, **Exec** görevi **databaseconnectionstring**, **TargetDatabase**ve **FullPath** meta veri değerlerinin benzersiz birleşimlerine göre toplu işler oluşturur ve her toplu işlem için görev bir kez yürütülür. Bu, *görev toplu işleme*örneğidir. Ancak, hedef düzeyi toplu işlem öğe koleksiyonumuzu zaten tek öğeli toplu işlerle ayırdığından, **Exec** görevi, hedefin her yinelemesi için bir kez ve yalnızca bir kez çalışır. Diğer bir deyişle, bu görev çözümdeki her veritabanı paketi için VSDBCMD yardımcı programını bir kez çağırır.

> [!NOTE]
> Hedef ve görev toplu işleme hakkında daha fazla bilgi için bkz. MSBuild [toplu](https://msdn.microsoft.com/library/ms171473.aspx)Işleme, [hedef toplu Işleme Içindeki öğe meta verileri](https://msdn.microsoft.com/library/ms228229.aspx)ve [görev toplu işlem içindeki öğe meta verileri](https://msdn.microsoft.com/library/ms171474.aspx)

### <a name="the-publishwebpackages-target"></a>PublishWebPackages hedefi

Bu noktada, örnek çözümde her proje için bir Web dağıtım paketi üreten **Buildprojects** hedefini çağırdınız. Her paket birlikte, paketi hedef ortama dağıtmak için gereken MSDeploy. exe komutlarını içeren bir *Deploy. cmd* dosyası ve hedef ortamın gerekli ayrıntılarını belirten bir *SetParameters. xml* dosyası. Ayrıca, ilgilendiğiniz *Deploy. cmd* dosyalarını içeren bir öğe koleksiyonu oluşturan **Gatherpackagesforpublishing** hedefini de çağırdınız. Temelde, **Publishwebpackages** hedefi şu işlevleri gerçekleştirir:

- Her bir paket için *SetParameters. xml* dosyasını, **XmlPoke** görevi kullanılarak hedef ortam için doğru ayrıntıları içerecek şekilde yönetir.
- Uygun anahtarları kullanarak her bir paket için *Deploy. cmd* dosyasını çağırır.

**Publishdbpackages** hedefi gibi **publishwebpackages** hedefi, hedefin her bir Web paketi için bir kez yürütülmesini sağlamak üzere hedef toplu işlem kullanır.

[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]

Hedef içinde, **Exec** görevi her bir Web paketi için *Deploy. cmd* dosyasını çalıştırmak için kullanılır.

[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]

Web paketlerinin dağıtımını yapılandırma hakkında daha fazla bilgi için bkz. [Web uygulaması projeleri oluşturma ve paketleme](building-and-packaging-web-application-projects.md).

## <a name="conclusion"></a>Sonuç

Bu konu, derleme ve dağıtım işleminin, Contact Manager örnek çözümü için baştan sona kadar olan yapı ve dağıtım sürecini denetlemek için nasıl kullanılacağını gösteren bir adım adım sunulmuştur. Bu yaklaşımı kullanmak, yalnızca ortama özgü bir komut dosyası çalıştırarak, karmaşık, kurumsal ölçekli dağıtımları tek ve yinelenebilir bir adımla çalıştırmanıza olanak sağlar.

## <a name="further-reading"></a>Daha Fazla Bilgi

Proje dosyalarına ve WPP 'ye yönelik daha ayrıntılı bir giriş için, bkz. [Microsoft Build Engine Içindeki MSBuild ve Team Foundation Build](http://amzn.com/0735645248) , Sayed Ibrampahashler ve William BARTHOLOMEW, ısbn: 978-0-7356-4524-0.

> [!div class="step-by-step"]
> [Önceki](understanding-the-project-file.md)
> [İleri](building-and-packaging-web-application-projects.md)
