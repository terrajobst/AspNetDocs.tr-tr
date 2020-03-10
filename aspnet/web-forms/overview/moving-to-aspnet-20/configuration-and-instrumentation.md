---
uid: web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
title: Yapılandırma ve Izleme | Microsoft Docs
author: microsoft
description: ASP.NET 2,0 ' de yapılandırma ve araçlardaki önemli değişiklikler vardır. Yeni ASP.NET Configuration API 'SI, yapılandırma değişikliklerinin PR 'ye yapılmasına izin verir...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 21ebbaee-7ed8-45ae-b6c1-c27c88342e48
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/configuration-and-instrumentation
msc.type: authoredcontent
ms.openlocfilehash: cd5bedce5459e8cf8e72df8de69ebd82f2d97789
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626030"
---
# <a name="configuration-and-instrumentation"></a>Yapılandırma ve İzleme

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 2,0 ' de yapılandırma ve araçlardaki önemli değişiklikler vardır. Yeni ASP.NET yapılandırma API 'SI, yapılandırma değişikliklerinin programlı olarak yapılmasına izin verir. Ayrıca, birçok yeni yapılandırma ayarı yeni yapılandırmalar ve izleme için izin verir.

ASP.NET 2,0 ' de yapılandırma ve araçlardaki önemli değişiklikler vardır. Yeni ASP.NET yapılandırma API 'SI, yapılandırma değişikliklerinin programlı olarak yapılmasına izin verir. Ayrıca, birçok yeni yapılandırma ayarı yeni yapılandırmalar ve izleme için izin verir.

Bu modülde, ASP.NET yapılandırma dosyalarını okuma ve yazma ile ilgili ASP.NET yapılandırma API 'sini tartışacağız ve ayrıca ASP.NET izleme ele alınacaktır. Ayrıca, ASP.NET izlenirken sunulan yeni özellikleri de ele alınacaktır.

## <a name="aspnet-configuration-api"></a>ASP.NET yapılandırma API 'SI

ASP.NET yapılandırma API 'SI, tek bir programlama arabirimi kullanarak uygulama yapılandırma verileri geliştirmenize, dağıtmanıza ve yönetmenize olanak tanır. Yapılandırma API 'sini, yapılandırma dosyalarındaki XML 'i doğrudan düzenlemeden, tüm ASP.NET yapılandırmalarını programlama yoluyla geliştirmek ve değiştirmek için kullanabilirsiniz. Ayrıca, Web tabanlı yönetim araçları ve Microsoft Yönetim Konsolu (MMC) ek bileşenlerinde, geliştirmeniz gereken konsol uygulamaları ve betikler içindeki yapılandırma API 'sini de kullanabilirsiniz.

Aşağıdaki iki yapılandırma yönetim aracı Yapılandırma API 'sini kullanır ve .NET Framework sürüm 2,0 ' ye dahildir:

- Yapılandırma hiyerarşisinin tüm düzeylerinde yerel yapılandırma verilerinin tümleşik bir görünümünü sağlayarak yönetim görevlerini basitleştirmek için yapılandırma API 'sini kullanan ASP.NET MMC ek bileşeni.
- Barındırılan siteler dahil olmak üzere yerel ve uzak uygulamalar için yapılandırma ayarlarını yönetmenizi sağlayan Web sitesi yönetim aracı.

ASP.NET yapılandırma API 'SI, Web siteleri ve uygulamaları programlı bir şekilde yapılandırmak için kullanabileceğiniz bir ASP.NET Yönetim nesneleri kümesi içerir. Yönetim nesneleri .NET Framework sınıf kitaplığı olarak uygulanır. Yapılandırma API 'SI programlama modeli, veri türlerini derleme zamanında zorlayarak kod tutarlılığı ve güvenilirliği sağlamaya yardımcı olur. Yapılandırma API 'SI, uygulama yapılandırmalarını daha kolay bir şekilde yönetmenizi sağlamak için, verileri ayrı koleksiyonlar olarak farklı bir koleksiyon olarak görüntülemek yerine, yapılandırma hiyerarşisindeki tüm noktalarından Birleştirilen verileri tek bir koleksiyon olarak görüntülemenizi sağlar yapılandırma dosyaları. Ayrıca, yapılandırma API 'si, yapılandırma dosyalarındaki XML 'i doğrudan düzenlemeden tüm uygulama yapılandırmalarını yönetmenize olanak sağlar. Son olarak, API, Web sitesi yönetim aracı gibi yönetim araçlarını destekleyerek yapılandırma görevlerini basitleştirir. Yapılandırma API 'SI bir bilgisayarda yapılandırma dosyalarının oluşturulmasını ve birden çok bilgisayarda yapılandırma betikleri çalıştırmayı destekleyerek dağıtımı basitleştirir.

> [!NOTE]
> Yapılandırma API 'SI IIS uygulamalarının oluşturulmasını desteklemez.

## <a name="working-with-local-and-remote-configuration-settings"></a>Yerel ve uzak yapılandırma ayarlarıyla çalışma

Bir yapılandırma nesnesi, bir bilgisayar gibi belirli bir fiziksel varlığa veya bir uygulama ya da bir Web sitesi gibi mantıksal bir varlığa uygulanan yapılandırma ayarlarının birleştirilmiş görünümünü temsil eder. Belirtilen mantıksal varlık yerel bilgisayarda veya uzak bir sunucuda bulunabilir. Belirtilen bir varlık için yapılandırma dosyası olmadığında, yapılandırma nesnesi Machine. config dosyası tarafından tanımlanan varsayılan yapılandırma ayarlarını temsil eder.

Aşağıdaki sınıflardan açık yapılandırma yöntemlerinden birini kullanarak bir yapılandırma nesnesi alabilirsiniz:

1. Varlığınız bir istemci uygulaması ise ConfigurationManager sınıfı.
2. Varlığınız bir Web uygulaması ise WebConfigurationManager sınıfı.

Bu yöntemler, temel yapılandırma dosyalarını işlemek için gerekli yöntemleri ve özellikleri sağlayan bir yapılandırma nesnesi döndürür. Bu dosyalara okuma veya yazma için erişebilirsiniz.

### <a name="reading"></a>Okuyamadı

Yapılandırma bilgilerini okumak için GetSection veya GetSectionGroup metodunu kullanın. Okuyan Kullanıcı veya işlemin hiyerarşideki tüm yapılandırma dosyaları üzerinde okuma izinlerine sahip olması gerekir.

> [!NOTE]
> Yol parametresi alan statik bir GetSection yöntemi kullanırsanız, path parametresinin kodun çalıştırıldığı uygulamaya başvurması gerekir. Aksi takdirde, parametresi yok sayılır ve çalışmakta olan uygulamanın yapılandırma bilgileri döndürülür.

### <a name="writing"></a>Yazıp

Yapılandırma bilgilerini yazmak için Save yöntemlerinden birini kullanın. Yazan Kullanıcı veya işlemin yapılandırma dosyasında ve geçerli yapılandırma hiyerarşisi düzeyinde dizinde yazma izinlerinin olması ve hiyerarşideki tüm yapılandırma dosyaları üzerinde okuma izinlerinin olması gerekir.

Belirtilen bir varlık için devralınan yapılandırma ayarlarını temsil eden bir yapılandırma dosyası oluşturmak için aşağıdaki kaydetme-yapılandırma yöntemlerinden birini kullanın:

1. Yeni bir yapılandırma dosyası oluşturmak için Kaydet yöntemi.
2. Başka bir konumda yeni bir yapılandırma dosyası oluşturmak için SaveAs yöntemi.

## <a name="configuration-classes-and-namespaces"></a>Yapılandırma sınıfları ve ad alanları

Birçok yapılandırma sınıfı ve yöntemi birbirlerine benzerdir. Aşağıdaki tabloda en yaygın olarak kullanılan yapılandırma sınıfları ve ad alanları açıklanmaktadır.

| **Yapılandırma sınıfı veya ad alanı** | **Açıklama** |
| --- | --- |
| [System. Configuration](https://msdn.microsoft.com/library/system.configuration.aspx) ad alanı | Tüm .NET Framework uygulamaları için ana yapılandırma sınıflarını içerir. Bölüm işleyici sınıfları, bir bölümün yapılandırma verilerini GetSection ve GetSectionGroup gibi yöntemlerle elde etmek için kullanılır. Bu iki yöntem statik değildir. |
| System. Configuration. Configuration sınıfı | Bir bilgisayar, uygulama, Web dizini veya diğer bir kaynak için bir yapılandırma verileri kümesini temsil eder. Bu sınıf, yapılandırma ayarlarını güncelleştirmek ve bölümlere ve bölüm gruplarına başvurular almak için GetSection ve GetSectionGroup gibi yararlı yöntemler içerir. Bu sınıf, Web ConfigurationManager ve ConfigurationManager sınıflarının yöntemleri gibi tasarım zamanı yapılandırma verilerini elde eden yöntemler için bir dönüş türü olarak kullanılır. |
| System. Web. Configuration ad alanı | [ASP.NET yapılandırma ayarları](https://msdn.microsoft.com/library/b5ysx397.aspx)'nda tanımlanan ASP.NET yapılandırma bölümlerinin bölüm işleyici sınıflarını içerir. Bölüm işleyici sınıfları, bir bölümün yapılandırma verilerini GetSection ve GetSectionGroup gibi yöntemlerle elde etmek için kullanılır. |
| System.Web.Configuration.WebConfigurationManager class | Çalışma zamanı ve tasarım zamanı yapılandırma ayarlarına başvurular almak için yararlı yöntemler sağlar. Bu yöntemler, bir dönüş türü olarak System. Configuration. Configuration sınıfını kullanır. Bu sınıfın statik GetSection yöntemini veya System. Configuration. ConfigurationManager sınıfının statik olmayan GetSection metodunu birbirinin yerine kullanabilirsiniz. Web uygulaması yapılandırmaları için System. Configuration. ConfigurationManager sınıfı yerine System. Web. Configuration. WebConfigurationManager sınıfı önerilir. |
| [System. Configuration. Provider](https://msdn.microsoft.com/library/system.configuration.provider.aspx) ad alanı | Yapılandırma sağlayıcısını özelleştirmek ve genişletmek için bir yol sağlar. Bu, yapılandırma sistemindeki tüm sağlayıcı sınıfları için temel sınıftır. |
| [System. Web. Management](https://msdn.microsoft.com/library/system.web.management.aspx) ad alanı | Web uygulamalarının sistem durumunu yönetmek ve izlemek için sınıflar ve arabirimler içerir. Kesinlikle konuşurken, bu ad alanı yapılandırma API 'sinin bir parçası olarak kabul edilmez. Örneğin, izleme ve olay tetikleme bu ad alanındaki sınıflar tarafından gerçekleştirilir. |
| [System. Management. Instrumentation](https://msdn.microsoft.com/library/system.management.instrumentation.aspx) ad alanı | , Uygulamaların yönetim bilgilerini ve olaylarını Windows Yönetim Araçları (WMI) aracılığıyla potansiyel tüketicilere sunmak için gereken sınıfları sağlar. ASP.NET sistem durumu izleme, olayları teslim etmek için WMI kullanır. Kesinlikle konuşurken, bu ad alanı yapılandırma API 'sinin bir parçası olarak kabul edilmez. |

## <a name="reading-from-aspnet-configuration-files"></a>ASP.NET yapılandırma dosyalarından okuma

WebConfigurationManager sınıfı, ASP.NET yapılandırma dosyalarından okuma için temel sınıftır. ASP.NET yapılandırma dosyalarını okumak için temel olarak üç adım vardır:

1. OpenWebConfiguration metodunu kullanarak bir yapılandırma nesnesi alın.
2. Yapılandırma dosyasında istenen bölüme bir başvuru alın.
3. Yapılandırma dosyasından istenen bilgileri okuyun.

Yapılandırma nesnesi, belirli bir yapılandırma dosyasını temsil etmez. Bunun yerine, bir bilgisayarın, uygulamanın veya Web sitesinin yapılandırmasının birleştirilmiş bir görünümünü temsil eder. Aşağıdaki kod örneği, *ProductInfo*adlı bir Web uygulamasının yapılandırmasını temsil eden bir yapılandırma nesnesi oluşturur.

[!code-csharp[Main](configuration-and-instrumentation/samples/sample1.cs)]

> [!NOTE]
> /ProductInfo yolu yoksa Yukarıdaki kod, Machine. config dosyasında belirtilen varsayılan yapılandırmayı döndürür.

Yapılandırma nesnesine sahip olduktan sonra yapılandırma ayarlarına gitmek için GetSection veya GetSectionGroup metodunu kullanabilirsiniz. Aşağıdaki örnek, yukarıdaki ProductInfo uygulamasının kimliğe bürünme ayarlarına bir başvuru alır:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample2.cs)]

## <a name="writing-to-aspnet-configuration-files"></a>ASP.NET yapılandırma dosyalarına yazma

Yapılandırma dosyalarından okurken, WebConfigurationManager sınıfı, Asp.NET yapılandırma dosyalarına yazmak için çekirdekdir. ASP.NET yapılandırma dosyalarına yazmanın üç adımı da vardır.

1. OpenWebConfiguration metodunu kullanarak bir yapılandırma nesnesi alın.
2. Yapılandırma dosyasında istenen bölüme bir başvuru alın.
3. İstenen bilgileri, Kaydet veya SaveAs metodunu kullanarak yapılandırma dosyasından yazın.

Aşağıdaki kod &lt;derlemesi&gt; öğesinin **hata ayıklama** özniteliğini false olarak değiştirir:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample3.cs)]

Bu kod yürütüldüğünde, *WebApp* uygulamasının Web. config dosyası için &lt;derleme&gt; öğesinin **hata ayıklama** özniteliği false olarak ayarlanır.

## <a name="systemwebmanagement-namespace"></a>System. Web. Management ad alanı

System. Web. Management ad alanı, ASP.NET uygulamalarının sistem durumunu yönetmeye ve izlemeye yönelik sınıfları ve arabirimleri sağlar.

Olayları bir sağlayıcıyla ilişkilendiren bir kural tanımlayarak günlüğe kaydetme gerçekleştirilir. Kural, sağlayıcıya gönderilen olayların türünü tanımlar. Aşağıdaki temel olaylar, oturum açmak için kullanılabilir:

| **WebBaseEvent** | Tüm olaylar için temel olay sınıfı. Olay kodu, Olay Ayrıntısı kodu, olayın oluşturulduğu tarih ve saat, sıra numarası, olay iletisi ve olay ayrıntıları gibi tüm olaylar için gerekli özellikleri içerir. |
| --- | --- |
| **WebManagementEvent** | Uygulama ömrü, istek, hata ve denetim olayları gibi yönetim olayları için temel olay sınıfı. |
| **WebHeartbeatEvent** | Yararlı çalışma zamanı durum bilgilerini yakalamak için uygulama tarafından düzenli aralıklarla oluşturulan olay. |
| **WebAuditEvent** | Yetkilendirme hatası, şifre çözme hatası *vb.* gibi koşulları işaretlemek için kullanılan güvenlik denetim olayları için temel sınıf. |
| **WebRequestEvent** | Tüm bilgilendirici istek olayları için temel sınıf. |
| **WebBaseErrorEvent** | Hata koşullarını belirten tüm olaylar için temel sınıf. |

Kullanılabilir sağlayıcı türleri Olay Görüntüleyicisi, SQL Server, Windows Yönetim Araçları (WMI) ve e-postaya olay çıktısı göndermenizi sağlar. Önceden yapılandırılmış sağlayıcılar ve olay eşlemeleri, olay çıkışının günlüğe kaydedilmesini sağlamak için gereken iş miktarını azaltır.

ASP.NET 2,0, uygulama etki alanlarına dayalı olayları günlüğe kaydetmek ve işlenmemiş özel durumları günlüğe kaydetmek için olay günlüğü sağlayıcısı 'nı kullanır. Bu, temel senaryolardan bazılarını ele almanıza yardımcı olur. Örneğin, uygulamanızın bir özel durum yarattığında, ancak kullanıcının hatayı kaydetmediğini ve yeniden oluşturamadığınızı varsayalım. Varsayılan olay günlüğü kuralıyla, ne tür bir hata oluştuğunu daha iyi bir fikir edinmek için özel durum ve yığın bilgilerini toplayabileceksiniz. Uygulamanız oturum durumunu kaybederce bir örnek geçerlidir. Bu durumda, uygulama etki alanının geri dönüşüm olup olmadığını ve uygulama etki alanının neden ilk yerde durdurulduğunu öğrenmek için olay günlüğüne bakabilirsiniz.

Ayrıca, sistem durumu izleme sistemi genişletilebilir. Örneğin, özel Web olayları tanımlayabilir, uygulamanızda tetikedebilir ve ardından olay bilgilerini e-postanız gibi bir sağlayıcıya göndermek için bir kural tanımlayabilirsiniz. Bu sayede, araçlarınızın durumunu kolayca sistem durumu izleme sağlayıcılarına bağlayabilir. Başka bir örnek olarak, bir sipariş her işlendiğinde bir olay harekete geçirebilir ve her olayı SQL Server veritabanına gönderen bir kural ayarlarsınız. Ayrıca, bir Kullanıcı bir satırda birden çok kez oturum açarken bir olay harekete geçirebilir ve e-posta tabanlı sağlayıcıları kullanmak için olayı ayarlayabilirsiniz.

Varsayılan sağlayıcılar ve olaylar için yapılandırma genel Web. config dosyasında depolanır. Global Web. config dosyası, ASP.NET 1x içindeki Machine. config dosyasında depolanan tüm Web tabanlı ayarları depolar. Genel Web. config dosyası aşağıdaki dizinde bulunur:

`%windir%\Microsoft.Net\Framework\v2.0.*\config\Web.config`

Global Web. config dosyasının &lt;healthMonitoring&gt; bölümü varsayılan yapılandırma ayarlarını sağlar. Uygulamanızın Web. config dosyasında &lt;healthMonitoring&gt; bölümünü uygulayarak bu ayarı geçersiz kılabilir veya kendi ayarlarınızı yapılandırabilirsiniz.

Global Web. config dosyasının &lt;healthMonitoring&gt; bölümü aşağıdaki öğeleri içerir:

| **sağlayıcılarla** | Olay Görüntüleyicisi, WMI ve SQL Server için ayarlanan sağlayıcıları içerir. |
| --- | --- |
| **eventMappings** | Çeşitli WebBase sınıfları için eşlemeler içerir. Kendi olay sınıfınızı oluşturursanız, bu listeyi genişletebilirsiniz. Kendi olay sınıfınızı oluşturmak, bilgi yollarındaki sağlayıcılar üzerinde daha ayrıntılı ayrıntı sahibi olmanızı sağlar. Örneğin, e-postaya özel olaylarınızı gönderirken, işlenmemiş özel durumları SQL Server gönderilmek üzere yapılandırabilirsiniz. |
| **kuralın** | EventMappings 'yi sağlayıcıya bağlar. |
| **ara** | Olayları sağlayıcıya ne sıklıkta temizleyeceğini öğrenmek için SQL Server ve e-posta sağlayıcılarıyla birlikte kullanılır. |

Genel Web. config dosyasından bir kod örneği aşağıda verilmiştir.

[!code-xml[Main](configuration-and-instrumentation/samples/sample4.xml)]

## <a name="how-to-store-events-to-event-viewer"></a>Olayları Olay Görüntüleyicisi depolama

Daha önce belirtildiği gibi, Olay Görüntüleyicisi olaylarını günlüğe kaydetme sağlayıcısı, Global Web. config dosyasında sizin için yapılandırılır. Varsayılan olarak, **WebBaseErrorEvent** ve **WebFailureAuditEvent** ' i temel alan tüm olaylar günlüğe kaydedilir. Olay günlüğüne ek bilgileri günlüğe kaydetmek için ek kurallar ekleyebilirsiniz. Örneğin, tüm olayları (*yani*, **WebBaseEvent**tabanlı her olay) günlüğe kaydetmek isterseniz, Web. config dosyanıza aşağıdaki kuralı ekleyebilirsiniz:

[!code-xml[Main](configuration-and-instrumentation/samples/sample5.xml)]

Bu kural **tüm olaylar** olay haritasını olay günlüğü sağlayıcısına bağlar. Hem eventMapping hem de sağlayıcı genel Web. config dosyasına dahil edilmiştir.

## <a name="how-to-store-events-to-sql-server"></a>Olayları SQL Server depolama

Bu yöntem, ASPNET\_regsql. exe aracı tarafından oluşturulan **aspnetdb** veritabanını kullanır. Varsayılan sağlayıcı, App\_Data klasöründe dosya tabanlı bir veritabanı ya da SQL Server yerel SQLExpress örneği kullanan LocalSqlServer bağlantı dizesini kullanır. Hem LocalSqlServer bağlantı dizesi hem de SqlProvider genel Web. config dosyasında yapılandırılır.

Global Web. config dosyasındaki LocalSqlServer bağlantı dizesi şuna benzer:

[!code-xml[Main](configuration-and-instrumentation/samples/sample6.xml)]

Başka bir SQL Server örneği kullanmak istiyorsanız,%windir%\Microsoft.Net\Framework\v2.0. içinde bulunan ASPNET\_regsql. exe aracını kullanmanız gerekir.\* klasörü. SQL Server örneğinde özel bir **aspnetdb** veritabanı oluşturmak için ASPNET\_regsql. exe aracını kullanın, sonra bağlantı dizesini uygulama yapılandırma dosyanıza ekleyin ve ardından yeni bağlantı dizesini kullanarak bir sağlayıcı ekleyin. **Aspnetdb** veritabanı oluşturulduktan sonra, bir eventMapping 'ı SqlProvider 'a bağlamak için bir kural ayarlamanız gerekir.

Varsayılan SqlProvider ' ı veya kendi sağlayıcınızı yapılandırdıktan sonra, sağlayıcıyı bir olay haritasına bağlayan bir kural eklemeniz gerekir. Aşağıdaki kural yukarıda oluşturduğunuz yeni sağlayıcıyı **tüm olaylar** olay haritasına bağlar. Bu kural **WebBaseEvent** temelinde tüm olayları günlüğe kaydeder ve MYASPNETDB bağlantı dizesini kullanacak MySqlWebEventProvider 'a gönderir. Aşağıdaki kod, sağlayıcıyı bir olay haritasına bağlamak için bir kural ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample7.xml)]

Yalnızca SQL Server hata göndermek istiyorsanız aşağıdaki kuralı ekleyebilirsiniz:

[!code-xml[Main](configuration-and-instrumentation/samples/sample8.xml)]

## <a name="how-to-forward-events-to-wmi"></a>Olayları WMI 'ya iletme

Olayları da WMI 'ya iletebilirsiniz. WMI sağlayıcısı, varsayılan olarak genel Web. config dosyasında sizin için yapılandırılır.

Aşağıdaki kod örneği, olayları WMI 'ya iletmek için bir kural ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample9.xml)]

Bir eventMapping 'i sağlayıcıya ve ayrıca olayları dinlemek için bir WMI dinleyici uygulamasına ilişkilenmek üzere bir kural eklemeniz gerekir. Aşağıdaki kod örneği, WMI sağlayıcısını **tüm olaylar** olay haritasına bağlamak için bir kural ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample10.xml)]

## <a name="how-to-forward-events-to-email"></a>Olayları e-postaya iletme

Ayrıca, olayları e-postaya da iletebilirsiniz. Yanlışlıkla SQL Server veya olay günlüğü için daha uygun olabilecek çok sayıda bilgi gönderebileceği için, e-posta sağlayıcınıza hangi olay kuralları eşleştirdiğinizden emin olun. İki e-posta sağlayıcısı vardır; SimpleMailWebEventProvider ve TemplatedMailWebEventProvider. Her ikisi de yalnızca TemplatedMailWebEventProvider üzerinde bulunan "Template" ve "detailedTemplateErrors" öznitelikleri dışında aynı yapılandırma özniteliklerine sahiptir.

> [!NOTE]
> Bu e-posta sağlayıcılarının hiçbiri sizin için yapılandırılmamış. Bunları Web. config dosyanıza eklemeniz gerekir.

Bu iki e-posta sağlayıcısı arasındaki temel fark, SimpleMailWebEventProvider, değiştirilemeyen bir genel şablonda e-posta gönderir. Örnek Web. config dosyası, bu e-posta sağlayıcısını aşağıdaki kuralı kullanarak yapılandırılan sağlayıcılar listesine ekler:

[!code-xml[Main](configuration-and-instrumentation/samples/sample11.xml)]

Ayrıca, e-posta sağlayıcısını **tüm olaylar** olay haritasına bağlamak için aşağıdaki kural de eklenmiştir:

[!code-xml[Main](configuration-and-instrumentation/samples/sample12.xml)]

## <a name="aspnet-20-tracing"></a>ASP.NET 2,0 Izleme

ASP.NET 2,0 ' de izlemenin üç önemli geliştirmesi vardır.

1. Tümleşik izleme işlevselliği
2. İzleme iletilerine programlı erişim
3. Geliştirilmiş uygulama düzeyi izleme

## <a name="integrated-tracing-functionality"></a>Tümleşik Izleme Işlevselliği

Artık System. Diagnostics. Trace sınıfı tarafından oluşturulan iletileri ASP.NET izleme çıktısına yönlendirebilir ve ASP.NET izleme tarafından yayılan iletileri System. Diagnostics. Trace 'e yönlendirebilirsiniz. Ayrıca, ASP.NET izleme olaylarını System. Diagnostics. Trace 'e iletebilirsiniz. Bu işlev, &lt;Trace&gt; öğesinin yeni **WriteToDiagnosticsTrace** özniteliği tarafından sağlanır. Bu Boole değeri true olduğunda, ASP.NET Trace iletileri, Izleme iletilerini göstermek için kayıtlı tüm dinleyiciler tarafından kullanılmak üzere System. Diagnostics izleme altyapısına iletilir.

## <a name="programmatic-access-to-trace-messages"></a>Izleme Iletilerine programlı erişim

ASP.NET 2,0, **TraceContextRecord** sınıfı ve izleme kayıtları **koleksiyonu aracılığıyla** tüm izleme iletilerine programlı erişim sağlar. İzleme iletilerine erişmenin en verimli yolu, yeni **TraceFinished** olayını işlemek Için bir **TraceContextEventHandler** temsilcisini (Ayrıca ASP.NET 2,0 ' de yeni) kaydetmektedir. Daha sonra izleme iletilerinde istediğiniz gibi döngü yapabilirsiniz.

Aşağıdaki kod örneği şunu gösterir:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample13.cs)]

Yukarıdaki örnekte, izleme ve yanıt akışına her iletiyi yazar.

## <a name="improved-application-level-tracing"></a>Geliştirilmiş uygulama düzeyi Izleme

Uygulama düzeyi izleme, &lt;Trace&gt; öğesinin yeni **Mostson** özniteliği tanıtımı aracılığıyla geliştirilmiştir. Bu öznitelik, en son uygulama düzeyi izleme çıktısının görüntülendiğini ve requestLimit tarafından belirtilen limitlerin ötesinde daha eski izleme verilerinin atılıp atılmadığını belirtir. Yanlışsa, requestLimit özniteliğine ulaşılana kadar istekler için izleme verileri görüntülenir.

## <a name="aspnet-command-line-tools"></a>ASP.NET komut satırı araçları

ASP.NET yapılandırmasına yardımcı olacak birkaç komut satırı aracı vardır. ASP.NET geliştiricileri, ASPNET\_regııs. exe aracını tanımanız gerekir. ASP.NET 2,0, yapılandırmaya yardımcı olmak için üç diğer komut satırı aracı sağlar.

Aşağıdaki komut satırı araçları kullanılabilir:

| **Araç** | **Kullanma** |
| --- | --- |
| **ASPNET\_regııs. exe** | IIS ile ASP.NET kaydına izin verir. Bu araçların ASP.NET 2,0, biri 32 bit sistemler için (Framework klasöründe) ve bir diğeri de 64-bit sistemler için (Framework64 klasöründe) ile birlikte gelen iki sürümü vardır. 64 bit sürümü 32 bit işletim sistemine yüklenmez. |
| **ASPNET\_regsql. exe** | ASP.NET SQL Server kayıt aracı, ASP.NET ' deki SQL Server sağlayıcıları tarafından kullanılmak üzere Microsoft SQL Server bir veritabanı oluşturmak veya var olan bir veritabanına seçenek eklemek veya kaldırmak için kullanılır. ASPNET\_regsql. exe dosyası Web sunucunuzdaki [Drive:] \WINDOWS\Microsoft.NET\Framework\versionNumber klasöründe bulunur. |
| **ASPNET\_regbrowsers. exe** | ASP.NET Browser kayıt aracı tüm sistem genelinde tarayıcı tanımlarını bir derlemede ayrıştırır ve derler ve derlemeyi genel derleme önbelleğine kurar. Araç tarayıcı tanım dosyalarını kullanır (. TARAYıCı dosyaları) .NET Framework tarayıcılar alt dizininden. Araç%SystemRoot%\Microsoft.NET\Framework\version\ dizininde bulunabilir. |
| **ASPNET\_Compiler. exe** | ASP.NET derleme aracı, bir ASP.NET Web uygulamasını yerinde veya bir üretim sunucusu gibi bir hedef konuma dağıtım için derlemenize olanak sağlar. Son kullanıcılar uygulama derlenirken uygulamaya yapılan ilk istekte bir gecikmeyle karşılaşmadığından, yerinde derleme uygulama performansına yardımcı olur. |

ASPNET\_regııs. exe aracı ASP.NET 2,0 ' ye yeni sahip olmadığından, burada ele alınacaktır.

## <a name="aspnet-sql-server-registration-tool---aspnet_regsqlexe"></a>ASP.NET SQL Server kayıt aracı-ASPNET\_regsql. exe

ASP.NET SQL Server kayıt aracını kullanarak birkaç seçenek türü ayarlayabilirsiniz. Bir SQL bağlantısı belirtebilir, hangi ASP.NET uygulama hizmetlerinin bilgilerini yönetmek için SQL Server kullandığını, SQL önbellek bağımlılığı için hangi veritabanının veya tablonun kullanılacağını belirteceğini ve yordamları ve oturum durumunu depolamak için SQL Server kullanma desteği eklemeyi veya kaldırmayı seçebilirsiniz.

Birçok ASP.NET uygulama hizmeti bir veri kaynağından verileri depolamayı ve almayı yönetmek için bir sağlayıcıya bağımlıdır. Her sağlayıcı veri kaynağına özeldir. ASP.NET, aşağıdaki ASP.NET özellikleri için bir SQL Server sağlayıcısı içerir:

- Üyelik ( [SqlMembershipProvider](https://msdn.microsoft.com/library/system.web.security.sqlmembershipprovider.aspx) sınıfı).
- Rol yönetimi ( [SqlRoleProvider](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx) sınıfı).
- Profil ( [SqlProfileProvider](https://msdn.microsoft.com/library/system.web.profile.sqlprofileprovider.aspx) sınıfı).
- Web Bölümleri kişiselleştirme ( [SqlPersonalizationProvider](https://msdn.microsoft.com/library/system.web.ui.webcontrols.webparts.sqlpersonalizationprovider.aspx) sınıfı).
- Web olayları ( [SqlWebEventProvider](https://msdn.microsoft.com/library/system.web.management.sqlwebeventprovider.aspx) sınıfı).

ASP.NET yüklediğinizde, sunucunuzun Machine. config dosyası bir sağlayıcıya dayalı ASP.NET özelliklerinin her biri için SQL Server sağlayıcıları belirten yapılandırma öğelerini içerir. Bu sağlayıcılar, varsayılan olarak, SQL Server Express 2005 yerel bir kullanıcı örneğine bağlanmak üzere yapılandırılır. Sağlayıcılar tarafından kullanılan varsayılan bağlantı dizesini değiştirirseniz, makine yapılandırmasında yapılandırılmış ASP.NET özelliklerinden hiçbirini kullanabilmeniz için önce, SQL Server veritabanını ve ASPNET\_regsql. exe ' yi kullanarak seçtiğiniz özelliği için veritabanı öğelerini yüklemelisiniz. SQL kayıt aracı ile belirttiğiniz veritabanı zaten mevcut değilse (aspnetdb, komut satırında belirtilmemişse, varsayılan veritabanı olur), geçerli kullanıcının SQL Server veritabanları oluşturma ve şema e-oluştur haklarına sahip olması gerekir. bir veritabanı içindeki öğeler.

### <a name="sql-cache-dependency"></a>SQL önbellek bağımlılığı

ASP.NET çıktı önbelleğinin gelişmiş bir özelliği SQL Cache bağımlılığıdır. SQL önbellek bağımlılığı iki farklı işlem modunu destekler: tablo yoklamanın ASP.NET uygulamasını kullanan bir ve SQL Server 2005 sorgu bildirim özelliklerini kullanan ikinci bir mod. SQL kayıt aracı, işlemin tablo yoklama modunu yapılandırmak için kullanılabilir.

### <a name="session-state"></a>Oturum Durumu

Varsayılan olarak, oturum durumu değerleri ve bilgileri ASP.NET işlemi içinde bellekte depolanır. Alternatif olarak, oturum verilerini birden çok Web sunucusu tarafından paylaşılabilecek bir SQL Server veritabanında saklayabilirsiniz. SQL kayıt aracı ile oturum durumu için belirttiğiniz veritabanı zaten mevcut değilse, geçerli kullanıcının SQL Server veritabanları oluşturma ve bir veritabanı içinde şema öğeleri oluşturma haklarına sahip olması gerekir. Veritabanı varsa, geçerli kullanıcının mevcut veritabanında şema öğeleri oluşturmak için haklara sahip olması gerekir.

SQL Server oturum durumu veritabanını yüklemek için, ASPNET\_regsql. exe aracını çalıştırın ve komutla aşağıdaki bilgileri sağlayın:

- SQL Server örneğinin adı, **-S** seçeneği kullanılarak.
- SQL Server çalıştıran bir bilgisayarda veritabanı oluşturma iznine sahip olan bir hesabın oturum açma kimlik bilgileri. Şu anda oturum açmış olan kullanıcıyı kullanmak için **-E** seçeneğini kullanın veya bir parola belirtmek için- **P** seçeneğini Ile birlikte bir kullanıcı kimliği belirtmek için- **U** seçeneğini kullanın.
- Oturum durumu veritabanını eklemek için **-SSADD** komut satırı seçeneği.

Varsayılan olarak, ASPNET\_regsql. exe aracını kullanarak oturum durumu veritabanını SQL Server 2005 Express Sürüm çalıştıran bir bilgisayara yükleyebilirsiniz.

### <a name="the-aspnet-browser-registration-tool---aspnet_regbrowsersexe"></a>ASP.NET Browser kayıt aracı-ASPNET\_regbrowsers. exe

ASP.NET sürüm 1,1 ' de, Machine. config dosyası &lt;browserCaps&gt;adlı bir bölüm içeriyordu. Bu bölüm, bir normal ifadeye göre çeşitli tarayıcıların yapılandırmasını tanımlayan bir dizi XML girişi içeriyordu. ASP.NET sürüm 2,0 için yeni bir. TARAYıCı dosyası, XML girdileri kullanılarak belirli bir tarayıcının parametrelerini tanımlar. Yeni bir tarayıcıya yeni bir tarayıcı ekleyerek bilgi eklersiniz. , Sisteminizde%SystemRoot%\Microsoft.NET\Framework\version\CONFIG\Browsers adresinde bulunan klasöre tarayıcı dosyası.

Bir uygulama, her tarayıcı bilgisi gerektirdiğinde bir. config dosyası okumadığından, yeni bir oluşturabilirsiniz. TARAYıCı dosyası ve gerekli değişiklikleri derlemeye eklemek için ASPNET\_regbrowsers. exe ' yi çalıştırın. Bu, sunucunun yeni tarayıcı bilgilerine hemen erişmesini sağlar, böylece bilgileri almak için uygulamalarınızı kapatmanız gerekmez. Bir uygulama, geçerli HttpRequest 'in Browser özelliği aracılığıyla tarayıcı özelliklerine erişebilir.

ASPNET\_regbrowser. exe ' yi çalıştırırken aşağıdaki seçenekler mevcuttur:

| **Seçenek** | **Açıklama** |
| --- | --- |
| **-?** | Komut penceresinde ASPNET\_regbbrowsers. exe yardım metnini görüntüler. |
| **-ı** | Çalışma zamanı tarayıcı yetenekleri derlemesini oluşturur ve onu genel bütünleştirilmiş kod önbelleğine yüklenir. |
| **-u** | Çalışma zamanı tarayıcı yetenekleri derlemesini genel bütünleştirilmiş kod önbelleğinden kaldırır. |

## <a name="the-aspnet-compilation-tool---aspnet_compilerexe"></a>ASP.NET derleme aracı-ASPNET\_Compiler. exe

ASP.NET derleme aracı iki genel şekilde kullanılabilir: yerinde derleme ve dağıtım için derleme için bir hedef çıktı dizini belirtildiğinde.

### <a name="compiling-an-application-in-place"></a>[Bir uygulamayı yerinde derleme](https://msdn.microsoft.com/library/ms229863.aspx)

ASP.NET derleme aracı bir uygulamayı yerinde derleyebilir, yani uygulamaya birden çok istek yapma davranışını taklit eder ve böylece normal derlemeye neden olur. Önceden derlenmiş bir sitenin kullanıcıları, ilk istekte Sayfa derlenirken oluşan bir gecikme yaşmaz.

Bir siteyi yerinde önceden derlediğinizde, aşağıdaki öğeler geçerlidir:

- Site, dosyalarını ve dizin yapısını korur.
- Sunucusunda site tarafından kullanılan tüm programlama dilleri için derleyiciler olmalıdır.
- Herhangi bir dosya derleme başarısız olursa, tüm site derleme başarısız olur.

Ayrıca, yeni kaynak dosyaları ekledikten sonra bir uygulamayı yerinde yeniden derleyebilirsiniz. Araç, **-c** seçeneğini eklemediğiniz takdirde yalnızca yeni veya değiştirilmiş dosyaları derler.

> [!NOTE]
> İç içe geçmiş bir uygulama içeren bir uygulamanın derlenmesi, iç içe geçmiş uygulamayı derlemez. İç içe yerleştirilmiş uygulama ayrı olarak derlenmelidir.

### <a name="compiling-an-application-for-deployment"></a>[Dağıtım için bir uygulamayı derleme](https://msdn.microsoft.com/library/ms229863.aspx)

TARGETDIR parametresini belirterek dağıtım için bir uygulamayı (bir hedef konuma derleme) derleyebilirsiniz. TARGETDIR, Web uygulaması için son konum olabilir veya derlenen uygulama daha fazla dağıtılabilir. **-U** seçeneğini kullanmak, uygulamayı yeniden derlemeden derlenen uygulamadaki belirli dosyalarda değişiklik yapabilmeniz için bu şekilde uygulamayı derler. ASPNET\_Compiler. exe, statik ve dinamik dosya türleri arasında ayrım yapar ve sonuçta elde edilen uygulamayı oluştururken bunları farklı işler.

- Statik dosya türleri, adı. css,. gif,. htm,. html,. jpg,. js vb. gibi uzantılara sahip olan dosyalar gibi ilişkili bir derleyici veya derleme sağlayıcısına sahip değildir. Bu dosyalar yalnızca hedef konuma kopyalanır ve bu, dizin yapısındaki göreli yerleri korunur.
- Dinamik dosya türleri,. asax,. ascx,. ashx,. aspx,. Browser,. Master vb. gibi ASP.NET özgü dosya adı uzantılarına sahip dosyalar da dahil olmak üzere, ilişkili bir derleyici veya yapı sağlayıcısına sahip olanlardır. ASP.NET derleme aracı bu dosyalardan derleme oluşturur. **-U** seçeneği atlanırsa, araç dosya adı uzantısına sahip dosyalar da oluşturur. Özgün kaynak dosyaları derlemelerinden eşleyen DERLENMIŞ. Uygulama kaynağının dizin yapısının korunduğundan emin olmak için, araç, Hedef uygulamadaki ilgili konumlarda yer tutucu dosyaları oluşturur.

Derlenen uygulamanın içeriğinin değiştirilemeyeceğini göstermek için **-u** seçeneğini kullanmanız gerekir. Aksi takdirde, sonraki değişiklikler yok sayılır veya çalışma zamanı hatalarına neden olur.

Aşağıdaki tabloda, **-u** seçeneği dahil edildiğinde ASP.NET derleme aracının farklı dosya türlerini nasıl işlediği açıklanmaktadır.

| **Dosya türü** | **Derleyici eylemi** |
| --- | --- |
| .ascx, .aspx, .master | Bu dosyalar, hem arka plan kod dosyalarını hem de &lt;betiği runat = "Server"&gt; öğelerine eklenen kodları içeren biçimlendirme ve kaynak koduna ayrılır. Kaynak kodu, bir karma algoritmadan türetilmiş adlara sahip derlemeler halinde derlenir ve derlemeler bin dizinine yerleştirilir. Herhangi bir satır içi kod, diğer bir deyişle, **&lt;%** ve **%&gt;** köşeli ayraç arasına alınmış kod, biçimlendirme ve derlenmiyor. Biçimlendirmeyi içerecek ve karşılık gelen çıkış dizinlerine yerleştirilecek kaynak dosyalarla aynı ada sahip yeni dosyalar oluşturulur. |
| . ashx,. asmx | Bu dosyalar derlenmez ve, derleme ve derlenmediği gibi çıkış dizinlerine taşınır. İşleyici kodu derlenmek isterseniz, kodu App\_Code dizinindeki kaynak kodu dosyalarına yerleştirin. |
| . cs,. vb,. JSL,. cpp (daha önce listelenen dosya türleri için arka plan kod dosyalarını dahil değil) | Bu dosyalar derlenir ve bunlara başvuran derlemelerdeki bir kaynak olarak eklenir. Kaynak dosyalar çıkış dizinine kopyalanmaz. Bir kod dosyasına başvurulmuyorsa, derlenmez. |
| Özel dosya türleri | Bu dosyalar derlenmiyor. Bu dosyalar ilgili çıkış dizinlerine kopyalanır. |
| Uygulama\_kodu alt dizinindeki kaynak kodu dosyaları | Bu dosyalar Derlemelerle derlenir ve bin dizinine yerleştirilir. |
| Uygulama\_GlobalResources alt dizinindeki. resx ve. Resource dosyaları | Bu dosyalar Derlemelerle derlenir ve bin dizinine yerleştirilir. Ana çıkış dizini altında hiçbir uygulama\_GlobalResources alt dizini oluşturulmaz ve kaynak dizinde bulunan hiçbir. resx veya. resources dosyası çıkış dizinlerine kopyalanmaz. |
| App\_LocalResources alt dizinindeki. resx ve. Resource dosyaları | Bu dosyalar derlenmez ve ilgili çıkış dizinlerine kopyalanır. |
| Uygulama\_Tema alt dizinindeki. Skin dosyaları | . Skin dosyaları ve statik Tema dosyaları derlenmez ve ilgili çıkış dizinlerine kopyalanır. |
| . Browser Web. config statik dosya türleri derlemeleri bin dizininde zaten var | Bu dosyalar, çıkış dizinlerine, olarak kopyalanır. |

Aşağıdaki tabloda, **-u** seçeneği atlandığında ASP.NET derleme aracının farklı dosya türlerini nasıl işlediği açıklanmaktadır.

| **Dosya türü** | **Derleyici eylemi** |
| --- | --- |
| .aspx, .asmx, .ashx, .master | Bu dosyalar, hem arka plan kod dosyalarını hem de &lt;betiği runat = "Server"&gt; öğelerine eklenen kodları içeren biçimlendirme ve kaynak koduna ayrılır. Kaynak kodu, bir karma algoritmadan türetilen adlarla Derlemelerle derlenir. Elde edilen derlemeler bin dizinine yerleştirilir. Herhangi bir satır içi kod, diğer bir deyişle, **&lt;%** ve **%&gt;** köşeli ayraç arasına alınmış kod, biçimlendirme ve derlenmiyor. Derleyici, kaynak dosyalarla aynı ada sahip biçimlendirmeyi içeren yeni dosyalar oluşturur. Bu elde edilen dosyalar bin dizinine yerleştirilir. Derleyici Ayrıca, kaynak dosyalarla aynı ada ancak uzantıya sahip dosyalar da oluşturur. Eşleme bilgilerini içeren DERLENMIŞ. İçin. DERLENEN dosyalar, kaynak dosyaların özgün konumuna karşılık gelen çıkış dizinlerine yerleştirilir. |
| .ascx | Bu dosyalar, biçimlendirme ve kaynak koduna bölünür. Kaynak kodu Derlemelerle derlenir ve bir karma algoritmadan türetilen adlarla bin dizinine yerleştirilir. Hiçbir işaretleme dosyası oluşturulmaz. |
| . cs,. vb,. JSL,. cpp (daha önce listelenen dosya türleri için arka plan kod dosyalarını dahil değil) | . Ascx,. ashx veya. aspx dosyalarından oluşturulan derlemelerin başvurduğu kaynak kodu derlemeler halinde derlenir ve bin dizinine yerleştirilir. Kopyalanan kaynak dosya yok. |
| Özel dosya türleri | Bu dosyalar dinamik dosyalar gibi derlenir. Temel aldığı dosyanın türüne bağlı olarak, derleyici eşleme dosyalarını çıkış dizinlerine yerleştirebilir. |
| Uygulama\_kodu alt dizinindeki dosyalar | Bu alt dizindeki kaynak kodu dosyaları Derlemelerle derlenir ve bin dizinine yerleştirilir. |
| Uygulama\_GlobalResources alt dizinindeki dosyalar | Bu dosyalar Derlemelerle derlenir ve bin dizinine yerleştirilir. Ana çıkış dizini altında hiçbir uygulama\_GlobalResources alt dizini oluşturulmaz. Yapılandırma dosyası appliesTo = "All",. resx ve. resources dosyalarını belirtiyorsa çıkış dizinlerine kopyalanır. Bunlar bir [BuildProvider](https://msdn.microsoft.com/library/system.web.configuration.buildprovider.aspx)tarafından başvuruluyorsa kopyalanmaz. |
| App\_LocalResources alt dizinindeki. resx ve. Resource dosyaları | Bu dosyalar benzersiz adlara sahip derlemeler halinde derlenir ve bin dizinine yerleştirilir. Çıkış dizinlerine hiçbir. resx veya. kaynak dosyası kopyalanmaz. |
| Uygulama\_Tema alt dizinindeki. Skin dosyaları | Temalar Derlemelerle derlenir ve bin dizinine yerleştirilir. Saplama dosyaları. Skin dosyaları için oluşturulur ve ilgili çıkış dizinine yerleştirilir. Statik dosyalar (örneğin,. css) çıkış dizinlerine kopyalanır. |
| . Browser Web. config statik dosya türleri derlemeleri bin dizininde zaten var | Bu dosyalar, çıkış dizinine, olarak kopyalanır. |

### <a name="fixed-assembly-names"></a>[Sabit derleme adları](https://msdn.microsoft.com/library/ms229863.aspx##)

MSI Windows Installer kullanarak bir Web uygulaması dağıtma gibi bazı senaryolar, tutarlı dosya adları ve içerikleri kullanımını ve güncelleştirmelerin derlemelerini veya yapılandırma ayarlarını belirlemek için tutarlı dizin yapılarını gerektirir. Bu durumlarda, ASP.NET derleme aracının derlemeler halinde birden çok sayfanın derlendiğini kullanmak yerine her kaynak dosya için bir derlemeyi derlenmesi gerektiğini belirtmek için **-FixedNames** seçeneğini kullanabilirsiniz. Bu çok sayıda derlemeye yol açabilir, bu nedenle ölçeklenebilirlik ile ilgileniyorlarsa bu seçeneği dikkatli bir şekilde kullanmanız gerekir.

### <a name="strong-name-compilation"></a>[Tanımlayıcı ad derlemesi](https://msdn.microsoft.com/library/ms229863.aspx##)

**-APTCA**, **-delaysign**, **-keycontainer** ve **-keyfile** seçenekleri, yalnızca [tanımlayıcı ad Aracı (sn. exe)](https://msdn.microsoft.com/library/k5b5tt23.aspx) kullanmadan kesin olarak adlandırılmış derlemeler oluşturmak için, ASPNET\_Compiler. exe ' yi kullanabilmeniz için sağlanır. Bu seçenekler sırasıyla **AllowPartiallyTrustedCallersAttribute**, **assemblydelaytifttribute**, **AssemblyKeyNameAttribute**ve **AssemblyKeyFileAttribute**öğesine karşılık gelir.

Bu özniteliklerin tartışması, bu kursun kapsamı dışındadır.

## <a name="labs"></a>Labs

Aşağıdaki laboratuvarların her biri, önceki laboratuvarlarda oluşturulur. Bunları sırasıyla yapmanız gerekir.

## <a name="lab-1-using-the-configuration-api"></a>Lab 1: Yapılandırma API 'sini kullanma

1. *Mod9lab*adlı yeni bir Web sitesi oluşturun.
2. Siteye yeni bir Web yapılandırma dosyası ekleyin.
3. Aşağıdakileri Web. config dosyasına ekleyin:

[!code-xml[Main](configuration-and-instrumentation/samples/sample14.xml)]

Bu, Web. config dosyasına değişiklikleri kaydetme izninizin olmasını sağlar.

1. Default. aspx dosyasına yeni bir etiket denetimi ekleyin ve KIMLIĞI **Lbldebugstatus**olarak değiştirin.
2. Default. aspx öğesine yeni bir düğme denetimi ekleyin.
3. Düğme denetiminin KIMLIĞINI **Btntoggledebug** ve metin olarak değiştirip **hata ayıklama durumuna geçiş yapın**.
4. Default. aspx dosyasının arka plan kod dosyası için kod görünümünü açın ve **System. Web. Configuration** için bir **using** ifadesini aşağıdaki şekilde ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample15.cs)]

1. Sınıfa ve aşağıda gösterildiği gibi bir sayfa\_Init yöntemine iki özel değişken ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample16.cs)]

1. Aşağıdaki kodu sayfa\_yüküne ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample17.cs)]

1. Default. aspx ' i kaydedin ve tarayın. Etiket denetiminin geçerli hata ayıklama durumunu görüntülediğini unutmayın.
2. Tasarımcıda düğme denetimine çift tıklayın ve düğme denetiminin Click olayına aşağıdaki kodu ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample18.cs)]

1. Default. aspx ' i kaydedin ve tarayın ve düğmesine tıklayın.
2. Her düğme tıkladıktan sonra Web. config dosyasını açın ve &lt;derleme&gt; bölümünde **Debug** özniteliğini gözlemleyin.

## <a name="lab-2-logging-application-restarts"></a>Laboratuvar 2: uygulama yeniden başlatmaları günlüğe kaydetme

Bu laboratuvarda, Olay Görüntüleyicisi uygulama kapatmaları, başlatmalar ve yeniden derlemeler için günlüğe kaydetmeyi açıp vereceğiniz bir kod oluşturacaksınız.

1. Default. aspx ' e bir DropDownList ekleyin ve KIMLIĞI ddlLogAppEvents olarak değiştirin.
2. DropDownList için **AutoPostBack** özelliğini **true**olarak ayarlayın.
3. DropDownList için Items koleksiyonuna üç öğe ekleyin. İlk öğe için **metin** seçin ve değer-1 ' i *seçin* . İkinci öğenin **metin** ve **değerini** **doğru** ve üçüncü öğe öğesinin **metin** ve **değerini** **false**yapın.
4. Default. aspx öğesine yeni bir etiket ekleyin. KIMLIĞI **Lbllogappevents**olarak değiştirin.
5. Default. aspx için arka plan kod görünümünü açın ve aşağıda gösterildiği gibi HealthMonitoringSection türünde bir değişken için yeni bir bildirim ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample19.cs)]

1. Aşağıdaki kodu sayfa\_Init 'teki mevcut koda ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample20.cs)]

1. DropDownList 'e çift tıklayın ve aşağıdaki kodu SelectedIndexChanged olayına ekleyin:

[!code-csharp[Main](configuration-and-instrumentation/samples/sample21.cs)]

1. Default. aspx ' i inceleyin.
2. Açılan menüyü **yanlış**olarak ayarlayın.
3. Olay Görüntüleyicisi uygulama günlüğünü temizleyin.
4. Uygulamanın hata ayıklama özniteliğini değiştirmek için düğmeye tıklayın.
5. Olay Görüntüleyicisi uygulama günlüğünü yenileyin. 

    1. Günlüğe kaydedilen olaylar var mı?
    2. Neden veya neden değil?
6. Açılan menüyü doğru olarak ayarlayın **.**
7. Uygulamanın hata ayıklama özniteliğini değiştirmek için düğmeye tıklayın.
8. Olay Görüntüleyicisi uygulama oturumunu yenileyin. 

    1. Günlüğe kaydedilen olaylar var mı?
    2. Uygulama kapatmasının nedeni neydi?
9. Günlük kaydını açıp kapatmayı deneyin ve Web. config dosyasında yapılan değişikliklere bakın.

## <a name="more-information"></a>Daha Fazla Bilgi:

ASP.NET 2.0 'ın sağlayıcı modeli, yalnızca uygulama araçları değil, diğer birçok kullanım için üyelik, profiller vb. için kendi sağlayıcılarınızı oluşturmanızı sağlar. Uygulama olaylarını bir metin dosyasına kaydetmek için özel bir sağlayıcı yazma hakkında ayrıntılı bilgi için [Bu bağlantıyı](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/ASPNETProvMod_Prt6.asp)ziyaret edin.
