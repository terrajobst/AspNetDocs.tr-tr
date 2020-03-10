---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: ASP.NET Web API 2,2 kullanarak OData v4 uç noktası oluşturma | Microsoft Docs
author: MikeWasson
description: Açık Veri Protokolü (OData) Web için bir veri erişim protokolüdür. OData, CRUD işlemleri aracılığıyla veri kümelerini sorgulamak ve işlemek için Tekdüzen bir yol sağlar...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598737"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a>ASP.NET Web API 'SI kullanarak OData v4 uç noktası oluşturma 

> Açık Veri Protokolü (OData) Web için bir veri erişim protokolüdür. OData, CRUD işlemleri (oluşturma, okuma, güncelleştirme ve silme) aracılığıyla veri kümelerini sorgulamak ve işlemek için Tekdüzen bir yol sağlar.
>
> ASP.NET Web API 'SI hem v3 hem de v4 protokolünü destekler. V3 uç noktasıyla yan yana çalışan bir v4 uç noktasına bile sahip olabilirsiniz.
>
> Bu öğreticide, CRUD işlemlerini destekleyen bir OData v4 uç noktası oluşturma işlemi gösterilmektedir.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
>
> - Web API 5,2
> - OData v4
> - Visual Studio 2017 (Visual Studio 2017 [buraya](https://visualstudio.microsoft.com/downloads/)indirin)
> - Entity Framework 6
> - .NET 4.7.2
>
> ## <a name="tutorial-versions"></a>Öğretici sürümleri
>
> OData sürüm 3 için bkz. [OData v3 uç noktası oluşturma](../odata-v3/creating-an-odata-endpoint.md).

## <a name="create-the-visual-studio-project"></a>Visual Studio projesi oluşturma

Visual Studio 'da, **Dosya** menüsünden **Yeni** &gt; **Proje**' yi seçin.

**Yüklü** &gt;  **C# Visual** &gt; **Web**' i genişletin ve **ASP.NET Web uygulaması (.NET Framework)** şablonunu seçin. Projeyi &quot;ProductService&quot;olarak adlandırın.

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

**Tamam**’ı seçin.

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

**Boş** şablonu seçin. **İçin klasör ve çekirdek başvuruları Ekle**altında **Web API 'si**' ni seçin. **Tamam**’ı seçin.

## <a name="install-the-odata-packages"></a>OData paketlerini yükler

**Araçlar** menüsünde **NuGet Paket Yöneticisi** &gt; **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsol penceresinde, şunu yazın:

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

Bu komut en son OData NuGet paketlerini yükleme.

## <a name="add-a-model-class"></a>Bir model sınıfı ekleme

*Model* , uygulamanızdaki bir veri varlığını temsil eden bir nesnedir.

Çözüm Gezgini modeller klasörüne sağ tıklayın. Bağlam menüsünden &gt; **sınıfı** **Ekle** ' yi seçin.

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> Kurala göre, model sınıfları modeller klasörüne yerleştirilir, ancak bu kuralı kendi projelerinizde izlemeniz gerekmez.

`Product`sınıfı adlandırın. Product.cs dosyasında, demirbaş kodu aşağıdaki kodla değiştirin:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

`Id` özelliği varlık anahtarıdır. İstemciler, varlıkları anahtara göre sorgulayabilir. Örneğin, KIMLIĞI 5 olan ürünü almak için URI `/Products(5)`. `Id` özelliği, arka uç veritabanında da birincil anahtar olacaktır.

## <a name="enable-entity-framework"></a>Entity Framework etkinleştir

Bu öğreticide, arka uç veritabanını oluşturmak için Entity Framework (EF) Code First kullanacağız.

> [!NOTE]
> Web API OData, EF gerektirmez. Veritabanı varlıklarını modellerle çevirebilirler herhangi bir veri erişim katmanını kullanın.

İlk olarak, EF için NuGet paketini yüklemeniz gerekir. **Araçlar** menüsünde **NuGet Paket Yöneticisi** &gt; **Paket Yöneticisi konsolu**' nu seçin. Paket Yöneticisi konsol penceresinde, şunu yazın:

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

Web. config dosyasını açın ve aşağıdaki bölümü, **configSections** öğesinden sonra **yapılandırma** öğesinin içine ekleyin.

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

Bu ayar, LocalDB veritabanı için bir bağlantı dizesi ekler. Bu veritabanı, uygulamayı yerel olarak çalıştırdığınızda kullanılacaktır.

Ardından modeller klasörüne `ProductsContext` adlı bir sınıf ekleyin:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

Oluşturucuda, `"name=ProductsContext"` bağlantı dizesinin adını verir.

## <a name="configure-the-odata-endpoint"></a>OData uç noktasını yapılandırma

Start/WebApiConfig. cs\_dosya uygulamasını açın. Aşağıdaki **using** deyimlerini ekleyin:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

Ardından **register** yöntemine aşağıdaki kodu ekleyin:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

Bu kod iki şeyi yapar:

- Bir Varlık Veri Modeli (EDM) oluşturur.
- Bir yol ekler.

EDM, verilerin soyut bir modelidir. EDM, hizmet meta verileri belgesi oluşturmak için kullanılır. **ODataConventionModelBuilder** sınıfı varsayılan adlandırma kurallarını kullanarak bir EDM oluşturur. Bu yaklaşım için en az kod gereklidir. EDM üzerinde daha fazla denetim istiyorsanız, özellik, anahtar ve gezinti özelliklerini açıkça ekleyerek EDM oluşturmak için **ODataModelBuilder** sınıfını kullanabilirsiniz.

Bir *yol* , Web API 'sine http isteklerini uç noktaya nasıl yönlendirildiğini söyler. OData v4 yolu oluşturmak için, **MapODataServiceRoute** genişletme yöntemini çağırın.

Uygulamanızda birden çok OData uç noktası varsa, her biri için ayrı bir yol oluşturun. Her rotaya benzersiz bir yol adı ve ön ek verin.

## <a name="add-the-odata-controller"></a>OData denetleyicisi ekleme

*Denetleyici* , http isteklerini işleyen bir sınıftır. OData hizmetinizde her bir varlık kümesi için ayrı bir denetleyici oluşturursunuz. Bu öğreticide, `Product` varlığı için bir denetleyici oluşturacaksınız.

Çözüm Gezgini, denetleyiciler klasörüne sağ tıklayın ve &gt; **sınıfı** **Ekle** ' yi seçin. `ProductsController`sınıfı adlandırın.

> [!NOTE]
> OData v3 için Bu öğreticinin sürümü, **denetleyiciyi Ekle** yapı iskelesi kullanır. Şu anda OData v4 için bir yapı iskelesi yoktur.

ProductsController.cs içindeki ortak kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

Denetleyici, EF kullanarak veritabanına erişmek için `ProductsContext` sınıfını kullanır. Denetleyicinin **Productscontext**'i atmak için **Dispose** metodunu geçersiz kıldığını unutmayın.

Bu, denetleyicinin başlangıç noktasıdır. Ardından, tüm CRUD işlemleri için yöntemler ekleyeceğiz.

## <a name="query-the-entity-set"></a>Varlık kümesini sorgulama

`ProductsController`için aşağıdaki yöntemleri ekleyin.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

`Get` yönteminin parametresiz sürümü tüm ürünler koleksiyonunu döndürür. *Anahtar* parametresine sahip `Get` yöntemi bir ürünü anahtarıyla arar (Bu durumda, `Id` özelliği).

**[Enablequery]** özniteliği, istemcilerin $filter, $sort ve $Page gibi sorgu seçeneklerini kullanarak sorguyu değiştirmesini sağlar. Daha fazla bilgi için bkz. [OData sorgu seçeneklerini destekleme](../supporting-odata-query-options.md).

## <a name="add-an-entity-to-the-entity-set"></a>Varlık kümesine varlık ekleme

İstemcilerin veritabanına yeni bir ürün eklemesini sağlamak için aşağıdaki yöntemi `ProductsController`ekleyin.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a>Varlığı güncelleştirme

OData, bir varlığı güncelleştirmek için iki farklı semantiğini destekler, yama ve PUT.

- Düzeltme Eki kısmi bir güncelleştirme gerçekleştirir. İstemci yalnızca güncelleştirilecek özellikleri belirtir.
- PUT, tüm varlığın yerini alır.

PUT 'in dezavantajı, istemcinin, değişmeyen değerler de dahil olmak üzere varlıktaki tüm özelliklerin değerlerini gönderebilmesi gerekir. [OData özelliği](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) , düzeltme ekinin tercih edildiğini belirtir.

Her durumda, hem düzeltme eki hem de PUT yöntemlerinin kodu aşağıda verilmiştir:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

Düzeltme durumunda, denetleyici değişiklikleri izlemek için **Delta&lt;t&gt;** türünü kullanır.

## <a name="delete-an-entity"></a>Bir varlığı silme

İstemcilerin bir ürünü veritabanından silmesini sağlamak için aşağıdaki yöntemi `ProductsController`ekleyin.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]
