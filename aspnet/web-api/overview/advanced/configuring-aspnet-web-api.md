---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: ASP.NET Web API 2-ASP.NET 4. x yapılandırma
author: MikeWasson
description: "ASP.NET 4. x için ASP.NET Web API 2 ' yi yapılandırın: ayarları, ASP.NET 4. x barındırma, OWıN Self-hosting, küresel hizmetler ve denetleyici öncesi yapılandırma."
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557724"
---
# <a name="configuring-aspnet-web-api-2"></a>ASP.NET Web API 2 yapılandırılıyor

, [Mike te son](https://github.com/MikeWasson)

Bu konu, ASP.NET Web API 'sinin nasıl yapılandırılacağını açıklamaktadır.

- [Yapılandırma ayarları](#settings)
- [ASP.NET Hosting ile Web API 'sini yapılandırma](#webhost)
- [Web API 'sini OWıN Self-hosting ile yapılandırma](#selfhost)
- [Küresel Web API hizmetleri](#services)
- [Denetleyici başına yapılandırma](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>Yapılandırma ayarları

Web API yapılandırma ayarları, [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) sınıfında tanımlanmıştır.

| Üye | Açıklama |
| --- | --- |
| **DependencyResolver** | Denetleyiciler için bağımlılık eklenmesine izin vermez. Bkz. [Web API bağımlılığı çözümleyici 'Yi kullanma](dependency-injection.md). |
| **Filtreler** | Eylem filtreleri. |
| **Biçimlendiricileri** | [Medya türü formatlayıcıları](../formats-and-model-binding/media-formatters.md). |
| **Includeerrordetailpolicy** | Sunucunun HTTP yanıt iletilerinde özel durum iletileri ve yığın izlemeleri gibi hata ayrıntılarını içerip içermediğini belirtir. Bkz. [ıncludeerrordetailpolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)). |
| **İzer** | **HttpConfiguration**'ın nihai başlatmasını gerçekleştiren bir işlev. |
| **MessageHandlers** | [Http ileti işleyicileri](http-message-handlers.md). |
| **ParameterBindingRules** | Denetleyici eylemleriyle ilgili parametreleri bağlama kuralları koleksiyonu. |
| **Özellikler** | Genel bir özellik paketi. |
| **Rotalar** | Yolların koleksiyonu. Bkz. [ASP.NET Web API 'de yönlendirme](../web-api-routing-and-actions/routing-in-aspnet-web-api.md). |
| **Hizmetler** | Hizmet koleksiyonu. Bkz. [Hizmetler](#services). |

## <a name="prerequisites"></a>Önkoşullar

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional veya Enterprise Edition.

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>ASP.NET Hosting ile Web API 'sini yapılandırma

Bir ASP.NET uygulamasında, **application\_start** yönteminde [Globalconfiguration. configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) ' ı çağırarak Web API 'sini yapılandırın. **Configure** yöntemi, **HttpConfiguration**türünde tek bir parametreye sahip bir temsilci alır. Temsilcinin içindeki tüm yapılandırmanızı gerçekleştirin.

Anonim bir temsilci kullanarak bir örnek aşağıda verilmiştir:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

Visual Studio 2017 ' de, **yeni ASP.NET proje** iletişim kutusunda "Web API 'si" seçeneğini belirlerseniz, "ASP.NET Web uygulaması" proje şablonu otomatik olarak yapılandırma kodunu ayarlar.

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

Proje şablonu, uygulama\_başlangıç klasörü içinde WebApiConfig.cs adlı bir dosya oluşturur. Bu kod dosyası, Web API yapılandırma kodunuzu yerleştirmeniz gereken temsilciyi tanımlar.

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

Proje şablonu, **uygulamayı\_Başlat**'dan çağıran kodu de ekler.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>Web API 'sini OWıN Self-hosting ile yapılandırma

OWIN ile kendi kendini barındırıyorsanız, yeni bir **HttpConfiguration** örneği oluşturun. Bu örnekte herhangi bir yapılandırma gerçekleştirin ve ardından örneği **Owin. UseWebApi** uzantı yöntemine geçirin.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

Öğreticide, [self-Host ASP.NET Web API 2 IÇIN OWIN kullanımı](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) tam adımları gösterir.

<a id="services"></a>
## <a name="global-web-api-services"></a>Küresel Web API hizmetleri

**HttpConfiguration. Services** koleksiyonu, Web API 'sinin denetleyici seçimi ve içerik anlaşması gibi çeşitli görevleri gerçekleştirmek için kullandığı küresel hizmetler kümesini içerir.

> [!NOTE]
> **Hizmetler** koleksiyonu, hizmet bulma veya bağımlılık ekleme için genel amaçlı bir mekanizma değildir. Yalnızca Web API çerçevesi tarafından bilinen hizmet türlerini depolar.

**Hizmetler** koleksiyonu varsayılan bir hizmet kümesiyle başlatılır ve kendi özel uygulamalarınızı sağlayabilirsiniz. Bazı hizmetler birden çok örneği destekler, diğerleri ise yalnızca bir örneğe sahip olabilir. (Ancak, denetleyici düzeyinde hizmetler de sağlayabilirsiniz; bkz. [Denetleyici başına yapılandırma](#percontrollerconfig).

Tek örnekli hizmetler

| Hizmet | Açıklama |
| --- | --- |
| **Iactionvalueciltçi** | Bir parametre için bir bağlama alır. |
| **IApiExplorer** | Uygulamanın açığa çıkarılan API 'lerin açıklamalarını alır. Bkz. [Web API 'si Için yardım sayfası oluşturma](../getting-started-with-aspnet-web-api/creating-api-help-pages.md). |
| **Ibirleştiricliesresolver** | Uygulama için derlemelerin bir listesini alır. Bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **Ibodymodelvalidator** | Bir medya türü biçimlendirici tarafından istek gövdesinden okunan modeli doğrular. |
| **Iditentnegotiator** | İçerik anlaşmasını gerçekleştirir. |
| **Ibelgetationprovider** | API 'Ler için belgeler sağlar. Varsayılan değer **null**. Bkz. [Web API 'si Için yardım sayfası oluşturma](../getting-started-with-aspnet-web-api/creating-api-help-pages.md). |
| **Ihostbufferpolicyselector** | Konağın HTTP ileti varlık gövdelerini arabelleğe kullanıp kullanmayacağını belirtir. |
| **Ihttpactionınvoker** | Bir denetleyici eylemi çağırır. Bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **Ihttpactionselector** | Bir denetleyici eylemi seçer. Bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **Ihttpcontrolleretkinleştirici** | Denetleyiciyi etkinleştirir. Bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **IHttpControllerSelector** | Bir denetleyici seçer. Bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **Ihttpcontrollertyperesolver** | Uygulamadaki Web API denetleyicisi türlerinin bir listesini sağlar. Bkz. [Yönlendirme ve eylem seçimi](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **Istracemanager** | İzleme çerçevesini başlatır. Bkz. [ASP.NET Web API 'de izleme](../testing-and-debugging/tracing-in-aspnet-web-api.md). |
| **Istracewriter** | Bir izleme yazıcısı sağlar. Varsayılan değer "Hayır-op" izleme yazdır. Bkz. [ASP.NET Web API 'de izleme](../testing-and-debugging/tracing-in-aspnet-web-api.md). |
| **Imodelvalidatorcache** | Model Doğrulayıcıları için bir önbellek sağlar. |

Birden çok örnekli hizmetler

|                 Hizmet                 |                                                                                                              Açıklama                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           Bir denetleyici eylemi için filtrelerin listesini döndürür.                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                Verilen tür için bir model Bağlayıcısı döndürür.                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     Bir model için meta veriler sağlar.                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   Bir model için doğrulayıcı sağlar.                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | Bir değer sağlayıcısı oluşturur. Daha fazla bilgi için bkz. Mike Cepin blog gönderisi, [WebAPI 'de özel değer sağlayıcısı oluşturma](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) |

Çok örnekli bir hizmete özel bir uygulama eklemek için, **Hizmetler** koleksiyonuna **Ekle** veya **Ekle** ' yi çağırın:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

Tek örnekli bir hizmeti özel bir uygulamayla değiştirmek için, **hizmet** koleksiyonundaki **değiştirme** 'yi çağırın:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>Denetleyici başına yapılandırma

Aşağıdaki ayarları denetleyiciye göre geçersiz kılabilirsiniz:

- Medya türü formatlayıcıları
- Parametre bağlama kuralları
- Hizmetler

Bunu yapmak için, **Icontrollerconfiguration** arabirimini uygulayan özel bir öznitelik tanımlayın. Ardından özniteliği denetleyiciye uygulayın.

Aşağıdaki örnek, varsayılan medya türü formatlayıcıları özel bir biçimlendirici ile değiştirilir.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

**Icontrollerconfiguration. Initialize** yöntemi iki parametre alır:

- Bir **Httpcontrollersettings** nesnesi
- Bir **Httpcontrollerdescriptor** nesnesi

**Httpcontrollerdescriptor** , denetleyicinin bir açıklamasını içerir ve bu, bilgilendirici amaçlar için inceleyebilirsiniz (iki denetleyiciyi ayırt etmek için deyin).

Denetleyiciyi yapılandırmak için **Httpcontrollersettings** nesnesini kullanın. Bu nesne, denetleyiciye göre geçersiz kılabileceğiniz yapılandırma parametrelerinin alt kümesini içerir. Varsayılan olarak, genel **HttpConfiguration** nesnesi olarak değiştirmezsiniz.
