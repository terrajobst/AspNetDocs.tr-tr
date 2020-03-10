---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Birim testi ASP.NET Web API 2 ' de Entity Framework Mocking | Microsoft Docs
author: Rick-Anderson
description: Bu kılavuz ve uygulama, Entity Framework kullanan Web API 2 uygulamanız için birim testlerinin nasıl oluşturulacağını göstermektedir. Nasıl değiştirileceği gösterilmektedir...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555092"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>Birim testi ASP.NET Web API 2 ' de Entity Framework Mocking

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

[Tamamlanmış projeyi indir](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> Bu kılavuz ve uygulama, Entity Framework kullanan Web API 2 uygulamanız için birim testlerinin nasıl oluşturulacağını göstermektedir. Bağlam nesnesinin test için geçirilmesini ve Entity Framework birlikte çalışan test nesnelerinin nasıl oluşturulacağını etkinleştirmek için, yapı iskelesi denetleyicisinin nasıl değiştirileceğini gösterir.
>
> ASP.NET Web API 'SI ile birim teste giriş için bkz. [ASP.NET Web API 2 Ile birim testi](unit-testing-with-aspnet-web-api.md).
>
> Bu öğreticide, ASP.NET Web API 'sinin temel kavramları hakkında bilgi sahibi olduğunuz varsayılır. Tanıtım öğreticisi için bkz. [ASP.NET Web API 2 Ile çalışmaya](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)başlama.
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
- [Model sınıfı oluşturma](#modelclass)
- [Denetleyiciyi ekleme](#controller)
- [Bağımlılık ekleme ekleme](#dependency)
- [NuGet paketlerini test projesine yükler](#testpackages)
- [Test bağlamı oluştur](#testcontext)
- [Test oluştur](#tests)
- [Testleri Çalıştır](#runtests)

[ASP.NET Web API 2 Ile birim testinde](unit-testing-with-aspnet-web-api.md)adımları zaten tamamladıysanız, [denetleyiciyi ekleme](#controller)bölümüne atlayabilirsiniz.

<a id="prereqs"></a>
## <a name="prerequisites"></a>Önkoşullar

Visual Studio 2017 Community, Professional veya Enterprise Edition

<a id="download"></a>
## <a name="download-code"></a>Kodu indirin

[Tamamlanmış projeyi](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)indirin. İndirilebilir proje, bu konu için birim test kodu ve [birim testi ASP.NET Web API 2](unit-testing-with-aspnet-web-api.md) konusu için içerir.

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>Birim testi projesiyle uygulama oluştur

Uygulamanızı oluştururken bir birim testi projesi oluşturabilir veya var olan bir uygulamaya bir birim testi projesi ekleyebilirsiniz. Bu öğretici, uygulamayı oluştururken bir birim testi projesi oluşturmayı gösterir.

**Storeapp**adlı yeni bir ASP.NET Web uygulaması oluşturun.

Yeni ASP.NET proje penceresinde **boş** şablonu seçin ve Web API 'si için klasörler ve çekirdek başvurular ekleyin. **Birim testleri Ekle** seçeneğini belirleyin. Birim testi projesi, otomatik olarak **Storeapp. Tests**olarak adlandırılır. Bu adı koruyabilirsiniz.

![birim testi projesi oluştur](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

Uygulamayı oluşturduktan sonra, bunu iki proje- **Storeapp** ve **Storeapp. Tests**içerdiğini görürsünüz.

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>Model sınıfı oluşturma

StoreApp projenizde, **Product.cs**adlı **modeller** klasörüne bir sınıf dosyası ekleyin. Dosyanın içeriğini aşağıdaki kodla değiştirin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

Çözümü derleyin.

<a id="controller"></a>
## <a name="add-the-controller"></a>Denetleyiciyi ekleme

Denetleyiciler klasörüne sağ tıklayın ve **Ekle** ve **yeni yapı iskelesi öğesi**' ni seçin. Entity Framework kullanarak, eylemlerle Web API 2 denetleyicisi ' ni seçin.

![Yeni denetleyici Ekle](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

Aşağıdaki değerleri ayarlayın:

- Denetleyici adı: **ProductController**
- Model Sınıfı: **ürün**
- Veri bağlamı sınıfı: [aşağıda görülen değerleri dolduran **Yeni veri bağlam** düğmesini seçin]

![denetleyiciyi belirtin](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

Denetleyiciyi otomatik olarak oluşturulan kodla oluşturmak için **Ekle** ' ye tıklayın. Kod, ürün sınıfının örneklerini oluşturma, alma, güncelleştirme ve silme yöntemlerini içerir. Aşağıdaki kod, ürün ekleme yöntemini gösterir. Metodun bir **ıhttpactionresult**örneği döndürtiğine dikkat edin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

Ihttpactionresult, Web API 2 ' deki yeni özelliklerden biridir ve birim testi geliştirmeyi basitleştirir.

Bir sonraki bölümde, test nesnelerini denetleyiciye geçirmeyi kolaylaştırmak için oluşturulan kodu özelleştirecek olursunuz.

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>Bağımlılık ekleme ekleme

Şu anda, ProductController sınıfı StoreAppContext sınıfının bir örneğini kullanmak için sabit olarak kodlanmıştır. Uygulamanızı değiştirmek ve bu sabit kodlanmış bağımlılığı kaldırmak için bağımlılık ekleme adlı bir model kullanacaksınız. Bu bağımlılığı bozarak, test ederken bir sahte nesne geçirebilirsiniz.

**Modeller** klasörüne sağ tıklayın ve **Istoreappcontext**adlı yeni bir arabirim ekleyin.

Kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

StoreAppContext.cs dosyasını açın ve aşağıdaki vurgulanan değişiklikleri yapın. Nottaki önemli değişiklikler şunlardır:

- StoreAppContext sınıfı ıtoreappcontext arabirimini uygular
- MarkAsModified yöntemi uygulandı

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

ProductController.cs dosyasını açın. Mevcut kodu vurgulanan kodla eşleşecek şekilde değiştirin. Bu değişiklikler StoreAppContext üzerindeki bağımlılığı keser ve diğer sınıfların bağlam sınıfı için farklı bir nesneye geçmesini sağlar. Bu değişiklik, birim testleri sırasında bir test bağlamı geçirmenize olanak sağlar.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

ProductController 'da yapmanız gereken bir değişiklik daha vardır. **Putproduct** yönteminde, varlık durumunu ayarlayan satırı, MarkAsModified yöntemine yapılan bir çağrı ile değiştirin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

Çözümü derleyin.

Şimdi test projesi ayarlamaya hazırsınız.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>NuGet paketlerini test projesine yükler

Bir uygulama oluşturmak için boş şablonu kullandığınızda, birim testi projesi (StoreApp. Tests) yüklü herhangi bir NuGet paketini içermez. Web API şablonu gibi diğer şablonlar, birim testi projesine bazı NuGet paketleri içerir. Bu öğreticide, Entity Framework paketini ve Microsoft ASP.NET Web API 2 Core paketini test projesine eklemeniz gerekir.

StoreApp. Tests projesine sağ tıklayın ve **NuGet Paketlerini Yönet**' i seçin. Paketleri bu projeye eklemek için StoreApp. Tests projesini seçmelisiniz.

![Paketleri yönetme](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

Çevrimiçi paketlerden EntityFramework paketini bulun ve (sürüm 6,0 veya üzeri) yükler. EntityFramework paketinin zaten yüklü olduğu görüntülenirse StoreApp. Tests projesi yerine StoreApp projesini seçmiş olabilirsiniz.

![Entity Framework Ekle](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

Microsoft ASP.NET Web API 2 çekirdek paketini bulun ve yükler.

![Web API Core paketini yükler](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

NuGet Paketlerini Yönet penceresini kapatın.

<a id="testcontext"></a>
## <a name="create-test-context"></a>Test bağlamı oluştur

Test projesine **Testdbset** adlı bir sınıf ekleyin. Bu sınıf, test veri kümesi için temel sınıf olarak hizmet verir. Kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

Aşağıdaki kodu içeren test projesine **Testproductdbset** adlı bir sınıf ekleyin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

**Teststoreappcontext** adlı bir sınıf ekleyin ve mevcut kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>Test oluştur

Varsayılan olarak, test projeniz **UnitTest1.cs**adlı boş bir test dosyası içerir. Bu dosya, test yöntemleri oluşturmak için kullandığınız öznitelikleri gösterir. Bu öğreticide, yeni bir test sınıfı ekleyeceğiniz için bu dosyayı silebilirsiniz.

Test projesine **Testproductcontroller** adlı bir sınıf ekleyin. Kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>Testleri çalıştırma

Şimdi testleri çalıştırmaya hazırsınız. **TestMethod** özniteliğiyle işaretlenen tüm yöntem test edilecek. **Test** menü öğesinden testleri çalıştırın.

![testleri çalıştırma](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

**Test Gezgini** penceresini açın ve testlerin sonuçlarına dikkat edin.

![test sonuçları](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)
