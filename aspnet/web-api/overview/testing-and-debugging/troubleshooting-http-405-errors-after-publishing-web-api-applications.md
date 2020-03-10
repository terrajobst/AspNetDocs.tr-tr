---
uid: web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
title: Visual Studio 'da çalışan ve üretim IIS sunucusunda başarısız olan Web API2 uygulamalarının sorunlarını giderme
author: rmcmurray
description: Visual Studio 'da çalışan ve üretim IIS sunucusunda başarısız olan Web API2 uygulamalarının sorunlarını giderme
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 07ec7d37-023f-43ea-b471-60b08ce338f7
msc.legacyurl: /web-api/overview/testing-and-debugging/troubleshooting-http-405-errors-after-publishing-web-api-applications
msc.type: authoredcontent
ms.openlocfilehash: 1b47f1ade3619cfd010260352f6a96985ab3598b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555022"
---
# <a name="troubleshoot-web-api2-apps-that-work-in-visual-studio-and-fail-on-a-production-iis-server"></a>Visual Studio 'da çalışan ve üretim IIS sunucusunda başarısız olan Web API2 uygulamalarının sorunlarını giderme

> Bu belgede, bir üretim IIS sunucusuna dağıtılan Web API2 uygulamalarının nasıl giderileceği açıklanmaktadır. Ortak HTTP 405 ve 501 hatalarını ele alınmaktadır.
> 
> ## <a name="software-used-in-this-tutorial"></a>Bu öğreticide kullanılan yazılım
> 
> 
> - [Internet Information Services (IIS)](https://www.iis.net/) (sürüm 7 veya üzeri)
> - [Web API](../../index.md) 

Web API Apps genellikle birkaç HTTP fiillerini kullanır: GET, POST, PUT, DELETE ve bazen PATCH. Bu şekilde, geliştiriciler, Visual Studio 'da veya bir geliştirme sunucusunda doğru şekilde çalışan bir Web API denetleyicisi olduğunda, bu fiillerin üretim IIS sunucusu üzerinde başka bir IIS modülü tarafından uygulandığı durumlara yol açabilir. üretim IIS sunucusuna dağıtıldığında bir HTTP 405 hatası döndürür.

## <a name="what-causes-http-405-errors"></a>HTTP 405 hatalarına neden olur?

HTTP 405 hatalarına nasıl sorun gidermeyi öğrenmekte olan ilk adım, bir HTTP 405 hatasının gerçekten ne anlama geldiğini anlamaktır. HTTP için birincil yöneten belge, HTTP 405 durum kodunu ***metodun Izin verilmeyen***şekilde tanımlayan [RFC 2616](http://www.ietf.org/rfc/rfc2616.txt)' dir ve bu durum kodunu, istek-satırında belirtilen yöntemin istek URI 'si tarafından tanımlanan kaynak için izin verilmeyen &quot;bir durum olarak açıklar. diğer bir deyişle&quot;, http fiiline bir HTTP istemcisinin istediği özel URL için izin verilmez.

Kısa bir inceleme olarak, RFC 2616, RFC 4918 ve RFC 5789 ' de tanımlanan en çok kullanılan HTTP yöntemlerinden birkaçı aşağıda verilmiştir:

| HTTP yöntemi | Açıklama |
| --- | --- |
| **GET** | Bu yöntem, bir URI 'den veri almak için kullanılır ve büyük olasılıkla en çok kullanılan HTTP yöntemidir. |
| **BAŞLı** | Bu yöntem GET yöntemine çok benzer, ancak gerçekte istek URI 'sinden veri almamaktır; yalnızca HTTP durumunu alır. |
| **POST** | Bu yöntem genellikle URI 'ye yeni veri göndermek için kullanılır; GÖNDERI genellikle form verileri göndermek için kullanılır. |
| **PUT** | Bu yöntem genellikle, URI 'ye ham veri göndermek için kullanılır; PUT, genellikle JSON veya XML verilerini Web API uygulamalarına göndermek için kullanılır. |
| **DELETE** | Bu yöntem, bir URI 'den verileri kaldırmak için kullanılır. |
| **Seçenekler** | Bu yöntem, genellikle bir URI için desteklenen HTTP yöntemlerinin listesini almak için kullanılır. |
| **TAŞıMA KOPYALA** | Bu iki yöntem WebDAV ile kullanılır ve kendi amacı kendi kendine açıklayıcıdır. |
| **MKCOL** | Bu yöntem, WebDAV ile kullanılır ve belirtilen URI 'de bir koleksiyon (ör. bir dizin) oluşturmak için kullanılır. |
| **PROPFIND PROPPATCH** | Bu iki yöntem WebDAV ile kullanılır ve bir URI 'nin özelliklerini sorgulamak veya ayarlamak için kullanılır. |
| **KILIT KILIDINI KILITLE** | Bu iki yöntem WebDAV ile kullanılır ve yazma sırasında istek URI 'SI tarafından tanımlanan kaynağı kilitlemek/kilidini açmak için kullanılır. |
| **DÜZELTMESI** | Bu yöntem, var olan bir HTTP kaynağını değiştirmek için kullanılır. |

Bu HTTP yöntemlerinden biri sunucuda kullanılmak üzere yapılandırıldığında, sunucu, istek için uygun olan HTTP durumu ve diğer verilerle yanıt verir. (Örneğin, bir GET yöntemi bir HTTP 200 ***ok*** yanıtı alabılır ve put YÖNTEMI bir http 201 ***oluşturma*** yanıtı alabilir.)

HTTP yöntemi sunucuda kullanılmak üzere yapılandırılmamışsa sunucu, bir HTTP 501 ***uygulanmamış*** hatasıyla yanıt verir.

Ancak, bir HTTP yöntemi sunucuda kullanılmak üzere yapılandırıldığında, ancak belirli bir URI için devre dışı bırakılmışsa, sunucu bir HTTP 405 ***yöntemi Izin verilmeyen*** hatasıyla yanıt verir.

## <a name="example-http-405-error"></a>Örnek HTTP 405 hatası

Aşağıdaki örnek HTTP isteği ve yanıtı, bir HTTP istemcisinin Web sunucusundaki bir Web API uygulamasına değer koymaya çalıştığı ve sunucu PUT yöntemine izin verilmediğini bildiren bir HTTP hatası döndüren bir durumu gösterir:

HTTP Isteği:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample1.cmd)]

HTTP yanıtı:

[!code-console[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample2.cmd)]

Bu örnekte, HTTP istemcisi Web sunucusundaki bir Web API uygulaması URL 'sine geçerli bir JSON isteği gönderdi, ancak sunucu, PUT yöntemine URL için izin verilmediğini belirten bir HTTP 405 hata iletisi döndürdü. Buna karşılık, istek URI 'SI Web API uygulaması için bir yol ile eşleşmezse, sunucu bir HTTP 404 ***bulunamadı*** hatası döndürür.

## <a name="resolve-http-405-errors"></a>HTTP 405 hatalarını çözümleme

Belirli bir HTTP fiiline izin verilmemesine neden olan bazı nedenler vardır, ancak IIS 'de bu hatanın önde gelen nedeni olan bir birincil senaryo vardır: aynı fiil/Yöntem için birden çok işleyici tanımlanmıştır ve işleyicilerden biri beklenen İşleyicinin isteği işlemesini engelliyor. Açıklama yoluyla IIS,, isteği işlemek için ilk eşleşen yol, fiil, kaynak, vb. bileşiminin, *ApplicationHost. config* ve *Web. config* dosyalarındaki Order Handler girişlerine göre ilk olarak işleyicileri işler.

Aşağıdaki örnek, bir Web API uygulamasına veri göndermek için PUT yöntemi kullanılırken HTTP 405 hatası döndüren bir IIS sunucusu için bir *ApplicationHost. config* dosyasından alıntıdır. Bu alıntıda, bazı HTTP işleyicileri tanımlanmıştır ve her işleyicinin yapılandırıldığı farklı bir HTTP yöntemi kümesi vardır; listedeki son giriş, diğer işleyiciler bir chanc olduktan sonra kullanılan varsayılan işleyici olan statik içerik işleyicisidir. e-isteği incelemek için:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample3.xml)]

Yukarıdaki örnekte, WebDAV işleyicisi ve ASP.NET için uzantı-daha seyrek URL Işleyicisi (Web API 'SI için kullanılır), HTTP yöntemlerinin ayrı listeleri için açıkça tanımlanmıştır. ISAPI DLL işleyicisinin tüm HTTP yöntemleri için yapılandırıldığını, ancak bu yapılandırmanın hataya neden olamayacağını unutmayın. Ancak, bunun gibi yapılandırma ayarlarının HTTP 405 hatalarıyla ilgili sorunları giderirken dikkate almanız gerekir.

Yukarıdaki örnekte, ISAPI DLL işleyicisi sorun değildi; Aslında, sorun IIS sunucusu için *ApplicationHost. config* dosyasında tanımlı değildi-sorun, Web API uygulaması Visual Studio 'da oluşturulduğunda *Web. config* dosyasında yapılan bir girdinin kaynaklanmasından kaynaklandı. Uygulamanın *Web. config* dosyasındaki aşağıdaki alıntıda sorunun konumunu gösterir:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample4.xml)]

Bu alıntıda, ASP.NET için uzantı-daha az URL Işleyicisi, Web API uygulamasıyla kullanılacak ek HTTP yöntemlerini içerecek şekilde yeniden tanımlanır. Ancak, WebDAV işleyicisi için benzer bir HTTP yöntemleri kümesi tanımlandığından, bir çakışma oluşur. Bu özel durumda, WebDAV işleyicisi, Web API uygulamasını içeren Web sitesi için WebDAV devre dışı bırakılmış olsa bile IIS tarafından tanımlanır ve yüklenir. HTTP PUT isteğinin işlenmesi sırasında, IIS, PUT fiili için tanımlandığından WebDAV modülünü çağırır. WebDAV modülü çağrıldığında, yapılandırmasını denetler ve devre dışı olduğunu görür, bu nedenle bir WebDAV isteğine benzer bir istek için bir HTTP 405 ***yöntemi Izin verilmeyen*** bir hata döndürür. Bu sorunu çözmek için, Web API uygulamanızın tanımlandığı Web sitesinin HTTP modülleri listesinden WebDAV 'yi kaldırmanız gerekir. Aşağıdaki örnek, şöyle görünebileceğini gösterir:

[!code-xml[Main](troubleshooting-http-405-errors-after-publishing-web-api-applications/samples/sample5.xml)]

Bu senaryo, genellikle bir uygulama geliştirme ortamından bir IIS üretim ortamına yayımlandıktan sonra ve bu durum, işleyiciler/modüller listesi geliştirme ve üretim ortamlarınız arasında farklılık yaptığından oluşur. Örneğin, bir Web API uygulaması geliştirmek için Visual Studio 2012 veya üstünü kullanıyorsanız, test için varsayılan Web sunucusudur IIS Express. Bu geliştirme Web sunucusu, bir sunucu ürününde sunulan tam IIS işlevselliğinin ölçeği genişletilmiş bir sürümüdür ve bu geliştirme Web sunucusu geliştirme senaryoları için eklenen birkaç değişiklik içerir. Örneğin, WebDAV modülü genellikle IIS 'nin tam sürümünü çalıştıran bir üretim Web sunucusuna yüklenir, ancak kullanımda olmayabilir. IIS 'nin geliştirme sürümü (IIS Express), WebDAV modülünü yüklerse, ancak WebDAV modülünün girişleri bilinçli olarak önceden belirlenir, bu nedenle IIS Express yapılandırmanızı özellikle değiştirmediğiniz müddetçe WebDAV modülü IIS Express hiçbir şekilde yüklenmez IIS Express yüklemenize WebDAV işlevselliği ekleme ayarları. Sonuç olarak, Web uygulamanız geliştirme bilgisayarınızda düzgün çalışabilir, ancak Web API uygulamanızı üretim IIS Web sunucunuza yayımladığınızda HTTP 405 hatalarıyla karşılaşabilirsiniz.

## <a name="http-501-errors"></a>HTTP 501 hataları

* Belirli işlevlerin sunucuda uygulanmadığını gösterir.
* Genellikle IIS ayarlarınızda tanımlanmış, HTTP isteğiyle eşleşen bir işleyici olmadığı anlamına gelir:
  * Büyük olasılıkla IIS 'de bir şeyin doğru yüklenmediğini belirtiyor
  * IIS ayarlarınızı, belirli HTTP yöntemini destekleyen hiçbir işleyici tanımlanmadığı şekilde değiştirdi.

Bu sorunu çözmek için, karşılık gelen bir modüle veya işleyici tanımına sahip olmayan bir HTTP yöntemini kullanmaya çalışan herhangi bir uygulamayı yeniden yüklemeniz gerekir.

## <a name="summary"></a>Özet

HTTP 405 hataları, bir HTTP yöntemine istenen URL için bir Web sunucusu tarafından izin verilmediği zaman neden olur. Bu durum genellikle belirli bir fiil için belirli bir işleyici tanımlandığında ve bu işleyici isteği işlemeyi düşündüğünüz işleyiciyi geçersiz kılıyorsa görülür.
