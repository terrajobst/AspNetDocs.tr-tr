---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: IIS Tümleşik ardışık düzeninde OWıN ara yazılımı | Microsoft Docs
author: Praburaj
description: Bu makalede, IIS Tümleşik ardışık düzeninde OWıN ara yazılım bileşenlerinin (OMCs) çalıştırılması ve bir OMC 'nin üzerinde çalıştığı işlem hattı olayının nasıl ayarlanacağı gösterilmektedir. Şunları yapmalısınız...
ms.author: riande
ms.date: 11/07/2013
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 7d157fb6bd9e2ae9b55af41ef06c1eb5e6310ce1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456718"
---
# <a name="owin-middleware-in-the-iis-integrated-pipeline"></a>IIS Tümleşik ardışık düzeninde OWıN ara yazılımı

tarafından [Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://twitter.com/RickAndMSFT)

> Bu makalede, IIS Tümleşik ardışık düzeninde OWıN ara yazılım bileşenlerinin (OMCs) çalıştırılması ve bir OMC 'nin üzerinde çalıştığı işlem hattı olayının nasıl ayarlanacağı gösterilmektedir. Bu öğreticiyi okumadan önce proje Katana ve [Owın başlangıç sınıfı algılamasına](owin-startup-class-detection.md) [Ilişkin bir genel bakışı](an-overview-of-project-katana.md) gözden geçirmeniz gerekir. Bu öğretici, Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Chris No, Praburaj Thiagarajan ve Howard dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ) tarafından yazılmıştır.

[Owın](an-overview-of-project-katana.md) ara yazılım bileşenleri (OMCS) öncelikle sunucu belirsiz işlem hattında çalışacak şekilde tasarlansa da, IIS Tümleşik ardışık düzeninde bir OMC çalıştırmak mümkündür (**Klasik mod desteklenmez** ). Paket Yöneticisi konsolundan (PMC) aşağıdaki paketi yükleyerek IIS Tümleşik işlem hattında çalışan bir OMC yapılabilir:

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

Bu, henüz IIS ve System. Web dışında çalıştırılmayan tüm uygulama çerçevelerinin, var olan OWıN ara yazılım bileşenlerinden faydalanabileceği anlamına gelir. 

> [!NOTE]
> `Microsoft.Owin.Security.*` paketlerin tümü, Visual Studio 2013 yeni kimlik sistemiyle (örneğin: tanımlama bilgileri, Microsoft hesabı, Google, Facebook, Twitter, [taşıyıcı belirteci](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html), OAuth, yetkilendirme sunucusu, JWT, Azure Active Directory ve Active Directory Federasyon Hizmetleri), OMCS olarak yazılır ve hem şirket içinde hem de IIS tarafından barındırılan senaryolarda kullanılabilir.

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>IIS Tümleşik ardışık düzeninde OWıN ara yazılımı nasıl çalıştırılır

OWıN konsol uygulamaları için, [Başlangıç yapılandırması](owin-startup-class-detection.md) kullanılarak oluşturulan uygulama ardışık düzeni, bileşenlerin `IAppBuilder.Use` yöntemi kullanılarak eklendiği sıraya göre ayarlanır. Diğer bir deyişle, [Katana](an-overview-of-project-katana.md) çalışma zamanındaki owın ardışık düzeni, OMCS 'yi, `IAppBuilder.Use`kullanılarak kaydedildikleri sırada işler. IIS Tümleşik işlem hattında, istek ardışık düzeni, [BeginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx), [doğruıbota](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)gibi işlem hattı olaylarının önceden tanımlanmış bir kümesine abone olan [httpModules](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx) 'tan oluşur.

Bir OMC 'yi ASP.NET dünyasında bir [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx) ile karşılaştırdığımızda, BIR OMC 'nin doğru önceden tanımlanmış ardışık düzen olayına kayıtlı olması gerekir. Örneğin, bir istek işlem hattındaki [kimlik doğrulayan Terequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) aşamasına geldiğinde, HttpModule `MyModule` çağrılır:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

Bir OMC 'nin bu aynı olay tabanlı yürütme sıralamasına katılmasını sağlamak için, [Katana](an-overview-of-project-katana.md) çalışma zamanı kodu [başlangıç yapılandırmasını](owin-startup-class-detection.md) tarar ve her bir ara yazılım bileşeninin her birini tümleşik bir ardışık düzen olayına abone olur. Örneğin, aşağıdaki OMC ve kayıt kodu, ara yazılım bileşenlerinin varsayılan olay kaydını görmenizi sağlar. (Bir OWıN başlangıç sınıfı oluşturma hakkında daha ayrıntılı yönergeler için bkz. [Owın başlangıç sınıfı algılama](owin-startup-class-detection.md).)

1. Boş bir Web uygulaması projesi oluşturun ve **owin2**olarak adlandırın.
2. Paket Yöneticisi konsolundan (PMC), aşağıdaki komutu çalıştırın: 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. `OWIN Startup Class` ekleyin ve `Startup`adlandırın. Oluşturulan kodu aşağıdaki kodla değiştirin (değişiklikler vurgulanır):  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. Uygulamayı çalıştırmak için F5 'e basın.

Başlangıç yapılandırması üç ara yazılım bileşeni olan bir işlem hattını ayarlar, ilk iki, tanılama bilgilerini ve en son bir olay yanıt vermeyi (ve ayrıca tanılama bilgilerini görüntüler) görüntüler. `PrintCurrentIntegratedPipelineStage` yöntemi, bu ara yazılımın çağrıldığı tümleşik işlem hattı olayını ve bir iletiyi görüntüler. Çıkış pencereleri aşağıdakileri görüntüler:

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

Katana çalışma zamanı, OWıN ara yazılım bileşenlerinden her birini varsayılan olarak [Preexecuterequesthandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) ile EŞLEŞTIREREK IIS işlem hattı Event [PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)'a karşılık gelir.

## <a name="stage-markers"></a>Aşama Işaretçileri

`IAppBuilder UseStageMarker()` uzantısı yöntemini kullanarak, işlem hattının belirli aşamalarını yürütmek üzere OMCs 'yi işaretleyebilirsiniz. Belirli bir aşamada bir ara yazılım bileşenleri kümesi çalıştırmak için, kayıt sırasında ayarlanan son bileşenden hemen sonra bir aşama işareti ekleyin. İşlem hattının hangi aşamasında ara yazılım yürütebileceği ve sipariş bileşenlerinin çalışması gereken kurallar vardır (kurallar Öğreticinin ilerleyen kısımlarında açıklanmıştır). `UseStageMarker` yöntemini aşağıda gösterildiği gibi `Configuration` koduna ekleyin:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

`app.UseStageMarker(PipelineStage.Authenticate)` çağrısı, daha önce kaydedilen tüm ara yazılım bileşenlerini (Bu durumda, iki tanılama bileşenimizin) işlem hattının kimlik doğrulama aşamasında çalışacak şekilde yapılandırır. Son ara yazılım bileşeni (Tanılamayı ve isteklerin yanıt verdiğini gösterir) `ResolveCache` aşamada ( [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx) olayı) çalışır.

Uygulamayı çalıştırmak için F5 'e basın. Çıkış penceresinde aşağıdakiler gösterilir:

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>Aşama Işaretçisi kuralları

Owın ara yazılım bileşenleri (OMC), aşağıdaki OWIN ardışık düzen aşaması olaylarında çalışacak şekilde yapılandırılabilir:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. Varsayılan olarak, OMCs son olayda çalışır (`PreHandlerExecute`). İlk örnek kodumuz "PreExecuteRequestHandler" olarak görüntülendi.
2. Bir OMC 'yi daha önce çalıştırmak üzere kaydetmek için bir `app.UseStageMarker` yöntemini kullanabilirsiniz. Bu işlem, `PipelineStage` numaralandırmasında listelenen OWıN işlem hattının herhangi bir aşamasında.
3. OWıN ardışık düzeni ve IIS işlem hattı sıralanmıştır, bu nedenle `app.UseStageMarker` çağrıları sırayla olmalıdır. Olay işleyicisini, `app.UseStageMarker`için kaydedilen son olaydan önce gelen bir olaya ayarlayamazsınız. Örneğin, öğesini çağırdıktan *sonra* :

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   `Authenticate` veya `PostAuthenticate` geçirme `app.UseStageMarker` çağrılar kabul edilmez ve hiçbir özel durum oluşturulmaz. OMCs, varsayılan olarak `PreHandlerExecute`en son aşamada çalışır. Aşama işaretçileri, daha önce çalıştırılmasını sağlamak için kullanılır. Aşama işaretlerini sıra dışında belirtirseniz, önceki İşaretleyiciye yuvarlıyoruz. Diğer bir deyişle, aşama işaretleyicisi eklemek "Aşama X 'ten sonra Hayır" ifadesini ifade ediyor. OMC 'nin, OWıN ardışık düzeninde olduktan sonra, ilk aşama işaretçisi üzerinde çalışması.
4. `app.UseStageMarker` WINS için en erken çağrı aşaması. Örneğin, önceki örneğimizdeki `app.UseStageMarker` çağrılarının sırasını değiştirirseniz:

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   Çıkış penceresi görüntülenir: 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   OMCs, `AuthenticateRequest` aşamada çalışır, çünkü son OMC `Authenticate` olayına kaydedilir ve `Authenticate` olayı diğer tüm olayların önüne geçer.
