---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: Paketleme Işleminde sorun giderme | Microsoft Docs
author: jrjlee
description: Bu konu başlığı altında, a... adlı EnablePackageProcessLoggingAndAssert özelliğini kullanarak paketleme işlemiyle ilgili ayrıntılı bilgileri nasıl toplayabileceğinizi açıklar.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628214"
---
# <a name="troubleshooting-the-packaging-process"></a>Paketleme İşleminin Sorunlarını Giderme

[Jason Lee](https://github.com/jrjlee) tarafından

[PDF 'YI indir](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Bu konu başlığı altında, Microsoft Build Engine (MSBuild) ' de **Enablepackageprocessloggingandassert** özelliğini kullanarak paketleme işlemi hakkında ayrıntılı bilgileri nasıl toplayabileceğinizi açıklamaktadır.
> 
> **Enablepackageprocessloggingandassert** özelliğini **true**olarak belirlediğinizde MSBuild şunları olur:
> 
> - Yapı günlüklerine paketleme işlemi hakkında daha fazla bilgi ekleyin.
> - Örneğin paketleme listesinde yinelenen dosyalar bulunursa, belirli koşullarda hataları günlüğe kaydedin.
> - *ProjectName*\_paket klasöründe bir günlük dizini oluşturun ve paketlediğiniz dosyalarla ilgili bilgileri kaydetmek için kullanın.
> 
> Paketleme işlemi başarısız olursa veya Web Dağıtım paketleriniz beklediği dosyaları içermiyorsa, bu bilgileri kullanarak işlemlerin yanlış olduğu işlem ve Pinpoint sorunlarını giderebilirsiniz.
> 
> > [!NOTE]
> > **Enablepackageprocessloggingandassert** özelliği yalnızca projenizi **hata ayıklama** yapılandırmasını kullanarak oluşturursanız işe yarar. Özelliği diğer yapılandırmalarda yok sayılır.

Bu konu, Fabrikam, Inc adlı kurgusal bir şirketin Kurumsal Dağıtım gereksinimlerini temel alarak bir öğretici serisinin bir parçasını oluşturur. Bu öğretici serisi, bir ASP.NET MVC&#x2014;3 uygulaması, Windows Communication Foundation (WCF) hizmeti ve bir veritabanı projesi dahil, gerçekçi bir karmaşıklık düzeyine sahip bir Web uygulamasını temsil etmek üzere bir örnek çözüm olan [Contact Manager çözümünü](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;kullanır.

Bu öğreticilerin temelini oluşturan dağıtım yöntemi, derleme işleminin her hedef ortam için uygulanan derleme yönergelerini içeren ve ortama özel yapı ve dağıtım ayarlarını içeren iki proje&#x2014;dosyası tarafından kontrol edilen proje [dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md)bölümünde açıklanan bölünmüş proje dosyası yaklaşımını temel alır. Derleme zamanında, ortama özgü proje dosyası, derleme yönergelerinin tam bir kümesini oluşturmak için ortam agtik proje dosyası ile birleştirilir.

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>EnablePackageProcessLoggingAndAssert özelliğini anlama

Web [uygulaması projelerini derleme ve paketleme](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) Web yayımlama işlem HATTıNıN (WPP), MSBuild 'in işlevselliğini genişleten ve Internet INFORMATION SERVICES (IIS) Web Dağıtım aracı (Web dağıtımı) ile tümleşmesini sağlayan bir MSBuild hedefleri kümesi sağlar. Bir Web uygulaması projesi paketlemeyi yaparken, WPP hedefleri çağrılıyor.

Bu WPP hedeflerinin çoğu, **Enablepackageprocessloggingandassert** özelliği **true**olarak ayarlandığında ek bilgileri kaydeden koşullu mantığı içerir. Örneğin, **paket** hedefini gözden geçirdikten sonra, ek bir günlük dizini oluşturduğunu ve **Enablepackageprocessloggingandassert** değeri **true**ise bir metin dosyasına bir dosya listesi yazabileceğini görebilirsiniz.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> WPP hedefleri,% PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web klasöründeki *Microsoft. Web. Publishing. targets* dosyasında tanımlanmıştır. Bu dosyayı açabilir ve Visual Studio 2010 veya herhangi bir XML düzenleyicisinde hedefleri gözden geçirebilirsiniz. Dosyanın içeriğini değiştirmemelidir.

## <a name="enabling-the-additional-logging"></a>Ek günlüğe kaydetme etkinleştiriliyor

Projenizin nasıl oluşturulduğuna bağlı olarak çeşitli yollarla **Enablepackageprocessloggingandassert** özelliği için bir değer sağlayabilirsiniz.

Projenizi komut satırından oluşturursanız, **Enablepackageprocessloggingandassert** özelliği için bir komut satırı bağımsız değişkeni olarak bir değer sağlayabilirsiniz:

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

Projelerinizi derlemek için özel bir proje dosyası kullanıyorsanız, **MSBuild** görevinin **Özellikler** özniteliğinde **Enablepackageprocessloggingandassert** değerini dahil edebilirsiniz:

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

Projelerinizi derlemek için bir Team Foundation Server (TFS) derleme tanımı kullanıyorsanız, **MSBuild bağımsız değişkenleri** satırında **Enablepackageprocessloggingandassert** özelliği için bir değer sağlayabilirsiniz:![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> Derleme tanımlarını oluşturma ve yapılandırma hakkında daha fazla bilgi için bkz. [dağıtımı destekleyen bir yapı tanımı oluşturma](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).

Alternatif olarak, paketi her yapıya eklemek istiyorsanız, Web uygulaması projeniz için proje dosyasını değiştirerek **Enablepackageprocessloggingandassert** özelliğini **true**olarak ayarlayabilirsiniz. Özelliği. csproj veya. vbproj dosyanızdaki ilk **PropertyGroup** öğesine eklemeniz gerekir.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a>Günlük dosyalarını gözden geçirme

**Enablepackageprocessloggingandassert** **değeri true**olarak ayarlanmış bir Web uygulaması projesi oluşturup paketlemeyi yaptığınızda MSBuild, *ProjectName*\_paket klasöründe log adlı ek bir klasör oluşturur. Günlük klasörü çeşitli dosyaları içerir:

![](troubleshooting-the-packaging-process/_static/image2.png)

Gördüğünüz dosyaların listesi, projenizdeki işlemlere ve yapı sürecinizdeki şeylere göre değişir. Ancak, bu dosyalar genellikle, işlemin çeşitli aşamalarında, WPP 'nin paketleme için topladığı dosyaların listesini kaydetmek için kullanılır:

- *PreExcludePipelineCollectFilesPhaseFileList. txt* dosyası, dışlama için belirtilen herhangi bir dosya kaldırılmadan önce MSBuild 'in paketlenmesi için topladığı dosyaları listeler.
- *Afterexcludefilesfileslist. txt* dosyası, dışlama için belirtilen tüm dosyalar kaldırıldıktan sonra değiştirilmiş dosya listesini içerir.

    > [!NOTE]
    > Paketleme işleminden dosya ve klasörlerin dışlanması hakkında daha fazla bilgi için, bkz. [dosyaları ve klasörleri dağıtımdan dışlama](excluding-files-and-folders-from-deployment.md).
- *Aftertransformwebconfig. txt* dosyası, herhangi bir *Web. config* dönüştürmesinden sonra paketleme için toplanan dosyaları listeler. Bu listede, *Web. Debug. config* ve *Web. Release. config*gibi yapılandırmaya özgü *Web. config* dönüştürme dosyaları paketleme için dosya listesinden çıkarılır. Tek bir dönüştürülmüş *Web. config* kendi yerine eklenir.
- *Postautoparameterizationwebconfigconnectionstrings. txt* dosyası, *Web. config* dosyasındaki bağlantı dizeleri parametreli olduktan sonra dosyaların listesini içerir. Bu, paketi dağıtırken bağlantı dizelerinizi hedef ortamınız için doğru ayarlarla değiştirmenize olanak tanıyan işlemdir.
- *Prepackage. txt* dosyası, pakete eklenecek dosyaların son oluşturma öncesi derleme listesini içerir.

> [!NOTE]
> Ek günlük dosyalarının adları genellikle WPP hedeflerine karşılık gelir. % PROGRAMFILES (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web klasöründeki *Microsoft. Web. Publishing. targets* dosyasını inceleyerek bu hedefleri gözden geçirebilirsiniz.

Web paketinizin içerikleri beklediğiniz gibi değilse, bu dosyaları gözden geçirmek, işlemin ne zaman hatalı olduğuna ilişkin yararlı bir yol olabilir.

## <a name="conclusion"></a>Sonuç

Bu konuda, paketleme işleminde sorun gidermek için MSBuild 'te **Enablepackageprocessloggingandassert** özelliğini nasıl kullanabileceğiniz açıklanmıştır. Yapı işlemine özellik değerini sağlayabilmeniz için farklı yollar açıklanmış ve özelliği **true**olarak ayarladığınızda kaydedilen ek bilgileri de açıklandı.

## <a name="further-reading"></a>Daha Fazla Bilgi

Dağıtım işlemini denetlemek için özel MSBuild proje dosyalarını kullanma hakkında daha fazla bilgi için bkz. [Proje dosyasını anlama](../web-deployment-in-the-enterprise/understanding-the-project-file.md) ve [derleme sürecini anlama](../web-deployment-in-the-enterprise/understanding-the-build-process.md). WPP ve paketleme sürecini yönetme hakkında daha fazla bilgi için bkz. [Web uygulaması projelerini oluşturma ve paketleme](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md). Belirli dosya ve klasörlerin Web Dağıtım paketlerinden nasıl dışlandığı hakkında yönergeler için, bkz. [dosyaları ve klasörleri dağıtımdan dışlama](excluding-files-and-folders-from-deployment.md).

> [!div class="step-by-step"]
> [Öncekini](running-windows-powershell-scripts-from-msbuild-project-files.md)
