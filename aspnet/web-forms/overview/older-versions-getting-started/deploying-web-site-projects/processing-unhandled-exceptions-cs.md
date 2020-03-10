---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
title: Işlenmemiş özel durumlar işleniyorC#() | Microsoft Docs
author: rick-anderson
description: Üretimde bir Web uygulamasında bir çalışma zamanı hatası oluştuğunda, bir geliştiriciye bildirimde bulundurulmaları ve hatayı günlüğe kaydetmek için bir La...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 5bc1afd5-2484-4528-b158-ab218ba150e8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs
msc.type: authoredcontent
ms.openlocfilehash: 27d827238d944f86cd913d2b8ecd12729b99f391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629271"
---
# <a name="processing-unhandled-exceptions-c"></a>İşlenmemiş Özel Durumları İşleme (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Örnek kodu görüntüleme veya indirme](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/web-forms/overview/older-versions-getting-started/deploying-web-site-projects/processing-unhandled-exceptions-cs/samples) ([nasıl indirileceği](/aspnet/core/tutorials/index#how-to-download-a-sample))

> Üretimde bir Web uygulamasında bir çalışma zamanı hatası oluştuğunda, bir geliştiriciye bildirimde bulunduğunu ve daha sonraki bir zamanda tanılanabilir olması için hatayı günlüğe kaydetmek önemlidir. Bu öğreticide, ASP.NET çalışma zamanı hatalarını işleme ve işlenmeyen bir özel durum kabarcıkları ASP.NET çalışma zamanına kadar her seferinde özel kodun yürütülmesi için bir yol sunulmaktadır.

## <a name="introduction"></a>Giriş

Bir ASP.NET uygulamasında işlenmeyen bir özel durum oluştuğunda, `Error` olayı oluşturan ve uygun hata sayfasını görüntüleyen ASP.NET çalışma zamanına göre balon oluşturur. Üç farklı hata sayfası türü vardır: çalışma zamanı hatası sarı ölüm ekranı (YSOD); Özel durum ayrıntıları-SOD; ve özel hata sayfaları. [Önceki öğreticide](displaying-a-custom-error-page-cs.md) , uygulamayı uzak kullanıcılar için özel bir hata sayfası kullanacak şekilde yapılandırdık ve yerel olarak ziyaret eden kullanıcılar Için özel durum ayrıntıları YSOD.

Sitenin görünümü ve hissiyle eşleşen bir insan kullanımı kolay özel hata sayfasının kullanılması, varsayılan çalışma zamanı hatası olarak tercih edilir, ancak özel hata sayfası görüntülemek, kapsamlı bir hata işleme çözümünün yalnızca bir parçasıdır. Üretimde bir uygulamada hata oluştuğunda, özel durumun nedenini ortaya çıkarabilir ve adresleşmeleri için geliştiricilere hata bildirilmesi önemlidir. Ayrıca, hatanın daha sonraki bir noktada İncelenme ve tanılanabilir olması için hatanın ayrıntıları günlüğe kaydedilir.

Bu öğreticide, işlenmemiş bir özel durumun ayrıntılarına nasıl erişebileceğiniz ve bu sayede günlüğe kaydedilecek bir geliştirici gösterilir. Bunu izleyen iki öğretici, bir yapılandırma biraz sonra, geliştiricilerin çalışma zamanı hatalarını otomatik olarak bilgilendirmesini ve ayrıntılarını günlüğe kaydetmelerini sağlayacak hata günlüğü kitaplıklarını keşfedebilir.

> [!NOTE]
> Bu öğreticide incelenen bilgiler, işlenmemiş özel durumları benzersiz veya özelleştirilmiş bir şekilde işleyebilmeniz gerektiğinde faydalıdır. Yalnızca özel durumu günlüğe kaydetmek ve bir geliştiriciye bildirimde olması gereken durumlarda, bir hata günlüğü kitaplığı kullanmak, gidilecek yoldur. Sonraki iki öğretici, bu iki kitaplık için genel bir bakış sağlar.

## <a name="executing-code-when-theerrorevent-is-raised"></a>`Error`olayı oluşturulduğunda kodu yürütme

Olaylar, ilginç bir şeyin oluştuğunu belirten sinyal için bir mekanizma ve yanıt olarak kod yürütmek için başka bir nesne sağlar. Bir ASP.NET geliştiricisi olarak, olaylar açısından düşünmek üzere alışkın olduğunuz bir geliştirici. Ziyaretçi belirli bir düğmeye tıkladığında bazı kodları çalıştırmak istiyorsanız, bu düğmenin `Click` olayı için bir olay işleyicisi oluşturun ve kodunuzu buraya koyun. İşlenmeyen bir özel durum oluştuğunda ASP.NET çalışma zamanının [`Error` olayını](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx) harekete geçirdiğinden, hata ayrıntılarını günlüğe kaydetme kodunun olay işleyicisine gitmesini de izler. Ancak `Error` olayı için nasıl bir olay işleyicisi oluşturursunuz?

`Error` olay, bir isteğin ömrü boyunca HTTP işlem hattının belirli aşamalarında oluşturulan [`HttpApplication` sınıfındaki](https://msdn.microsoft.com/library/system.web.httpapplication.aspx) birçok olaydan biridir. Örneğin, `HttpApplication` sınıfın [`BeginRequest` olayı](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx) her isteğin başlangıcında tetiklenir; [`AuthenticateRequest` olayı](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) , bir güvenlik modülü istek sahibine tanımlamışsa tetiklenir. Bu `HttpApplication` olaylar, sayfa geliştiricisinin bir isteğin ömrü boyunca çeşitli noktalarda özel mantık yürütmesi için bir yol sunar.

`HttpApplication` olaylar için olay işleyicileri `Global.asax`adlı özel bir dosyaya yerleştirilebilir. Bu dosyayı Web sitenizde oluşturmak için, `Global.asax`adlı genel uygulama sınıfı şablonunu kullanarak Web sitenizin köküne yeni bir öğe ekleyin.

[![](processing-unhandled-exceptions-cs/_static/image2.png)](processing-unhandled-exceptions-cs/_static/image1.png)

**Şekil 1**: Web uygulamanıza `Global.asax` ekleme  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](processing-unhandled-exceptions-cs/_static/image3.png))

Visual Studio tarafından oluşturulan `Global.asax` dosyanın içeriği ve yapısı, bir Web uygulaması projesi (WAP) veya Web sitesi projesi (WSP) kullanıp kullanana kadar biraz farklılık gösterir. WAP ile `Global.asax` iki ayrı dosya olarak uygulanır-`Global.asax` ve `Global.asax.cs`. `Global.asax` dosyası hiçbir şey içermez, ancak `.cs` dosyasına başvuran bir `@Application` yönergesi; İlgilendiğiniz olay işleyicileri `Global.asax.cs` dosyasında tanımlanmıştır. WSPs için yalnızca tek bir dosya oluşturulur, `Global.asax`ve olay işleyicileri bir `<script runat="server">` bloğunda tanımlanmıştır.

Visual Studio 'nun genel uygulama sınıfı şablonu tarafından WAP 'da oluşturulan `Global.asax` dosyası, `HttpApplication` olayları `BeginRequest`, `AuthenticateRequest`ve `Error`için olay işleyicileri olan `Application_BeginRequest`, `Application_AuthenticateRequest`ve `Application_Error`adlı olay işleyicilerini içerir. `Application_Start`, `Session_Start`, `Application_End`ve `Session_End`adlı olay işleyicileri de vardır. Bu, yeni bir oturum başlatıldığında, uygulamanın ne zaman sona ereceğini ve bir oturumun ne zaman bittiğini, Web uygulaması başladığında harekete geçen olay işleyicileridir. Visual Studio tarafından bir WSP içinde oluşturulan `Global.asax` dosyası yalnızca `Application_Error`, `Application_Start`, `Session_Start`, `Application_End`ve `Session_End` olay işleyicilerini içerir.

> [!NOTE]
> ASP.NET uygulamasını dağıttığınızda, `Global.asax` dosyasını üretim ortamına kopyalamanız gerekir. WAP 'da oluşturulan `Global.asax.cs` dosyasının, bu kod projenin derlemesine derlendiğinden, üretime kopyalanması gerekmez.

Visual Studio 'nun genel uygulama sınıfı şablonuyla oluşturulan olay işleyicileri ayrıntılı değildir. Olay işleyicisi `Application_EventName`adlandırarak herhangi bir `HttpApplication` olayı için bir olay işleyicisi ekleyebilirsiniz. Örneğin, [`AuthorizeRequest` olayı](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)için bir olay işleyicisi oluşturmak üzere aşağıdaki kodu `Global.asax` dosyasına ekleyebilirsiniz:

[!code-cs[Main](processing-unhandled-exceptions-cs/samples/sample1.cs)]

Benzer şekilde, genel uygulama sınıfı şablonu tarafından oluşturulan tüm olay işleyicilerini gerekli olmayan şekilde kaldırabilirsiniz. Bu öğretici için yalnızca `Error` olayı için bir olay işleyicisi gerekir; diğer olay işleyicilerini `Global.asax` dosyasından kaldırmayı ücretsiz olarak hissetmekten çekinmeyin.

> [!NOTE]
> *Http modülleri* , `HttpApplication` olayları için olay işleyicilerini tanımlamaya yönelik başka bir yol sunar. HTTP modülleri, doğrudan Web uygulaması projesine yerleştirilebilecek veya ayrı bir sınıf kitaplığına ayrılmış bir sınıf dosyası olarak oluşturulur. Bunlar bir sınıf kitaplığında ayrılabildiğinden, HTTP modülleri `HttpApplication` olay işleyicileri oluşturmak için daha esnek ve yeniden kullanılabilir bir model sunar. `Global.asax` dosyası, bulunduğu Web uygulamasına özel olduğunda, HTTP modüllerinin bir Web sitesine eklenmesi, derlemeyi `Bin` klasöründe bırakmak ve modülü `Web.config`kaydetmek kadar basit bir işlemdir. Bu öğretici, HTTP modülleri oluşturma ve kullanma konusunda görünmüyor, ancak aşağıdaki iki öğreticide kullanılan iki hata günlüğü kitaplığı HTTP modülleri olarak uygulanır. HTTP modüllerinin avantajları hakkında daha fazla arka plan için, [eklenebilir ASP.NET bileşenleri oluşturmak üzere http modülleri ve Işleyicileri kullanma](https://msdn.microsoft.com/library/aa479332.aspx)konusuna bakın.

## <a name="retrieving-information-about-the-unhandled-exception"></a>Işlenmeyen özel durum hakkında bilgi alma

Bu noktada, `Application_Error` olay işleyicisi olan bir Global. asax dosyanız vardır. Bu olay işleyicisi yürütüldüğünde hatanın bir geliştiricisine bildirimde bulunan ayrıntıları günlüğe kaydedilir. Bu görevleri gerçekleştirmek için ilk olarak oluşturulan özel durumun ayrıntılarını belirlememiz gerekir. `Error` olayının tetiklenmesine neden olan işlenmemiş özel durum ayrıntılarını almak için sunucu nesnesinin [`GetLastError` yöntemini](https://msdn.microsoft.com/library/system.web.httpserverutility.getlasterror.aspx) kullanın.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample2.cs)]

`GetLastError` yöntemi, .NET Framework tüm özel durumlar için temel tür olan `Exception`türünde bir nesne döndürür. Ancak, yukarıdaki kodda `GetLastError` tarafından döndürülen özel durum nesnesini bir `HttpException` nesnesine dönüştürmem. Bir ASP.NET kaynağının işlenmesi sırasında bir özel durum oluşturulduğu için `Error` olayı tetikleniyorsa, oluşturulan özel durum bir `HttpException`içinde sarmalanır. Precipitated hata olayına ilişkin asıl özel durumu almak için `InnerException` özelliğini kullanın. `Error` olayı, var olmayan bir sayfa için bir istek gibi HTTP tabanlı bir özel durum nedeniyle oluşturulduysa, bir `HttpException` oluşturulur, ancak iç özel durumu yoktur.

Aşağıdaki kod, `HttpException` `lastErrorWrapper`adlı bir değişkende depolayarak `Error` olayını tetikleyen özel durum hakkında bilgi almak için `GetLastErrormessage` kullanır. Daha sonra, kaynak özel durumun tür, ileti ve yığın izlemesini üç dize değişkenine depolar, `lastErrorWrapper` `Error` olayını tetikleyen gerçek özel durum olup olmadığını denetler (HTTP tabanlı özel durumlar durumunda) veya yalnızca istek işlenirken oluşan bir özel durum için bir sarmalayıcı olup olmadığını kontrol edin.

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample3.cs)]

Bu noktada, özel durumun ayrıntılarını bir veritabanı tablosuna yazacak kod yazmak için ihtiyacınız olan tüm bilgilere sahip olursunuz. İlgilendiğiniz hata ayrıntılarının her biri için sütunlar içeren bir veritabanı tablosu oluşturabilirsiniz. tür, ileti, yığın izi, vb., istenen sayfanın URL 'SI ve şu anda oturum açmış kullanıcının adı gibi diğer yararlı bilgi parçalarından oluşur. `Application_Error` olay işleyicisinde veritabanına bağlanıp tabloya bir kayıt eklersiniz. Benzer şekilde, e-posta yoluyla hatanın bir geliştiricisini uyarmak için kod ekleyebilirsiniz.

Sonraki iki öğreticilerde incelenen hata günlüğü kitaplıkları, bu tür işlevselliği kullanıma sunar. bu nedenle, bu hata günlüğünü ve bildirimi kendiniz oluşturmanız gerekmez. Ancak, `Error` olayın yükseltilmekte olduğunu ve `Application_Error` olay işleyicisinin hata ayrıntılarını günlüğe kaydetmek ve bir geliştiriciye bildirimde bulunduğunu anlamak için bir hata oluştuğunda geliştiriciye bildiren kodu ekleyelim.

## <a name="notifying-a-developer-when-an-unhandled-exception-occurs"></a>Işlenmeyen bir özel durum oluştuğunda geliştiriciye bildirme

Üretim ortamında işlenmeyen bir özel durum oluştuğunda, hatayı değerlendirebilmeleri ve hangi eylemlerin alınması gerektiğini belirleyebilmeleri için geliştirme ekibine uyarı vermek önemlidir. Örneğin, veritabanına bağlanırken bir hata oluşursa, Bağlantı dizenizi çift denetlemeniz ve belki de Web barındırma şirketinizle bir destek bileti açmanız gerekir. Bir programlama hatası nedeniyle özel durum oluştuysa, gelecekte bu hataların oluşmasını engellemek için ek kodun veya doğrulama mantığının eklenmesi gerekebilir.

[`System.Net.Mail` ad alanındaki](https://msdn.microsoft.com/library/system.net.mail.aspx) .NET Framework sınıfları bir e-posta gönderilmesini kolaylaştırır. [`MailMessage` sınıfı](https://msdn.microsoft.com/library/system.net.mail.mailmessage.aspx) bir e-posta iletisini temsil eder ve `To`, `From`, `Subject`, `Body`ve `Attachments`gibi özelliklere sahiptir. `SmtpClass`, belirtilen SMTP sunucusunu kullanarak bir `MailMessage` nesnesi göndermek için kullanılır; SMTP sunucusu ayarları, `Web.config file`[`<system.net>` öğesinde](https://msdn.microsoft.com/library/6484zdc1.aspx) program aracılığıyla veya bildirimli olarak belirlenebilir. Bir ASP.NET uygulamasında e-posta iletileri gönderme hakkında daha fazla bilgi için, makaleme göz atın, [ASP.net 'de e-posta gönderme](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)ve [sistem .net. Mail hakkında SSS](http://systemnetmail.com/).

> [!NOTE]
> `<system.net>` öğesi, bir e-posta gönderilirken `SmtpClient` sınıfı tarafından kullanılan SMTP sunucusu ayarlarını içerir. Web barındırma şirketinizin muhtemelen uygulamanızdan e-posta göndermek için kullanabileceğiniz bir SMTP sunucusu vardır. Web uygulamanızda kullanmanız gereken SMTP sunucusu ayarları hakkında bilgi edinmek için Web ana bilgisayarınızın destek bölümüne başvurun.

Bir hata oluştuğunda geliştirici e-postası göndermek için `Application_Error` olay işleyicisine aşağıdaki kodu ekleyin:

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample4.cs)]

Yukarıdaki kod oldukça uzun olsa da, toplu işlemin geliştiricisi, geliştiriciye gönderilen e-postada görüntülenen HTML 'yi oluşturur. Kod, `GetLastError` yöntemi (`lastErrorWrapper`) tarafından döndürülen `HttpException` başvuruda bulunarak başlar. İstek tarafından oluşturulan gerçek özel durum `lastErrorWrapper.InnerException` aracılığıyla alınır ve `lastError`değişkenine atanır. Tür, ileti ve yığın izleme bilgileri `lastError` alınır ve üç dize değişkenine depolanır.

Sonra, `mm` adlı bir `MailMessage` nesnesi oluşturulur. E-posta gövdesi HTML olarak biçimlendirilir ve istenen sayfanın URL 'sini, şu anda oturum açmış kullanıcının adını ve özel durum (tür, ileti ve yığın izleme) hakkındaki bilgileri görüntüler. `HttpException` sınıfıyla ilgili çok sayıda şey, [GetHtmlErrorMessage yöntemini](https://msdn.microsoft.com/library/system.web.httpexception.gethtmlerrormessage.aspx)çağırarak özel durum ayrıntıları sarı ekran ölümün (rivd) oluşturulması IÇIN kullanılan HTML 'yi oluşturabileceğiniz bir durumdur. Bu yöntem, burada özel durum ayrıntıları almak ve e-postaya ek olarak eklemek için kullanılır. Dikkatli bir sözcük: `Error` olayı tetikleyen özel durum HTTP tabanlı bir özel durumdur (mevcut olmayan bir sayfa için bir istek gibi), `GetHtmlErrorMessage` yöntemi `null`döndürür.

Son adım `MailMessage`göndermektir. Bu, yeni bir `SmtpClient` yöntemi oluşturularak ve `Send` yöntemi çağırarak yapılır.

> [!NOTE]
> Web uygulamanızda bu kodu kullanmadan önce, `ToAddress` değerleri ve `FromAddress` sabitlerini support@example.com, hata bildirimi e-postası gönderilen ve giden e-postanın gönderildiği e-posta adresine değiştirmek isteyeceksiniz. Ayrıca, `Web.config``<system.net>` bölümünde SMTP sunucusu ayarlarını belirtmeniz gerekir. Kullanılacak SMTP sunucusu ayarlarını öğrenmek için Web barındırma sağlayıcınıza danışın.

Bu kod, geliştiriciye bir hata olduğunda, hatayı özetleyen bir e-posta iletisi gönderilir ve YSOD 'yi içerir. Önceki öğreticide, tarz. aspx ' i ziyaret ederek bir çalışma zamanı hatası ve `Genre.aspx?ID=foo`gibi QueryString aracılığıyla geçersiz bir `ID` değeri geçirdik. `Global.asax` dosyanın bulunduğu sayfayı ziyaret eden, önceki öğreticide olduğu gibi, geliştirme ortamında özel durum ayrıntıları sarı ekranını görmeye devam edersiniz, ancak üretim ortamında özel hata sayfasını görürsünüz. Bu mevcut davranışa ek olarak, geliştiriciye bir e-posta gönderilir.

**Şekil 2** `Genre.aspx?ID=foo`ziyaret edildiğinde alınan e-postayı gösterir. E-posta gövdesi özel durum bilgilerini özetler, ancak `YSOD.htm` eki özel durum ayrıntılarında gösterilen içeriği görüntüler (bkz. **Şekil 3**).

[![](processing-unhandled-exceptions-cs/_static/image5.png)](processing-unhandled-exceptions-cs/_static/image4.png)

**Şekil 2**: Işlenmeyen bir özel durum olduğunda geliştiriciye bir e-posta bildirimi gönderilir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](processing-unhandled-exceptions-cs/_static/image6.png))

[![](processing-unhandled-exceptions-cs/_static/image8.png)](processing-unhandled-exceptions-cs/_static/image7.png)

**Şekil 3**: e-posta bildirimi, ek olarak özel durum ayrıntılarını içerir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](processing-unhandled-exceptions-cs/_static/image9.png))

## <a name="what-about-using-the-custom-error-page"></a>Özel hata sayfasını kullanma hakkında ne olacak?

Bu öğreticide `Global.asax` ve işlenmeyen bir özel durum oluştuğunda kodu yürütmek için `Application_Error` olay işleyicisinin nasıl kullanılacağı gösterildi. Özellikle bir hata geliştiricisine bildirmek için bu olay işleyicisini kullandık; Ayrıca, hata ayrıntılarını bir veritabanında günlüğe kaydetmek için genişletebiliriz. `Application_Error` olay işleyicisinin varlığı, son kullanıcının deneyimini etkilemez. Yine de yapılandırılan hata sayfasını görür, hata ayrıntıları YSOD, çalışma zamanı hatası YSOD veya özel hata sayfası görüntülenir.

Özel hata sayfası kullanılırken `Global.asax` dosyası ve `Application_Error` olayının gerekli olup olmadığını merak etmek doğal bir hatadır. Bir hata oluştuğunda, kullanıcıya özel hata sayfası gösterilir ve bu nedenle, geliştiriciyi bilgilendirmek için kodu koyamıyoruz ve hata ayrıntılarını özel hata sayfasının arka plan kod sınıfına kaydeder. Özel hata sayfasının arka plan kod sınıfına kesinlikle kod ekleyebiliriz, ancak önceki öğreticide araştırdığımız tekniği kullanırken `Error` olayı tetikleyen özel durumun ayrıntılarına erişemezsiniz. Özel hata sayfasından `GetLastError` yönteminin çağrılması `Nothing`döndürür.

Bu davranışın nedeni, özel hata sayfasına yeniden yönlendirme aracılığıyla ulaşılmasından kaynaklanır. İşlenmeyen bir özel durum ASP.NET çalışma zamanına ulaştığında, ASP.NET altyapısı `Error` olayını (`Application_Error` olay işleyicisini yürüten) başlatır ve ardından bir `Response.Redirect(customErrorPageUrl)`vererek kullanıcıyı özel hata sayfasına *yönlendirir* . `Response.Redirect` yöntemi, bir HTTP 302 durum kodu ile istemciye bir yanıt gönderir ve bu, özel hata sayfası gibi tarayıcıyı yeni bir URL istemek üzere iletir. Tarayıcı bu yeni sayfayı otomatik olarak ister. Özel hata sayfasının hatanın kaynaklandığı sayfadan ayrı olarak istendiğini söyleyebilirsiniz, çünkü tarayıcının adres çubuğu özel hata sayfası URL 'SI olarak değişir (bkz. **Şekil 4**).

[![](processing-unhandled-exceptions-cs/_static/image11.png)](processing-unhandled-exceptions-cs/_static/image10.png)

**Şekil 4**: bir hata oluştuğunda tarayıcı özel hata sayfası URL 'Sine yeniden yönlendirilir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](processing-unhandled-exceptions-cs/_static/image12.png))

Net etkisi, işlenmemiş özel durumun oluştuğu isteğin, sunucu HTTP 302 yeniden yönlendirme ile yanıt verdiğinde sona erdiği durumdur. Özel hata sayfasına yapılan sonraki istek yepyeni bir istek; Bu noktada, ASP.NET motoru hata bilgilerini attı ve ayrıca, önceki istekteki işlenmeyen özel durumu özel hata sayfası için yeni istekle ilişkilendirmenin bir yolu yoktur. `GetLastError`, özel hata sayfasından çağrıldığında `null` döndürmesinin nedeni budur.

Ancak, hataya neden olan istek sırasında özel hata sayfasının yürütülmesi mümkündür. [`Server.Transfer(url)`](https://msdn.microsoft.com/library/system.web.httpserverutility.transfer.aspx) yöntemi, YÜRÜTMEYI belirtilen URL 'ye aktarır ve aynı istek içinde işler. `Application_Error` olay işleyicisindeki kodu, özel hata sayfasının arka plan kod sınıfına taşıyabilir, bu kodu `Global.asax` aşağıdaki kodla değiştirin:

[!code-csharp[Main](processing-unhandled-exceptions-cs/samples/sample5.cs)]

Artık işlenmeyen bir özel durum oluştuğunda, `Application_Error` olay işleyicisi denetimi HTTP durum koduna göre uygun özel hata sayfasına aktarır. Denetim aktarıldığından, özel hata sayfasında işlenmemiş özel durum bilgilerine `Server.GetLastError` aracılığıyla erişim vardır ve hatanın geliştiricisine bildirimde bulunabilir ve ayrıntılarını günlüğe kaydedebilir. `Server.Transfer` çağrısı, ASP.NET altyapısının kullanıcıyı özel hata sayfasına yönlendirmesini sonlandırır. Bunun yerine, özel hata sayfasının içeriği hatayı oluşturan sayfanın yanıtı olarak döndürülür.

## <a name="summary"></a>Özet

Bir ASP.NET Web uygulamasında işlenmeyen bir özel durum oluştuğunda, ASP.NET çalışma zamanı `Error` olayını başlatır ve yapılandırılan hata sayfasını görüntüler. Hata olayı için bir olay işleyicisi oluşturarak hatanın geliştiricisine bildirimde bulunabilir, ayrıntılarını günlüğe kaydedebilir veya başka bir biçimde işleyebilir. `Error`gibi `HttpApplication` olaylar için bir olay işleyicisi oluşturmanın iki yolu vardır: `Global.asax` dosyasında veya bir HTTP modülünden. Bu öğretici, bir e-posta iletisi aracılığıyla bir hata geliştiricilerine bildiren `Global.asax` dosyasında `Error` olay işleyicisinin nasıl oluşturulacağını gösterdi.

İşlenmemiş özel durumları benzersiz veya özelleştirilmiş bir şekilde işleyebilmeniz gerekiyorsa `Error` olay işleyicisi oluşturma yararlı olur. Ancak, özel durumu günlüğe kaydetmek veya bir geliştiriciye bildirmek için kendi `Error` olay işleyicinizin oluşturulması, birkaç dakika içinde yalnızca ücretsiz ve kolay bir şekilde kullanılabilecek hata günlüğü kitaplıklarını daha verimli bir şekilde kullanıma sunmamakta. Sonraki iki öğreticinin böyle iki kitaplığı incelemektir.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP.NET HTTP modülleri ve HTTP Işleyicilerine genel bakış](https://support.microsoft.com/kb/307985)
- [Işlenmemiş özel durumlara düzgün şekilde yanıt verme-Işlenmemiş özel durumları Işleme](http://aspnet.4guysfromrolla.com/articles/091306-1.aspx)
- [`HttpApplication` sınıfı ve ASP.NET uygulama nesnesi](http://www.eggheadcafe.com/articles/20030211.asp)
- [ASP.NET içinde HTTP Işleyicileri ve HTTP modülleri](http://www.15seconds.com/Issue/020417.htm)
- [ASP.NET 'de e-posta gönderme](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx)
- [`Global.asax` dosyasını anlama](http://aspalliance.com/1114_Understanding_the_Globalasax_file.all)
- [Takılabilir ASP.NET bileşenleri oluşturmak için HTTP modülleri ve Işleyicileri kullanma](https://msdn.microsoft.com/library/aa479332.aspx)
- [ASP.NET `Global.asax` dosyasıyla çalışma](http://articles.techrepublic.com.com/5100-10878_11-5771721.html)
- [`HttpApplication` örneklerle çalışma](https://msdn.microsoft.com/library/a0xez8f2.aspx)

> [!div class="step-by-step"]
> [Önceki](displaying-a-custom-error-page-cs.md)
> [İleri](logging-error-details-with-asp-net-health-monitoring-cs.md)
