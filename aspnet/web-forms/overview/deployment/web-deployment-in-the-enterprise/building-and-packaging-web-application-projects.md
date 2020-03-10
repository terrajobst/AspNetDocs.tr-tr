---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: Web uygulaması projelerini derleme ve paketleme | Microsoft Docs
author: jrjlee
description: Bir Web uygulaması projesini uzak bir sunucu ortamına dağıtmak istediğinizde, ilk göreviniz projeyi derlemek ve bir Web dağıtımı Packa oluşturması...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: 1d0ee0264ce6461d7b0159f1a44de4de31e2d079
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573922"
---
# <a name="building-and-packaging-web-application-projects"></a>Web Uygulaması Projelerini Derleme ve Paketleme

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bir Web uygulaması projesini uzak bir sunucu ortamına dağıtmak istediğinizde, ilk göreviniz projeyi derlemek ve bir Web dağıtım paketi oluşturmak olur. Bu konuda, derleme işleminin Web uygulaması projeleri için nasıl çalıştığı açıklanmaktadır. Özellikle şunları açıklar:
> 
> - Web yayımlama ardışık düzeni (WPP), yapı işlemini dağıtım işlevlerini içerecek şekilde genişletir.
> - Internet Information Services (IIS) Web Dağıtım Aracı (Web Dağıtımı) Web uygulamanızı bir dağıtım paketine nasıl dönüştürür.
> - Oluşturma ve paketleme işleminin nasıl çalıştığı ve hangi dosyaların oluşturulduğu.

Visual Studio 2010 ' de, Web uygulaması projelerine yönelik derleme ve dağıtım işlemi WPP tarafından desteklenir. WPP, MSBuild işlevlerini genişleten ve Web Dağıtımı tümleştirilmesine olanak tanıyan Microsoft Build Engine (MSBuild) hedefleri kümesi sağlar. Visual Studio 'da, Web uygulaması projenizin özellik sayfalarında bu genişletilmiş işlevi görebilirsiniz. Paketle/ **Yayımla Web** sayfası, **paket/yayımlama SQL** sayfasıyla birlikte, derleme işlemi tamamlandığında Web uygulaması projenizin dağıtım için nasıl paketlenmekte olduğunu yapılandırmanıza olanak tanır.

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>WPP nasıl çalışır?

Bir C#tabanlı Web uygulaması projesi için proje dosyasına göz atalım, iki. targets dosyasını içeri aktaracağı görebilirsiniz.

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]

İlk **Içeri aktarma** deyimleri tüm görsel C# projelerde ortaktır. Bu dosya, *Microsoft. CSharp. targets*, görsele C#özgü hedefleri ve görevleri içerir. Örneğin, C# derleyici (**CSC**) görevi burada çağrılır. İçindeki *Microsoft. CSharp. targets* dosyası, *Microsoft. Common. targets* dosyasını içeri aktarır. Bu, **derleme**, **yeniden oluşturma**, **çalıştırma**, **derleme**ve **Temizleme**gibi tüm projelerde ortak olan hedefleri tanımlar. İkinci **Içeri aktarma** ekstresi Web uygulaması projelerine özgüdür. İçindeki *Microsoft. WebApplication. targets* dosyası, *Microsoft. Web. Publishing. targets* dosyasını içeri aktarır. *Microsoft. Web. Publishing. targets* dosyası temelde WPP *'dir* . Çeşitli dağıtım görevlerini tamamlamaya yönelik Web Dağıtımı çağıran **Package** ve **Msdeploypyayımla**gibi hedefleri tanımlar.

Bu ek hedeflerin nasıl kullanıldığını anlamak için, Contact Manager örnek çözümünde *Publish. proj* dosyasını açın ve **buildprojects** hedefine göz atın.

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]

Bu hedef, çeşitli projeler oluşturmak için **MSBuild** görevini kullanır. **Deployonbuild** ve **deploytarget** özelliklerine dikkat edin:

- **Deployonbuild = true** özelliği temelde "derleme başarıyla tamamlandığında ek bir hedef yürütmek istiyorum." anlamına gelir.
- **Deploytarget** özelliği, **deployonbuild** özelliği **true**değerine eşitse yürütmek istediğiniz hedefin adını tanımlar. Bu durumda, projeyi oluşturduktan sonra MSBuild 'in **paket** hedefini yürütmesini istediğinizi belirteceğiz.

**Paket** hedefi, *Microsoft. Web. Publishing. targets* dosyasında tanımlanmıştır. Temelde, bu hedef Web uygulaması projenizin derleme çıkışını alır ve bir IIS Web sunucusuna yayımlanbilen bir Web dağıtım paketine dönüştürür.

> [!NOTE]
> Visual Studio 2010 ' de bir proje dosyası (örneğin, <em>ContactManager. Mvc. csproj</em>) görüntülemek için, önce projeyi çözümünüzde kaldırmanız gerekir. <strong>Çözüm Gezgini</strong> penceresinde, proje düğümüne sağ tıklayın ve ardından <strong>Projeyi Kaldır</strong>' a tıklayın. Proje düğümüne tekrar sağ tıklayın ve ardından <strong>Düzenle</strong><em>[proje dosyası]</em>' e tıklayın. Proje dosyası ham XML biçiminde açılır. İşiniz bittiğinde projeyi yeniden yüklemeyi unutmayın.  
> MSBuild hedefleri, görevler ve <strong>Içeri aktarma</strong> deyimleri hakkında daha fazla bilgi için bkz. [Proje dosyasını anlama](understanding-the-project-file.md). Proje dosyalarına ve WPP 'ye yönelik daha ayrıntılı bir giriş için, bkz. [Microsoft Build Engine Içindeki MSBuild ve Team Foundation Build](http://amzn.com/0735645248) , Sayed Ibrampahashler ve William BARTHOLOMEW, ısbn: 978-0-7356-4524-0.

## <a name="what-is-a-web-deployment-package"></a>Web dağıtım paketi nedir?

Visual Studio 2010 kullanarak veya doğrudan MSBuild kullanarak bir Web uygulaması projesi derleyip dağıtırken, nihai sonuç genellikle bir *Web Dağıtım paketidir*. Web dağıtım paketi bir. zip dosyasıdır. Web uygulamanızı yeniden oluşturmak için IIS ve Web Dağıtımı gereken her şeyi içerir, örneğin:

- Web uygulamanızın, içerik, kaynak dosyaları, yapılandırma dosyaları, JavaScript ve geçişli stil sayfaları (CSS) kaynakları dahil olmak üzere derlenmiş çıktısı.
- Web uygulaması projeniz ve çözümünüzde başvurulan tüm projeler için derlemeler.
- Web uygulamanızla dağıttığınız herhangi bir veritabanı oluşturmak için SQL komut dosyaları.

Web dağıtım paketi oluşturulduktan sonra, çeşitli yollarla bir IIS Web sunucusunda yayımlayabilirsiniz. Örneğin, Web Dağıtımı uzak aracı hizmetini veya hedef Web sunucusunda Web Dağıtımı Işleyicisini hedefleyerek uzaktan dağıtabilir veya paketi hedef Web sunucusunda el ile içeri aktarmak için IIS Yöneticisi 'Ni kullanabilirsiniz. Dağıtıma yönelik bu yaklaşımlar hakkında daha fazla bilgi için bkz. [Web dağıtımına doğru yaklaşımı seçme](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md).

## <a name="how-does-the-build-process-work"></a>Yapı Işlemi nasıl çalışır?

Bu, bir Web uygulaması projesi oluşturup paketlemeyi yaptığınızda ne olacağını gösterir:

![](building-and-packaging-web-application-projects/_static/image2.png)

Bir Web uygulaması projesi oluşturduğunuzda, derleme işlemi *[proje adı] adlı bir dosya oluşturur. SourceManifest. xml*. Proje dosyası ve derleme çıkışıyla birlikte bu *. SourceManifest. xml* dosyası, Web dağıtım paketine eklemesi gereken Web dağıtımı söyler. Bu girdileri kullanarak, Web Dağıtımı *[proje adı]. zip*adlı bir Web dağıtım paketi oluşturur.

Web dağıtım paketinin yanı sıra, yapı işlemi, paketi kullanmanıza yardımcı olabilecek iki dosya üretir:

- *. Deploy. cmd* dosyası, Web Dağıtım paketinizi uzak bir IIS Web sunucusuna yayımlatabilecek parametreli Web dağıtımı (MSDeploy. exe) komutları kümesi içerir. *. Deploy. cmd* dosyasını uygun parametrelerle çalıştırmak, genellikle MSDeploy. exe komutlarını kendiniz el ile oluşturmak için daha hızlı ve daha kolay bir alternatif sağlar.
- *SetParameters. xml* dosyası MSDeploy. exe komutuna parametre değerleri kümesi sağlar. Bu değerler, paketini dağıtmak istediğiniz IIS Web uygulamasının adı, *Web. config* dosyasında tanımlanan herhangi bir hizmet bitiş noktası ve bağlantı dizesi ve proje özellikleri sayfalarında tanımlanan dağıtım özelliği değerleri gibi özellikleri içerir.

*SetParameters. xml* dosyası, dağıtım işlemini yönetmeye yönelik bir anahtardır. Bu dosya, Web uygulaması projenizin içeriğine göre dinamik olarak oluşturulur. Örneğin, *Web. config* dosyanıza bir bağlantı dizesi eklerseniz, yapı işlemi otomatik olarak bağlantı dizesini algılar, dağıtımı uygun şekilde parametreleştirin ve *SetParameters. xml* dosyasında bir giriş oluşturur ve bu bağlantı dizesini dağıtım işleminin bir parçası olarak değiştirmenize olanak sağlar. Sonraki konu, [Web paketi dağıtımı Için parametreleri yapılandırmak](configuring-parameters-for-web-package-deployment.md), bu dosyanın rolünü daha ayrıntılı bir şekilde açıklar ve derleme ve dağıtım sırasında değişiklik yapmak için farklı yolları açıklar.

> [!NOTE]
> Visual Studio 2010 ' de, WPP, paketlemeden önce bir Web uygulamasındaki sayfaların ön derlemesini desteklemez. Visual Studio 'nun sonraki sürümü ve WPP, bir Web uygulamasını paketleme seçeneği olarak ön derleme özelliğini içerir.

## <a name="conclusion"></a>Sonuç

Bu konu, Visual Studio 2010 ' deki Web uygulaması projelerine yönelik derleme ve paketleme sürecine genel bir bakış sağlamıştır. WPP 'nin MSBuild 'ten Web Dağıtımı komutları çağırmayı ve derleme ve paketleme işleminin nasıl çalıştığını anlatıldığı açıklanmaktadır.

Bir Web dağıtım paketi oluşturduktan sonra, bir sonraki adımınız bunu dağıtmaktır. Bunun hakkında daha fazla bilgi için bkz. [Web paketi dağıtımı Için parametreleri yapılandırma](configuring-parameters-for-web-package-deployment.md) ve [Web paketleri dağıtma](deploying-web-packages.md).

## <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticideki sonraki konular, [Web paketi dağıtımı Için parametreleri yapılandırmak](configuring-parameters-for-web-package-deployment.md) ve [Web paketlerini dağıtmak](deploying-web-packages.md)için, oluşturduğunuz Web paketinin nasıl kullanılacağına ilişkin yönergeler sağlar. Bu serideki son öğretici olan [Gelişmiş kurumsal Web dağıtımı](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md), Paketleme işlemini özelleştirme ve sorun giderme hakkında rehberlik sağlar.

Proje dosyalarına ve WPP 'ye yönelik daha ayrıntılı bir giriş için, bkz. [Microsoft Build Engine Içindeki MSBuild ve Team Foundation Build](http://amzn.com/0735645248) , Sayed Ibrampahashler ve William BARTHOLOMEW, ısbn: 978-0-7356-4524-0.

> [!div class="step-by-step"]
> [Önceki](understanding-the-build-process.md)
> [İleri](configuring-parameters-for-web-package-deployment.md)
