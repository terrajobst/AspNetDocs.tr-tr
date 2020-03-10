---
uid: web-api/overview/older-versions/self-host-a-web-api
title: Self-Host ASP.NET Web API 1 (C#)-ASP.NET 4. x
author: MikeWasson
description: Kod ile öğretici, bir Web API 'sinin bir konsol uygulaması içinde nasıl barındıralınacağını gösterir.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525090"
---
# <a name="self-host-aspnet-web-api-1-c"></a>Self-Host ASP.NET Web API 1 (C#)

, [Mike te son](https://github.com/MikeWasson)

> Bu öğreticide, bir Web API 'sinin konsol uygulaması içinde nasıl barındırılacağını gösterilmektedir. ASP.NET Web API 'SI IIS gerektirmez. Kendi ana bilgisayar sürecinizdeki bir Web API 'sini kendi kendinize barındırabilirsiniz. 
> 
> **Yeni uygulamalar, Web API 'sini Self barındırmak için OWıN kullanmalıdır.** Bkz. [OWIN kullanarak Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Web API 1
> - Visual Studio 2012

## <a name="create-the-console-application-project"></a>Konsol uygulaması projesi oluşturma

Visual Studio 'Yu başlatın ve **Başlangıç** sayfasından **Yeni proje** ' yi seçin. Ya da **Dosya** menüsünde **Yeni** ' yi ve ardından **Proje**' yi seçin.

**Şablonlar** bölmesinde, **yüklü şablonlar** ' ı seçin ve **görsel C#**  düğümünü genişletin. **Görsel C#** altında **Windows**' u seçin. Proje şablonları listesinde **konsol uygulaması**' nı seçin. Projeyi &quot;SelfHost&quot; olarak adlandırın ve **Tamam**' a tıklayın.

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>Hedef Framework 'Ü ayarlama (Visual Studio 2010)

Visual Studio 2010 kullanıyorsanız, hedef çerçeveyi 4,0 .NET Framework değiştirin. (Varsayılan olarak, proje şablonu [.NET Framework Istemci profilini](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile)hedefler.)

Çözüm Gezgini, projeye sağ tıklayın ve **Özellikler**' i seçin. **Hedef çerçeve** açılan listesinde, hedef framework 'ü .NET Framework 4,0 olarak değiştirin. Değişikliği uygulamak isteyip istemediğiniz sorulduğunda **Evet**' e tıklayın.

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>NuGet Paket Yöneticisi 'Ni yükler

NuGet Paket Yöneticisi, Web API derlemelerini bir non-ASP.NET projesine eklemenin en kolay yoludur.

NuGet Paket Yöneticisi 'nin yüklü olup olmadığını denetlemek için Visual Studio 'daki **Araçlar** menüsüne tıklayın. **NuGet Paket Yöneticisi**adlı bir menü öğesi görürseniz, NuGet Paket Yöneticisi ' ne sahip olursunuz.

NuGet Paket Yöneticisi 'Ni yüklemek için:

1. Visual Studio’yu çalıştırın.
2. **Araçlar** menüsünde **Uzantılar ve güncelleştirmeler**' i seçin.
3. **Uzantılar ve güncelleştirmeler** Iletişim kutusunda **çevrimiçi**' ı seçin.
4. "NuGet Paket Yöneticisi" ni görmüyorsanız, arama kutusuna "NuGet Paket Yöneticisi" yazın.
5. NuGet Paket Yöneticisi ' ni seçin ve **İndir**' e tıklayın.
6. Yükleme tamamlandıktan sonra yüklemesi istenir.
7. Yükleme tamamlandıktan sonra, Visual Studio 'Yu yeniden başlatmanız istenebilir.

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>Web API NuGet paketini ekleme

NuGet Paket Yöneticisi yüklendikten sonra, Web API Self-Host paketini projenize ekleyin.

1. **Araçlar** menüsünde **NuGet Paket Yöneticisi**' ni seçin. *Not*: Bu menü öğesini görmüyorsanız, NuGet Paket Yöneticisi 'nin doğru şekilde yüklendiğinden emin olun.
2. **Çözüm Için NuGet Paketlerini Yönet** ' i seçin
3. **NugGet paketlerini Yönet** Iletişim kutusunda **çevrimiçi**' ı seçin.
4. Arama kutusuna Microsoft. AspNet. WebApi. SelfHost&quot;&quot;yazın.
5. ASP.NET Web API Self Host paketi ' ni seçin ve ardından **yükler**' e tıklayın.
6. Paket yüklendikten sonra, iletişim kutusunu kapatmak için **Kapat** ' a tıklayın.

> [!NOTE]
> Microsoft. AspNet. WebApi. SelfHost adlı paketi, AspNetWebApi. SelfHost değil ' yi yüklediğinizden emin olun.

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>Modeli ve denetleyiciyi oluşturma

Bu [öğretici, başlangıç öğreticisiyle](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) aynı model ve denetleyici sınıflarını kullanır.

`Product`adlı bir ortak sınıf ekleyin.

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

`ProductsController`adlı bir ortak sınıf ekleyin. Bu sınıfı **System. Web. http. ApiController**öğesinden türet.

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

Bu denetleyicideki kod hakkında daha fazla bilgi için bkz. [Başlangıç](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) öğreticisi. Bu denetleyici üç GET eylemini tanımlar:

| URI | Açıklama |
| --- | --- |
| /api/Products | Tüm ürünlerin bir listesini alın. |
| /api/Products/*ID* | KIMLIĞE göre bir ürün alın. |
| /api/Products/? Category =*Kategori* | Kategoriye göre ürünlerin bir listesini alın. |

## <a name="host-the-web-api"></a>Web API 'sini barındırma

Program.cs dosyasını açın ve aşağıdaki using deyimlerini ekleyin:

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

**Program** sınıfına aşağıdaki kodu ekleyin.

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>Seçim HTTP URL ad alanı ayırması ekleme

Bu uygulama `http://localhost:8080/`dinler. Varsayılan olarak, belirli bir HTTP adresini dinlemek için yönetici ayrıcalıkları gerekir. Bu öğreticiyi çalıştırdığınızda şu hatayı alabilirsiniz: "HTTP URL 'SI kaydedilemedi http://+:8080/" Bu hatayı önlemenin iki yolu vardır:

- Visual Studio 'Yu yükseltilmiş yönetici izinleriyle çalıştırın veya
- Hesap izinlerinize URL 'YI ayırmasını sağlamak için Netsh. exe ' yi kullanın.

Netsh. exe ' yi kullanmak için, yönetici ayrıcalıklarıyla bir komut istemi açın ve aşağıdaki komutu girin:

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

burada, *MakineAdı* kullanıcı hesabıdır.

Kendi kendine barındırmayı bitirdiğinizde ayırmayı silmeyi unutmayın:

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>Bir Istemci uygulamasından (C#) Web API 'sini çağırma

Web API 'sini çağıran basit bir konsol uygulaması yazalım.

Çözüme yeni bir konsol uygulama projesi ekleyin:

- Çözüm Gezgini, çözüme sağ tıklayın ve **Yeni Proje Ekle**' yi seçin.
- &quot;ClientApp&quot;adlı yeni bir konsol uygulaması oluşturun.

![](self-host-a-web-api/_static/image5.png)

ASP.NET Web API çekirdek kitaplıkları paketini eklemek için NuGet Paket Yöneticisi 'Ni kullanın:

- Araçlar menüsünde **NuGet Paket Yöneticisi**' ni seçin.
- **Çözüm Için NuGet Paketlerini Yönet** ' i seçin
- **NuGet Paketlerini Yönet** Iletişim kutusunda **çevrimiçi**' ı seçin.
- Arama kutusuna &quot;Microsoft. AspNet. WebApi. Client&quot;yazın.
- Microsoft ASP.NET Web API Istemci kitaplıkları paketini seçin ve ardından **Install**' a tıklayın.

ClientApp ' de SelfHost projesine bir başvuru ekleyin:

- Çözüm Gezgini, ClientApp projesine sağ tıklayın.
- **Başvuru Ekle**' yi seçin.
- **Başvuru Yöneticisi** iletişim kutusunda, **çözüm**altında **Projeler**' i seçin.
- SelfHost projesini seçin.
- **Tamam**’a tıklayın.

![](self-host-a-web-api/_static/image6.png)

Client/program. cs dosyasını açın. Aşağıdaki **using** ifadesini ekleyin:

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

Statik bir **HttpClient** örneği ekleyin:

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

Tüm ürünleri listelemek, KIMLIĞE göre ürün listelemek ve ürünleri kategoriye göre listelemek için aşağıdaki yöntemleri ekleyin.

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

Bu yöntemlerin her biri aynı düzene uyar:

1. Uygun URI 'ye bir GET isteği göndermek için **HttpClient. GetAsync** çağrısı yapın.
2. **HttpResponseMessage. EnsureSuccessStatusCode**öğesini çağırın. HTTP yanıt durumu bir hata kodu ise, bu yöntem bir özel durum oluşturur.
3. HTTP yanıtından bir CLR türü serisini kaldırmak için **Readasasync&lt;t&gt;** çağırın. Bu yöntem, **System .net. http. Httpcontenbir**'da tanımlanan bir genişletme yöntemidir.

**GetAsync** ve **readasasync** yöntemlerinin her ikisi de zaman uyumsuzdur. Zaman uyumsuz işlemi temsil eden **görev** nesnelerini döndürür. **Result** özelliğinin alınması, işlem tamamlanana kadar iş parçacığını engeller.

Engelleme olmayan çağrılar yapma da dahil olmak üzere HttpClient kullanımı hakkında daha fazla bilgi için bkz. [.net Istemcisinden Web API çağırma](../advanced/calling-a-web-api-from-a-net-client.md).

Bu yöntemleri çağırmadan önce HttpClient örneğindeki BaseAddress özelliğini "`http://localhost:8080`" olarak ayarlayın. Örneğin:

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

Bu, aşağıdaki çıktıyı göstermelidir. (Önce SelfHost uygulamasını çalıştırmayı unutmayın.)

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)
