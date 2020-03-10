---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: ASP.NET Web API 'SI için yardım sayfaları oluşturma-ASP.NET 4. x
author: MikeWasson
description: Bu kod ile bu öğretici, ASP.NET 4. x içinde ASP.NET Web API 'SI için yardım sayfaları oluşturmayı gösterir.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556877"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a>ASP.NET Web API 'SI için yardım sayfaları oluşturma

, [Mike te son](https://github.com/MikeWasson)

Bu kod ile bu öğretici, ASP.NET 4. x içinde ASP.NET Web API 'SI için yardım sayfaları oluşturmayı gösterir.

Bir Web API 'SI oluşturduğunuzda, diğer geliştiricilerin API 'nizi nasıl çağırabileceğini bilmesi için, genellikle bir yardım sayfası oluşturmak yararlı olur. Tüm belgeleri el ile oluşturabilirsiniz, ancak mümkün olduğunca yeniden oluşturulması daha iyidir. Bu görevi daha kolay hale getirmek için ASP.NET Web API 'SI, çalışma zamanında otomatik olarak yardım sayfaları oluşturmak için bir kitaplık sağlar.

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a>API Yardım sayfaları oluşturma

[ASP.NET and Web Tools 2012,2 güncelleştirmesini](https://go.microsoft.com/fwlink/?LinkId=282650)yükler. Bu güncelleştirme yardım sayfalarını Web API 'SI proje şablonuyla tümleştirir.

Sonra, yeni bir ASP.NET MVC 4 projesi oluşturun ve Web API 'SI proje şablonunu seçin. Proje şablonu, `ValuesController`adlı örnek bir API denetleyicisi oluşturur. Şablon, API yardım sayfalarını da oluşturur. Yardım sayfası için tüm kod dosyaları projenin Areas klasörüne yerleştirilir.

![](creating-api-help-pages/_static/image2.png)

Uygulamayı çalıştırdığınızda, giriş sayfası API yardım sayfasına bir bağlantı içerir. Giriş sayfasından göreli yol/Help' dir.

![](creating-api-help-pages/_static/image3.png)

Bu bağlantı sizi bir API özet sayfasına getirir.

![](creating-api-help-pages/_static/image4.png)

Bu sayfanın MVC görünümü alanlarda/HelpPage/views/Help/Index. cshtml içinde tanımlanmıştır. Bu sayfayı düzen, giriş, başlık, stiller vb. değiştirmek için düzenleyebilirsiniz.

Sayfanın ana bölümü, denetleyiciye göre gruplandırılan bir API tablosudur. Tablo girdileri, **IApiExplorer** arabirimi kullanılarak dinamik olarak oluşturulur. (Bu arabirim hakkında daha sonra daha fazla konuşacak.) Yeni bir API denetleyicisi eklerseniz, tablo çalışma zamanında otomatik olarak güncelleştirilir.

"API" sütunu, HTTP yöntemini ve göreli URI 'yi listeler. "Açıklama" sütunu her API için belgeler içerir. Başlangıçta, belgeler yalnızca yer tutucu metindir. Sonraki bölümde, XML açıklamalarından nasıl belge ekleneceğini göstereceğiz.

Her API, örnek istek ve yanıt gövdeleri dahil olmak üzere daha ayrıntılı bilgiler içeren bir sayfanın bağlantısını içerir.

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a>Mevcut bir projeye yardım sayfaları ekleme

NuGet Paket Yöneticisi 'Ni kullanarak var olan bir Web API projesine yardım sayfaları ekleyebilirsiniz. Bu seçenek, "Web API" şablonundan farklı bir proje şablonundan başlayabilmeniz için faydalıdır.

**Araçlar** menüsünde, **NuGet Paket Yöneticisi**' ni seçin ve ardından **Paket Yöneticisi konsolu**' nu seçin. [Paket Yöneticisi konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) penceresinde, aşağıdaki komutlardan birini yazın:

Bir **C#** uygulama için: `Install-Package Microsoft.AspNet.WebApi.HelpPage`

**Visual Basic** bir uygulama için: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

Biri için C# bir diğeri Visual Basic olmak üzere iki paket vardır. Projenizle eşleşen birini kullandığınızdan emin olun.

Bu komut, gerekli derlemeleri yükleyip yardım sayfaları (Areas/HelpPage klasöründe bulunur) için MVC görünümlerini ekler. Yardım sayfasına el ile bir bağlantı eklemeniz gerekir. URI,/Help. Razor görünümünde bir bağlantı oluşturmak için aşağıdakileri ekleyin:

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

Ayrıca, alanların kaydettirildiğinizden emin olun. Global. asax dosyasında, zaten mevcut değilse, **uygulama\_start** yöntemine aşağıdaki kodu ekleyin:

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a>API belgeleri ekleme

Varsayılan olarak, yardım sayfalarında belgeler için yer tutucu dizeleri vardır. Belgeleri oluşturmak için [XML belge açıklamalarını](https://msdn.microsoft.com/library/b2s063f7.aspx) kullanabilirsiniz. Bu özelliği etkinleştirmek için, Start/HelpPageConfig. cs\_dosya bölgelerini/HelpPage/App açın ve aşağıdaki satırın açıklamasını kaldırın:

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

Şimdi XML belgelerini etkinleştirin. Çözüm Gezgini, projeye sağ tıklayın ve **Özellikler**' i seçin. **Yapı** sayfasını seçin.

![](creating-api-help-pages/_static/image6.png)

**Çıkış**' ın altında, **XML belge dosyasını**denetleyin. Düzenleme kutusuna "App\_Data/XmlDocument. xml" yazın.

![](creating-api-help-pages/_static/image7.png)

Daha sonra,/Controllers/valuescontroller.exe. csv dosyasında tanımlanan `ValuesController` API denetleyicisi için kodu açın. Denetleyici yöntemlerine bazı belge açıklamalarını ekleyin. Örneğin:

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> İpucu: giriş işaretini yöntemin üzerindeki satıra konumlandırır ve üç eğik çizgi yazarsanız, Visual Studio otomatik olarak XML öğelerini ekler. Daha sonra boşlukları doldurabilirsiniz.

Şimdi uygulamayı yeniden derleyin ve çalıştırın ve yardım sayfalarına gidin. Belge dizeleri API tablosunda görünmelidir.

![](creating-api-help-pages/_static/image8.png)

Yardım sayfası, XML dosyasındaki dizeleri çalışma zamanında okur. (Uygulamayı dağıtırken, XML dosyasını dağıttığınızdan emin olun.)

## <a name="under-the-hood"></a>Üzerinde

Yardım sayfaları, Web API çerçevesinin bir parçası olan **Apiexplorer** sınıfının üzerine kurulmuştur. **Apiexplorer** sınıfı, yardım sayfası oluşturmak için ham malzeme sağlar. Her API için **Apiexplorer** , API 'yi açıklayan bir **apidescription** içerir. Bu amaçla, bir "API" HTTP yönteminin ve göreli URI 'nin birleşimi olarak tanımlanmıştır. Örneğin, bazı farklı API 'Ler şunlardır:

- /Api/Products al
- /Api/Products/{ID} Al
- GÖNDERI/api/Products

Bir denetleyici eylemi birden çok HTTP yöntemini destekliyorsa, **Apiexplorer** her bir yöntemi ayrı bir API olarak değerlendirir.

**Apiexplorer**'DAN bir API 'yi gizlemek için, eyleme **Apiexplorersettings** özniteliğini ekleyin ve *ıgnoreapı* değerini doğru olarak ayarlayın.

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

Denetleyicinin tamamını hariç tutmak için bu özniteliği denetleyiciye de ekleyebilirsiniz.

ApiExplorer sınıfı, **ıbelgelertationprovider** arabiriminden belge dizelerini alır. Daha önce gördüğünüz gibi yardım sayfaları kitaplığı, XML belge dizelerinden belgeler alan bir **ıbelgelertationprovider** sağlar. Kod/Areas/helppage/xmlbelgetationprovider.exe konumunda bulunur. Kendi **ıbelgeleribelgelerinizi**yazarak başka bir kaynaktan belge alabilirsiniz. Bunu yapmak için, **Helppageconfigurationextensions** Içinde tanımlanan **Setbelgetationprovider** uzantı yöntemini çağırın.

**Apiexplorer** , her API için belge dizelerini almak üzere otomatik olarak **ıbelgelertationprovider** arabirimine çağırır. Bunları **Apidescription** ve **apiparameterdescription** nesnelerinin **documentation** özelliğinde depolar.

## <a name="next-steps"></a>Sonraki Adımlar

Burada gösterilen yardım sayfalarıyla sınırlı değilsiniz. Aslında, **Apiexplorer** yardım sayfaları oluşturmak için sınırlı değildir. Yao Huang Lin, daha fazla bilgi edinmek için harika blog gönderileri yazmıştır:

- [ASP.NET Web API 'SI yardım sayfasına basit bir test Istemcisi ekleme](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [ASP.NET Web API Yardım sayfası, şirket içinde barındırılan hizmetler üzerinde çalışır hale getirme](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [ASP.NET Web API 'SI için tasarım zamanı oluşturma Yardım sayfası (veya istemcisi)](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [Gelişmiş yardım sayfası özelleştirmeleri](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)
