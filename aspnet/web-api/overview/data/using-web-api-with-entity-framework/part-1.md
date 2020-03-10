---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Entity Framework 6 ile Web API 2 kullanma | Microsoft Docs
author: MikeWasson
description: Bu öğretici, ASP.NET Web API arka ucu ile bir Web uygulaması oluşturma hakkında temel bilgileri öğretir. Öğretici, veri düzenleme için Entity Framework 6 kullanır...
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622481"
---
# <a name="using-web-api-2-with-entity-framework-6"></a>Web API 2’yi Entity Framework 6 ile Kullanma

[Tamamlanmış projeyi indir](https://github.com/MikeWasson/BookService)

> Bu öğretici, ASP.NET Web API arka ucu ile bir Web uygulaması oluşturma hakkında temel bilgileri öğretir. Öğretici, veri katmanı için Entity Framework 6 ve istemci tarafı JavaScript uygulaması için altını gizleme. js ' yi kullanır. Öğreticide Ayrıca uygulamanın Azure App Service Web Apps nasıl dağıtılacağı gösterilmektedir.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
> - Web API 2.1
> - Visual Studio 2017 (Visual Studio 2017 [buraya](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)indirin)
> - Entity Framework 6
> - .NET 4.7
> - [Altını gizleme. js](http://knockoutjs.com/) 3,1

Bu öğretici, arka uç veritabanını işleyen bir Web uygulaması oluşturmak için Entity Framework 6 ile ASP.NET Web API 2 kullanır. Burada oluşturacağınız uygulamanın ekran görüntüsü gösterilir.

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

Uygulama, tek sayfalı uygulama (SPA) tasarımı kullanır. "Tek sayfalı uygulama", tek bir HTML sayfası yükleyen bir Web uygulaması için genel bir terimdir ve sonra yeni sayfalar yüklemek yerine sayfayı dinamik olarak güncelleştirir. İlk sayfa yüklendikten sonra uygulama, AJAX istekleri aracılığıyla sunucusuyla iletişim kuran bir uygulamadır. AJAX istekleri, uygulamanın kullanıcı arabirimini güncelleştirmek için kullandığı JSON verilerini döndürür.

AJAX yeni değil, ancak bugün büyük bir Gelişmiş SPA uygulaması oluşturmayı ve bakımını kolaylaştıran JavaScript çerçeveleri vardır. Bu öğretici, [altını gizleme. js](http://knockoutjs.com/)kullanır, ancak herhangi bir JavaScript istemci çerçevesini kullanabilirsiniz.

Bu uygulama için ana yapı taşları aşağıda verilmiştir:

- ASP.NET MVC HTML sayfasını oluşturur.
- ASP.NET Web API 'SI AJAX isteklerini işler ve JSON verileri döndürür.
- Altını gizleme. js verileri-HTML öğelerini JSON verilerine bağlar.
- Entity Framework veritabanı ile konuşuyor.

## <a name="see-this-app-running-on-azure"></a>Bkz. Azure 'da çalışan bu uygulama

Canlı bir Web uygulaması olarak çalışan tamamlanmış siteyi görmek istiyor musunuz? Aşağıdaki düğmeyi seçerek uygulamanın tüm sürümünü Azure hesabınıza dağıtabilirsiniz.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

Bu çözümü Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir. Henüz bir hesabınız yoksa, aşağıdaki seçeneklere sahip olursunuz:

- [Ücretsiz bir Azure hesabı açarak](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler edinin ve hatta kullanıldıktan sonra bile hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.
- [MSDN abonesi avantajlarınızı etkinleştirin](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) -MSDN aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.

## <a name="create-the-project"></a>Projeyi oluşturma

Visual Studio'yu açın. **Dosya** menüsünde **Yeni**' yi ve ardından **Proje**' yi seçin. (Veya başlangıç sayfasında **Yeni proje** ' yi seçin.)

**Yeni proje** iletişim kutusunda sol bölmedeki Web ' i ve **ASP.NET Web uygulaması ' nı (.NET Framework)** ortadaki bölmedeki **Web** ' i seçin. Proje **Bookservice** 'i adlandırın ve **Tamam**' ı seçin.

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

**Yeni ASP.NET projesi** Iletişim kutusunda **Web API** şablonunu seçin.

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

Projeyi oluşturmak için **Tamam**'ı seçin.

## <a name="configure-azure-settings-optional"></a>Azure ayarlarını yapılandırma (isteğe bağlı)

Projeyi oluşturduktan sonra dilediğiniz zaman Azure App Service Web Apps dağıtmayı seçebilirsiniz. 

1. Çözüm Gezgini, projenize sağ tıklayın ve **Yayımla**' yı seçin.

2. Görüntülenen pencerede **Başlat**' ı seçin. **Bir Yayımla hedefi seç** iletişim kutusu görüntülenir.

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. **Profil oluştur**' u seçin. **App Service oluştur** iletişim kutusu görüntülenir.

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   Varsayılanları kabul edin veya uygulama adı, kaynak grubu, barındırma planı, Azure aboneliği ve coğrafi bölge için farklı değerler girin. 

4. **SQL veritabanı oluştur**' u seçin. **SQL Server Yapılandır** iletişim kutusu görüntülenir. 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   Varsayılanları kabul edin veya farklı değerler girin. Yeni veritabanınız için bir **Yönetici Kullanıcı adı** ve **yönetici parolası** girin. İşiniz bittiğinde **Tamam ' ı** seçin. **App Service oluştur** sayfası yeniden görüntülenir.

5. Profilinizi oluşturmak için **Oluştur** ' u seçin. Sağ alt köşede, dağıtımın devam ettiğini belirten bir ileti görünür. Kısa bir süre sonra, **Yayımla** penceresi yeniden görüntülenir.

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    Uygulamayı dağıtmak için oluşturduğunuz profil artık kullanılabilir. 

> [!div class="step-by-step"]
> [Next](part-2.md)
