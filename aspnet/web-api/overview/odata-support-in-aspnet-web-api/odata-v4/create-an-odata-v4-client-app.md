---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: OData v4 Istemci uygulaması oluşturma (C#) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556296"
---
# <a name="create-an-odata-v4-client-app-c"></a>OData v4 İstemci Uygulaması Oluşturma (C#)

, [Mike te son](https://github.com/MikeWasson)

Önceki öğreticide CRUD işlemlerini destekleyen temel bir OData hizmeti oluşturdunuz. Şimdi hizmet için bir istemci oluşturalım.

Visual Studio 'nun yeni bir örneğini başlatın ve yeni bir konsol uygulaması projesi oluşturun. **Yeni proje** iletişim kutusunda,  **C# Visual** &gt; **Windows Masaüstü**&gt; **yüklü** &gt; **şablonları** ' nı seçin ve **konsol uygulaması** şablonunu seçin. Projeyi &quot;ProductsApp&quot;olarak adlandırın.

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> Ayrıca, konsol uygulamasını OData hizmetini içeren aynı Visual Studio çözümüne ekleyebilirsiniz.

## <a name="install-the-odata-client-code-generator"></a>OData Istemci kod oluşturucuyu yükler

**Araçlar** menüsünde **Uzantılar ve güncelleştirmeler**' i seçin. **Çevrimiçi** &gt; **Visual Studio Galerisi**' ni seçin. Arama kutusuna &quot;OData Istemci kodu Oluşturucu&quot;aratın. VSıX 'i yüklemek için **İndir** 'e tıklayın. Visual Studio 'Yu yeniden başlatmanız istenebilir.

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>OData hizmetini yerel olarak çalıştırma

Visual Studio 'dan ProductService projesini çalıştırın. Varsayılan olarak, Visual Studio uygulama köküne bir tarayıcı başlatır. URI 'yi aklınızda bulunan Bu, bir sonraki adımda gerekli olacaktır. Uygulamayı çalışır durumda bırakın.

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> Her iki projeyi de aynı çözüme yerleştirirseniz, ProductService projesini hata ayıklama olmadan çalıştırdığınızdan emin olun. Bir sonraki adımda, konsol uygulama projesini değiştirirken hizmeti çalışır durumda tutmanız gerekecektir.

## <a name="generate-the-service-proxy"></a>Hizmet proxy 'Si oluşturma

Hizmet proxy 'si OData hizmetine erişim yöntemlerini tanımlayan bir .NET sınıfıdır. Proxy, Yöntem çağrılarını HTTP isteklerine çevirir. Bir [T4 şablonu](https://msdn.microsoft.com/library/bb126445.aspx)çalıştırarak proxy sınıfını oluşturacaksınız.

Projeye sağ tıklayın. &gt; **Yeni öğe** **Ekle** ' yi seçin.

![](create-an-odata-v4-client-app/_static/image5.png)

**Yeni öğe Ekle** iletişim kutusunda,  **C# Visual Items** &gt; **Code** &gt; **OData Client**' ı seçin. Şablonu &quot;ProductClient.tt&quot;olarak adlandırın. **Ekle** ' ye tıklayın ve Güvenlik Uyarısı ' na tıklayın.

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

Bu noktada, yoksayabilirsiniz bir hata alırsınız. Visual Studio şablonu otomatik olarak çalıştırır, ancak şablonda önce bazı yapılandırma ayarları gerekir.

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

ProductClient. OData. config dosyasını açın. `Parameter` öğesinde, ProductService projesinden URI 'yi (önceki adımda) yapıştırın. Örneğin:

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

Şablonu yeniden çalıştırın. Çözüm Gezgini ' de, ProductClient.tt dosyasına sağ tıklayın ve **özel araç Çalıştır**' ı seçin.

Şablon, proxy 'yi tanımlayan ProductClient.cs adlı bir kod dosyası oluşturur. Uygulamanızı geliştirirken, OData uç noktasını değiştirirseniz, proxy 'yi güncelleştirmek için şablonu yeniden çalıştırın.

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>OData hizmetini çağırmak için hizmet proxy 'sini kullanma

Program.cs dosyasını açın ve ortak kodu aşağıdaki kodla değiştirin.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

*Serviceurı* değerini daha önce gelen hizmet URI 'siyle değiştirin.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

Uygulamayı çalıştırdığınızda, aşağıdakilerden çıkış yapmanız gerekir:

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]
