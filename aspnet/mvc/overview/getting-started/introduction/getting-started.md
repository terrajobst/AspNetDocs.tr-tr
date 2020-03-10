---
uid: mvc/overview/getting-started/introduction/getting-started
title: ASP.NET MVC 5 ' i kullanmaya başlama | Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602769"
---
# <a name="getting-started-with-aspnet-mvc-5"></a>ASP.NET MVC 5 ile çalışmaya başlama

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

[!INCLUDE [consider RP](../../../../includes/razor.md)]

Bu öğretici, [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)kullanarak ASP.NET MVC 5 Web uygulaması oluşturma hakkında temel bilgileri öğretir. Öğreticinin son kaynak kodu [GitHub](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie)' da bulunur.

Bu öğretici [Scott Guthrie](https://weblogs.asp.net/scottgu/) (Twitter[@scottgu](https://twitter.com/scottgu) ), [Scott Hanselman](http://www.hanselman.com/blog/) (Twitter: [@shanselman](https://twitter.com/shanselman) ) ve [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ) tarafından yazılmıştır

Bu uygulamayı Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir:

- Ücretli Azure hizmetlerini denemek için kullanabileceğiniz ücretsiz krediler [için bir Azure hesabı açabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ve hatta bunları kullandıktan sonra da hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.
- [MSDN abone avantajlarınızı etkinleştirebilirsiniz](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) . MSDN aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.

## <a name="get-started"></a>Başlangıç

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)' i yükleyerek başlayın. Ardından, Visual Studio 'Yu açın.

Visual Studio, IDE veya tümleşik bir geliştirme ortamıdır. Belgeleri yazmak için Microsoft Word kullandığınızda olduğu gibi, uygulamalar oluşturmak için IDE kullanacaksınız. Visual Studio 'da, sizin için kullanabileceğiniz çeşitli seçenekleri gösteren bir liste vardır. Ayrıca, IDE 'de görevler gerçekleştirmek için başka bir yol sağlayan bir menü de vardır. Örneğin, **Başlangıç sayfasında** **Yeni proje** ' yi seçmek yerine, menü çubuğunu kullanabilir ve **Yeni proje** > **Dosya** ' yı seçebilirsiniz.

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>İlk uygulamanızı oluşturma

**Başlangıç sayfasında** **Yeni proje**' yi seçin. **Yeni proje** iletişim kutusunda, sol taraftaki **görsel C#**  kategorisini ve ardından **Web**' i seçin ve **ASP.NET Web uygulaması (.NET Framework)** proje şablonunu seçin. Projenizi "Mvcfilmi" olarak adlandırın ve ardından **Tamam**' ı seçin.

![](getting-started/_static/image2.png)

**Yeni ASP.NET Web uygulaması** Iletişim kutusunda **MVC** ' yi ve ardından **Tamam**' ı seçin.

![](getting-started/_static/image3.png)

Visual Studio, az önce oluşturduğunuz ASP.NET MVC projesi için varsayılan bir şablon kullandı, bu nedenle artık herhangi bir şey yapmadan çalışan bir uygulamaya sahipsiniz! Bu basit bir "Merhaba Dünya!" Project ve uygulamanızı başlatmak için iyi bir yerdir.

![](getting-started/_static/image4.png)

Hata ayıklamaya başlamak için **F5**'e basın. **F5**tuşuna bastığınızda, Visual Studio [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) başlar ve Web uygulamanızı çalıştırır. Daha sonra Visual Studio bir tarayıcı başlatır ve uygulamanın giriş sayfasını açar. Tarayıcının adres çubuğunun `example.com`gibi `localhost:port#` söydiğine dikkat edin. Bunun nedeni `localhost` her zaman kendi yerel bilgisayarınıza işaret ettiğinden, bu durumda yeni oluşturduğunuz uygulamayı çalıştırıyor olur. Visual Studio bir Web projesi çalıştırdığında, Web sunucusu için rastgele bir bağlantı noktası kullanılır. Aşağıdaki görüntüde, bağlantı noktası numarası 1234 ' dir. Uygulamayı çalıştırdığınızda, farklı bir bağlantı noktası numarası görürsünüz.

![](getting-started/_static/image5.png)

Bu varsayılan şablon size hemen `Home`, `Contact`ve `About` sayfaları sağlar. Aşağıdaki görüntüde **ana**, **hakkında**ve **iletişim** bağlantıları gösterilmez. Tarayıcı pencerenizin boyutuna bağlı olarak, bu bağlantıları görmek için gezinti simgesine tıklamanız gerekebilir.

![](getting-started/_static/image6.png)

Uygulama, kaydolmak ve oturum açmak için destek de sağlar. Sonraki adım, bu uygulamanın nasıl çalıştığını değiştirmek ve ASP.NET MVC hakkında biraz bilgi sağlamaktır. ASP.NET MVC uygulamasını kapatın ve bazı kodları değiştirelim.

Geçerli öğreticilerin bir listesi için bkz. [MVC Önerilen makaleler](../mvc-learning-sequence.md).

## <a name="see-this-app-running-on-azure"></a>Bkz. Azure 'da çalışan bu uygulama

Canlı bir Web uygulaması olarak çalışan tamamlanmış siteyi görmek istiyor musunuz? Aşağıdaki düğmeye tıklayarak uygulamanın tüm sürümünü Azure hesabınıza dağıtabilirsiniz.

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

Bu çözümü Azure 'a dağıtmak için bir Azure hesabınızın olması gerekir. Henüz bir hesabınız yoksa, bir hesap oluşturmak için aşağıdaki seçeneklerden birini kullanın:

- [Ücretsiz bir Azure hesabı açarak](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) ücretli Azure hizmetlerini denemek için kullanabileceğiniz krediler edinin ve hatta kullanıldıktan sonra bile hesabı tutabilir ve ücretsiz Azure hizmetlerini kullanabilirsiniz.
- [Visual Studio abone avantajlarınızı etkinleştirin](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) -Visual Studio aboneliğiniz, ücretli Azure hizmetleri için kullanabileceğiniz her ay krediler sunar.

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)
