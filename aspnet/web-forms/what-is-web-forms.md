---
uid: web-forms/what-is-web-forms
title: Web Forms nedir? | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 5fa1daf9-1161-4cfa-bd4c-658f48b2c229
msc.legacyurl: /web-forms/what-is-web-forms
msc.type: content
ms.openlocfilehash: 19be419c499759713971a6c77674c924867d1bbc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636579"
---
# <a name="what-is-web-forms"></a>Web Forms nedir?

ASP.NET Web Forms, ASP.NET Web uygulaması çerçevesinin bir parçasıdır ve [Visual Studio 'ya](https://www.asp.net/downloads)dahildir. ASP.NET Web uygulamaları oluşturmak için kullanabileceğiniz dört programlama modelinden biridir, diğerleri ASP.NET MVC, ASP.NET Web sayfaları ve ASP.NET tek sayfalı uygulamalardır.

Web Forms kullanıcılarınızın tarayıcılarını kullanmasını talep eden sayfalardır. Bu sayfalar, HTML, istemci betiği, sunucu denetimleri ve sunucu kodu birleşimi kullanılarak yazılabilir. Kullanıcılar bir sayfa talep verdiğinde, bu, altyapı tarafından sunucu üzerinde derlenir ve yürütülür ve ardından Framework, tarayıcının oluşturabileceği HTML işaretlemesini oluşturur. Bir ASP.NET Web Forms sayfası, kullanıcıya herhangi bir tarayıcı veya istemci cihazında bilgi sunar.

Visual Studio 'yu kullanarak ASP.NET Web Forms oluşturabilirsiniz. Visual Studio tümleşik geliştirme ortamı (IDE), Web Forms sayfanızı düzenlemek için sunucu denetimlerini sürükleyip bırakmanızı sağlar. Daha sonra sayfadaki veya sayfanın kendisi için özellikleri, yöntemleri ve olayları kolayca ayarlayabilirsiniz. Bu özellikler, Yöntemler ve olaylar Web sayfasının davranışını, görünümünü ve hisyi tanımlamak için kullanılır. Sayfanın mantığını işlemek üzere sunucu kodu yazmak için Visual Basic veya C#gibi bir .net dili kullanabilirsiniz.

> [!NOTE] 
> 
> ASP.NET ve Visual Studio belgeleri birçok sürümü kapsar. Önceki sürümlerden özellikleri vurgulayan konular, en son sürümleri kullanarak geçerli görevleriniz ve senaryolarınız için yararlı olabilir.

**ASP.NET Web Forms:** 

- Sunucu üzerinde çalışan kodun tarayıcı veya istemci cihazına dinamik olarak Web sayfası çıktısı oluşturduğu Microsoft ASP.NET teknolojisine göre.
- Herhangi bir tarayıcı veya mobil cihazla uyumludur. Bir ASP.NET Web sayfası, stiller, düzen ve benzeri özellikler için doğru tarayıcıyla uyumlu HTML 'yi otomatik olarak işler.
- Microsoft Visual Basic ve Microsoft Visual C#gibi .NET ortak dil çalışma zamanı tarafından desteklenen herhangi bir dille uyumludur.
- Microsoft .NET Framework üzerine kurulmuştur. Bu, yönetilen ortam, tür güvenliği ve devralma dahil olmak üzere Framework 'ün tüm avantajlarını sağlar.
- Kullanıcı tarafından oluşturulan ve üçüncü taraf denetimleri bunlara ekleyebileceğiniz için esnek.

**ASP.NET Web Forms teklifi:** 

- Uygulama mantığındaki HTML ve diğer kullanıcı arabirimi kodu ayrımı.
- Veri erişimi de dahil olmak üzere ortak görevler için zengin bir sunucu denetimi paketi.
- Harika araç desteğiyle güçlü veri bağlama.
- Tarayıcıda yürütülen istemci tarafı komut dosyası desteği.
- Yönlendirme, güvenlik, performans, uluslararası hale getirme, test, hata ayıklama, hata işleme ve durum yönetimi dahil olmak üzere çeşitli diğer yetenekler için destek.

## <a name="aspnet-web-forms-helps-you-overcome-challenges"></a>ASP.NET Web Forms sorunları aşmanıza yardımcı olur

Web uygulaması programlama, genellikle geleneksel istemci tabanlı uygulamaları programlarken ortaya çıkan güçlükleri sunar. Aralarındaki sorunlar şunlardır:

- **Zengin bir Web Kullanıcı arabirimi uygulama** -özellikle sayfanın karmaşık bir yerleşimi, büyük miktarda dinamik içerik ve tam özellikli kullanıcı etkileşimli nesneleri varsa temel HTML olanaklarını kullanarak bir kullanıcı arabirimi tasarlamak ve uygulamak zor olabilir.
- **İstemci ve sunucu ayrımı** -bir Web uygulamasında, istemci (tarayıcı) ve sunucu, genellikle farklı bilgisayarlarda (ve hatta farklı işletim sistemlerinde) çalışan farklı programlardır. Sonuç olarak, uygulama paylaşımının iki yarısı çok az bilgi; Kullanıcılar iletişim kurabilir, ancak genellikle basit bilgilerin yalnızca küçük öbeklerini değiş tokuş edebilir.
- **Durum bilgisiz yürütme** -bir Web sunucusu bir sayfa için istek aldığında, sayfayı bulur, işler, tarayıcıya gönderir ve sonra tüm sayfa bilgilerini atar. Kullanıcı aynı sayfayı yeniden isterse, sunucu tüm diziyi yineler, sayfanın sıfırdan yeniden işlenmesini ister. Başka bir yöntem de, bir sunucuda işlendiği sayfaların belleği yoktur — sayfa durumsuz olur. Bu nedenle, bir uygulamanın bir sayfa hakkında bilgi tutması gerekiyorsa, durum bilgisiz doğası bir sorun haline gelebilir.
- **Bilinmeyen istemci özellikleri** -birçok durumda Web uygulamalarına farklı tarayıcılar kullanan birçok kullanıcı erişebilir. Tarayıcılar farklı yeteneklere sahiptir ve bunların tümünde eşit olarak çalışacak bir uygulama oluşturmayı zorlaştırır.
- **Veri erişimiyle Ilgili zorluklar** -geleneksel Web uygulamalarında veri kaynağına okuma ve yazma karmaşık ve kaynak kullanımı yoğun olabilir.
- **Ölçeklenebilirlik Ile karmaşıklıklar** -birçok durumda, mevcut yöntemlerle tasarlanan Web uygulamaları, uygulamanın çeşitli bileşenleri arasında uyumluluk olmaması nedeniyle ölçeklenebilirlik hedeflerini karşılamaz. Bu genellikle ağır büyüme döngüsünün altındaki uygulamalar için yaygın bir hata noktasıdır.

Web uygulamaları için bu zorlukların karşılanmasıyla ilgili önemli ölçüde zaman ve çaba gerekebilir. ASP.NET Web Forms ve ASP.NET Framework bu zorlukları aşağıdaki yollarla ele alır:

- **Sezgisel, tutarlı nesne modeli** -ASP.net Page Framework, formlarınızı ayrı istemci ve sunucu parçaları olarak değil, birim olarak düşünmenizi sağlayan bir nesne modeli sunar. Bu modelde, sayfa öğelerinin özelliklerini ayarlama ve olaylara yanıt verme özelliği de dahil olmak üzere, sayfayı geleneksel Web uygulamalarından daha sezgisel bir şekilde programlayabilirsiniz. Ayrıca, ASP.NET Server denetimleri, HTML sayfasının fiziksel içeriğinden ve tarayıcı ile sunucu arasındaki doğrudan etkileşiminden bir soyutlama niteliğindedir. Genel olarak, sunucu denetimlerini, bir istemci uygulamasındaki denetimlerle çalışma gibi kullanabilirsiniz ve denetimleri ve bunların içeriklerini sunmak ve işlemek için HTML oluşturmayı düşünmek zorunda değildir.
- **Olay odaklı programlama modeli** -ASP.NET Web Forms Web uygulamalarına, istemci ya da sunucuda gerçekleşen olaylar için olay işleyicilerini yazma hakkında tanıdık bir model getirir. ASP.NET Page Framework, bu modeli, istemci üzerinde bir olayı yakalamak, onu sunucusuna iletmek ve uygun yöntemi çağırmak için otomatik ve sizin görecağından, temel alınan bir olayın bulunduğu bir şekilde soyutlar. Sonuç, olay odaklı geliştirmeyi destekleyen açık ve kolayca yazılmış bir kod yapısıdır.
- **Sezgisel durum yönetimi** -ASP.net Page Framework, sayfanızın ve denetimlerin durumunu koruma görevini otomatik olarak işler ve uygulamaya özgü bilgilerin durumunu korumak için size açık yollar sunar. Bu, sunucu kaynaklarının yoğun kullanımı olmadan gerçekleştirilir ve tarayıcıya tanımlama bilgisi göndermeksizin veya ile uygulanabilir.
- **Tarayıcıdan bağımsız uygulamalar** -ASP.net Page Framework, sunucuda tüm uygulama mantığını oluşturmanıza olanak tanıdığından, tarayıcılarda farklılıklar için açıkça kod oluşturma gereğini ortadan kaldırır. Ancak, daha iyi performans ve daha zengin bir istemci deneyimi sağlamak için istemci tarafı kodu yazarak tarayıcıya özgü özelliklerden yararlanmanızı sağlar.
- **.NET Framework ortak dil çalışma zamanı desteği** -ASP.net page Framework .NET Framework oluşturulmuştur, bu nedenle tüm Framework tüm ASP.NET uygulamaları tarafından kullanılabilir. Uygulamalarınız, çalışma zamanı ile uyumlu olan herhangi bir dilde yazılabilir. Ayrıca, veri erişimi, ADO.NET dahil olmak üzere .NET Framework tarafından belirtilen veri erişim altyapısı kullanılarak basitleştirilmiştir.
- **Ölçeklenebilir sunucu performansını .NET Framework** -ASP.net Page Framework, Web uygulamanızı tek işlemcili bir bilgisayardan çoklu bilgisayarlı bir Web grubuna ve uygulamanın mantığındaki karmaşık değişiklikler yapmadan ölçeklendirmenize olanak sağlar.

## <a name="features-of-aspnet-web-forms"></a>ASP.NET Web Forms Özellikleri

- **Sunucu denetimleri**-ASP.NET Web sunucusu denetimleri, sayfa istendiğinde çalışan ASP.NET Web sayfalarındaki nesnelerdir ve tarayıcıya biçimlendirme işlemi yapılır. Birçok Web sunucusu denetimi, düğmeler ve metin kutuları gibi tanıdık HTML öğelerine benzerdir. Diğer denetimler, Takvim denetimleri gibi karmaşık davranışları ve veri kaynaklarına bağlanmak ve verileri göstermek için kullanabileceğiniz denetimleri kapsayabilir.
- **Ana sayfalar**-ASP.NET ana sayfaları, uygulamanızdaki sayfalar için tutarlı bir düzen oluşturmanızı sağlar. Tek bir ana sayfa, uygulamanızdaki tüm sayfalar (veya bir sayfa grubu) için istediğiniz görünüm ve standart davranışı tanımlar. Daha sonra, göstermek istediğiniz içeriği içeren bireysel içerik sayfaları oluşturabilirsiniz. Kullanıcılar içerik sayfalarını istediklerinde, ana sayfanın yerleşimini içerik sayfasındaki içerikle birleştiren çıktıyı oluşturmak için ana sayfayla birleşir.
- **Data-ASP.net Ile çalışmak**, verileri depolamak, almak ve görüntülemek için birçok seçenek sunar. ASP.NET Web Forms uygulamasında, tablo ve metin kutuları ve açılan listeler gibi Web sayfası kullanıcı arabirimi öğelerindeki sunumu veya veri girişini otomatikleştirmek için veri bağlantılı denetimleri kullanırsınız.
- **Üyelik**-ASP.NET Identity kullanıcılarınızın kimlik bilgilerini uygulama tarafından oluşturulan bir veritabanında depolar. Kullanıcılarınız oturum açarken, uygulamayı veritabanını okuyarak kimlik bilgilerini doğrular. Projenizin *Hesap* klasörü, üyelik: kaydolma, oturum açma, parolayı değiştirme ve erişimi yetkilendirme gibi çeşitli bölümleri uygulayan dosyaları içerir. Ayrıca, ASP.NET Web Forms OAuth ve OpenID 'yi destekler. Bu kimlik doğrulama geliştirmeleri, kullanıcıların, Facebook, Twitter, Windows Live ve Google gibi hesapların mevcut kimlik bilgilerini kullanarak sitenizde oturum açmasına olanak tanır. Varsayılan olarak, şablon, Web için Visual Studio Express 2013 ile birlikte sunulan geliştirme veritabanı sunucusu olan SQL Server Express LocalDB örneğinde varsayılan veritabanı adı kullanarak bir üyelik veritabanı oluşturur.
- **Istemci betiği ve Istemci çerçeveleri**-ASP.NET Web form sayfalarına istemci komut dosyası işlevselliği ekleyerek ASP.net 'in sunucu tabanlı özelliklerini geliştirebilirsiniz. Kullanıcılara daha zengin ve daha hızlı yanıt veren bir kullanıcı arabirimi sağlamak için istemci komut dosyası kullanabilirsiniz. Ayrıca, bir sayfa tarayıcıda çalışırken Web sunucusuna zaman uyumsuz çağrılar yapmak için istemci betiği de kullanabilirsiniz.
- **Yönlendirme**-URL yönlendirmesi, bir uygulamayı fiziksel dosyalarla eşlenmez Istek URL 'lerini kabul edecek şekilde yapılandırmanıza olanak tanır. İstek URL 'si, bir kullanıcının Web sitenizde bir sayfa bulmak için tarayıcılarına girdiği URL 'dir. Kullanıcılara anlam açısından anlamlı olan ve arama motoru iyileştirmesi (SEO) konusunda yardımcı olabilecek URL 'Leri tanımlamak için yönlendirmeyi kullanırsınız.
- **Durum yönetimi**-ASP.NET Web Forms, hem sayfa temelinde hem de uygulama genelinde verileri korumanıza yardımcı olan çeşitli seçenekler içerir.
- **Güvenlik**-daha güvenli bir uygulama geliştirmesinin önemli bir bölümü, BT 'nin tehditleri öğrenmektir. Microsoft tehditleri kategorilere ayırmak için bir yol geliştirmiştir: sahtekarlık, Izinsiz değişiklik, geri çevirme, bilgilerin açıklanması, hizmet reddi, ayrıcalık yükselmesi (Ilerleme). ASP.NET Web Forms ' de, ASP.NET Web Forms çeşitli güvenlik davranışlarını özelleştirmenizi sağlayan genişletilebilirlik noktaları ve yapılandırma seçenekleri ekleyebilirsiniz.
- **Performans**performansı, başarılı bir Web sitesinde veya projede önemli bir faktör olabilir. ASP.NET Web Forms, sayfa ve sunucu denetim işleme, durum yönetimi, veri erişimi, uygulama yapılandırması ve yükleme ve verimli kodlama uygulamalarıyla ilgili performansı değiştirmenize olanak sağlar.
- **Uluslararası duruma getirme**-ASP.NET Web Forms, tarayıcı için tercih edilen dil ayarına göre veya kullanıcının açık dil seçimine bağlı olarak içerik ve diğer verileri elde eden Web sayfaları oluşturmanızı sağlar. İçerik ve diğer veriler kaynak olarak adlandırılır ve bu veriler kaynak dosyalarında veya diğer kaynaklarda depolanabilir. Bir ASP.NET Web Forms sayfasında, denetim değerlerini kaynaklardan almak için denetimleri yapılandırırsınız. Çalışma zamanında, kaynak ifadeleri uygun yerelleştirilmiş kaynak dosyasındaki kaynaklarla değiştirilmiştir.
- **Hata ayıklama ve hata işleme**-ASP.NET, Web Forms uygulamanızda oluşabilecek sorunları tanılamanıza yardımcı olacak özellikler içerir. Uygulamalarınızın etkili bir şekilde derlenmesi ve çalışması için ASP.NET Web Forms içinde hata ayıklama ve hata işleme iyi desteklenir.
- **Dağıtım ve barındırma**; Visual Studio, ASP.net, Azure ve ııs, Web Forms uygulamanızı dağıtma ve barındırma sürecinde size yardımcı olacak araçlar sağlar.

## <a name="deciding-when-to-create-a-web-forms-application"></a>Web Forms uygulamasının ne zaman oluşturulacağı karar verme

ASP.NET Web Forms modelini veya ASP.NET MVC çerçevesi gibi başka bir modeli kullanarak bir Web uygulaması uygulayıp uygulamamalısınız. MVC çerçevesi, Web Forms modelini değiştirmez; Web uygulamaları için ikisinden birini kullanabilirsiniz. Belirli bir Web sitesi için Web Forms modeli veya MVC çerçevesini kullanmaya karar vermeden önce her yaklaşımın avantajlarına ağırlık koyun.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Web Forms Tabanlı Web Uygulamasının Avantajları

Web Forms tabanlı çerçeve aşağıdaki avantajları sağlamaktadır:

- İş dalına özel Web uygulaması geliştirmeleri için faydalı olan, HTTP üzerindeki durumu koruyan olay modelini destekler. Web Forms tabanlı uygulama, yüzlerce sunucu denetiminde desteklenen düzinelerce olayı sağlar.
- Belirli sayfalara işlevsellik ekleyen Page Controller örüntüsünü kullanır. Daha fazla bilgi için MSDN Web sitesindeki [sayfa denetleyicisi](https://go.microsoft.com/fwlink/?LinkId=106359 "Sayfa denetleyicisi") ' ne bakın.
- Durum bilgilerini yönetmeyi kolaylaştırmak için görünüm durumunu veya sunucu tabanlı formları kullanır.
- Hızlı uygulama geliştirme için çok sayıdaki mevcut bileşenden faydalanmak isteyen küçük Web geliştiricileri ve tasarımcıları ekipleri için uygundur.
- Genel olarak, uygulama geliştirme için daha az karmaşıktır çünkü bileşenler ( **sayfa** sınıfı, denetimler, vb.) sıkı bir şekilde tümleşiktir ve genellikle MVC modelinden daha az kod gerektirir.

### <a name="advantages-of-an-mvc-based-web-application"></a>MVC Tabanlı Web Uygulamasının Avantajları

ASP.NET MVC çerçevesi aşağıdaki avantajları sağlamaktadır:

- Uygulamayı modele, görünüme ve denetleyiciye bölerek karışıklığın yönetilmesini kolaylaştırır.
- Görünüm durumu veya sunucu tabanlı formlar kullanmaz. Bu, uygulamanın davranışı üzerinde tam denetim sağlamak isteyen geliştiriciler için MVC çerçevesini ideal kılar.
- Tek bir denetleyici üzerinden Web uygulama isteklerini işleyen bir Front Controller örüntüsü kullanır. Zengin yönlendirme altyapısını destekleyen bir uygulama tasarlamanızı sağlar. Daha fazla bilgi için bkz. MSDN Web sitesindeki [ön denetleyici](https://go.microsoft.com/fwlink/?LinkId=106357 "Ön denetleyici") .
- Teste dayalı geliştirme (TDD) için daha iyi destek sunar.
- Büyük geliştiriciler ve uygulama davranışı üzerinde yüksek düzeyde denetim gerektiren web tasarımcıları tarafından desteklenen Web uygulamaları için iyi sonuç verir.
