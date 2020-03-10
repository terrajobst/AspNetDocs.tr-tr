---
uid: web-forms/overview/deployment/visual-studio-web-deployment/project-properties
title: 'Visual Studio kullanarak Web dağıtımını ASP.NET: proje özellikleri | Microsoft Docs'
author: tdykstra
description: Bu öğretici serisi, bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf bir barındırma sağlayıcısına, usin...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ec1cec4c-a75f-47af-a2ba-b1e2f971d24b
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/project-properties
msc.type: authoredcontent
ms.openlocfilehash: b2811791a897c9166f6222c23dddc6921e5267ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78643600"
---
# <a name="aspnet-web-deployment-using-visual-studio-project-properties"></a>Visual Studio kullanarak Web dağıtımını ASP.NET: proje özellikleri

[Tom Dykstra](https://github.com/tdykstra) tarafından

[Başlatıcı projesi indir](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> Bu öğretici serisi, Visual Studio 2012 veya Visual Studio 2010 kullanarak bir ASP.NET Web uygulamasını Azure App Service Web Apps veya üçüncü taraf barındırma sağlayıcısına dağıtmayı (yayımlamayı) gösterir. Seriler hakkında daha fazla bilgi için, [serideki ilk öğreticiye](introduction.md)bakın.

## <a name="overview"></a>Genel bakış

Bazı dağıtım seçenekleri, proje dosyasında ( *. csproj* veya *. vbproj* dosyası) depolanan proje özelliklerinde yapılandırılır. Çoğu durumda, bu ayarların varsayılan değerleri istediğiniz şeydir, ancak bunları değiştirmeniz gerekiyorsa bu ayarlarla çalışmak için Visual Studio 'da yerleşik olarak bulunan **Proje özellikleri** Kullanıcı arabirimini kullanabilirsiniz. Bu öğreticide, **Proje özellikleri**' nde dağıtım ayarlarını gözden geçirin. Ayrıca boş bir klasörün dağıtılmasına neden olan bir yer tutucu dosyası oluşturursunuz.

## <a name="configure-deployment-settings-in-the-project-properties-window"></a>Proje Özellikleri penceresinde dağıtım ayarlarını yapılandırma

Dağıtım sırasında ne olduğunu etkileyen çoğu ayar, aşağıdaki öğreticilerde göreceğiniz gibi yayımlama profiline dahil edilir. Bilmeniz gereken birkaç ayar, **Proje özellikleri** penceresinin **Package/Publish** sekmelerinde bulunur. Bu ayarlar her derleme yapılandırması için belirtilir — diğer bir deyişle, bir yayın derlemesi için bir hata ayıklama derlemesi için farklı ayarlarınıza sahip olabilirsiniz.

**Çözüm Gezgini**, **contosouniversity** projesine sağ tıklayın, **Özellikler**' i seçin ve ardından **paket/Web 'i Yayımla** sekmesini seçin.

![Web 'i paketle/Yayımla sekmesi](project-properties/_static/image1.png)

Pencere görüntülendiğinde, çözüm için şu anda etkin olan derleme yapılandırmasına yönelik ayarları gösterir. **Yapılandırma** kutusu **etkin (sürüm)** ' i belirtmezse, yayın derleme yapılandırması ayarlarını göstermek için **yayın** ' ı seçin. Hem test hem de üretim ortamlarınıza yayın derlemeleri dağıtırsınız.

![Yayın derleme yapılandırması seçiliyor](project-properties/_static/image2.png)

**Etkin (yayın)** veya **Sürüm** seçiliyken, yayın yapı yapılandırmasını kullanarak dağıtırken geçerli olan değerleri görürsünüz:

- **Dağıtılacak öğeler** kutusunda **yalnızca uygulamayı çalıştırmak için gereken dosyalar** seçilir. Diğer Seçenekler **Bu projedeki tüm dosyalar** ya da **Bu proje klasöründeki tüm dosyalar**. Varsayılan seçimi değiştirmeden, örneğin kaynak kodu dosyalarını dağıtmaktan kaçının. Bu ayar, SQL Server Compact ikili dosyaları içeren klasörlerin projeye dahil edilmesini neden olma nedenidir. Bu ayar hakkında daha fazla bilgi **için bkz.** [ASP.NET Web uygulaması proje dağıtımı hakkında SSS](https://msdn.microsoft.com/library/ee942158.aspx).
- **Oluşturulan hata ayıklama sembolleri Dışla** seçildi. Bu derleme yapılandırmasını kullandığınızda hata ayıklamayacağız.
- **SQL 'ı paketle/Yayımla sekmesinde yapılandırılmış tüm veritabanlarını içer** seçilidir. Visual Studio 'Nun veritabanlarının yanı sıra veritabanlarını dağıtıp dağıtmayacağını belirtir. Onay kutusu etiketi yalnızca **paket/YAYıMLAMA SQL** sekmesine bahsetse de, bu onay kutusunun temizlenmesi, yayımlama profilinde yapılandırılan veritabanı dağıtımını devre dışı bırakır. Daha sonra bu işlemi yaptığınız için onay kutusunun seçili kalması gerekir. Bu öğreticilerde kullanmadığınız eski bir veritabanı yayımlama yöntemi için **Package/PUBLISH SQL** sekmesi kullanılır.
- **Web dağıtım paketi ayarları** bölümü uygulanmaz çünkü bu öğreticilerde tek tıklamayla yayımlama kullanıyorsunuz.

Hata ayıklama Derlemeleriyle ilgili varsayılan ayarları görmek için **yapılandırma** açılan kutusunu hata ayıkla olarak değiştirin. Bir hata ayıklama derlemesini dağıtırken hata ayıklayabilmeniz için, **oluşturulan hata ayıklama simgelerinin hariç tutulması** hariç değerler aynıdır.

## <a name="make-sure-that-the-elmah-folder-gets-deployed"></a>ELMAH klasörünün dağıtıldığından emin olun

Önceki öğreticide gördüğünüz gibi, [ELMAH NuGet paketi](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) hata günlüğü ve raporlama için işlevsellik sağlar. Contoso University uygulamasındaki ELMAH, hata ayrıntılarını *ELMAH*adlı bir klasörde depolayacak şekilde yapılandırılmıştır:

![ELMAH klasörü](project-properties/_static/image3.png)

Belirli dosya veya klasörlerin dağıtımdan dışlanması ortak bir gereksinimdir; diğer bir örnek, kullanıcıların dosyaları karşıya yükleyebilecek bir klasördür. Geliştirme ortamınızda oluşturulan günlük dosyalarının veya karşıya yüklenen dosyaların üretime dağıtılmasını istemezsiniz. Üretime bir güncelleştirme dağıtıyorsanız, dağıtım işleminin üretimde bulunan dosyaları silmesini istemezsiniz. (Dağıtım seçeneğini ayarlama yönteminize bağlı olarak, hedef sitede bir dosya varsa ancak dağıtım sırasında kaynak sitede yoksa, Web Dağıtımı bu kaynağı hedefin içinden siler.)

Bu öğreticide daha önce gördüğünüz gibi, **paket/yayımlama Web** sekmesindeki **dağıtılacak öğeler** seçeneği, **yalnızca bu uygulamayı çalıştırmak için gereken dosyalar**olarak ayarlanır. Sonuç olarak, geliştirmede ELMAH tarafından oluşturulan günlük dosyaları dağıtılmayacak ve bu durum bu şekilde yapılmayacak. (Dağıtılması için, projeye dahil olmaları ve **derleme eylemi** özelliğinin **içerik**olarak ayarlanması gerekir. Daha fazla bilgi **için bkz.** [ASP.NET Web UYGULAMASı proje dağıtımı SSS](https://msdn.microsoft.com/library/ee942158.aspx)). Ancak, kopyalamak için en az bir dosya olmadığı takdirde, hedef sitede bir klasör oluşturmaz Web Dağıtımı. Bu nedenle, klasörü kopyalamak için bir yer tutucu görevi görecek klasöre bir *. txt* dosyası eklersiniz.

**Çözüm Gezgini**, *ELMAH* klasörüne sağ tıklayın, **Yeni öğe Ekle**' yi seçin ve *yer tutucu. txt*adlı bir metin dosyası oluşturun. Aşağıdaki metni içine koyun: "Bu, klasörün dağıtılmasını sağlamak için bir yer tutucu dosyasıdır." ve dosyayı kaydedin. Visual Studio 'nun bu dosyayı ve bulunduğu klasörü dağıttığı ve *. txt* dosyalarının **derleme eylemi** özelliği varsayılan olarak **içeriğe** ayarlandığından emin olmak için bunu yapmanız gerekir.

## <a name="summary"></a>Özet

Artık tüm dağıtım kurulum görevlerini tamamladınız. Sonraki öğreticide, Contoso Üniversitesi sitesini test ortamına dağıtırsınız ve test edin.

> [!div class="step-by-step"]
> [Önceki](web-config-transformations.md)
> [İleri](deploying-to-iis.md)
