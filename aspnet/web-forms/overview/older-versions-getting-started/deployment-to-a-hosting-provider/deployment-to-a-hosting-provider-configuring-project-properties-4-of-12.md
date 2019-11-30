---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 'Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: proje özelliklerini yapılandırma-4/12 | Microsoft Docs'
author: tdykstra
description: Bu öğretici dizisinde, Visual Stu kullanarak bir SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesinin nasıl dağıtılacağı (yayımlanacağı) gösterilmektedir.
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: 6e63e75dca3d776fb9a1bd7e420ef48891daac69
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74569807"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a>Visual Studio veya Visual Web Developer kullanarak SQL Server Compact bir ASP.NET Web uygulaması dağıtma: proje özelliklerini yapılandırma-4/12

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> Bu öğretici serisi, Visual Studio 2012 RC veya Web için Visual Studio Express 2012 RC kullanarak SQL Server Compact veritabanı içeren bir ASP.NET Web uygulaması projesini dağıtmayı (yayımlamayı) gösterir. Ayrıca, Web yayımlama güncelleştirmesini yüklerseniz Visual Studio 2010 de kullanabilirsiniz. Seriye giriş için, [serideki ilk öğreticiye](deployment-to-a-hosting-provider-introduction-1-of-12.md)bakın.
> 
> Visual Studio 2012 RC yayımlandıktan sonra tanıtılan dağıtım özelliklerini gösteren bir öğretici için, SQL Server Compact dışındaki SQL Server sürümlerinin nasıl dağıtılacağını gösterir ve Web Apps Azure App Service nasıl dağıtılacağını gösterir. bkz. [Visual Studio kullanarak ASP.NET Web dağıtımı](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Genel bakış

Bazı dağıtım seçenekleri, proje dosyasında ( *. csproj* veya *. vbproj* dosyası) depolanan proje özelliklerinde yapılandırılır. Çoğu durumda, bu ayarların varsayılan değerleri istediğiniz şeydir, ancak bunları değiştirmeniz gerekiyorsa bu ayarlarla çalışmak için Visual Studio 'da yerleşik olarak bulunan **Proje özellikleri** Kullanıcı arabirimini kullanabilirsiniz. Bu öğreticide, **Proje özellikleri**' nde dağıtım ayarlarını gözden geçirin. Ayrıca boş bir klasörün dağıtılmasına neden olan bir yer tutucu dosyası oluşturursunuz.

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a>Proje Özellikleri penceresinde dağıtım ayarlarını yapılandırma

Dağıtım sırasında ne olduğunu etkileyen çoğu ayar, aşağıdaki öğreticilerde göreceğiniz gibi yayımlama profiline dahil edilir. Bilmeniz gereken birkaç ayar, **Proje özellikleri** penceresinin **Package/Publish** sekmelerinde bulunur. Bu ayarlar her derleme yapılandırması için belirtilir — diğer bir deyişle, bir yayın derlemesi için bir hata ayıklama derlemesi için farklı ayarlarınıza sahip olabilirsiniz.

**Çözüm Gezgini**, **contosouniversity** projesine sağ tıklayın, **Özellikler**' i seçin ve ardından **paket/Web 'i Yayımla** sekmesini seçin.

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

Pencere görüntülendiğinde, çözüm için şu anda etkin olan derleme yapılandırmasına yönelik ayarları gösterir. **Yapılandırma** kutusu **etkin (sürüm)** ' i belirtmezse, yayın derleme yapılandırması ayarlarını göstermek için **yayın** ' ı seçin. Hem test hem de üretim ortamlarınıza yayın derlemeleri dağıtırsınız.

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

**Etkin (yayın)** veya **Sürüm** seçiliyken, yayın yapı yapılandırmasını kullanarak dağıtırken geçerli olan değerleri görürsünüz:

- **Dağıtılacak öğeler** kutusunda **yalnızca uygulamayı çalıştırmak için gereken dosyalar** seçilir. Diğer Seçenekler **Bu projedeki tüm dosyalar** ya da **Bu proje klasöründeki tüm dosyalar**. Varsayılan seçimi değiştirmeden, örneğin kaynak kodu dosyalarını dağıtmaktan kaçının. Bu ayar, SQL Server Compact ikili dosyaları içeren klasörlerin projeye dahil edilmesini neden olma nedenidir. Bu ayar hakkında daha fazla bilgi **için bkz.** [ASP.NET Web uygulaması proje dağıtımı hakkında SSS](https://msdn.microsoft.com/library/ee942158.aspx).
- **Oluşturulan hata ayıklama sembolleri Dışla** seçildi. Bu derleme yapılandırmasını kullandığınızda hata ayıklamayacağız.
- **Dosyaları uygulama\_verileri klasöründen Dışla** seçilmemiş. Üyelik veritabanının SQL Server Compact dosyanız bu klasörde ve dağıtmanız gerekir. Veritabanı değişikliklerini içermeyen güncelleştirmeleri dağıttığınızda, bu onay kutusunu seçersiniz.
- **Yayımlamadan önce bu uygulamayı ön derleme** seçilmemiş. Çoğu senaryoda, Web uygulaması projelerini önceden derlemeye gerek yoktur. Bu seçenek hakkında daha fazla bilgi için bkz. [paket/yayımlama Web sekmesi, proje özellikleri](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx) ve [Gelişmiş ön derleme ayarları iletişim kutusu](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx).
- **SQL 'ı paketle/Yayımla sekmesinde yapılandırılmış tüm veritabanlarını dahil et sekmesi** seçilidir, ancak **paket/yayımlama SQL** sekmesini yapılandırmamakta olmadığınızdan bu seçeneğin hiçbir etkisi yoktur. Bu sekme, SQL Server veritabanlarının dağıtılması için tek seçenek olmak üzere kullanılan eski bir veritabanı dağıtım yöntemine yöneliktir. [SQL Server geçiş](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) öğreticisindeki **paket/yayımlama SQL** sekmesini kullanacaksınız.
- **Web dağıtım paketi ayarları** bölümü uygulanmaz çünkü bu öğreticilerde tek tıklamayla yayımlama kullanıyorsunuz.

Hata ayıklama Derlemeleriyle ilgili varsayılan ayarları görmek için **yapılandırma** açılan kutusunu hata ayıkla olarak değiştirin. Bir hata ayıklama derlemesini dağıtırken hata ayıklayabilmeniz için, **oluşturulan hata ayıklama simgelerinin hariç tutulması** hariç değerler aynıdır.

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a>ELMAH klasörünün dağıtıldığından emin olma

Önceki öğreticide gördüğünüz gibi, [ELMAH NuGet paketi](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) hata günlüğü ve raporlama için işlevsellik sağlar. Contoso University uygulamasındaki ELMAH, hata ayrıntılarını *ELMAH*adlı bir klasörde depolayacak şekilde yapılandırılmıştır:

![ELMAH klasörü](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

Belirli dosya veya klasörlerin dağıtımdan dışlanması ortak bir gereksinimdir; diğer bir örnek, kullanıcıların dosyaları karşıya yükleyebilecek bir klasördür. Geliştirme ortamınızda oluşturulan günlük dosyalarının veya karşıya yüklenen dosyaların üretime dağıtılmasını istemezsiniz. Üretime bir güncelleştirme dağıtıyorsanız, dağıtım işleminin üretimde bulunan dosyaları silmesini istemezsiniz. (Dağıtım seçeneğini ayarlama yönteminize bağlı olarak, hedef sitede bir dosya varsa ancak dağıtım sırasında kaynak sitede yoksa, Web Dağıtımı bu kaynağı hedefin içinden siler.)

Bu öğreticide daha önce gördüğünüz gibi, **paket/yayımlama Web** sekmesindeki **dağıtılacak öğeler** seçeneği, **yalnızca bu uygulamayı çalıştırmak için gereken dosyalar**olarak ayarlanır. Sonuç olarak, geliştirmede ELMAH tarafından oluşturulan günlük dosyaları dağıtılmayacak ve bu durum bu şekilde yapılmayacak. (Dağıtılması için, projeye dahil olmaları ve **derleme eylemi** özelliğinin **içerik**olarak ayarlanması gerekir. Daha fazla bilgi **için bkz.** [ASP.NET Web UYGULAMASı proje dağıtımı SSS](https://msdn.microsoft.com/library/ee942158.aspx)). Ancak, kopyalamak için en az bir dosya olmadığı takdirde, hedef sitede bir klasör oluşturmaz Web Dağıtımı. Bu nedenle, klasörü kopyalamak için bir yer tutucu görevi görecek klasöre bir *. txt* dosyası eklersiniz.

**Çözüm Gezgini**, *ELMAH* klasörüne sağ tıklayın, **Yeni öğe Ekle**' yi seçin ve *yer tutucu. txt*adlı bir dosya oluşturun. Aşağıdaki metni içine koyun: "Bu, klasörün dağıtılmasını sağlamak için bir yer tutucu dosyasıdır." ve dosyayı kaydedin. Visual Studio 'nun bu dosyayı ve bulunduğu klasörü dağıttığı ve *. txt* dosyalarının **derleme eylemi** özelliği varsayılan olarak **içeriğe** ayarlandığından emin olmak için bunu yapmanız gerekir.

Artık tüm dağıtım kurulum görevlerini tamamladınız. Sonraki öğreticide, Contoso Üniversitesi sitesini test ortamına dağıtırsınız ve test edin.

> [!div class="step-by-step"]
> [Önceki](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [İleri](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)
