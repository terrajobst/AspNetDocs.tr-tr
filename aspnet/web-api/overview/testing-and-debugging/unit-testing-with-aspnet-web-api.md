---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: Birim testi ASP.NET Web API 2 | Microsoft Docs
author: Rick-Anderson
description: Bu kılavuz ve uygulama, Web API 2 uygulamanız için basit birim testlerin nasıl oluşturulacağını göstermektedir. Bu öğreticide bir birim testi proj 'i nasıl dahil edileceğini gösterilmektedir...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554973"
---
# <a name="unit-testing-aspnet-web-api-2"></a>Birim testi ASP.NET Web API 2

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> Bu kılavuz ve uygulama, Web API 2 uygulamanız için basit birim testlerin nasıl oluşturulacağını göstermektedir. Bu öğreticide, çözümünüze bir birim testi projesinin nasıl dahil edileceğini ve döndürülen değerleri bir denetleyici yönteminden denetleyen test yöntemlerini nasıl yazacağınız gösterilmektedir.
>
> Bu öğreticide, ASP.NET Web API 'sinin temel kavramları hakkında bilgi sahibi olduğunuz varsayılır. Tanıtım öğreticisi için bkz. [ASP.NET Web API 2 Ile çalışmaya](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)başlama.
>
> Bu konudaki birim testleri, basit veri senaryolarıyla kasıtlı olarak sınırlıdır. Birim testi daha gelişmiş veri senaryoları için bkz. [ASP.NET Web API 2 birim testi sırasında Mocking Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Web API 2

## <a name="in-this-topic"></a>Bu konuda

Bu konu aşağıdaki bölümleri içermektedir:

- [Önkoşullar](#prereqs)
- [Kodu indir](#download)
- [Birim testi projesiyle uygulama oluştur](#appwithunittest)
    - [Uygulamayı oluştururken birim testi projesi Ekle](#whencreate)
    - [Varolan bir uygulamaya birim testi projesi Ekle](#addtoexisting)
- [Web API 2 uygulamasını ayarlama](#setupproject)
- [NuGet paketlerini test projesine yükler](#testpackages)
- [Test oluştur](#tests)
- [Testleri Çalıştır](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>Önkoşullar

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise sürümü

<a id="download"></a>
## <a name="download-code"></a>Kodu indirin

[Tamamlanmış projeyi](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)indirin. İndirilebilir proje, bu konu için birim test kodu ve [birim testi ASP.NET Web API konusu olduğunda Mocking Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) içerir.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>Birim testi projesiyle uygulama oluştur

Uygulamanızı oluştururken bir birim testi projesi oluşturabilir veya var olan bir uygulamaya bir birim testi projesi ekleyebilirsiniz. Bu öğreticide, birim testi projesi oluşturmak için her iki yöntem de gösterilmektedir. Bu öğreticiyi izlemek için her iki yaklaşımı de kullanabilirsiniz.

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>Uygulamayı oluştururken birim testi projesi Ekle

**Storeapp**adlı yeni bir ASP.NET Web uygulaması oluşturun.

![proje oluştur](unit-testing-with-aspnet-web-api/_static/image1.png)

Yeni ASP.NET proje penceresinde **boş** şablonu seçin ve Web API 'si için klasörler ve çekirdek başvurular ekleyin. **Birim testleri Ekle** seçeneğini belirleyin. Birim testi projesi, otomatik olarak **Storeapp. Tests**olarak adlandırılır. Bu adı koruyabilirsiniz.

![birim testi projesi oluştur](unit-testing-with-aspnet-web-api/_static/image2.png)

Uygulamayı oluşturduktan sonra, bunu iki proje içerdiğini görürsünüz.

![iki proje](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>Varolan bir uygulamaya birim testi projesi Ekle

Uygulamanızı oluştururken birim testi projesi oluşturmadıysanız, herhangi bir zamanda bir tane ekleyebilirsiniz. Örneğin, StoreApp adlı bir uygulamanız olduğunu ve birim testleri eklemek istediğinizi varsayalım. Bir birim testi projesi eklemek için çözümünüze sağ tıklayın ve **Ekle** ve **Yeni proje**' yi seçin.

![çözüme yeni proje Ekle](unit-testing-with-aspnet-web-api/_static/image4.png)

Sol bölmedeki **Test** ' i seçin ve proje türü Için **birim testi projesi** ' ni seçin. Projeyi **Storeapp. Tests**olarak adlandırın.

![birim testi projesi Ekle](unit-testing-with-aspnet-web-api/_static/image5.png)

Çözümünüzde birim testi projesini görürsünüz.

Birim testi projesinde, özgün projeye bir proje başvurusu ekleyin.

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>Web API 2 uygulamasını ayarlama

StoreApp projenizde, **Product.cs**adlı **modeller** klasörüne bir sınıf dosyası ekleyin. Dosyanın içeriğini aşağıdaki kodla değiştirin.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

Çözümü derleyin.

Denetleyiciler klasörüne sağ tıklayın ve **Ekle** ve **yeni yapı iskelesi öğesi**' ni seçin. **Web API 2 denetleyici-boş**seçeneğini belirleyin.

![Yeni denetleyici Ekle](unit-testing-with-aspnet-web-api/_static/image6.png)

Denetleyici adını **Simpleproductcontroller**olarak ayarlayın ve **Ekle**' ye tıklayın.

![denetleyiciyi belirtin](unit-testing-with-aspnet-web-api/_static/image7.png)

Mevcut kodu aşağıdaki kodla değiştirin. Bu örneği basitleştirmek için, veriler veritabanı yerine bir listede depolanır. Bu sınıfta tanımlanan liste üretim verilerini temsil eder. Denetleyicinin, ürün nesnelerinin listesini parametre olarak alan bir Oluşturucu içerdiğine dikkat edin. Bu Oluşturucu, birim testi sırasında test verilerini geçirmenize olanak sağlar. Denetleyici Ayrıca, zaman uyumsuz yöntemleri birim testi göstermek için iki **zaman uyumsuz** yöntem içerir. Bu zaman uyumsuz yöntemler, gereksiz kodu en aza indirmek için **Task. FromResult** çağırarak uygulanmıştır, ancak normalde Yöntemler Kaynak yoğunluklu işlemleri içerir.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

GetProduct yöntemi **ıhttpactionresult** arabiriminin bir örneğini döndürür. Ihttpactionresult, Web API 2 ' deki yeni özelliklerden biridir ve birim testi geliştirmeyi basitleştirir. Ihttpactionresult arabirimini uygulayan sınıflar [System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) ad alanında bulunur. Bu sınıflar bir eylem isteğinden olası yanıtları temsil eder ve HTTP durum kodlarına karşılık gelir.

Çözümü derleyin.

Şimdi test projesi ayarlamaya hazırsınız.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>NuGet paketlerini test projesine yükler

Bir uygulama oluşturmak için boş şablonu kullandığınızda, birim testi projesi (StoreApp. Tests) yüklü herhangi bir NuGet paketini içermez. Web API şablonu gibi diğer şablonlar, birim testi projesine bazı NuGet paketleri içerir. Bu öğretici için, test projesine Microsoft ASP.NET Web API 2 Core paketini dahil etmeniz gerekir.

StoreApp. Tests projesine sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin. Paketleri bu projeye eklemek için StoreApp. Tests projesini seçmelisiniz.

![Paketleri yönetme](unit-testing-with-aspnet-web-api/_static/image8.png)

Microsoft ASP.NET Web API 2 çekirdek paketini bulun ve yükler.

![Web API Core paketini yükler](unit-testing-with-aspnet-web-api/_static/image9.png)

NuGet Paketlerini Yönet penceresini kapatın.

<a id="tests"></a>
## <a name="create-tests"></a>Test oluştur

Varsayılan olarak, test projeniz UnitTest1.cs adlı boş bir test dosyası içerir. Bu dosya, test yöntemleri oluşturmak için kullandığınız öznitelikleri gösterir. Birim testleriniz için bu dosyayı kullanabilir ya da kendi dosyanızı oluşturabilirsiniz.

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

Bu öğretici için kendi test sınıfınızı oluşturacaksınız. UnitTest1.cs dosyasını silebilirsiniz. **TestSimpleProductController.cs**adlı bir sınıf ekleyin ve kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>Testleri çalıştırma

Şimdi testleri çalıştırmaya hazırsınız. **TestMethod** özniteliğiyle işaretlenen tüm yöntem test edilecek. **Test** menü öğesinden testleri çalıştırın.

![testleri çalıştırma](unit-testing-with-aspnet-web-api/_static/image11.png)

**Test Gezgini** penceresini açın ve testlerin sonuçlarına dikkat edin.

![test sonuçları](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>Özet

Bu öğreticiyi tamamladınız. Bu öğreticideki verilerin birim testi koşullarına odaklanmak için bilerek basitleştirilmiştir. Birim testi daha gelişmiş veri senaryoları için bkz. [ASP.NET Web API 2 birim testi sırasında Mocking Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).
