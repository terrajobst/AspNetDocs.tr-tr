---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: Web uygulamalarını Web Dağıtımı çevrimdışına alma | Microsoft Docs
author: jrjlee
description: Bu konuda, bir Web uygulamasını Internet Information Services (IIS) Web depl kullanılarak otomatik dağıtım süresince çevrimdışına alma açıklanmaktadır...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: ba60664a0c3daa0650cd7e7cfc4ab9da08df3440
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075144"
---
# <a name="taking-web-applications-offline-with-web-deploy"></a>Web Dağıtımı ile Web Uygulamalarını Çevrimdışı Yapma

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu, Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) kullanılarak otomatik dağıtım süresince bir Web uygulamasını çevrimdışına alma işlemini açıklar. Web uygulamasına gözatabilen kullanıcılar, dağıtım tamamlanana kadar *çevrimdışı. htm dosyası\_bir uygulamaya* yeniden yönlendirilir.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="task-overview"></a>Göreve genel bakış

Birçok senaryoda, veritabanları veya Web Hizmetleri gibi ilgili bileşenlerde değişiklik yaparken bir Web uygulamasını çevrimdışı duruma getirmek isteyeceksiniz. Genellikle IIS ve ASP.NET ' de, IIS Web sitesinin veya Web uygulamasının kök klasöründe, *\_offline. htm* adlı bir dosya yerleştirerek bunu gerçekleştirirsiniz. *App\_offline. htm* dosyası standart bir HTML dosyasıdır ve genellikle kullanıcıya, bakım nedeniyle sitenin geçici olarak kullanılamadığını bildiren basit bir ileti içerecektir. *App\_offline. htm* dosyası Web sitesinin kök klasöründe mevcut olsa da IIS, tüm istekleri otomatik olarak dosyaya yönlendirir. Güncelleştirme yapmayı tamamladığınızda, *uygulamayı çevrimdışı. htm dosyası\_* kaldırırsınız ve Web sitesi her zamanki gibi isteklere hizmet vermeye devam eder.

Bir hedef ortama otomatik veya tek adımlı dağıtımlar gerçekleştirmek için Web Dağıtımı kullandığınızda, *uygulamayı\_çevrimdışı. htm* dosyasını dağıtım sürecinizde ekleme ve kaldırma dahil etmek isteyebilirsiniz. Bunu yapmak için, bu üst düzey görevleri gerçekleştirmeniz gerekir:

- Dağıtım işlemini denetlemek için kullandığınız Microsoft Build Engine (MSBuild) proje dosyasında, herhangi bir dağıtım görevinin başlamadan önce, bir *uygulamayı çevrimdışı. htm dosyasını\_* hedef sunucuya kopyalayan bir MSBuild hedefi oluşturun.
- Tüm dağıtım görevleri tamamlandığında, uygulamayı hedef sunucudan *\_çevrimdışı. htm* dosyasını kaldıran başka bir MSBuild hedefi ekleyin.
- Web uygulaması projesinde, Web Dağıtımı çağrıldığında bir *uygulamanın çevrimdışı. htm dosyası\_* dağıtım paketine eklenmesini sağlayan bir *. WPP. targets* dosyası oluşturun.

Bu konu başlığı altında, bu yordamların nasıl gerçekleştirileceği gösterilmektedir. Bu konudaki görevler ve izlenecek yollar, en az bir Web uygulaması projesi içeren bir çözüm oluşturmuş ve [kuruluştaki Web dağıtımında](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)açıklandığı şekilde dağıtım işlemini denetlemek için özel bir proje dosyası kullandığınız varsayılır. Alternatif olarak, konusundaki örnekleri izlemek için [Ilgili Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) örnek çözümünü kullanabilirsiniz.

## <a name="adding-an-app_offline-file-to-a-web-application-project"></a>Bir Web uygulaması projesine bir uygulama\_çevrimdışı dosya ekleme

Gerçekleştirmeniz gereken ilk görev, Web uygulaması projenize bir *uygulama\_çevrimdışı* dosya eklemektir:

- Dosyanın geliştirme süreciyle kesintiye uğramasını engellemek için (uygulamanızın kalıcı olarak çevrimdışı olmasını istemezsiniz), bunu *App\_offline. htm*' den başka bir şekilde çağırmanız gerekir. Örneğin, *Offline-Template. htm\_dosya uygulamasını*adlandırın.
- Dosyanın olduğu gibi dağıtılmasını engellemek için derleme eylemini **none**olarak ayarlamanız gerekir.

**Bir Web uygulaması projesine bir App\_çevrimdışı dosya eklemek için**

1. Çözümünüzü Visual Studio 2010 ' de açın.
2. **Çözüm Gezgini** penceresinde, Web uygulaması projenize sağ tıklayın, **Ekle**' nin üzerine gelin ve ardından **Yeni öğe**' ye tıklayın.
3. **Yeni öğe Ekle** Iletişim kutusunda **HTML sayfası**' nı seçin.
4. **Ad** kutusuna **App\_offline-Template. htm**yazın ve ardından **Ekle**' ye tıklayın.

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. Kullanıcılara uygulamanın kullanılamadığını bildirmek için bazı basit HTML ekleyin ve dosyayı kaydedin. Herhangi bir sunucu tarafı etiketi (örneğin, "ASP:" önekini kullanan tüm Etiketler) eklemeyin. 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. **Çözüm Gezgini** penceresinde, yeni dosyaya sağ tıklayın ve ardından **Özellikler**' e tıklayın.
7. **Özellikler** penceresinde, **derleme eylemi** satırında **hiçbiri**' ni seçin.

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-app_offline-file"></a>Bir uygulama\_çevrimdışı dosya dağıtma ve silme

Bir sonraki adım, dağıtım mantığının başlangıcında dosyayı hedef sunucuya kopyalamak ve sonunda kaldırmak için dağıtım mantığınızı değiştirmektir.

> [!NOTE]
> Sonraki yordam, [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklandığı gibi, dağıtım işleminizi denetlemek için özel bir MSBuild proje dosyası kullandığınızı varsayar. Doğrudan Visual Studio 'dan dağıtım yapıyorsanız, farklı bir yaklaşım kullanmanız gerekir. Sayıed Ibrat, [Yayımlama sırasında Web uygulamanızı çevrimdışına alma konusunda](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx)bu tür bir yaklaşımı açıklar.

Bir *uygulama\_çevrimdışı* dosyayı hedef IIS Web sitesine dağıtmak için, [Web dağıtımı **contentPath** sağlayıcısını](https://technet.microsoft.com/library/dd569034(WS.10).aspx)kullanarak MSDeploy. exe ' yi çağırmanız gerekir. **ContentPath** sağlayıcısı hem fiziksel dizin yollarını hem de IIS Web sitesini ya da uygulama yollarını destekler, bu da bir Visual Studio proje klasörü Ile bir IIS Web uygulaması arasında dosya eşitlemek için ideal seçim yapar. Dosyayı dağıtmak için MSDeploy komutunuz şuna benzemelidir:

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]

Dağıtım işleminin sonundaki dosyayı hedef siteden kaldırmak için MSDeploy komutunuz şuna benzemelidir:

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]

Bu komutları derleme ve dağıtım sürecinin bir parçası olarak otomatikleştirmek için, bunları özel MSBuild proje dosyanıza tümleştirmeniz gerekir. Sonraki yordamda bunun nasıl yapılacağı açıklanmaktadır.

**Bir uygulama\_çevrimdışı dosya dağıtmak ve silmek için**

1. Visual Studio 2010 ' de, dağıtım işleminizi denetleyen MSBuild proje dosyasını açın. [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) örnek çözümünde, *Publish. proj* dosyasıdır.
2. Kök **Proje** öğesinde, *uygulama\_çevrimdışı* dağıtım için değişkenleri depolamak üzere yeni bir **PropertyGroup** öğesi oluşturun:

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. **SourceRoot** özelliği *Publish. proj* dosyasında başka bir yerde tanımlanır. Kaynak içeriğin kök klasörünün konumunu, diğer sözcükteki geçerli yola&#x2014;göreli olarak *Publish. proj* dosyasının konumuna göre gösterir.
4. **ContentPath** sağlayıcısı göreli dosya yollarını kabul etmez, bu nedenle dağıtmadan önce kaynak dosyanıza Mutlak bir yol almanız gerekir. Bunu yapmak için [ConvertToAbsolutePath](https://msdn.microsoft.com/library/bb882668.aspx) görevini kullanabilirsiniz.
5. **GetAppOfflineAbsolutePath**adlı yeni bir **hedef** öğe ekleyin. Bu hedef içinde, proje klasörünüzdeki *çevrimdışı şablon dosyası\_uygulamanın* mutlak yolunu almak için **ConvertToAbsolutePath** görevini kullanın.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. Bu hedef, uygulamanın göreli yolunu proje klasörünüzde *çevrimdışı şablon dosyası\_* alır ve yeni bir özelliğe mutlak dosya yolu olarak kaydeder. **BeforeTargets** özniteliği, bu hedefin, bir sonraki adımda oluşturacağınız **dağıtıcı** hedeften önce yürütmesini istediğinizi belirtir.
7. **Dağıtılanın**adlı yeni bir hedef ekleyin. Bu hedef içinde, *uygulamanızı\_çevrimdışı* dosyayı hedef Web sunucusuna dağıtan MSDeploy. exe komutunu çağırın.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. Bu örnekte, **Contactmanageriispath** özelliği proje dosyasında başka bir yerde tanımlanır. Bu, *[IIS Web sitesi adı]/[uygulama adı]* biçiminde yalnızca bir IIS uygulama yoludur. Hedefe bir koşul eklemek, kullanıcıların bir özellik değerini değiştirerek veya bir komut satırı parametresi sağlayarak *uygulama\_çevrimdışı* dağıtım üzerinde geçiş yapmasına olanak sağlar.
9. **Deleteappoffline**adlı yeni bir hedef ekleyin. Bu hedef içinde, hedef Web sunucusundan *uygulamanızı\_çevrimdışı* dosyayı kaldıran MSDeploy. exe komutunu çağırın.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. Son görev, proje dosyanızın yürütülmesi sırasında bu yeni hedefleri uygun noktalarda çağırmada kullanılır. Bunu çeşitli şekillerde yapabilirsiniz. Örneğin, *Publish. proj* dosyasında, **Fullpublishbağımlıdson** özelliği, **fullpublish** varsayılan hedefinin çağrıldığı sırada yürütülmesi gereken hedeflerin bir listesini belirtir.
11. Yayımlama sürecinde uygun noktalarda **dağıtıcı** ve **deleteappoffline** hedeflerini çağırmak için MSBuild proje dosyanızı değiştirin.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

Özel MSBuild proje dosyanızı çalıştırdığınızda, başarılı bir derlemeden sonra *uygulama\_çevrimdışı* dosya sunucuya hemen dağıtılır. Dağıtım görevlerinin tümü tamamlandıktan sonra sunucudan silinir.

## <a name="adding-an-app_offline-file-to-deployment-packages"></a>Dağıtım paketlerine bir uygulama\_çevrimdışı dosya ekleme

Dağıtımınızı nasıl yapılandırdığınıza bağlı olarak, hedef IIS Web uygulamasındaki&#x2014; *App\_çevrimdışı. htm* &#x2014;gibi herhangi bir içerik, hedefe bir Web paketi dağıttığınızda otomatik olarak silinebilir. Dağıtım süresince *App\_offline. htm* dosyasının yerinde kaldığından emin olmak için dosyayı doğrudan dağıtım işleminin başlangıcında dağıtmaya ek olarak Web dağıtım paketinin içine eklemeniz gerekir.

- Bu konudaki önceki görevleri izlediyseniz, uygulamayı farklı bir dosya adı altında ( *app\_offline-Template. htm*kullandık) *\_çevrimdışı. htm* dosyasını Web uygulaması projenize **eklediniz.** Bu değişiklikler, dosyanın geliştirme ve hata ayıklama ile kesintiye uğramasını engellemek için gereklidir. Sonuç olarak, *uygulama\_çevrimdışı. htm* dosyasının Web dağıtım paketine eklendiğinden emin olmak için Paketleme işlemini özelleştirmeniz gerekir.

Web yayımlama işlem hattı (WPP), Web dağıtım paketine dahil edilecek dosyaların bir listesini oluşturmak için **Filesforpackagingfromproject** adlı bir öğe listesi kullanır. Bu listeye kendi öğelerinizi ekleyerek Web paketlerinizin içeriğini özelleştirebilirsiniz. Bunu yapmak için, aşağıdaki üst düzey adımları gerçekleştirmeniz gerekir:

1. Proje dosyanız ile aynı klasörde *[proje adı]. WPP. targets* adlı özel bir proje dosyası oluşturun.

    > [!NOTE]
    > *. WPP. targets* dosyasının, derleme ve dağıtım işlemini denetlemek için kullandığınız özel proje dosyalarıyla aynı klasörde değil&#x2014; *,* &#x2014;Web uygulaması proje dosyası ile aynı klasöre gitmesi gerekir.
2. *. WPP. targets* dosyasında, **Copyallfilestosinglefolderforpackage** hedefinden *önce* yürütülen yeni bir MSBuild hedefi oluşturun. Bu, pakete eklenecek öğelerin bir listesini oluşturan WPP hedefidir.
3. Yeni hedefte bir **ItemGroup** öğesi oluşturun.
4. **ItemGroup** öğesinde bir **Filesforpackagingfromproject** öğesi ekleyin ve *App\_offline. htm* dosyasını belirtin.

*. WPP. targets* dosyası şuna benzemelidir:

[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]

Bu örnekte notun önemli noktaları bulunmaktadır:

- **BeforeTargets** özniteliği, **Copyallfilestosinglefolderforpackage** hedefinden hemen önce yürütülmesi GEREKTIĞINI belirterek bu hedefi WPP 'ye ekler.
- **Filesforpackagingfromproject** öğesi, *offline-template. htm\_app* to App\_, listeye eklendikçe dosyayı *çevrimdışı. htm* olarak yeniden adlandırmak için **destinationrelativepath** meta veri değerini kullanır.

Sonraki yordamda, bu *. WPP. targets* dosyasını bir Web uygulaması projesine nasıl ekleyeceğiniz gösterilmektedir.

**Bir Web dağıtım paketine. WPP. targets dosyası eklemek için**

1. Çözümünüzü Visual Studio 2010 ' de açın.
2. **Çözüm Gezgini** penceresinde, Web uygulaması proje düğümünüz (örneğin, **ContactManager. Mvc**) sağ tıklayın, **Ekle**' nin üzerine gelin ve ardından **Yeni öğe**' ye tıklayın.
3. **Yeni öğe Ekle** iletişim kutusunda, **XML dosya** şablonunu seçin.
4. **Ad** kutusuna *[proje adı] * * *. WPP. targets** yazın (örneğin, **ContactManager. Mvc. WPP. targets**) ve ardından **Ekle**' ye tıklayın.

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > Projenin kök düğümüne yeni bir öğe eklerseniz, dosya proje dosyası ile aynı klasörde oluşturulur. Bunu, Windows Gezgini 'nde klasörünü açarak doğrulayabilirsiniz.
5. Dosyasında, daha önce açıklanan MSBuild işaretlemesini ekleyin.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. *[Proje adı]. WPP. targets* dosyasını kaydedin ve kapatın.

Web uygulaması projenizi bir sonraki derleme ve paketleme sırasında, WPP *. WPP. targets* dosyasını otomatik olarak algılar. *App\_offline-Template. htm* dosyası, *uygulama\_çevrimdışı. htm*olarak elde edilen Web dağıtım paketine dahil edilecek.

> [!NOTE]
> Dağıtımınız başarısız olursa, *App\_offline. htm* dosyası yerinde kalır ve uygulamanız çevrimdışı kalır. Bu genellikle istenen davranıştır. Uygulamanızı tekrar çevrimiçi duruma getirmek için, uygulamayı Web sunucunuzdaki *çevrimdışı. htm dosyasını\_* silebilirsiniz. Alternatif olarak, tüm hataları düzeltip başarılı bir dağıtım çalıştırırsanız, *App\_offline. htm* dosyası kaldırılır.

## <a name="conclusion"></a>Sonuç

Bu konu, dağıtım işleminin başlangıcında bir *App\_çevrimdışı. htm* dosyası yayımlayarak ve bu dosyayı sonda kaldırarak bir dağıtım süresince bir Web uygulamasını çevrimdışına alma hakkında açıklanmıştır. Ayrıca, bir Web dağıtım paketine bir *uygulama\_çevrimdışı. htm* dosyasının nasıl ekleneceğini de kapsar.

## <a name="further-reading"></a>Daha Fazla Bilgi

Paketleme ve dağıtım işlemi hakkında daha fazla bilgi için bkz. [Web uygulaması projelerini oluşturma ve paketleme](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Web paketi dağıtımı için parametreleri yapılandırma](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)ve [Web paketleri dağıtma](../web-deployment-in-the-enterprise/deploying-web-packages.md).

Web uygulamalarınızı, bu öğreticilerde açıklanan özel MSBuild proje dosyası yaklaşımını kullanmak yerine doğrudan Visual Studio 'dan yayımlarsanız, yayımlama sırasında uygulamanızı çevrimdışına almak için biraz farklı bir yaklaşım kullanmanız gerekir işle.

> [!div class="step-by-step"]
> [Önceki](excluding-files-and-folders-from-deployment.md)
> [İleri](running-windows-powershell-scripts-from-msbuild-project-files.md)
