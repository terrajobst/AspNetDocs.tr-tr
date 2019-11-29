---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-cs
title: Forms kimlik doğrulaması yapılandırması ve gelişmiş konularC#() | Microsoft Docs
author: rick-anderson
description: Bu öğreticide çeşitli form kimlik doğrulama ayarlarını inceleyeceğiz ve bunları Forms öğesi aracılığıyla nasıl değiştireceğiniz gösterilir. Bu, ayrıntılı bir şekilde kuyruğa alınır...
ms.author: riande
ms.date: 01/14/2008
ms.assetid: b9c29865-a34e-48bb-92c0-c443a72cb860
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-cs
msc.type: authoredcontent
ms.openlocfilehash: b296f31da1c73df97175d94402b4d618df425d8d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74579254"
---
# <a name="forms-authentication-configuration-and-advanced-topics-c"></a>Forms Kimlik Doğrulaması Yapılandırması ve Gelişmiş Konular (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_cs.pdf)

> Bu öğreticide çeşitli form kimlik doğrulama ayarlarını inceleyeceğiz ve bunları Forms öğesi aracılığıyla nasıl değiştireceğiniz gösterilir. Bu, Forms kimlik doğrulama biletinin zaman aşımı değerini özelleştirmeye, özel bir URL (login. aspx yerine Sign. aspx gibi) ve tanımlama bilgisi olmayan formların kimlik doğrulama biletlerine sahip bir oturum açma sayfası kullanmaya ilişkin ayrıntılı bir bakış oluşturur.

## <a name="introduction"></a>Giriş

[Önceki öğreticide](an-overview-of-forms-authentication-cs.md) , kimliği doğrulanmış ve anonim kullanıcılar için farklı içerikleri görüntülemek üzere Web. config 'deki yapılandırma ayarlarını belirtmekten ASP.NET uygulamasında form kimlik doğrulaması uygulamak için gereken adımlara baktık. &lt;Authentication&gt; öğesinin mode özniteliğini Forms olarak ayarlayarak, Web sitesini Forms kimlik doğrulamasını kullanacak şekilde yapılandırdığımızda hatırlayın. &lt;Authentication&gt; öğesi, isteğe bağlı olarak bir &lt;Forms&gt; alt öğesi içerebilir ve bu, bir form kimlik doğrulama ayarları sınıfısına sahip olabilir.

Bu öğreticide çeşitli form kimlik doğrulama ayarlarını inceleyeceğiz ve &lt;Forms&gt; öğesi aracılığıyla nasıl değiştireceğiniz gösterilir. Bu, Forms kimlik doğrulama biletinin zaman aşımı değerini özelleştirmeye, özel bir URL (login. aspx yerine Sign. aspx gibi) ve tanımlama bilgisi olmayan formların kimlik doğrulama biletlerine sahip bir oturum açma sayfası kullanmaya ilişkin ayrıntılı bir bakış oluşturur. Ayrıca, form kimlik doğrulama biletini daha yakından inceleyerek, Bilet verilerinin incelemeden ve izinsiz değişikliklere karşı güvende olduğundan emin olmak için ASP.NET önlemler görürsünüz. Son olarak, form kimlik doğrulama biletinde ek kullanıcı verilerinin nasıl depolanacağını ve bu verilerin özel bir asıl nesne üzerinden nasıl modellendirilebileceklerini inceleyeceğiz.

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>Adım 1: &lt;formları&gt; yapılandırma ayarlarını Inceleme

ASP.NET ' deki Forms kimlik doğrulama sistemi, uygulama temelinde özelleştirilebilen bir dizi yapılandırma ayarı sunar. Bu, aşağıdaki gibi ayarları içerir: form kimlik doğrulama anahtarının yaşam süresi; Bilet için ne tür bir koruma uygulanır; tanımlama bilgisi olmayan kimlik doğrulama biletlerinin altında hangi koşullarda kullanılır? oturum açma sayfasının yolu; ve diğer bilgiler. Varsayılan değerleri değiştirmek için, [&lt;kimlik doğrulaması&gt; öğesinin](https://msdn.microsoft.com/library/532aee0e.aspx)bir alt öğesi olarak bir [&lt;Forms&gt; öğesi](https://msdn.microsoft.com/library/1d3t3c61.aspx) ekleyın ve bunun gibi XML öznitelikleri olarak özelleştirmek istediğiniz özellik değerlerini belirtin:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample1.xml)]

Tablo 1, &lt;Forms&gt; öğesi aracılığıyla özelleştirilebilecek özellikleri özetler. Web. config bir XML dosyası olduğundan, sol sütundaki öznitelik adları büyük/küçük harfe duyarlıdır.

| <strong>Öznitelik</strong> |                                                                                                                                                                                                                                     <strong>Açıklama</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         Cookieless         |                                                                                                                Bu öznitelik, kimlik doğrulama anahtarının URL 'ye katıştırılması için bir tanımlama bilgisinde hangi koşullarda depolandığını belirtir. İzin verilen değerler: UseCookies; UseUri; Seçildiğinde ve UseDeviceProfile (varsayılan). 2\. adım bu ayarı daha ayrıntılı olarak inceler.                                                                                                                |
|         defaultUrl         |                                                                                                                                                         QueryString içinde bir RedirectUrl değeri belirtilmemişse, oturum açma sayfasından oturum açtıktan sonra kullanıcıların yönlendirileceği URL 'YI gösterir. Varsayılan değer Default. aspx ' dir.                                                                                                                                                         |
|           etki alanı           | Tanımlama bilgisi tabanlı kimlik doğrulama biletlerini kullanırken, bu ayar tanımlama bilgisinin etki alanı değerini belirtir. Varsayılan değer boş bir dizedir ve bu, tarayıcının verildiği etki alanını kullanmasına neden olur (örneğin, www.yourdomain.com). Bu durumda, admin.yourdomain.com gibi alt etki alanlarına istek yapıldığında tanımlama bilgisi gönderilmez. Tanımlama bilgisinin tüm alt etki alanlarına geçirilmesini istiyorsanız, yourdomain.com olarak, etki alanı özniteliğini özelleştirmeniz gerekir. |
|  Enableçapraz Sappreyönlendirir   |                                                                                                                                                                   Aynı sunucudaki diğer Web uygulamalarındaki URL 'lere yeniden yönlendirildiğinde, kimliği doğrulanmış kullanıcıların hatırlanıp hatırlamadığını gösteren bir Boole değeri. Varsayılan değer false.                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      Oturum açma sayfasının URL 'SI. Varsayılan değer Login. aspx ' dir.                                                                                                                                                                                                                      |
|            {1&gt;name&lt;1}            |                                                                                                                                                                                                   Tanımlama bilgisi tabanlı kimlik doğrulama biletlerini kullanırken, tanımlama bilgisinin adı. Varsayılan değer. ASPXAUTH 'tur.                                                                                                                                                                                                   |
|            yol            |                                                                             Tanımlama bilgisi tabanlı kimlik doğrulama biletleri kullanılırken, bu ayar tanımlama bilgisinin yol özniteliğini belirtir. Path özniteliği, bir geliştiricinin bir tanımlama bilgisinin kapsamını belirli bir dizin hiyerarşisine sınırlandırmalarını sağlar. Varsayılan değer/olur ve bu, tarayıcıya kimlik doğrulama bileti tanımlama bilgisini, etki alanına yapılan tüm istekler için gönderecek şekilde bildirir.                                                                              |
|         koruma         |                                                                                                                                            Form kimlik doğrulama biletini korumak için kullanılan teknikleri gösterir. İzin verilen değerler: ALL (varsayılan); Şifreleme Seçim ve doğrulama. Bu ayarlar adım 3 ' te ayrıntılı olarak ele alınmıştır.                                                                                                                                            |
|         requireSSL         |                                                                                                                                                                                Kimlik doğrulama tanımlama bilgisini iletmek için bir SSL bağlantısının gerekli olup olmadığını belirten bir Boolean değer. Varsayılan değer false'tur.                                                                                                                                                                                |
|     slidingExpiration      |                                                                                                 Tek bir oturum sırasında kullanıcının siteyi ziyaret ettiği her seferinde kimlik doğrulama tanımlama bilgisinin zaman aşımının sıfırlanıp sıfırlanmayacağını belirten bir Boole değeri. Varsayılan değer true 'dur. Kimlik doğrulama anahtarı zaman aşımı ilkesi, Bilet 'nin zaman aşımı değeri belirtme bölümünde daha ayrıntılı bir şekilde ele alınmıştır.                                                                                                 |
|          Aş           |                                                                                                                               Kimlik doğrulama anahtarı tanımlama bilgisinin süresinin dolacağı süreyi dakika olarak belirtir. Varsayılan değer 30 ' dur. Kimlik doğrulama anahtarı zaman aşımı ilkesi, Bilet 'nin zaman aşımı değeri belirtme bölümünde daha ayrıntılı bir şekilde ele alınmıştır.                                                                                                                               |

**Tablo 1**: &lt;formların&gt; öğenin özniteliklerinin Özeti

ASP.NET 2,0 ve ötesinde, varsayılan form kimlik doğrulama değerleri .NET Framework FormsAuthenticationConfiguration sınıfında sabit olarak kodlanmıştır. Herhangi bir değişiklik, Web. config dosyasında uygulamaya göre uygulama temelinde uygulanmalıdır. Bu, varsayılan form kimlik doğrulama değerlerinin Machine. config dosyasında depolandığı (ve bu nedenle Machine. config 'i düzenleyen aracılığıyla değiştirilebilecek) ASP.NET 1. x öğesinden farklıdır. ASP.NET 1. x konusunda, bir dizi form kimlik doğrulama sistemi ayarı ASP.NET 2,0 ' de farklı varsayılan değerlere sahip ve ASP.NET 1. x ' in ötesinde değil. Uygulamanızı bir ASP.NET 1. x ortamından geçiriyorsanız, bu farklılıklardan haberdar olmanız önemlidir. Farklılıkların bir listesi için [&lt;forms&gt; öğesi teknik belgelerine](https://msdn.microsoft.com/library/1d3t3c61.aspx) başvurun.

> [!NOTE]
> Zaman aşımı, etki alanı ve yol gibi çeşitli form kimlik doğrulama ayarları, elde edilen Forms kimlik doğrulama bileti tanımlama bilgisinin ayrıntılarını belirtir. Tanımlama bilgileri, nasıl çalıştıkları ve çeşitli özellikleri hakkında daha fazla bilgi için [Bu tanımlama bilgileri öğreticisini](http://www.quirksmode.org/js/cookies.html)okuyun.

### <a name="specifying-the-tickets-timeout-value"></a>Bilet zaman aşımı değerini belirtme

Forms kimlik doğrulama bileti, bir kimliği temsil eden bir simgedir. Tanımlama bilgisi tabanlı kimlik doğrulama biletleri ile, bu belirteç tanımlama bilgisi biçiminde tutulur ve her istekte Web sunucusuna gönderilir. Belirtecin sahibi, temelde Kullanıcı *adı*, oturum açdım, oturum açmış olduğum ve bir kullanıcının kimliğinin sayfa ziyaretlerine hatırlanabilmesi için kullanılıyor.

Forms kimlik doğrulama bileti yalnızca kullanıcının kimliğini içermez, ancak belirtecin bütünlüğünü ve güvenliğini sağlamaya yardımcı olacak bilgiler de içerir. Tüm bunları yaptıktan sonra, nefarli bir kullanıcının sahte bir belirteç oluşturabilme veya bazı düşük bir şekilde bir mevzuıt belirtecini değiştirebilmemiz mümkün değildir.

Bilette bulunan bilgilerin bir bit süresi, anahtarın artık geçerli olmadığı tarih ve saat olan bir *süre sonu*. FormsAuthenticationModule bir kimlik doğrulama bileti her inceler, Bilet süresinin dolmamasını sağlar. Varsa, bileti yoksayar ve kullanıcıyı anonim olarak tanımlar. Bu koruma, yeniden yürütme saldırılarına karşı korunmaya yardımcı olur. Süre sonu olmadan, bir korsan bir kullanıcının geçerli kimlik doğrulama biletini (Belki de kendi bilgisayarlarına fiziksel erişim elde ederek ve kendi tanımlama bilgileri aracılığıyla) alıyorsa, bu çalınmış kimlik doğrulama bileti ile sunucuya bir istek gönderebilir ve kazanç girişi. Süre sonu bu senaryoyu engellemez, ancak böyle bir saldırının başarılı olması için pencereyi sınırlandırır.

> [!NOTE]
> 3\. adım, kimlik doğrulama anahtarını korumak için Forms kimlik doğrulama sistemi tarafından kullanılan ek tekniklerin ayrıntılarına bakın.

Kimlik doğrulama anahtarı oluştururken, form kimlik doğrulama sistemi, zaman aşımı ayarına danışarak süre sonunu belirler. Tablo 1 ' de belirtildiği gibi, zaman aşımı ayarı varsayılan olarak 30 dakika olur, yani formlar kimlik doğrulama anahtarının süre sonu değeri, gelecekte bir tarih ve saat 30 dakika olarak ayarlanır.

Süre sonu, form kimlik doğrulama anahtarının süresi sona erdiğinde bir sonraki adımda mutlak bir zaman tanımlar. Ancak geliştiriciler, kullanıcının siteyi yeniden ziyaret ettiği her seferinde sıfırlanarak bir kayan süre sonu uygulamak ister. Bu davranış, slidingExpiration ayarları tarafından belirlenir. True olarak ayarlanırsa (varsayılan), FormsAuthenticationModule her kullanıcı kimliğini doğruladığında, anahtarın süre sonunu günceller. False olarak ayarlanırsa, her istekte süre sonu güncellenmez ve bu nedenle, Bilet ilk kez oluşturulduğunda, anahtarın tam zaman aşımı dakikalarının süresinin dolmasına neden olur.

> [!NOTE]
> Kimlik doğrulama biletinde saklanan süre sonu, 2 Ağustos 2008 11:34 gibi mutlak bir tarih ve saat değeridir. Ayrıca, tarih ve saat, Web sunucusunun yerel saatine göre değişir. Bu tasarım kararı gün ışığından yararlanma saati (DST) boyunca bazı ilginç yan etkilere sahip olabilir. Bu durumda, Birleşik Devletler saatleri bir saat sonra (Web sunucusunun gün ışığından yararlanma saatinin gözlemlendiği bir yerel ayarda barındırıldığından). ASP.NET Web sitesi için, DST 'nin başladığı zamandan (2:00 ' de olan) yaklaşık 30 dakikalık bir süre sonu ile neler olacağını göz önünde bulundurun. Bir ziyaretçi, 12 Mart 2008 ' de 1:55 Mart 'ta sitede oturum açdığına düşünün. Bu, 11 Mart 2:25 2008 ' de süresi dolan bir Forms kimlik doğrulama bileti üretir (gelecekte 30 dakika). Ancak, 2:00 bir kez kaydedildikten sonra saat, DST nedeniyle 3:00 ' e atlar. Kullanıcı 3:01 oturum açtıktan sonra altı dakika sonra yeni bir sayfa yüklediğinde, FormsAuthenticationModule anahtarının süresi dolduktan sonra kullanıcıyı oturum açma sayfasına yönlendirir. Bu ve diğer kimlik doğrulama bileti zaman aşımı odlamalarında daha kapsamlı bir tartışma ve geçici çözüm için, Stefan Schackow 'ın *Professional ASP.NET 2,0 güvenlik, üyelik ve rol yönetimi* (ısbn: 978-0-7645-9698-8) ' nin bir kopyasını alın.

Şekil 1, slidingExpiration değeri false olarak ayarlandığında ve zaman aşımı 30 olarak ayarlandığında iş akışını gösterir. Oturum açma sırasında oluşturulan kimlik doğrulama anahtarının sona erme tarihini içerdiğini ve bu değerin sonraki isteklerde güncelleştirilmediğini unutmayın. FormsAuthenticationModule, anahtarın süresi dolmuşsa, bunu atar ve isteği anonim olarak değerlendirir.

[slidingExpiration yanlış olduğunda form kimlik doğrulama biletinin son tarihinin grafik gösterimini ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image1.png)

**Şekil 01**: slidingExpiration false olduğunda form kimlik doğrulama biletinin son kullanma süresinin grafik bir gösterimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image3.png))

Şekil 2, slidingExpiration değeri true olarak ayarlandığında ve zaman aşımı 30 olarak ayarlandığında iş akışını gösterir. Kimliği doğrulanmamış bir istek alındığında (süresi dolmayan bir bilet), süre sonu, gelecekte zaman aşımı süresi dakika olarak güncelleştirilir.

[slidingExpiration değeri true olduğunda form kimlik doğrulama biletinin grafik gösterimini ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image4.png)

**Şekil 02**: slidingExpiration değeri true olduğunda form kimlik doğrulama biletinin grafik gösterimi ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image6.png))

Tanımlama bilgisi tabanlı kimlik doğrulama biletlerini kullanırken (varsayılan), bu tartışma daha karmaşık hale gelir çünkü tanımlama bilgilerinin kendi sorguları de belirtilmiş olabilir. Tanımlama bilgisinin süre sonu (veya eksikliği), tanımlama bilgisi yok edildiğinde tarayıcıya bildirir. Tanımlama bilgisinde süre sonu yoksa, tarayıcı kapandığında yok edilir. Ancak bir süre sonu mevcutsa, süre sonu içinde belirtilen tarih ve saat geçtikten sonra tanımlama bilgisi kullanıcının bilgisayarında depolanır. Tarayıcı tarafından bir tanımlama bilgisi yok edildiğinde, artık Web sunucusuna gönderilmez. Bu nedenle, bir tanımlama bilgisinin yok edilmesi, sitede oturum açan kullanıcıya benzer.

> [!NOTE]
> Kuşkusuz, bir kullanıcı bilgisayarında depolanan tüm tanımlama bilgilerini önceden kaldırabilir. Internet Explorer 7 ' de araçlar, Seçenekler ' e gidip göz atma geçmişi bölümünde Sil düğmesine tıklayabilirsiniz. Buradan, tanımlama bilgilerini Sil düğmesine tıklayın.

Forms kimlik doğrulama sistemi, *Persistcookie* parametresine geçirilen değere göre oturum tabanlı veya süre sonu tabanlı tanımlama bilgileri oluşturur. FormsAuthentication sınıfının GetAuthCookie, SetAuthCookie ve RedirectFromLoginPage yöntemlerinin iki giriş parametresi içinde sürmesine geri çekin: *UserName* ve *persistcookie*. Önceki öğreticide oluşturduğumuz oturum açma sayfası, kalıcı bir tanımlama bilgisinin oluşturulup oluşturulmayacağını belirleyen beni anımsa onay kutusunu içeriyordu. Kalıcı tanımlama bilgileri zaman aşımı tabanlıdır; kalıcı olmayan tanımlama bilgileri oturum tabanlıdır.

Zaten tartışılan zaman aşımı ve slidingExpiration kavramları, hem oturum hem de süre sonu tabanlı tanımlama bilgileri için de geçerlidir. Yürütmede yalnızca bir küçük fark vardır: slidingTimeout değeri true olarak ayarlandığında süre sonu tabanlı tanımlama bilgileri kullanılırken, tanımlama bilgisinin süre sonu yalnızca belirtilen sürenin yarısından fazlası geçtiğinde güncelleştirilir.

Şimdi Web sitesinin kimlik doğrulama anahtarı zaman aşımı ilkelerini, anahtarların bir saatten sonra zaman aşımına uğramasını (60 dakika), kayan bir süre sonu kullanarak güncelleştirelim. Bu değişikliği uygulamak için, Web. config dosyasını güncelleştirin ve &lt;kimlik doğrulaması&gt; öğesine aşağıdaki biçimlendirmeye sahip bir &lt;Forms&gt; öğesi ekleyin:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>Login. aspx dışında bir oturum açma sayfası URL 'SI kullanma

FormsAuthenticationModule, yetkisiz kullanıcıları otomatik olarak oturum açma sayfasına yönlendirdiğinden, oturum açma sayfasının URL 'sini bilmeleri gerekir. Bu URL, &lt;Forms&gt; öğesindeki loginUrl özniteliği tarafından belirtilir ve varsayılan olarak Login. aspx ' dir. Var olan bir Web sitesi üzerinden bağlantı noktası oluşturuyorsanız, farklı bir URL 'ye sahip bir oturum açma sayfanız zaten var ve bu, arama motorları tarafından önceden işaretlenmiş ve dizine alınmış bir URL 'ye sahip olabilir. Var olan oturum açma sayfanızı, oturum açma. aspx ve en son bağlantılar ve kullanıcıların yer işaretleri için yeniden adlandırmak yerine, oturum açma sayfanıza işaret etmek için loginUrl özniteliğini değiştirebilirsiniz.

Örneğin, oturum açma sayfanız Signıd. aspx olarak adlandırıldıysa ve kullanıcılar dizininde yer alıyorsa, loginUrl yapılandırma ayarını ~/Users/SignIn.aspx olarak işaret edebilirsiniz:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample3.xml)]

Geçerli uygulamamız Login. aspx adlı bir oturum açma sayfasına zaten sahip olduğundan, &lt;Forms&gt; öğesinde özel bir değer belirtmeniz gerekmez.

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>2\. Adım: tanımlama bilgisi olmayan formları kullanma kimlik doğrulama biletleri

Varsayılan olarak, Forms kimlik doğrulama sistemi, kimlik doğrulama biletlerini tanımlama bilgileri koleksiyonunda depolayıp saklamamayı veya siteyi ziyaret eden kullanıcı aracısına göre URL 'ye eklemeyi belirler. Internet Explorer, Firefox, Opera ve Safari gibi tüm temel masaüstü tarayıcıları, tanımlama bilgilerini destekler, ancak tüm mobil cihazları desteklemez.

Forms kimlik doğrulama sistemi tarafından kullanılan tanımlama bilgisi İlkesi, dört değerden biri atanabilen &lt;Forms&gt; öğesindeki tanımlama bilgisi olmayan ayara bağlıdır:

- UseCookies-tanımlama bilgisi tabanlı kimlik doğrulama biletlerinin her zaman kullanılacağını belirtir.
- UseUri-tanımlama bilgisi tabanlı kimlik doğrulama biletlerinin hiçbir şekilde kullanılmayacağını gösterir.
- Otomatik Algıla-cihaz profili tanımlama bilgilerini desteklemiyorsa, tanımlama bilgisi tabanlı kimlik doğrulama biletleri kullanılmaz; Cihaz profili tanımlama bilgilerini destekliyorsa, tanımlama bilgilerinin etkinleştirilip etkinleştirilmediğini anlamak için bir yoklama mekanizması kullanılır.
- UseDeviceProfile-varsayılan; yalnızca cihaz profili tanımlama bilgilerini destekliyorsa, tanımlama bilgisi tabanlı kimlik doğrulama biletlerini kullanır. Hiçbir yoklama mekanizması kullanılmaz.

Otomatik Algıla ve UseDeviceProfile ayarları, tanımlama bilgisi tabanlı veya tanımlama bilgisi olmayan kimlik doğrulama biletleri kullanıp kullanmayacağınızı belirlemek için bir *cihaz profilini* kullanır. ASP.NET, çeşitli cihazların ve bu özellikleri, tanımlama bilgilerini destekledikleri, hangi JavaScript 'in destekledikleri ve bu gibi özelliklerine sahip bir veritabanını tutar. Bir cihaz, cihaz türünü tanımlayan bir *Kullanıcı Aracısı* http üst bilgisi aracılığıyla gönderdiği bir Web sunucusundan bir Web sayfası istediğinde. ASP.NET, sağlanan Kullanıcı Aracısı dizesiyle, veritabanında belirtilen ilişkili profille otomatik olarak eşleşir.

> [!NOTE]
> Bu cihaz özellikleri veritabanı, [tarayıcı tanımı dosya şemasına](https://msdn.microsoft.com/library/ms228122.aspx)bağlı BIR dizi xml dosyasında depolanır. Varsayılan Cihaz profili dosyaları%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers. konumunda bulunur Ayrıca uygulamanızın App\_tarayıcıları klasörüne özel dosyalar ekleyebilirsiniz. Daha fazla bilgi için bkz. [nasıl yapılır: ASP.NET Web sayfalarında tarayıcı türlerini algılama](https://msdn.microsoft.com/library/3yekbd5b.aspx).

Varsayılan ayar UseDeviceProfile olduğundan, site profili tanımlama bilgilerini desteklemediği bir cihaz tarafından ziyaret edildiğinde, tanımlama bilgisi olmayan formlar kimlik doğrulama biletleri kullanılacaktır.

### <a name="encoding-the-authentication-ticket-in-the-url"></a>URL 'de kimlik doğrulama biletini kodlama

Tanımlama bilgileri, belirli bir Web sitesine her istekte tarayıcıdan bilgi eklemek için doğal bir ortamdır. Bu, varsayılan formların kimlik doğrulama ayarlarının, ziyaret edilen cihaz tarafından desteklense de tanımlama bilgilerini kullanmasına neden olur. Tanımlama bilgileri desteklenmiyorsa, kimlik doğrulama anahtarının istemciden sunucuya geçirilmesi için alternatif bir yol gerekir. Tanımlama bilgisi olmayan ortamlarda kullanılan yaygın bir geçici çözüm, URL 'deki tanımlama bilgisi verilerini kodlamadır.

Bu tür bilgilerin URL içine nasıl katıştırılabildiğinden en iyi yol, siteyi tanımlama bilgisi olmayan kimlik doğrulama biletleri kullanmaya zorlamaktır. Bu, tanımlama bilgisi olmayan yapılandırma ayarı UseUri olarak ayarlanarak gerçekleştirilebilir:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample4.xml)]

Bu değişikliği yaptıktan sonra, bir tarayıcı aracılığıyla siteyi ziyaret edin. Anonim kullanıcı olarak ziyaret edildiğinde, URL 'Ler tam olarak daha önce olduğu gibi görünecektir. Örneğin, varsayılan. aspx sayfasını ziyaret ederken Tarayıcımın adres çubuğu şu URL 'YI gösterir:

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

Ancak, oturum açma sırasında Forms kimlik doğrulama bileti URL 'ye katıştırılır. Örneğin, oturum açma sayfasını ziyaret ettikten ve Sam olarak oturum açtıktan sonra, varsayılan. aspx sayfasına döndürüyorum, ancak URL şu anda:

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

Forms kimlik doğrulama bileti URL içine eklenmiş. Dize (F (jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-EYC Malxjfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2), onaltılı kodlu kimlik doğrulama bilet bilgilerini temsil eder ve genellikle bir tanımlama bilgisinde depolanan veriler aynıdır.

Tanımlama bilgisi olmayan kimlik doğrulama biletlerinin çalışması için, sistemin sayfadaki tüm URL 'Leri kimlik doğrulama bileti verilerini içerecek şekilde kodlanması gerekir, aksi takdirde Kullanıcı bir bağlantıya tıkladığında kimlik doğrulama anahtarı kaybedilir. Ktam, bu ekleme mantığı otomatik olarak gerçekleştirilir. Bu işlevi göstermek için default. aspx sayfasını açın ve metin ve NavigateUrl özelliklerini test bağlantısı ve SomePage. aspx olarak ayarlayarak bir köprü denetimi ekleyin. Aslında, projemizdeki SomePage. aspx adında bir sayfanın olmadığı önemi yoktur.

Varsayılan. aspx değişikliklerini kaydedin ve ardından bir tarayıcıdan ziyaret edin. Forms kimlik doğrulama anahtarının URL 'ye katıştırılması için sitede oturum açın. Ardından, default. aspx ' den test bağlantısı bağlantısına tıklayın. Ne oldu? SomePage. aspx adında bir sayfa yoksa, bir 404 hatası oluşmuştur, ancak burada önemli olan bu değildir. Bunun yerine, tarayıcınızdaki Adres çubuğuna odaklanın. URL 'ye Forms kimlik doğrulama bileti dahil olduğunu unutmayın!

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

Bağlantıdaki SomePage. aspx URL 'SI otomatik olarak kimlik doğrulama biletini içeren bir URL 'ye dönüştürüldü; bir kod tat yazmak zorunda kalmadık! Form kimlik doğrulama bileti, `http://` veya `/`başlamamış herhangi bir köprünün URL 'sine otomatik olarak gömülecektir. Köprünün Response. Redirect çağrısında, bir köprü denetiminde veya bir tutturucu HTML öğesinde (örn. `<a href="...">...</a>`) bir biçimde görünüp görüntülendiğine bakılmaksızın. URL `http://www.someserver.com/SomePage.aspx` veya `/SomePage.aspx`gibi bir şey olmadığı sürece, Forms kimlik doğrulama bileti ABD için gömülecektir.

> [!NOTE]
> Tanımlama bilgisi olmayan formlarda kimlik doğrulama biletleri, tanımlama bilgisi tabanlı kimlik doğrulama biletleri ile aynı zaman aşımı ilkelerine uyar. Ancak, kimlik doğrulama bileti doğrudan URL 'ye katıştırıldığından, tanımlama bilgisi olmayan kimlik doğrulama biletleri yeniden yürütme saldırılarına açıktır. Bir Web sitesini ziyaret eden, oturum açan ve sonra da bir e-postadaki URL 'YI bir iş arkadaşınıza yapıştırabilen bir Kullanıcı düşünün. İş arkadaşınız bitiş süresine ulaşılmadan önce bu bağlantıyı tıklatırsa, e-postayı gönderen Kullanıcı olarak oturum açar!

## <a name="step-3-securing-the-authentication-ticket"></a>3\. Adım: kimlik doğrulama anahtarının güvenliğini sağlama

Forms kimlik doğrulama bileti, bir tanımlama bilgisinde veya doğrudan URL içinde gömülü bir bağlantı üzerinden iletilir. Kimlik bilgilerine ek olarak, kimlik doğrulama bileti Kullanıcı verilerini de içerebilir (4. adımda göreceğiniz gibi). Sonuç olarak, Bilet verilerinin, anahtar ve (daha da daha da önemlisi) ve Forms kimlik doğrulama sisteminin, Bilet kurcalanmadığını garanti edemeyeceği önem taşır.

Bilet verilerinin gizliliğini sağlamak için, Forms kimlik doğrulama sistemi bilet verilerini şifreleyebilir. Bilet verileri şifrelememe hatası, düz metin içinde potansiyel olarak hassas bilgileri kablolu olarak gönderir.

Bir anahtarın özgünlüğünü garantilemek için, Forms kimlik doğrulama sisteminin bileti *doğrulaması gerekir.* Doğrulama, belirli bir veri parçasının değiştirilmeyeceğinden ve bir *[ileti kimlik doğrulama kodu (Mac)](http://en.wikipedia.org/wiki/Message_authentication_code)* aracılığıyla gerçekleştirilmesinin bir parçasıdır. Bir Nutshell 'de MAC, doğrulanması gereken verileri (Bu durumda bilet) tanımlayan küçük bir bilgi parçasıdır. MAC tarafından temsil edilen veriler değiştirilirse MAC ve veriler eşleşmeyecektir. Üstelik, bir korsanın her ikisi de verileri değiştirip değiştirilen verilerle uyumlu olacak kendi MAC 'i oluşturmasını sağlamak için de hesaplama zor olur.

Bir bilet oluştururken (veya değiştirirken), Forms kimlik doğrulama sistemi bir MAC oluşturur ve bunu bilet verilerine ekler. Sonraki bir istek geldiğinde, Forms kimlik doğrulama sistemi, Bilet verilerinin orijinalliğini doğrulamak üzere MAC ve bilet verilerini karşılaştırır. Şekil 3 ' te bu iş akışı grafiksel olarak gösterilmiştir.

[Bilet Için kimlik doğrulaması bir MAC aracılığıyla ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image7.png)

**Şekil 03**: bilet kimlik doğrulaması bir Mac aracılığıyla yapılır ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image9.png))

Kimlik doğrulama biletlerine uygulanan güvenlik ölçüleri, &lt;Forms&gt; öğesindeki koruma ayarına bağlıdır. Koruma ayarı aşağıdaki üç değerden birine atanabilir:

- All-bilet hem şifreli hem de dijital olarak imzalanır (varsayılan).
- Yalnızca şifreleme şifrelemesi uygulandı-hiçbir MAC oluşturulmaz.
- Hiçbiri-bilet şifrelenmedi veya dijital olarak imzalanmamıştır.
- Doğrulama-bir MAC oluşturulur, ancak bilet verileri düz metin olarak kablo üzerinden gönderilir.

Microsoft, tüm ayarların kullanılmasını kesinlikle önerir.

### <a name="setting-the-validation-and-decryption-keys"></a>Doğrulama ve şifre çözme anahtarlarını ayarlama

Form kimlik doğrulama sistemi tarafından kimlik doğrulama biletini şifrelemek ve doğrulamak için kullanılan şifreleme ve karma algoritmalar, Web. config 'deki [&lt;machineKey&gt; öğesi](https://msdn.microsoft.com/library/w8h3skw9.aspx) aracılığıyla özelleştirilebilir. Tablo 2 &lt;machineKey&gt; öğesinin özniteliklerini ve olası değerlerini özetler.

| **Öznitelik** | **Açıklama** |
| --- | --- |
| şifre çözme | Şifreleme için kullanılan algoritmayı belirtir. Bu öznitelik aşağıdaki dört değerden birine sahip olabilir:-Auto varsayılan; , decryptionKey özniteliğinin uzunluğuna bağlı olarak algoritmayı belirler. -AES- [Gelişmiş Şifreleme Standardı (AES)](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) algoritmasını kullanır. -DES- [veri şifreleme standardı (DES)](http://en.wikipedia.org/wiki/Data_Encryption_Standard) kullanır Bu algoritma hesaplama açısından zayıf olarak değerlendirilir ve kullanılmamalıdır. -3DES-DES algoritmasını üç kez uygulayarak çalışacak olan [Üçlü des](http://en.wikipedia.org/wiki/Triple_DES) algoritmasını kullanır. |
| decryptionKey | Şifreleme algoritması tarafından kullanılan gizli anahtar. Bu değer, uygun uzunluktaki (şifre çözme değerine göre), otomatik olarak veya herhangi bir değer, ısoteapps ile eklenen bir onaltılı dize olmalıdır. Isoteapps eklemek, ASP.NET 'in her uygulama için benzersiz bir değer kullanmasını sağlar. Varsayılan olarak AutoGenerate, ısoteapps. |
| doğrulama | Doğrulama için kullanılan algoritmayı belirtir. Bu öznitelik, aşağıdaki dört değerden birine sahip olabilir:-AES-Gelişmiş Şifreleme Standardı (AES) algoritmasını kullanır. -MD5- [Ileti Özeti 5 (MD5)](http://en.wikipedia.org/wiki/MD5) algoritmasını kullanır. -SHA1- [SHA1](http://en.wikipedia.org/wiki/Sha1) algoritmasını (varsayılan) kullanır. -3DES-Üçlü DES algoritmasını kullanır. |
| validationKey | Doğrulama algoritması tarafından kullanılan gizli anahtar. Bu değer, uygun uzunlukta bir onaltılı dize olmalıdır (doğrulamanın değerine göre), AutoGenerate veya ya da ısoteapps ile eklenen değer. Isoteapps eklemek, ASP.NET 'in her uygulama için benzersiz bir değer kullanmasını sağlar. Varsayılan olarak AutoGenerate, ısoteapps. |

**Tablo 2**: &lt;machineKey&gt; öğesi öznitelikleri

Bu şifreleme ve doğrulama seçenekleri hakkında kapsamlı bir tartışma ve çeşitli algoritmaların profesyonelleri ve dezavantajları Bu öğreticinin kapsamı dışındadır. Hangi şifreleme ve doğrulama algoritmalarının, kullanılacak anahtar uzunluklarının ve bu anahtarların en iyi şekilde nasıl üretilebileceğine ilişkin yönergeler de dahil olmak üzere bu sorunlara derinlemesine bir bakış için, *profesyonel ASP.NET 2,0 güvenlik, üyelik ve rol yönetimine*bakın.

Varsayılan olarak, şifreleme ve doğrulama için kullanılan anahtarlar her uygulama için otomatik olarak oluşturulur ve bu anahtarlar yerel güvenlik yetkilisinde (LSA) depolanır. Kısacası, varsayılan ayarlar bir Web sunucusu tarafından Web sunucusu ve uygulama temelinde benzersiz anahtarların garanti edilir. Sonuç olarak, bu varsayılan davranış aşağıdaki iki senaryo için çalışmaz:

- **Web grupları** -bir [Web grubu](http://en.wikipedia.org/wiki/Web_farm) senaryosunda, tek bir Web uygulaması ölçeklenebilirlik ve artıklık amacıyla birden çok Web sunucusunda barındırılır. Her gelen istek, gruptaki bir sunucuya gönderilir, yani bir kullanıcı oturumunun kullanım ömrü boyunca çeşitli istekleri işlemek için farklı sunucular kullanılabilir. Sonuç olarak, her sunucu aynı şifreleme ve doğrulama anahtarlarını kullanmalıdır, böylece bir sunucuda oluşturulan, şifrelenen ve doğrulanan formlar kimlik doğrulama biletinin şifresi çözülür ve gruptaki farklı bir sunucuda doğrulanabilir.
- **Çapraz uygulama bileti paylaşımı** -tek bir Web sunucusu birden çok ASP.NET uygulamasını barındıramayabilir. Bu farklı uygulamaların tek bir form kimlik doğrulama bileti paylaşması gerekiyorsa, şifreleme ve doğrulama anahtarlarının eşleşmesi zorunludur.

Bir Web çiftliği ayarında çalışırken veya aynı sunucudaki uygulamalarda kimlik doğrulama biletlerini paylaşarak, bu durumda, decryptionKey ve validationKey değerlerinin eşleşmesi için etkilenen uygulamalardaki &lt;machineKey&gt; öğesini yapılandırmanız gerekir.

Yukarıdaki senaryolardan hiçbiri örnek uygulamamız için geçerli olmasa da, açık decryptionKey ve validationKey değerlerini belirtebilir ve kullanılacak algoritmaları tanımlayabilirsiniz. Web. config dosyasına bir &lt;machineKey&gt; ayarı ekleyin:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample5.xml)]

Daha fazla bilgi için bkz. [ASP.NET 2,0 'de machineKey yapılandırma](https://msdn.microsoft.com/library/ms998288.aspx).

> [!NOTE]
> DecryptionKey ve validationKey değerleri, her sayfada ziyaret edildiğinde 64 rastgele onaltılı karakter üreten [Steve Rason](http://www.grc.com/stevegibson.htm)'un [mükemmel parolalar Web sayfasından](https://www.grc.com/passwords.htm)alınmıştır. Bu anahtarların, üretim uygulamalarınıza yönelik biçimini azaltmak için yukarıdaki anahtarları kusursuz parolalar sayfasından rastgele oluşturulmuş olanlarla değiştirmeniz önerilir.

## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>4\. Adım: ek kullanıcı verilerini bilette depolama

Birçok Web uygulaması, şu anda oturum açmış olan kullanıcının sayfa görüntüsünü görüntüleyen veya temel alan bilgileri görüntüler. Örneğin, bir Web sayfası, kullanıcının adını ve her sayfanın üst köşesinde son oturum açmış olan tarihi gösterebilir. Forms kimlik doğrulama anahtarı şu anda oturum açmış olan kullanıcının Kullanıcı adını depolar, ancak başka herhangi bir bilgi gerektiğinde, kimlik doğrulama anahtarında depolanmayan bilgileri aramak için, sayfanın Kullanıcı deposuna gitmesi gerekir-genellikle bir veritabanı.

Küçük bir kod sayesinde, Forms kimlik doğrulama biletinde ek kullanıcı bilgileri depolayabiliriz. Bu tür veriler [FormsAuthenticationTicket sınıfının](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx) [UserData özelliği](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)aracılığıyla ifade edilebilir. Bu, yaygın olarak gereken kullanıcı hakkında küçük miktarlarda bilgi yerleştirmek için kullanışlı bir yerdir. UserData özelliğinde belirtilen değer, kimlik doğrulama anahtarı tanımlama bilgisinin bir parçası olarak dahil edilmiştir ve diğer bilet alanları gibi, Forms kimlik doğrulaması sisteminin yapılandırmasına göre şifrelenir ve onaylanır. Varsayılan olarak, UserData boş bir dizedir.

Kimlik doğrulama biletinde Kullanıcı verilerini depolamak için, oturum açma sayfasında kullanıcıya özgü bilgileri gösteren ve bilet içinde depolayan bir kod yazmanız gerekir. UserData, dize türünde bir özellik olduğundan, içinde depolanan verilerin bir dize olarak doğru şekilde serileştirilmesi gerekir. Örneğin, Kullanıcı mağazamız her kullanıcının Doğum tarihini ve işverenin adını dahil etseyk ve bu iki özellik değerini kimlik doğrulama biletinde depolamak istiyorduk. Bu değerleri, kullanıcının Doğum tarihini bir ardışık düzen (|) ve ardından işveren adı ile birleştirerek bir dizeye dizitebiliriz. 15 Ağustos 1974 ' de bulunan ve Northwind Traders için çalıştırılan bir kullanıcı için, UserData özelliğini şu dize olarak atayacağız: 1974-08-15 | Northwind Traders.

Bilet içinde depolanan verilere erişmeniz gerektiğinde, yakalayıp geçerli isteğin FormsAuthenticationTicket ve UserData özelliğinin serisini kaldırarak bunu yapabiliriz. Doğum tarihi ve işveren adı örneği söz konusu olduğunda, (|) sınırlayıcı temelinde UserData dizesini iki alt dizeye böyoruz.

[![ek kullanıcı bilgileri kimlik doğrulama biletinde depolanabilir](forms-authentication-configuration-and-advanced-topics-cs/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image10.png)

**Şekil 04**: ek kullanıcı bilgileri kimlik doğrulama biletinde depolanabilir ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image12.png))

### <a name="writing-information-to-userdata"></a>UserData bilgi yazma

Ne yazık ki, bir form kimlik doğrulama biletinde kullanıcıya özel bilgiler eklemek, bir tane beklendiğinden basit değil. FormsAuthenticationTicket sınıfının UserData Özelliği salt okunurdur ve yalnızca FormsAuthenticationTicket sınıf oluşturucusu aracılığıyla belirtilebilir. Oluşturucuda UserData özelliğini belirtirken, Bilet diğer değerlerini de sağlıyoruz: Kullanıcı adı, sorun tarihi, süre sonu vb. Önceki öğreticide oturum açma sayfasını oluşturduğumuz, bu, hepsi de FormsAuthentication sınıfı tarafından bizim için işlendi. FormsAuthenticationTicket 'e UserData eklerken, FormsAuthentication sınıfı tarafından zaten sağlanmış olan işlevlerin çoğunu çoğaltmak için kod yazalım olacaktır.

Login. aspx sayfasını, kullanıcı hakkındaki ek bilgileri kimlik doğrulama biletini kaydedecek şekilde güncelleştirerek, UserData ile çalışmaya yönelik gerekli kodu keşfedelim. Kullanıcı mağazamız, kullanıcının kullandığı şirket hakkındaki bilgileri ve bunların unvanlarını ve bu bilgileri kimlik doğrulama biletinde yakalamak istediğimizi içerir. Kodun aşağıdaki gibi görünmesi için login. aspx sayfasının LoginButton ' ı tıklatın olay işleyicisi ' ne tıklayın:

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample6.cs)]

Tek seferde bu kodda bir satır ilerlim. Yöntemi, dört dize dizisi tanımlayarak başlar: kullanıcılar, parolalar, companyName ve titleAtCompany. Bu diziler, sistem içindeki kullanıcı hesapları için Kullanıcı adları, parolalar, şirket adları ve başlıkları, üç: Scott, Jisun ve Sam olarak tutar. Gerçek bir uygulamada, bu değerler, sayfanın kaynak kodunda sabit kodlanmış değil, Kullanıcı mağazasından sorgulanmalıdır.

Önceki öğreticide, sağlanan kimlik bilgileri geçerliyse yalnızca FormsAuthentication. RedirectFromLoginPage (UserName. Text, RememberMe. Checked) olarak adlandırdık ve aşağıdaki adımları gerçekleştirdi:

1. Forms kimlik doğrulama bileti oluşturuldu
2. Bilet uygun depoya yazdı. Tanımlama bilgileri tabanlı kimlik doğrulama biletleri için tarayıcının tanımlama bilgileri koleksiyonu kullanılır; tanımlama bilgisi olmayan kimlik doğrulama biletleri için, Bilet verileri URL 'ye serileştirilir
3. Kullanıcı uygun sayfaya yönlendirildi

Bu adımlar yukarıdaki kodda çoğaltılır. İlk olarak, önce UserData özelliğinde depolayacağız dize, şirket adı ve başlığı birleştirilerek, iki değeri bir kanal karakteriyle (|) ayırarak oluşturulur.

String userDataString = dize. Concat (companyName [i], "|", titleAtCompany [i]);

Daha sonra, bir kimlik doğrulama bileti oluşturan FormsAuthentication. GetAuthCookie yöntemi çağrılır, yapılandırma ayarlarına göre şifreler ve doğrular ve bir HttpCookie nesnesine koyar.

HttpCookie authCookie = FormsAuthentication. GetAuthCookie (UserName. Text, RememberMe. Checked);

Tanımlama bilgisinde gömülü Formauthenticationbilet ile çalışabilmek için, tanımlama bilgisi değerini geçirerek FormAuthentication sınıfının [şifre çözme yöntemini](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)çağırmanız gerekir.

FormsAuthenticationTicket bilet = FormsAuthentication. şifre çözme (authCookie. Value);

Daha sonra var olan FormsAuthenticationTicket değerlerini temel alarak *Yeni* bir FormsAuthenticationTicket örneği oluşturacağız. Ancak, bu yeni bilet kullanıcıya özgü bilgileri (userDataString) içerir.

FormsAuthenticationTicket newTicket = New FormsAuthenticationTicket (bilet. Sürüm, Bilet. Ad, Bilet. IssueDate, Bilet. Süre sonu, Bilet. IsPersistent, userDataString);

Daha sonra, [şifreleme yöntemini](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx)çağırarak yeni FormsAuthenticationTicket örneğini şifreler (ve doğrular) ve bu şifrelenen (ve doğrulanan) verileri authCookie 'e geri koyabilirsiniz.

authCookie. Value = FormsAuthentication. Encrypt (Newbilet);

Son olarak, authCookie Response. Cookies koleksiyonuna eklenir ve GetRedirectUrl yöntemi, kullanıcıyı göndermek için uygun sayfayı tespit etmek üzere çağırılır.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample7.cs)]

UserData Özelliği salt okunurdur ve FormsAuthentication sınıfı, GetAuthCookie, SetAuthCookie veya RedirectFromLoginPage yöntemlerinde UserData bilgilerini belirtmek için herhangi bir yöntem sağlamadığından bu kodun tümü gereklidir.

> [!NOTE]
> Az önce incelediğimiz kod, kullanıcıya özgü bilgileri tanımlama bilgileri tabanlı bir kimlik doğrulama bileti içinde depolar. Form kimlik doğrulama biletinin URL 'ye serileştirilmesinden sorumlu sınıflar, .NET Framework iç olarak kullanılır. Uzun hikaye kısaltması, Kullanıcı verilerini tanımlama bilgisi olmayan bir form kimlik doğrulama biletinde depolayamezsiniz.

### <a name="accessing-the-userdata-information"></a>UserData bilgilerine erişme

Bu noktada, her kullanıcının şirket adı ve başlığı, oturum açtıklarında Forms kimlik doğrulama biletinin UserData özelliğinde depolanır. Bu bilgilere, Kullanıcı deposuna seyahat gerekmeden herhangi bir sayfada kimlik doğrulama biletinden erişilebilir. Bu bilgilerin UserData özelliğinden nasıl alınabileceğini göstermek için default. aspx ' i güncellemenize izin verin. böylece, hoş geldiniz iletisi yalnızca kullanıcının adını değil, ayrıca çalıştıkları şirketi ve bunların unvanlarını içerir.

Şu anda default. aspx, WelcomeBackMessage adlı bir etiket denetimiyle bir kimlik doğrulayan Tedmessagepanel paneli içerir. Bu panel yalnızca kimliği doğrulanmış kullanıcılar için görüntülenir. Aşağıdaki gibi görünmesi için, varsayılan. aspx sayfası\_yükleme olay işleyicisindeki kodu güncelleştirin:

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample8.cs)]

Istek. IsAuthenticated değeri true ise, WelcomeBackMessage 'ın Text özelliği ilk olarak hoş geldiniz 'e, *Kullanıcı adına*ayarlanır. Ardından, temel FormsAuthenticationTicket erişebilmemiz için User. Identity özelliği bir FormsIdentity nesnesine ayarlanır. FormsAuthenticationTicket sahip olduktan sonra, UserData özelliğinin şirket adı ve başlığına serisini çıkardık. Bu işlem, kanal karakteri üzerindeki dize bölünerek gerçekleştirilir. Şirket adı ve başlığı, daha sonra WelcomeBackMessage etiketinde görüntülenir.

Şekil 5 ' te bu görüntülemenin bir ekran görüntüsü gösterilir. Scott olarak oturum açmak Scott 'ın şirketini ve başlığını içeren bir karşılama geri iletisi görüntüler.

[Şu anda oturum açmış olan kullanıcının şirketi ve unvanı görüntülenir ![](forms-authentication-configuration-and-advanced-topics-cs/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image13.png)

**Şekil 05**: Şu anda oturum açmış kullanıcının şirketi ve unvanı görüntülenir ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image15.png))

> [!NOTE]
> Kimlik doğrulama biletinin UserData özelliği, kullanıcı deposu için bir önbellek görevi görür. Her türlü önbellekte olduğu gibi, temel alınan veriler değiştirildiğinde güncelleştirilmesi gerekir. Örneğin, kullanıcıların profilini güncelleştirebileceği bir Web sayfası varsa, UserData özelliğinde önbelleğe alınan alanlar Kullanıcı tarafından yapılan değişiklikleri yansıtacak şekilde yenilenmelidir.

## <a name="step-5-using-a-custom-principal"></a>5\. Adım: özel bir sorumlu kullanma

Gelen tüm istekler üzerinde FormsAuthenticationModule Kullanıcı kimliğini doğrulamaya çalışır. Süre dolmayan bir kimlik doğrulama bileti varsa, FormsAuthenticationModule HttpContext. User özelliğini yeni bir GenericPrincipal nesnesine atar. Bu GenericPrincipal nesnesinin, Forms kimlik doğrulama bileti başvurusunu içeren FormsIdentity türünde bir kimliği vardır. GenericPrincipal sınıfı, IPrincipal uygulayan bir sınıf için gereken en düşük işlevselliği içerir. yalnızca bir Identity özelliğine ve bir ıınrole metoduna sahiptir.

Asıl nesnenin iki sorumluluğu vardır: kullanıcının hangi rollere ait olduğunu göstermek ve kimlik bilgilerini sağlamak için. Bu, sırasıyla IPrincipal arabiriminin IsInRole (*roleName*) yöntemi ve kimlik özelliği aracılığıyla gerçekleştirilir. GenericPrincipal sınıfı, rol adlarının dize dizisinin Oluşturucu aracılığıyla belirtilmesini sağlar; IsInRole (*roleName*) yöntemi, yalnızca geçirilen *roleName* öğesinin dize dizisi içinde varolup olmadığını denetler. FormsAuthenticationModule GenericPrincipal oluşturduğunda, GenericPrincipal 'ın oluşturucusuna boş bir dize dizisi geçirir. Sonuç olarak, IsInRole öğesine yapılan herhangi bir çağrı her zaman false döndürür.

GenericPrincipal sınıfı, rollerin kullanılmayan çoğu form tabanlı kimlik doğrulama senaryosuna yönelik ihtiyaçları karşılar. Varsayılan rol işlemenin yetersiz olduğu durumlarda veya özel bir IIdentity nesnesini kullanıcıyla ilişkilendirmeniz gerektiğinde, kimlik doğrulama iş akışı sırasında özel bir IPrincipal nesnesi oluşturabilir ve bunu HttpContext. User özelliğine atayabilirsiniz.

> [!NOTE]
> Daha sonraki öğreticilerde, ASP. NET 'in rol çerçevesi etkin değil; [RolePrincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx) türünde özel bir Principal nesnesi oluşturur ve form kimlik doğrulaması tarafından oluşturulan GenericPrincipal nesnesinin üzerine yazar. Bu, Principal 'ın ıbırole yöntemini rol çerçevesinin API 'siyle arayüze özelleştirmek için yapar.

Henüz rollerle ilgilenmediğimiz için, bu kavşakta 'te özel bir sorumlu oluşturmak için sahip olduğumuz tek neden, özel bir IIdentity nesnesini sorumlu ile ilişkilendirmelidir. Adım 4 ' te, kullanıcının şirket adı ve başlığında ek kullanıcı bilgilerini kimlik doğrulama biletinin UserData özelliğinde depolıyoruz. Ancak, UserData bilgisine yalnızca kimlik doğrulama bileti ve yalnızca serileştirilmiş bir dize olarak erişilebilir, yani UserData özelliğini ayrıştırabilmemiz için gereken bilet içinde depolanan kullanıcı bilgilerini görüntülemek istiyoruz.

IIdentity uygulayan ve CompanyName ve title özelliklerini içeren bir sınıf oluşturarak geliştirici deneyimini iyileştirebiliriz. Bu şekilde, bir geliştirici Şu anda oturum açmış olan kullanıcının şirket adına ve başlığına, UserData özelliğinin nasıl ayrıştırılacağından emin olmadan doğrudan CompanyName ve başlık özellikleri aracılığıyla erişebilir.

### <a name="creating-the-custom-identity-and-principal-classes"></a>Özel kimlik ve asıl sınıfları oluşturma

Bu öğreticide, uygulama\_kodu klasöründe özel sorumlu ve kimlik nesnelerini oluşturalım. Projenize bir uygulama\_kod klasörü ekleyerek başlayın-Çözüm Gezgini ' de proje adına sağ tıklayın, ASP.NET klasörünü Ekle seçeneğini belirleyin ve uygulama\_kodu ' nu seçin. Uygulama\_kodu klasörü, Web sitesine özel sınıf dosyalarını tutan özel bir ASP.NET klasörüdür.

> [!NOTE]
> Uygulama\_kodu klasörü yalnızca projeniz Web sitesi proje modeli aracılığıyla yönetirken kullanılmalıdır. [Web uygulaması proje modeli](https://msdn.microsoft.com/asp.net/Aa336618.aspx)kullanıyorsanız, standart bir klasör oluşturun ve bu sınıfa sınıfları ekleyin. Örneğin, sınıflar adlı yeni bir klasör ekleyebilir ve kodunuzu buraya yerleştirebilirsiniz.

Ardından, App\_Code klasörüne, biri CustomIdentity.cs ve diğeri CustomPrincipal.cs adlı iki yeni sınıf dosyası ekleyin.

[![Customıdentity ve CustomPrincipal sınıflarını projenize ekleyin](forms-authentication-configuration-and-advanced-topics-cs/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image16.png)

**Şekil 06**: Customıdentity ve CustomPrincipal sınıflarını projenize ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image18.png))

Customıdentity sınıfı, AuthenticationType, IsAuthenticated ve ad özelliklerini tanımlayan IIdentity arabirimini uygulamaktan sorumludur. Gerekli özelliklere ek olarak, temel form kimlik doğrulama biletini ve kullanıcının şirket adı ve başlığına ilişkin özellikleri de açığa çıkarıyoruz. Customıdentity sınıfına aşağıdaki kodu girin.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample9.cs)]

Sınıfının bir FormsAuthenticationTicket üye değişkeni (\_bileti) içerdiğine ve bu bilet bilgilerinin Oluşturucu aracılığıyla sağlanması gerektiğini unutmayın. Bu bilet verileri, kimliğin adını döndürmek için kullanılır; UserData özelliği, CompanyName ve title özelliklerinin değerlerini döndürecek şekilde ayrıştırılır.

Sonra, CustomPrincipal sınıfını oluşturun. Bu juncture 'teki rollerle ilgilenmediğimiz için, CustomPrincipal sınıfının Oluşturucusu yalnızca bir Customıdentity nesnesi kabul eder; IsInRole yöntemi her zaman false döndürür.

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample10.cs)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>Gelen Isteğin güvenlik bağlamına bir CustomPrincipal nesnesi atama

Artık, varsayılan IIdentity belirtimini, CompanyName ve title özelliklerinin yanı sıra özel kimliği kullanan özel bir asıl sınıfı kapsayacak şekilde genişleten bir sınıftır. ASP.NET ardışık düzeninde çalışmaya ve özel sorumlu nesnemizi gelen isteğin güvenlik bağlamına atamaya hazırız.

ASP.NET işlem hattı gelen bir isteği alır ve bir dizi adım aracılığıyla işler. Her adımda, geliştiricilerin ASP.NET işlem hattına dokunmasını ve isteği yaşam döngüsünün belirli noktalarında değiştirmesini olanaklı hale getiren belirli bir olay tetiklenir. Örneğin, FormsAuthenticationModule, bir kimlik doğrulama bileti için gelen isteği inceleyerek, ASP.NET tarafından kimlik [doğrulayan Terequest olayını](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx)tetiklememesini bekler. Bir kimlik doğrulama anahtarı bulunursa, bir GenericPrincipal nesnesi oluşturulur ve HttpContext. User özelliğine atanır.

Kimlik doğrulayan Terequest olayından sonra, ASP.NET işlem hattı, FormsAuthenticationModule tarafından oluşturulan GenericPrincipal nesnesini CustomPrincipal nesnemizin örneğiyle değiştirecek olan Postakimliği [Caterequest olayını](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx)oluşturur. Şekil 7 Bu iş akışını gösterir.

[![GenericPrincipal, PostAuthenticationRequest olaydaki bir CustomPrincipal ile değiştirilmiştir](forms-authentication-configuration-and-advanced-topics-cs/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image19.png)

**Şekil 07**: GenericPrincipal, PostAuthenticationRequest olaydaki bir CustomPrincipal ile değiştirilmiştir ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image21.png))

Kodu bir ASP.NET işlem hattı olayına yanıt olarak yürütmek için, Global. asax dosyasında uygun olay işleyicisini oluşturabilir veya kendi HTTP modülümüzü oluşturabilirsiniz. Bu öğreticide, Global. asax dosyasında olay işleyicisini oluşturalım. Web sitenize Global. asax ekleyerek başlayın. Çözüm Gezgini içindeki proje adına sağ tıklayın ve Global. asax adlı genel uygulama sınıfı türünde bir öğe ekleyin.

[![Web sitenize Global. asax dosyası ekleyin](forms-authentication-configuration-and-advanced-topics-cs/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-cs/_static/image22.png)

**Şekil 08**: Web sitenize Global. asax dosyası ekleme ([tam boyutlu görüntüyü görüntülemek için tıklayın](forms-authentication-configuration-and-advanced-topics-cs/_static/image24.png))

Varsayılan Global. asax şablonu, diğer bir deyişle, başlangıç, bitiş ve [hata olayı](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx)dahil olmak üzere bir dizi ASP.NET işlem hattı olayına yönelik olay işleyicilerini içerir. Bu uygulama için gerekli olmadığı için bu olay işleyicilerini kaldırmayı ücretsiz olarak hissettik. İlgilendiğiniz olay postasız Caterequest ' dir. Global. asax dosyanızı, biçimlendirmesi şuna benzer şekilde güncelleştirin:

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample11.aspx)]

Uygulama\_Onpostano Caterequest yöntemi, her gelen sayfa isteğinde bir kez gerçekleştirilen her bir ASP.NET çalışma zamanı için postano Caterequest olayını her seferinde yürütülür. Olay işleyicisi, kullanıcının kimliğinin doğrulandığına ve Forms kimlik doğrulaması aracılığıyla kimlik doğrulamasından geçirilme olup olmadığını denetleyerek başlar. Bu durumda, yeni bir Customıdentity nesnesi oluşturulur ve kendi oluşturucusunda geçerli isteğin kimlik doğrulama bileti geçirilir. Bunun ardından, bir CustomPrincipal nesnesi oluşturulur ve yapıcısında yeni oluşturulmuş Customıdentity nesnesini geçirilir. Son olarak, geçerli isteğin güvenlik bağlamı yeni oluşturulan CustomPrincipal nesnesine atanır.

Son adım-CustomPrincipal nesnesini isteğin güvenlik içeriğiyle ilişkilendirme-sorumluyu iki özelliğe atar: HttpContext. User ve Thread. CurrentPrincipal. Bu iki atama, güvenlik bağlamlarının ASP.NET içinde işlendiği şekilde gereklidir. .NET Framework, çalışan her iş parçacığıyla bir güvenlik bağlamını ilişkilendirir; Bu bilgiler, [Iş parçacığı nesnesinin](https://msdn.microsoft.com/library/system.threading.thread.aspx) [CurrentPrincipal özelliği](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx)aracılığıyla bir IPrincipal nesnesi olarak kullanılabilir. Kafa karıştırıcı nedir, ASP.NET kendi güvenlik bağlamı bilgisine (HttpContext. User) sahiptir.

Bazı senaryolarda, Iş parçacığı. CurrentPrincipal özelliği güvenlik bağlamı belirlenirken incelenir; diğer senaryolarda, HttpContext. User kullanılır. Örneğin, .NET ' te, geliştiricilerin hangi kullanıcıların veya rollerin bir sınıf örneği oluşturmasını veya belirli yöntemleri çağırabilmesini sağlayan güvenlik özellikleri vardır (bkz. [PrincipalPermissionAttributes kullanarak iş ve veri katmanlarına yetkilendirme kuralları ekleme](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)). Kapakların altında, bu bildirim temelli teknikler Iş parçacığı. CurrentPrincipal özelliği aracılığıyla güvenlik bağlamını tespit.

Diğer senaryolarda, HttpContext. User özelliği kullanılır. Örneğin, önceki öğreticide bu özelliği şu anda oturum açmış kullanıcının Kullanıcı adını görüntüleyecek şekilde kullandık. Açık olarak, Iş parçacığı. CurrentPrincipal ve HttpContext. User özelliklerindeki Güvenlik bağlamı bilgilerinin eşleşmesi zorunludur.

ASP.NET çalışma zamanı, bu özellik değerlerini ABD için otomatik olarak eşitler. Ancak, bu eşitleme, kimlik doğrulayan Terequest olayından sonra, vb. Caterequest olayından *önce* oluşur. Sonuç olarak, postakimliği \ Terequest olayında özel bir sorumlu eklendiğinde, Iş parçacığını el ile atamak için belirli bir sorumlusu olması gerekir. CurrentPrincipal veya else Thread. CurrentPrincipal ve HttpContext. User eşitlenmemiş. Bu sorunla ilgili daha ayrıntılı bir tartışma için bkz. [Context. User vs. Thread. CurrentPrincipal](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/) .

### <a name="accessing-the-companyname-and-title-properties"></a>CompanyName ve title özelliklerine erişme

Bir istek ulaştığında ve ASP.NET altyapısına her bağlandığında, Global. asax dosyasındaki uygulama\_Onpostano Caterequest olay işleyicisi başlatılır. İstek, FormsAuthenticationModule tarafından başarıyla doğrulanmışsa, olay işleyicisi form kimlik doğrulama biletini temel alan bir Customıdentity nesnesi ile yeni bir CustomPrincipal nesnesi oluşturur. Bu mantığa sahip olmak üzere, şu anda oturum açmış kullanıcının şirket adı ve başlığıyla ilgili bilgilere erişmek inanılmaz basittir.

Varsayılan. aspx dosyasında, 1. adımda form kimlik doğrulama anahtarını almak için kod yazdığımızda ve kullanıcının şirket adını ve başlığını göstermek için UserData özelliğini ayrıştırtığımız sayfa\_yükleme olay işleyicisine geri dönün. CustomPrincipal ve Customıdentity nesneleri şu anda kullanımda olduğunda, Bilet 'nin UserData özelliğinden değerleri ayrıştırmaya gerek yoktur. Bunun yerine, Customıdentity nesnesine bir başvuru alın ve CompanyName ve title özelliklerini kullanın:

[!code-csharp[Main](forms-authentication-configuration-and-advanced-topics-cs/samples/sample12.cs)]

## <a name="summary"></a>Özet

Bu öğreticide, Forms kimlik doğrulaması sisteminin ayarlarını Web. config aracılığıyla özelleştirmeyi inceledik. Kimlik doğrulama anahtarının süre sonunu nasıl ele aldığımızda ve şifreleme ve doğrulama korumalarının bilet İnceleme ve değiştirme işlemleri için nasıl kullanıldığını inceledik. Son olarak, Bilet içinde ek kullanıcı bilgilerini depolamak için kimlik doğrulama biletinin UserData özelliğini kullanarak ve bu bilgileri daha kolay bir şekilde kullanıma sunmak için özel sorumlu ve kimlik nesneleri kullanmayı tartıştık.

Bu öğreticide, ASP.NET 'de form kimlik doğrulaması incelemesi yer aldığı için sonlanır. Bir sonraki öğreticide, üyelik çerçevesine yönelik yolculuğa başlanır.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [Form kimlik doğrulamasını ayırma](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [Açıklanıyor: ASP.NET 2,0 'de Forms kimlik doğrulaması](https://msdn.microsoft.com/library/aa480476.aspx)
- [Nasıl yapılır: ASP.NET 2,0 'de form kimlik doğrulamasını koruma](https://msdn.microsoft.com/library/ms998310.aspx)
- [Professional ASP.NET 2,0 güvenlik, üyelik ve rol yönetimi](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ısbn: 978-0-7645-9698-8)
- [Oturum açma denetimlerinin güvenliğini sağlama](https://msdn.microsoft.com/library/ms178346.aspx)
- [&lt;Authentication&gt; öğesi](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&lt;Forms &lt;kimlik doğrulaması için&gt; öğesi&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [&lt;machineKey&gt; öğesi](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [Forms kimlik doğrulama biletini ve tanımlama bilgisini anlama](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Bu öğreticide bulunan konularda video eğitimi

- [Form kimlik doğrulama özelliklerini değiştirme](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [ASP.NET uygulamasında tanımlama bilgisi-Less kimlik doğrulamasını ayarlama ve kullanma](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [ASP Forms Oturum Açmayı Yeniden Konumlandırma](../../../videos/authentication/asp-forms-login-relocation.md)
- [Forms Oturum Açma Özel Anahtar Yapılandırması](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [Kimlik Doğrulama Metoduna Özel Veri Ekleme](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [Özel Asıl Nesneler Kullanma](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>Yazar hakkında

Birden çok ASP/ASP. NET Books ve 4GuysFromRolla.com 'in yazarı Scott Mitchell, 1998 sürümünden bu yana Microsoft Web teknolojileriyle birlikte çalışıyor. Scott bağımsız danışman, Trainer ve yazıcı olarak çalışıyor. En son kitabı, *[24 saat içinde ASP.NET 2,0 kendi kendinize eğitim](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* ister. Scott 'a [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) veya blogundan [http://ScottOnWriting.NET](http://scottonwriting.net/)üzerinden erişilebilir.

### <a name="special-thanks-to"></a>Özel olarak teşekkürler

Bu öğretici serisi birçok yararlı gözden geçirenler tarafından incelendi. Bu öğretici için lider gözden geçiren Alicja Maziarz. Yaklaşan MSDN makalelerimi gözden geçiriyor musunuz? Öyleyse, beni [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com)bir satır bırakın.

> [!div class="step-by-step"]
> [Önceki](an-overview-of-forms-authentication-cs.md)
> [İleri](security-basics-and-asp-net-support-vb.md)
