---
uid: web-api/samples-list
title: Web API örnekleri listesi-ASP.NET 4. x
author: rick-anderson
description: ASP.NET 4. x için ASP.NET Web API örnekleri listesi
ms.author: riande
ms.date: 09/18/2012
ms.custom: seoapril2019
ms.assetid: 8cbd9d7f-7027-4390-b098-cb81a63ecd6f
msc.legacyurl: /web-api/samples-list
msc.type: content
ms.openlocfilehash: 24368fc80e7fc3c840f1f1f9accf13fa15a06c1b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598464"
---
# <a name="web-api-samples-list"></a>Web API Örnekleri Listesi

## <a name="httpclient-samples"></a>HttpClient örnekleri

**Bing çeviri örnek** | [vs 2012 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/BingTranslateSample)

**HttpClient** sınıfı kullanılarak [Microsoft Translator hizmetinin](https://msdn.microsoft.com/library/ff512419.aspx) nasıl çağrılacağını gösterir. Microsoft Translator Service API 'SI, uygulamanın her bir istek için Azure belirteç sunucusuna bir istek göndererek aldığı bir OAuth belirteci gerektirir. Belirteç sunucusundan elde edilen sonuç, çeviri hizmetine gönderilen istek içine beslenir. Bu örneği çalıştırmadan önce, [Azure Marketi 'nden bir uygulama anahtarı](https://msdn.microsoft.com/library/hh454950.aspx) edinmeniz ve AccessTokenMessageHandler örnek sınıfındaki bilgileri doldurmanız gerekir.

**Google Maps örnek** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/downloading-a-google-map-to-local-file.aspx) | [vs 2012 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/GoogleMapsSample)

[Google Maps API](https://developers.google.com/maps/)'den Redmond, WA haritasını Indirmek Için **HttpClient** kullanır, yerel bir dosya olarak kaydeder ve varsayılan görüntü görüntüleyicisini açar.

**Twitter Istemci örneği** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/extending-httpclient-with-oauth-to-access-twitter.aspx) | [vs 2012 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/TwitterSample)

**HttpClient**kullanarak basit bir Twitter istemcisinin nasıl yazılacağını gösterir. Örnek, OAuth kimlik doğrulama bilgilerini giden **HttpRequestMessage**dosyasına eklemek Için bir **HttpMessageHandler** kullanır. Twitter 'dan elde edilen sonuç, JSON.NET kullanılarak okundu. Bu örneği çalıştırmadan önce [Twitter 'dan bir uygulama anahtarı](https://dev.twitter.com/)edinmeniz ve OAuthMessageHandler örnek sınıfındaki bilgileri doldurmanız gerekir.

**Dünya Bankası örnek** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/02/16/httpclient-is-here.aspx) | [vs 2010 Kaynak](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net40) | [vs 2012 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/HttpClient/WorldBankSample/Net45)

JSON.NET kullanarak Dünya Bankası veri sitesinden verilerin nasıl alınacağını gösterir.

## <a name="web-api-samples"></a>Web API örnekleri

**ASP.NET Web API 'si Ile çalışmaya** başlama | [vs 2012 kaynağı](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)

HTTP GET isteklerini destekleyen temel bir Web API 'sinin nasıl oluşturulacağını gösterir. [İlk ASP.NET Web API 'nizi](overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)öğreticinin kaynak kodunu içerir.

**ASP.NET Web API JavaScript senaryoları – açıklamalar** | [vs 2012 kaynağı](https://code.msdn.microsoft.com/ASPNET-Web-API-JavaScript-d0d64dd7)

Tarayıcı istemcilerini destekleyen ve jQuery kullanılarak kolayca çağrılabilecek Web API 'Leri oluşturmak için ASP.NET Web API 'sini nasıl kullanacağınızı gösterir.

**Ilgili kişi yöneticisi** | [vs 2010 kaynağı](https://code.msdn.microsoft.com/Contact-Manager-Web-API-0e8e373d)

Bu örnek, basit bir Contact Manager uygulaması oluşturmak için ASP.NET Web API 'sini kullanır. Uygulama, bir ASP.NET MVC uygulaması tarafından kullanılan bir Contact Manager Web API 'sinden ve bir kişi listesini göstermek ve yönetmek için bir Windows Phone uygulaması içerir.

**Toplu Işleme örnek** | [ayrıntılı açıklama](http://trocolate.wordpress.com/2012/07/19/mitigate-issue-260-in-batching-scenario/) | [vs 2012 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/BatchSample)

ASP.NET içinde HTTP toplu işleme nasıl uygulanacağını gösterir. Toplu işlem, birden çok HTTP isteğini tek bir MIME çok parçalı varlık gövdesinde yerleştirmekten oluşur. Bu, daha sonra sunucuya bir HTTP POST olarak gönderilir. İstekler ayrı ayrı işlenir ve yanıtlar istemciye döndürülen başka bir MIME çok parçalı varlık gövdesine konur.

**Içerik denetleyicisi örneği** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/02/24/async-actions-in-asp-net-web-api.aspx) | [vs 2010 Kaynak](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net40) | [vs 2012 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/ContentControllerSample/Net45)

Akışlar kullanılarak istek ve yanıt varlıklarının zaman uyumsuz olarak nasıl okunacağını ve yazılacağını gösterir. Örnek denetleyicinin iki eylemi vardır: istek varlığı gövdesini zaman uyumsuz olarak okuyan bir PUT eylemi ve yerel dosyanın içeriğini döndüren bir GET eylemi.

**Özel derleme çözümleyici örnek** | [vs 2012 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomAssemblyResolverSample)

Dinamik olarak yüklenen bir kitaplık derlemesinden denetleyici bulmayı desteklemek için ASP.NET Web API 'sinin nasıl değiştirileceğini gösterir. Örnek, varsayılan uygulamayı çağıran ve ardından Kitaplık derlemesini varsayılan sonuçlara ekleyen özel bir **ıcompcompesresolver** uygular.

**Özel medya türü biçimlendirici örnek** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/04/23/using-cookies-with-asp-net-web-api.aspx) | [vs 2010 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomMediaTypeFormatterSample)

**Bufferedmediatypeformatter** temel sınıfını kullanarak özel medya türü biçimlendirici oluşturmayı gösterir. Bu temel sınıf, öncelikle zaman uyumlu okuma ve yazma işlemleri kullanan formatlayıcılar için tasarlanmıştır. Örnek, medya türü biçimlendirici göstermesinin yanı sıra, uygulamanız için **HttpConfiguration** 'ın bir parçası olarak kaydederek nasıl devralınacağını gösterir. Genellikle zaman uyumsuz okuma ve yazma işlemleri kullanan formatlayıcılar için **MediaTypeFormatter** temel sınıfını da kullanmanın mümkün olduğunu unutmayın.

**Özel parametre bağlama örneği** | [ayrıntılı açıklama](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx) | [vs 2010 kaynağı](https://github.com/aspnet/samples/blob/master/samples/aspnet/WebApi/CustomParameterBinding)

Bir istekten gelen bilgilerin eylem parametrelerine nasıl bağlandığını belirleyen işlem olan parametre bağlama işleminin nasıl özelleştirileceğini gösterir. Bu örnekte, ana denetleyicinin dört eylemi vardır:

1. BindPrincipal bir HTTP GET iletisinden değil, özel genel sorumlu öğesinden bir IPrincipal parametresinin nasıl bağlanacağını gösterir;
2. BindCustomComplexTypeFromUriOrBody, ileti gövdesinden veya bir HTTP POST iletisinin istek URI 'sinden gelen karmaşık tür bir parametre bağlamayı gösterir;
3. BindCustomComplexTypeFromUriWithRenamedProperty shows how to bind a complex-type parameter with a renamed property which comes from the request URI of an HTTP POST message;
4. PostMultipleParametersFromBody, bir POST iletisi için gövdeden birden çok parametre bağlamayı gösterir;

**Karşıya dosya yükleme örneği** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/03/01/file-upload-and-asp-net-web-api.aspx) | [vs 2012 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/FileUploadSample)

MIME çok parçalı dosya yükleme kullanılarak bir **Apicontroller** 'e dosya yüklemeyi ve **ProgressNotificationHandler**kullanarak **HttpClient** ile ilerleme bildirimleri ayarlamayı gösterir. Denetleyici bir HTML dosyasının karşıya yükleme içeriğini zaman uyumsuz olarak okur ve bir veya daha fazla gövde parçasını yerel bir dosyaya yazar. Yanıt, karşıya yüklenen dosya (veya dosyalar) hakkında bilgiler içerir.

**Azure Blob Depolama örneğine dosya yükleme** | [ayrıntılı açıklama](https://blogs.msdn.com/b/yaohuang1/archive/2012/07/02/asp-net-web-api-and-azure-blob-storage.aspx) | [vs 2012 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/AzureBlobsFileUploadSample)

Bu örnek, dosya yükleme örneğine benzerdir, ancak karşıya yüklenen dosyaları yerel diske kaydetmek yerine, [.net Için Microsoft Azure SDK 'sını](https://www.windowsazure.com/develop/net/)kullanarak dosyaları zaman uyumsuz olarak [Azure Blob deposuna](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs) yükler. Ayrıca, şu anda bir [Azure Blob depolama kapsayıcısında](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)bulunan Blobları listelemek için bir mekanizma sağlar. Azure SDK ile birlikte gelen **Azure Storage öykünücüsüne** karşı çalışan örneği deneyebilirsiniz. Bir [Azure depolama hesabınız](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs)varsa gerçek depolama hizmeti ile de çalıştırabilirsiniz.

**Http Ileti Işleyicisi ardışık düzen örneği** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/08/07/httpclient-httpclienthandler-and-httpwebrequesthandler.aspx) | [vs 2010 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/HttpMessageHandlerPipelineSample)

Hem istemci (**HttpClient**) hem de sunucu (ASP.NET Web API) üzerinde **HttpMessageHandler** örneklerinin nasıl yapılacağını gösterir. Örnekte, aynı işleyici hem istemci hem de sunucu üzerinde kullanılır. Aynı işleyicinin her iki yerde de çalışması nadir olsa da, nesne modeli istemci ve sunucu tarafında aynı olur.

**JSON karşıya yükleme örnek** | [vs 2012 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/JsonUploadSample)

Bir **Apicontroller**'a JSON yükleme ve yükleme işleminin nasıl yapılacağını gösterir. Örnek, en az bir **Apicontroller** kullanır ve **HttpClient**kullanarak ona erişir.

**Karma örnek** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/03/03/async-mashups-using-asp-net-web-api.aspx) | [vs 2012 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MashupSample)

Bir **Apicontroller** eylemi içinden zaman uyumsuz olarak birden çok uzak siteye nasıl erişekullanacağınızı gösterir. Eyleme her ulaşıldığında istekler zaman uyumsuz olarak gerçekleştirilir, böylece hiçbir iş parçacığı engellenmez.

**Bellek Izleme örneği** | [ayrıntılı açıklama](https://blogs.msdn.com/b/roncain/archive/2012/04/12/tracing-in-asp-net-web-api.aspx) | [vs 2010 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MemoryTracingSample)

Bu örnek proje, ASP.NET Web API uygulamalarına özel bir bellek içi izleme yazıcısı yükleyecek bir NuGet paketi oluşturur.

**MongoDB örnek** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/02/19/using-web-api-with-mongodb.aspx) | [vs 2012 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/MongoSample)

Bir depo deseninin kullanıldığı bir **Apicontroller**Için MongoDB 'nin kalıcı depolama olarak nasıl kullanılacağını gösterir.

**Yanıt gövdesi Işlemcisi örnek** | [vs 2012 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ResponseEntityProcessorSample)

Bir yanıt varlığının (yani, bir HTTP yanıt gövdesi) istemciye iletilmeden önce yerel bir dosyaya nasıl kopyalanacağını ve bu dosyada zaman uyumsuz olarak ek işlem gerçekleştirmeyi gösterir. Örnek, yanıt varlığını her ikisi de normal ve yerel bir dosyaya yazan bir **HttpMessageHandler** uygular.

**XDocument örnek** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/02/17/push-and-pull-streams-using-httpclient.aspx) | [vs 2012 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/UploadXDocumentSample) yükle

**Pushstreamcontent** ve **HttpClient**kullanarak bir XDocument 'ı bir **apicontroller** 'a yükleme işleminin nasıl yapılacağını gösterir.

**Doğrulama örneği** | [vs 2010 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/ValidationSample)

HTTP isteğinin içeriğini doğrulamak için ASP.NET WebAPI içindeki modellerinizde doğrulama özniteliklerini nasıl kullanabileceğinizi gösterir. Özellikleri gerektiğinde nasıl işaretleyeceğinizi, modelinize açıklama eklemek için hem çerçeve tanımlı hem de özel doğrulama özniteliklerinin nasıl kullanılacağını ve geçersiz model durumları için hata yanıtlarının nasıl döndürülmeyeceğini gösterir.

**Web formu örneği** | [ayrıntılı açıklama](https://blogs.msdn.com/b/henrikn/archive/2012/02/23/using-asp-net-web-api-with-asp-net-web-forms.aspx) | [vs 2010 kaynağı](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/WebFormSample)

Web Forms projesine eklenen bir ApiController gösterir.

**[RestBugs örneği](https://github.com/howarddierking/RestBugs)**

RestBugs, hiper medya temelli bir sistem oluşturmak için ASP.NET Web API 'SI ve yeni HTTP Istemci kitaplığı 'nın nasıl kullanılacağını gösteren basit bir hata izleme uygulamasıdır. Örnek, ASP.NET Web API 'sini kullanarak hem istemci hem de sunucu uygulamalarını içerir. Sunucu, kaynak temsilleri oluşturmak için özel bir Razor biçimlendiricisi kullanır. Örnek ayrıca, istemcileri ve sunucuları ayırmak için hipermedya tasarımını kullanmanın sağladığı avantajları göstermek üzere bir Node. js sunucusu sağlar.
