---
uid: web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
title: Profiller, Temalar ve Web Bölümleri | Microsoft Docs
author: microsoft
description: ASP.NET 2,0 ' de yapılandırma ve araçlardaki önemli değişiklikler vardır. Yeni ASP.NET Configuration API 'SI, yapılandırma değişikliklerinin PR 'ye yapılmasına izin verir...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 92df4051-77c6-492c-bd34-23d24189cea4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/profiles-themes-and-web-parts
msc.type: authoredcontent
ms.openlocfilehash: cf5c45781be6d003d28c6aa27efa08032579a6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587236"
---
# <a name="profiles-themes-and-web-parts"></a>Profiller, Temalar ve Web Bölümleri

[Microsoft](https://github.com/microsoft) tarafından

> ASP.NET 2,0 ' de yapılandırma ve araçlardaki önemli değişiklikler vardır. Yeni ASP.NET yapılandırma API 'SI, yapılandırma değişikliklerinin programlı olarak yapılmasına izin verir. Ayrıca, birçok yeni yapılandırma ayarı yeni yapılandırmalar ve izleme için izin verir.

ASP.NET 2,0, kişiselleştirilmiş Web siteleri alanındaki önemli bir gelişimi temsil eder. Zaten kapsandığımız üyelik özelliklerine ek olarak, ASP.NET profilleri, Temalar ve Web bölümleri, Web sitelerinde kişiselleştirmeyi önemli ölçüde geliştirir.

## <a name="aspnet-profiles"></a>ASP.NET profilleri

ASP.NET profilleri oturumlara benzerdir. Bu fark, tarayıcı kapandığında bir oturumun kaybedilmesi durumunda bir profilin kalıcı olduğu farktır. Oturumlar ve profiller arasındaki başka bir büyük fark, profillerin kesin bir şekilde yazılmasından dolayı geliştirme sürecinde IntelliSense 'i sağlamaktır.

Bir profil, uygulamanın makineler yapılandırma dosyasında veya Web. config dosyasında tanımlanır. (Bir profili alt klasörler Web. config dosyasında tanımlayamazsınız.) Aşağıdaki kod, Web sitesi ziyaretçilerinin ilk ve son adını depolamak için bir profil tanımlar.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample1.xml)]

Bir profil özelliği için varsayılan veri türü System. String 'dir. Yukarıdaki örnekte, veri türü belirtilmedi. Bu nedenle, FirstName ve LastName özelliklerinin ikisi de tür dizesidir. Daha önce belirtildiği gibi, profil özellikleri kesin olarak türdedir. Aşağıdaki kod, Int32 türünde bir yaş için yeni bir özellik ekler.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample2.xml)]

Profiller genellikle ASP.NET Forms kimlik doğrulamasıyla kullanılır. Form kimlik doğrulamasıyla birlikte kullanıldığında, her kullanıcının Kullanıcı KIMLIĞIYLE ilişkili ayrı bir profili vardır. Bununla birlikte, aşağıdaki gibi, **AllowAnonymous** özniteliğiyle birlikte yapılandırma dosyasında &lt;anonymousıdentification&gt; öğesi kullanılarak adsız bir uygulamadaki profillerin kullanılmasına izin vermek da mümkündür:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample3.xml)]

Anonim Kullanıcı siteye gözattığında, ASP.NET Kullanıcı için bir **ProfileCommon** örneği oluşturur. Bu profil, kullanıcıyı benzersiz bir ziyaretçi olarak tanımlamak için tarayıcıda bir tanımlama bilgisinde depolanan benzersiz bir KIMLIK kullanır. Bu şekilde, anonim olarak gözalayan kullanıcılar için profil bilgilerini saklayabilirsiniz.

## <a name="profile-groups"></a>Profil grupları

Profillerin özelliklerini gruplamak mümkündür. Özellikleri gruplandırarak, belirli bir uygulama için birden çok profilin benzetimini yapmak mümkündür.

Aşağıdaki yapılandırma iki grup için bir FirstName ve LastName özelliği yapılandırır; Alıcılar ve aday.

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample4.xml)]

Daha sonra belirli bir gruptaki özellikleri aşağıdaki gibi ayarlamak mümkündür:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample5.cs)]

## <a name="storing-complex-objects"></a>Karmaşık nesneleri depolama

Şimdiye kadar, kapsandığımız örneklerde basit veri türleri bir profilde depolanmaktadır. Ayrıca, **SerializeAs** özniteliğini kullanarak serileştirme yöntemini aşağıdaki şekilde belirterek, karmaşık veri türlerini bir profilde depolamak mümkündür:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample6.xml)]

Bu durumda, türü PurchaseInvoice ' dir. PurchaseInvoice sınıfının seri hale getirilebilir olarak işaretlenmesi ve herhangi bir sayıda özellik içermesi gerekir. Örneğin, PurchaseInvoice **Numıtemspurchased**adlı bir özelliğe sahipse, koddaki bu özelliğe aşağıdaki gibi başvurabilirsiniz:

[!code-css[Main](profiles-themes-and-web-parts/samples/sample7.css)]

## <a name="profile-inheritance"></a>Profil devralma

Birden çok uygulamada kullanılmak üzere bir profil oluşturmak mümkündür. ProfileBase 'den türetilen bir profil sınıfı oluşturarak, aşağıda gösterildiği gibi **Inherits** özniteliğini kullanarak birkaç uygulamada bir profili yeniden kullanabilirsiniz:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample8.xml)]

Bu durumda, **Purchasingprofile** sınıfı şöyle görünür:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample9.cs)]

## <a name="profile-providers"></a>Profil sağlayıcıları

ASP.NET profilleri sağlayıcı modelini kullanır. Varsayılan sağlayıcı, bilgileri, SqlProfileProvider sağlayıcısını kullanarak Web uygulamasının App\_Data klasöründe bir SQL Server Express veritabanında depolar. Veritabanı yoksa, profil bilgileri depolamayı denediğinde ASP.NET otomatik olarak oluşturur.

Ancak bazı durumlarda, kendi profil sağlayıcınızı geliştirmek isteyebilirsiniz. ASP.NET profili özelliği, farklı sağlayıcıları kolayca kullanmanıza olanak sağlar.

Şu durumlarda bir özel profil sağlayıcısı oluşturursunuz:

- Profil bilgilerini, .NET Framework dahil edilen profil sağlayıcıları tarafından desteklenmeyen bir FoxPro veritabanı veya Oracle veritabanı gibi bir veri kaynağında depolamanız gerekir.
- .NET Framework bulunan sağlayıcılar tarafından kullanılan veritabanı şemasından farklı bir veritabanı şeması kullanarak profil bilgilerini yönetmeniz gerekir. Ortak bir örnek, profil bilgilerini var olan bir SQL Server veritabanındaki kullanıcı verileriyle tümleştirmenizi istiyoruz.

### <a name="required-classes"></a>Gerekli sınıflar

Bir profil sağlayıcısı uygulamak için, System. Web. Profile. ProfileProvider soyut sınıfını devralan bir sınıf oluşturursunuz. İçindeki **ProfileProvider** soyut sınıfı, System. Configuration. Provider. ProviderBase soyut sınıfını devralan System. Configuration. SettingsProvider soyut sınıfını devralır. Bu devralma zinciri nedeniyle, **ProfileProvider** sınıfının gerekli üyelerine ek olarak, **SettingsProvider** ve **ProviderBase** sınıflarının gerekli üyelerini uygulamanız gerekir.

Aşağıdaki tablolarda, **ProviderBase**, **SettingsProvider**ve **ProfileProvider** soyut sınıflarından uygulamanız gereken özellikler ve yöntemler açıklanır.

### <a name="providerbase-members"></a>ProviderBase üyeleri

| **Üyesidir** | **Açıklama** |
| --- | --- |
| Initialize yöntemi | , Sağlayıcı örneğinin adını ve yapılandırma ayarlarının NameValueCollection öğesini giriş olarak alır. Makine yapılandırması veya Web. config dosyasında belirtilen uygulamaya özgü değerler ve seçenekler dahil olmak üzere, sağlayıcı örneği için seçenekleri ve özellik değerlerini ayarlamak için kullanılır. |

### <a name="settingsprovider-members"></a>SettingsProvider üyeleri

| **Üyesidir** | **Açıklama** |
| --- | --- |
| ApplicationName özelliği | Her bir profille depolanan uygulama adı. Profil sağlayıcısı, her bir uygulama için profil bilgilerini ayrı olarak depolamak üzere uygulama adını kullanır. Bu, farklı uygulamalarda aynı Kullanıcı adı oluşturulduysa, birden çok ASP.NET uygulamasının bir çakışma olmadan aynı veri kaynağını kullanmasına olanak sağlar. Alternatif olarak, birden çok ASP.NET uygulaması aynı uygulama adını belirterek bir profil veri kaynağını paylaşabilir. |
| GetPropertyValues yöntemi | Bir SettingsContext ve SettingsPropertyCollection nesnesi giriş olarak alır. **SettingsContext** Kullanıcı hakkında bilgi sağlar. Kullanıcının profil özellik bilgilerini almak için bilgileri birincil anahtar olarak kullanabilirsiniz. Kullanıcı adını ve kullanıcının kimliği doğrulanmış veya anonim olup olmadığını almak için **SettingsContext** nesnesini kullanın. **SettingsPropertyCollection** , SettingsProperty nesnelerinin bir koleksiyonunu içerir. Her **SettingsProperty** nesnesi, özelliğin adını ve türünü ve özellik için varsayılan değer gibi ek bilgileri ve özelliğin salt okunurdur olduğunu sağlar. **GetPropertyValues** yöntemi, giriş olarak sunulan **SettingsProperty** nesnelerine bağlı olarak SettingsPropertyValueCollection 'ı SettingsPropertyValue nesneleriyle doldurur. Belirtilen kullanıcı için veri kaynağından alınan değerler her **SettingsPropertyValue** nesnesinin PropertyValue özelliklerine atanır ve tüm koleksiyon döndürülür. Yöntemi çağırmak, belirtilen kullanıcı profili için LastActivityDate değerini geçerli tarih ve saate da güncelleştirir. |
| SetPropertyValues yöntemi | Bir **SettingsContext** ve **SettingsPropertyValueCollection** nesnesini giriş olarak alır. **SettingsContext** Kullanıcı hakkında bilgi sağlar. Kullanıcının profil özellik bilgilerini almak için bilgileri birincil anahtar olarak kullanabilirsiniz. Kullanıcı adını ve kullanıcının kimliği doğrulanmış veya anonim olup olmadığını almak için **SettingsContext** nesnesini kullanın. **SettingsPropertyValueCollection** , **SettingsPropertyValue** nesnelerinin bir koleksiyonunu içerir. Her **SettingsPropertyValue** nesnesi, özelliğin adını, türünü ve değerini, özelliği için varsayılan değer ve özelliğin salt okunurdur gibi ek bilgileri sağlar. **SetPropertyValues** yöntemi, belirtilen kullanıcı için veri kaynağındaki profil özellik değerlerini güncelleştirir. Yöntemi çağırmak, belirtilen kullanıcı profili için **LastActivityDate** ve LastUpdatedDate değerlerini geçerli tarih ve saate da güncelleştirir. |

### <a name="profileprovider-members"></a>ProfileProvider üyeleri

| **Üyesidir** | **Açıklama** |
| --- | --- |
| DeleteProfiles yöntemi | Giriş olarak, uygulama adının **ApplicationName** özelliği değeri ile eşleşen belirtilen adların tüm profil bilgileri ve özellik değerleri için bir dizi Kullanıcı adı ve veri kaynağından siler olarak alır. Veri kaynağınız işlemleri destekliyorsa, tüm silme işlemlerini bir işlemde eklemeniz ve işlemi geri almanız ve herhangi bir silme işlemi başarısız olursa bir özel durum oluşturmanız önerilir. |
| DeleteProfiles yöntemi | Bir ProfileInfo nesneleri koleksiyonunu giriş olarak alır ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği her profil için veri kaynağından tüm profil bilgileri ve özellik değerleri silinir. Veri kaynağınız işlemleri destekliyorsa, tüm silme işlemlerini bir işlem içinde dahil etmeniz ve işlemi geri almanız ve herhangi bir silme işlemi başarısız olursa bir özel durum oluşturmanız önerilir. |
| DeleteInactiveProfiles yöntemi | Bir ProfileAuthenticationOption değeri ve bir DateTime nesnesi girişi yapın ve son etkinlik tarihinin belirtilen tarih ve saatten küçük ya da buna eşit olduğu ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği tüm profil bilgileri ve özellik değerleri veri kaynağından siler. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimliği doğrulanmış profillerin mi yoksa tüm profillerin mi silineceğini belirtir. Veri kaynağınız işlemleri destekliyorsa, tüm silme işlemlerini bir işlem içinde dahil etmeniz ve işlemi geri almanız ve herhangi bir silme işlemi başarısız olursa bir özel durum oluşturmanız önerilir. |
| GetAllProfiles yöntemi | Bir **ProfileAuthenticationOption** değeri, sayfa dizinini belirten bir tamsayı, sayfa boyutunu belirten bir tamsayı ve toplam profil sayısı olarak ayarlanacak bir tamsayıya başvuru olarak alır. Uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profiller Için **ProfileInfo** nesnelerini Içeren bir ProfileInfoCollection döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimliği doğrulanmış profillerin veya tüm profillerin döndürülüp döndürülmeyeceğini belirtir. **GetAllProfiles** yöntemi tarafından döndürülen sonuçlar sayfa dizini ve sayfa boyutu değerleri tarafından sınırlandırılır. Sayfa boyutu değeri, **ProfileInfoCollection**içinde döndürülecek olan en fazla **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri döndürülecek sonuç sayfasını belirtir; burada 1 ilk sayfayı tanımlar. Toplam kayıt parametresi, toplam profil sayısına ayarlanmış bir out parametresidir (Visual Basic **ByRef** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizini değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** , onuncu profiller aracılığıyla altıncı ' i içerir. Yöntemin döndürdüğü toplam kayıtlar değeri 13 olarak ayarlanır. |
| GetAllInactiveProfiles yöntemi | Bir **ProfileAuthenticationOption** değeri, bir **DateTime** nesnesi, sayfa dizinini belirten bir tamsayı, sayfa boyutunu belirten bir tamsayı ve toplam profil sayısı olarak ayarlanacak bir tamsayıya başvuru olarak alır. Son etkinlik tarihinin belirtilen **Tarih/** saatten küçük veya bu değere eşit olduğu ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profiller için **ProfileInfo** nesnelerini içeren bir **ProfileInfoCollection** döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimliği doğrulanmış profillerin veya tüm profillerin döndürülüp döndürülmeyeceğini belirtir. **Getallinactiveprofiles** yöntemi tarafından döndürülen sonuçlar sayfa dizini ve sayfa boyutu değerleri tarafından sınırlandırılır. Sayfa boyutu değeri, **ProfileInfoCollection**içinde döndürülecek olan en fazla **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri döndürülecek sonuç sayfasını belirtir; burada 1 ilk sayfayı tanımlar. Toplam kayıt parametresi, toplam profil sayısına ayarlanmış bir out parametresidir (Visual Basic **ByRef** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizini değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** , onuncu profiller aracılığıyla altıncı ' i içerir. Yöntemin döndürdüğü toplam kayıtlar değeri 13 olarak ayarlanır. |
| FindProfilesByUserName yöntemi | Bir **ProfileAuthenticationOption** değeri, bir Kullanıcı adı içeren bir dize, sayfa dizinini belirten bir tamsayı, sayfa boyutunu belirten bir tamsayı ve toplam profil sayısı olarak ayarlanacak bir tamsayı başvurusu olan giriş olarak alır. Kullanıcı adının belirtilen kullanıcı adıyla eşleştiği ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği veri kaynağındaki tüm profiller Için **ProfileInfo** nesnelerini Içeren bir **ProfileInfoCollection** döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimliği doğrulanmış profillerin veya tüm profillerin döndürülüp döndürülmeyeceğini belirtir. Veri kaynağınız joker karakterler gibi ek arama özelliklerini destekliyorsa, Kullanıcı adları için daha kapsamlı arama özellikleri sağlayabilirsiniz. **FindProfilesByUserName** yöntemi tarafından döndürülen sonuçlar sayfa dizini ve sayfa boyutu değerleri tarafından sınırlandırılır. Sayfa boyutu değeri, **ProfileInfoCollection**içinde döndürülecek olan en fazla **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri döndürülecek sonuç sayfasını belirtir; burada 1 ilk sayfayı tanımlar. Toplam kayıt parametresi, toplam profil sayısına ayarlanmış bir out parametresidir (Visual Basic **ByRef** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizini değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** , onuncu profiller aracılığıyla altıncı ' i içerir. Yöntemin döndürdüğü toplam kayıtlar değeri 13 olarak ayarlanır. |
| Finınactiveprofilesbyusername yöntemi | Bir **ProfileAuthenticationOption** değeri, bir Kullanıcı adı içeren bir dize, bir **DateTime** nesnesi, sayfa dizinini belirten bir tamsayı, sayfa boyutunu belirten bir tamsayı ve toplam profil sayısı olarak ayarlanacak bir tamsayıya başvuru olarak alır. Veri kaynağındaki tüm profiller için, Kullanıcı adının belirtilen **Tarih/saatteki**değerden küçük veya bu değere eşit olduğu ve uygulama adının **ApplicationName** özellik değeriyle eşleştiği tüm profiller için **ProfileInfo** nesnelerini içeren bir **ProfileInfoCollection** döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimliği doğrulanmış profillerin veya tüm profillerin döndürülüp döndürülmeyeceğini belirtir. Veri kaynağınız joker karakterler gibi ek arama özelliklerini destekliyorsa, Kullanıcı adları için daha kapsamlı arama özellikleri sağlayabilirsiniz. **FindInactiveProfilesByUserName** yöntemi tarafından döndürülen sonuçlar sayfa dizini ve sayfa boyutu değerleri tarafından sınırlandırılır. Sayfa boyutu değeri, **ProfileInfoCollection**içinde döndürülecek olan en fazla **ProfileInfo** nesne sayısını belirtir. Sayfa dizini değeri döndürülecek sonuç sayfasını belirtir; burada 1 ilk sayfayı tanımlar. Toplam kayıt parametresi, toplam profil sayısına ayarlanmış bir out parametresidir (Visual Basic **ByRef** kullanabilirsiniz). Örneğin, veri deposu uygulama için 13 profil içeriyorsa ve sayfa dizini değeri 5 sayfa boyutuyla 2 ise, döndürülen **ProfileInfoCollection** , onuncu profiller aracılığıyla altıncı ' i içerir. Yöntemin döndürdüğü toplam kayıtlar değeri 13 olarak ayarlanır. |
| GetNumberOfInactiveProfiles yöntemi | Bir **ProfileAuthenticationOption** değeri ve bir **DateTime** nesnesi girişi yapın ve veri kaynağındaki tüm profillerin sayısını, son etkinlik tarihinin belirtilen **Tarih/** saatten küçük veya bu değere eşit ya da uygulama adının **ApplicationName** özellik değeriyle eşleştiği yere döndürür. **ProfileAuthenticationOption** parametresi yalnızca anonim profillerin, yalnızca kimliği doğrulanmış profillerin veya tüm profillerin sayılıp sayılmayacağını belirtir. |

### <a name="applicationname"></a>ApplicationName

Profil sağlayıcıları her bir uygulama için profil bilgilerini ayrı olarak depoladığından, veri şemanızın uygulama adını içerdiğinden ve sorguların ve güncelleştirmelerin de uygulama adını içerdiğinden emin olmanız gerekir. Örneğin, aşağıdaki komut, Kullanıcı adına göre bir veritabanından bir özellik değeri almak için kullanılır ve profilin anonim olup olmadığını ve **ApplicationName** değerinin sorguya dahil edilmesini sağlar.

[!code-sql[Main](profiles-themes-and-web-parts/samples/sample10.sql)]

## <a name="aspnet-themes"></a>ASP.NET Temalar

## <a name="what-are-aspnet-20-themes"></a>ASP.NET 2,0 temaları nelerdir?

Bir Web uygulamasının en önemli özelliklerinden biri, site genelinde tutarlı bir görünüm ve kullanım açısından. ASP.NET 1. x geliştiricileri, tutarlı bir görünüm uygulamak için genellikle Geçişli Stil Sayfaları (CSS) kullanır. ASP.NET 2,0 temaları, ASP.NET geliştiricilerine ASP.NET sunucu denetimlerinin yanı sıra HTML öğelerinin görünümünü tanımlama olanağı sağladığından, CSS üzerinde önemli ölçüde iyileştirilmesine olanak sağlar. ASP.NET temaları tek tek denetimlere, belirli bir Web sayfasına veya bir Web uygulamasına uygulanabilir. Temalar bir CSS dosyaları, isteğe bağlı bir kaplama dosyası ve görüntüler gerekiyorsa isteğe bağlı bir görüntüler dizini kullanır. Dış görünüm dosyası, ASP.NET Server denetimlerinin görsel görünümünü denetler.

## <a name="where-are-themes-stored"></a>Temalar nerede depolanır?

Temaların depolanacağı konum kapsamlarına göre farklılık gösterir. Herhangi bir uygulamaya uygulanabilecek Temalar şu klasörde depolanır:

`C:\WINDOWS\Microsoft.NET\Framework\v2.x.xxxxx\ASP.NETClientFiles\Themes\<Theme_Name>`

Belirli bir uygulamaya özgü bir tema, Web sitesinin kökündeki bir `App\_Themes\<Theme\_Name>` dizininde depolanır.

> [!NOTE]
> Bir kaplama dosyası yalnızca görünümü etkileyen sunucu denetimi özelliklerini değiştirmeli.

Genel tema, Web sunucusu üzerinde çalışan herhangi bir uygulamaya veya Web sitesine uygulanabilen bir temadır. Bu Temalar, varsayılan olarak v2. x. xxxxx dizininin içindeki ASP. NETClientfiles\Themes dizininde saklanır. Alternatif olarak, tema dosyalarını web sitenizin kökündeki ASPNET\_Client/System\_Web/[Version]/Themes/[Theme\_Name] klasörüne taşıyabilirsiniz.

Uygulamaya özgü Temalar yalnızca dosyaların bulunduğu uygulamaya uygulanabilir. Bu dosyalar, Web sitesinin kökündeki `App\_Themes/<theme\_name>` dizininde depolanır.

## <a name="the-components-of-a-theme"></a>Bir temanın bileşenleri

Bir tema, bir veya daha fazla CSS dosyasından, isteğe bağlı bir kaplama dosyasından ve isteğe bağlı bir görüntüler klasöründen oluşur. CSS dosyaları istediğiniz herhangi bir ad olabilir (yani default. CSS veya Theme. css, vb.) ve Temalar klasörünün kökünde olması gerekir. CSS dosyaları, belirli seçicilerin normal CSS sınıflarını ve özniteliklerini tanımlamak için kullanılır. CSS sınıflarından birini bir sayfa öğesine uygulamak için **CssClass** özelliği kullanılır.

Dış görünüm dosyası, ASP.NET Server denetimleri için özellik tanımlarını içeren bir XML dosyasıdır. Aşağıda listelenen kod örnek bir dış görünüm dosyasıdır.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample11.aspx)]

Aşağıdaki **Şekil 1** ' de bir tema uygulanmadan gözatılan küçük bir ASP.NET sayfası görülmektedir. **Şekil 2** ' de tema uygulanmış aynı dosya gösterilmektedir. Arka plan rengi ve metin rengi bir CSS dosyası aracılığıyla yapılandırılır. Düğme ve metin kutusunun görünümü yukarıda listelenen dış görünüm dosyası kullanılarak yapılandırılır.

![Tema yok](profiles-themes-and-web-parts/_static/image1.gif)

**Şekil 1**: tema yok

![Tema uygulandı](profiles-themes-and-web-parts/_static/image2.gif)

**Şekil 2**: Tema uygulandı

Yukarıda listelenen dış görünüm dosyası, tüm TextBox denetimleri ve düğme denetimleri için varsayılan bir kaplama tanımlar. Diğer bir deyişle, bir sayfaya eklenen her TextBox denetimi ve düğme denetiminin bu görünümde gerçekleştirilecek olması anlamına gelir. Ayrıca, denetimin **SkinID** özelliğini kullanarak bu denetimlerin belirli örneklerine uygulanabilen bir kaplama de tanımlayabilirsiniz.

Aşağıdaki kod bir düğme denetimi için bir kaplama tanımlar. Yalnızca **Gobtan** 'ın **SkinID** özelliğine sahip düğme denetimleri, kaplamanın görünümünde yer alır.

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample12.aspx)]

Sunucu denetim türü başına yalnızca bir varsayılan dış görünüme sahip olabilirsiniz. Ek kaplamalar gerekiyorsa, SkinID özelliğini kullanmanız gerekir.

## <a name="applying-themes-to-pages"></a>Sayfalara tema uygulama

Bir tema, aşağıdaki yöntemlerden biri kullanılarak uygulanabilir:

- Web. config dosyasının &lt;Pages&gt; öğesi
- Bir sayfanın @Page yönergesinde
- Programlı olarak

## <a name="applying-a-theme-in-the-configuration-file"></a>Yapılandırma dosyasına bir tema uygulama

Uygulama yapılandırma dosyasına bir tema uygulamak için aşağıdaki sözdizimini kullanın:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample13.xml)]

Burada belirtilen tema adı, Temalar klasörünün adıyla eşleşmelidir. Bu klasör, bu kursun önceki kısımlarında bahsedilen konumlardan herhangi birinde bulunabilir. Mevcut olmayan bir temayı uygulamaya çalışırsanız, bir yapılandırma hatası oluşur.

## <a name="applying-a-theme-in-the-page-directive"></a>Sayfa yönergesinde Tema uygulama

Ayrıca @ Page yönergesinde bir tema uygulayabilirsiniz. Bu yöntem, belirli bir sayfa için bir tema kullanmanıza olanak sağlar.

@Page yönergesinde bir tema uygulamak için aşağıdaki sözdizimini kullanın:

[!code-aspx[Main](profiles-themes-and-web-parts/samples/sample14.aspx)]

Bir kez daha, burada belirtilen tema, daha önce belirtildiği gibi tema klasörüyle aynı olmalıdır. Mevcut olmayan bir temayı uygulamaya çalışırsanız, bir derleme hatası oluşur. Visual Studio aynı zamanda özniteliği vurgulayacaktır ve böyle bir temanın mevcut olmadığını size bildirir.

## <a name="applying-a-theme-programmatically"></a>Bir temayı programlı olarak uygulama

Bir temayı programlı bir şekilde uygulamak için, **sayfa\_PreInit** yöntemi içindeki sayfa için **Tema** özelliğini belirtmeniz gerekir.

Bir temayı programlı bir şekilde uygulamak için aşağıdaki sözdizimini kullanın:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample15.cs)]

Sayfa yaşam döngüsü nedeniyle temayı PreInit yönteminde uygulamak gereklidir. Bu noktadan sonra uygularsanız, sayfalar teması çalışma zamanı tarafından zaten uygulanmış olur ve o noktadaki bir değişiklik yaşam döngülerinde çok geç olur. Mevcut olmayan bir tema uygularsanız, bir **HttpException** oluşur. Bir tema programlı olarak uygulandığında, herhangi bir sunucu denetiminin bir SkinID özelliği belirtilmişse bir yapı uyarısı oluşur. Bu uyarı, hiçbir temanın bildirimli olarak uygulandığını ve yoksayılamayacağını bildirmek için tasarlanmıştır.

## <a name="exercise-1--applying-a-theme"></a>Alıştırma 1: Tema uygulama

Bu alıştırmada, bir Web sitesine ASP.NET teması uygulayacaksınız.

> [!IMPORTANT]
> Bir dış görünüm dosyasına bilgi girmek için Microsoft Word kullanıyorsanız, normal tırnakları akıllı tırnaklarla değiştirdiğinizden emin olun. Akıllı tırnaklar, dış görünüm dosyaları ile ilgili sorunlara neden olur.

1. Yeni bir ASP.NET Web sitesi oluşturun.
2. Çözüm Gezgini projeye sağ tıklayın ve yeni öğe Ekle ' yi seçin.
3. Dosya listesinden Web yapılandırma dosyası ' nı seçin ve Ekle ' ye tıklayın.
4. Çözüm Gezgini projeye sağ tıklayın ve yeni öğe Ekle ' yi seçin.
5. Kaplama dosyası ' nı seçin ve Ekle ' ye tıklayın.
6. Dosyayı uygulama\_Temalar klasörünün içine yerleştirmek isteyip istemediğiniz sorulduğunda Evet ' e tıklayın.
7. Çözüm Gezgini içindeki uygulama\_Temalar klasörünün içindeki SkinFile klasörüne sağ tıklayın ve yeni öğe Ekle ' yi seçin.
8. Dosya listesinden stil sayfası ' nı seçin ve Ekle ' ye tıklayın. Artık yeni temanızı uygulamak için gereken tüm dosyalar var. Ancak, Visual Studio 'Nun Temalar klasörü SkinFile 'ı adı vardır. Bu klasöre sağ tıklayın ve adı CoolTheme olarak değiştirin.
9. SkinFile. Skin dosyasını açın ve aşağıdaki kodu dosyanın sonuna ekleyin: 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample16.aspx)]
10. SkinFile. Skin dosyasını kaydedin.
11. Stil sayfası. css açın.
12. İçindeki tüm metni aşağıdakiler ile değiştirin: 

    [!code-css[Main](profiles-themes-and-web-parts/samples/sample17.css)]
13. Stil sayfası. css dosyasını kaydedin.
14. Default. aspx sayfasını açın.
15. TextBox denetimi ve bir düğme denetimi ekleyin.
16. Sayfayı kaydedin. Şimdi default. aspx sayfasına gözatamazsınız. Normal bir Web formu olarak görüntülenmelidir.
17. Web. config dosyasını açın.
18. Şunu doğrudan açma `<system.web>` etiketinin altına ekleyin: 

    [!code-xml[Main](profiles-themes-and-web-parts/samples/sample18.xml)]
19. Web. config dosyasını kaydedin. Şimdi default. aspx sayfasına gözatamazsınız. Tema uygulanmış olarak görüntülenmelidir.
20. Zaten açık değilse, Visual Studio 'da default. aspx sayfasını açın.
21. Düğmeyi seçin.
22. **SkinID** özelliğini gobtan olarak değiştirin. Visual Studio 'Nun bir düğme denetimi için geçerli SkinID değerleriyle bir açılan menü sağladığını unutmayın.
23. Sayfayı kaydedin. Şimdi tarayıcıda sayfayı yeniden önizleyin. Düğme şimdi "Go" deyin ve görünümün daha geniş olması gerekir.

**SkinID** özelliğini kullanarak belirli bir sunucu denetimi türünün farklı örnekleri için farklı kaplamaları kolayca yapılandırabilirsiniz.

## <a name="the-stylesheettheme-property"></a>StyleSheetTheme özelliği

Şimdiye kadar, yalnızca Tema özelliğini kullanarak temalar uygulama hakkında konuşuyoruz. Tema özelliği kullanılırken, Skin dosyası sunucu denetimleri için tüm bildirim temelli ayarları geçersiz kılacaktır. Örneğin, 1. alıştırmada düğme denetimi için "Gobtan" bir SkinID belirttiniz ve düğmenin metnini "Go" olarak değiştirdi. Tasarımcı 'daki düğmenin metin özelliğinin "Button" olarak ayarlandığını fark etmiş olabilirsiniz, ancak bu tema de bunun üzerine gelin. Tema her zaman tasarımcıda özellik ayarlarını geçersiz kılar.

Tasarımcıda belirtilen özellikleri içeren temanın dış görünüm dosyasında tanımlanan özellikleri geçersiz kılabilmek istiyorsanız, Tema özelliği yerine **StyleSheetTheme** özelliğini kullanabilirsiniz. StyleSheetTheme özelliği, Theme özelliği gibi tüm açık özellik ayarlarını geçersiz kılmadığından, Tema özelliği ile aynıdır.

Bu işlemi yapmak için, alıştırma 1 ' deki projeden Web. config dosyasını açın ve `<pages>` öğesini aşağıdaki şekilde değiştirin:

[!code-xml[Main](profiles-themes-and-web-parts/samples/sample19.xml)]

Şimdi default. aspx sayfasına gözatıp, düğme denetiminin bir "Button" metin özelliğine yeniden sahip olduğunu görürsünüz. Bunun nedeni, tasarımcıda açık özellik ayarı Gobtan SkinID tarafından ayarlanan metin özelliğini geçersiz kıldığından.

## <a name="overriding-themes"></a>Temaları geçersiz kılma

Uygulamanın uygulama\_temalar klasöründe aynı ada sahip bir tema uygulanarak, genel bir tema geçersiz kılınabilir. Ancak, tema, doğru bir geçersiz kılma senaryosunda uygulanmaz. Çalışma zamanı, uygulama\_temalar klasöründe Tema dosyalarıyla karşılaşırsa, bu dosyaları kullanarak temayı uygular ve genel temayı yoksayar.

StyleSheetTheme özelliği geçersiz kılınabilir ve kodda aşağıdaki gibi geçersiz kılınabilir:

[!code-csharp[Main](profiles-themes-and-web-parts/samples/sample20.cs)]

## <a name="web-parts"></a>Web Bölümleri

ASP.NET Web Bölümleri, son kullanıcıların Web sayfalarının içeriğini, görünümünü ve davranışını doğrudan bir tarayıcıdan değiştirmesini sağlayan Web siteleri oluşturmaya yönelik tümleşik bir denetim kümesidir. Değişiklikler sitedeki tüm kullanıcılara veya bireysel kullanıcılara uygulanabilir. Kullanıcılar sayfaları ve denetimleri değiştirirken, kullanıcının kişisel tercihlerini daha sonra kişiselleştirme adlı bir özellik olan gelecekteki tarayıcı oturumlarında koruyacak şekilde ayarlar kaydedebilirsiniz. Bu Web Bölümleri özellikleri, geliştiricilerin son kullanıcılara bir Web uygulamasını geliştirici veya yönetici müdahalesi olmadan dinamik olarak kişiselleştirmesini sağlayabildiği anlamına gelir.

Web Bölümleri denetim kümesini kullanarak bir geliştirici, son kullanıcıların şunları kullanmasını olanaklı hale getirebilirsiniz:

- Sayfa içeriğini kişiselleştirin. Kullanıcılar bir sayfaya yeni Web Bölümleri denetimleri ekleyebilir, bunları kaldırabilir, gizleyebilir veya sıradan pencereler gibi en aza indirebilir.
- Sayfa mizanpajını kişiselleştirin. Kullanıcılar bir Web Bölümleri denetimini sayfadaki farklı bir bölgeye sürükleyebilir veya görünümünü, özelliklerini ve davranışını değiştirebilir.
- Denetimleri dışarı ve içeri aktarma. Kullanıcılar, diğer sayfalarda veya sitelerde kullanılmak üzere Web Bölümleri denetim ayarlarını içeri aktarabilir veya dışarı aktarabilir, özellikleri, görünümü ve hatta denetimlerde verileri korur. Bu, son kullanıcılar için veri girişini ve yapılandırma taleplerini azaltır.
- Bağlantı oluşturun. Kullanıcılar, örneğin bir grafik denetimi bir stok şeridi denetimindeki veriler için bir grafik görüntülemesi gibi denetimler arasında bağlantı kurabilir. Kullanıcılar yalnızca bağlantının kendisini değil, grafik denetiminin verileri görüntüleme şekli ve ayrıntıları.
- Site düzeyi ayarlarını yönetin ve kişiselleştirin. Yetkili kullanıcılar site düzeyinde ayarları yapılandırabilir, bir siteye veya sayfaya kimlerin erişebileceğini belirleyebilir, denetimlere rol tabanlı erişim ayarlayabilir ve bu şekilde devam edebilir. Örneğin, bir yönetici rolündeki bir Kullanıcı, tüm kullanıcılar tarafından paylaşılacak bir Web Bölümleri denetimi ayarlayabilir ve yönetici olmayan kullanıcıların paylaşılan denetimi kişiselleştirmasını önler.

Genellikle Web Bölümleri üç farklı şekilde çalışırsınız: Web Bölümleri denetimleri kullanan sayfalar oluşturma, bireysel Web Bölümleri denetimleri oluşturma veya Portal gibi tamamen, kişiselleştirilebilir bir Web uygulaması oluşturma.

## <a name="page-development"></a>Sayfa geliştirme

Sayfa geliştiricileri, Web Bölümleri kullanan sayfalar oluşturmak için Microsoft Visual Studio 2005 gibi görsel tasarım araçlarını kullanabilir. Visual Studio gibi bir araç kullanmanın avantajlarından biri, Web Bölümleri denetim kümesinin, görsel bir tasarımcıda Web Bölümleri denetimlerinin sürükle ve bırak özelliği ve yapılandırması için özellikler sunabilleridir. Örneğin, tasarımcı kullanarak bir Web Bölümleri bölgesini veya bir Web Bölümleri düzenleyici denetimini tasarım yüzeyine sürükleyebilir ve sonra Web Bölümleri denetim kümesi tarafından sunulan kullanıcı arabirimini kullanarak tasarımcıda denetimi doğrudan yapılandırabilirsiniz. Bu, Web Bölümleri uygulamaların geliştirilmesini hızlandırabilir ve yazmak istediğiniz kod miktarını azaltabilir.

## <a name="control-development"></a>Denetim geliştirme

Var olan herhangi bir ASP.NET denetimini standart Web sunucusu denetimleri, özel sunucu denetimleri ve Kullanıcı denetimleri gibi Web Bölümleri denetim olarak kullanabilirsiniz. Ortamınızın en yüksek programlı denetimi için, WebPart sınıfından türetilen özel Web Bölümleri denetimleri de oluşturabilirsiniz. Bireysel Web Bölümleri denetim geliştirmesi için, genellikle bir kullanıcı denetimi oluşturup bunu bir Web Bölümleri denetimi olarak kullanacaksınız ya da özel bir Web Bölümleri denetimi geliştirirsiniz.

Özel bir Web Bölümleri denetimi geliştirmesinin bir örneği olarak, diğer ASP.NET Server denetimleri tarafından sunulan ve kişiselleştirilebilir bir Web Bölümleri denetimi olarak paketleme yararlı olabilecek özelliklerden herhangi birini sağlamak üzere bir denetim oluşturabilirsiniz: takvimler, listeler, finansal bilgiler, Haberler, hesaplayıcılar, içerik güncelleştirme için zengin metin denetimleri, veritabanlarına bağlanan düzenlenebilir kılavuzlar, ekranları dinamik olarak güncelleştiren grafikler veya hava durumu ve seyahat bilgileri. Denetiminizin bulunduğu bir görsel tasarımcı sağlarsanız, Visual Studio kullanan herhangi bir sayfa geliştiricisi, denetiminizi bir Web Bölümleri bölgesine sürükleyebilir ve ek kod yazmak zorunda kalmadan tasarım zamanında yapılandırabilir.

Kişiselleştirme Web Bölümleri özelliğinin temelidir. Kullanıcıların bir sayfada Web Bölümleri denetimlerinin düzen, görünüm ve davranışını değiştirmesine veya kişiselleştirmesine olanak sağlar. Kişiselleştirilmiş ayarlar uzun ömürlü: yalnızca geçerli tarayıcı oturumunda (Görünüm durumunda olduğu gibi) değil, ayrıca uzun vadeli depolamada değil, bir kullanıcının ayarlarının gelecekteki tarayıcı oturumları için kaydedilmesi için de kalıcı hale getirilir. Kişiselleştirme, Web Bölümleri sayfaları için varsayılan olarak etkinleştirilmiştir.

Kullanıcı arabirimi yapısal bileşenleri kişiselleştirmeye dayanır ve tüm Web Bölümleri denetimleri için gereken çekirdek yapıyı ve hizmetleri sağlar. Her Web Bölümleri sayfasında gerekli bir kullanıcı arabirimi yapısal bileşeni WebPartManager denetimidir. Bu denetimde hiçbir şey görünmese de, bir sayfadaki tüm Web Bölümleri denetimlerini koordine etme kritik görevi vardır. Örneğin, tüm bireysel Web Bölümleri denetimlerini izler. Web Bölümleri bölgelerini (bir sayfada Web Bölümleri denetimleri içeren bölgeleri) ve hangi denetimlerin hangi bölgelerde olduğunu yönetir. Ayrıca, gezinme, bağlanma, düzenleme veya katalog modu gibi bir sayfanın içinde yer aldığı farklı görüntüleme modlarını izler ve denetler ve kişiselleştirme değişikliklerinin tüm kullanıcılara veya bireysel kullanıcılara uygulanıp uygulanmayacağı. Son olarak, Web Bölümleri denetimleri arasındaki bağlantıları ve iletişimi başlatır ve izler.

UI yapısal bileşeni ikinci türü bölgedir. Bölgeler, Web Bölümleri sayfasında düzen yöneticileri olarak davranır. Bunlar, Bölüm sınıfından (Bölüm denetimleri) türetilen denetimleri içerir ve düzenler ve hem yatay ya da dikey yönde modüler sayfa düzeni yapma yeteneği sağlar. Bölgeler Ayrıca içerdikleri her denetim için ortak ve tutarlı kullanıcı arabirimi öğeleri (üst bilgi ve alt bilgi stili, başlık, kenarlık stili, eylem düğmeleri vb.) sunar; Bu ortak öğeler, bir denetimin Chrome olarak bilinir. Farklı görüntü modlarında ve çeşitli denetimlerle birçok özel bölge türü kullanılır. Farklı bölge türleri aşağıdaki Web Bölümleri temel denetimler bölümünde açıklanmıştır.

**Bölüm** sınıfından türeten Web bölümleri UI denetimleri, bir Web bölümleri sayfasında birincil kullanıcı arabirimini oluşturur. Web Bölümleri denetim kümesi, Bölüm denetimleri oluşturmak için size verdiği seçeneklerde esnektir ve dahil değildir. Kendi özel Web Bölümleri denetimlerinizi oluşturmaya ek olarak, var olan ASP.NET Server denetimlerini, kullanıcı denetimlerini veya özel sunucu denetimlerini Web Bölümleri denetimleri olarak da kullanabilirsiniz. Web Bölümleri sayfaları oluşturmak için en yaygın olarak kullanılan denetim, sonraki bölümde açıklanmaktadır.

## <a name="web-parts-essential-controls"></a>Web Bölümleri temel denetimler

Web Bölümleri denetim kümesi kapsamlıdır, ancak Web Bölümleri çalışması için gerekli olduklarından veya Web Bölümleri sayfalarında en sık kullanılan denetimler olduklarından, bazı denetimler önemlidir. Web Bölümleri kullanmaya ve temel Web Bölümleri sayfaları oluşturmaya başladığınızda, aşağıdaki tabloda açıklanan temel Web Bölümleri denetimleri hakkında bilgi sahibi olmanız yararlı olur.

| **Web Bölümleri denetimi** | **Açıklama** |
| --- | --- |
| WebPartManager | Sayfadaki tüm Web Bölümleri denetimlerini yönetir. Her Web Bölümleri sayfası için bir (ve yalnızca bir) **WebPartManager** denetimi gereklidir. |
| 'U | CatalogPart denetimlerini içerir. Kullanıcıların bir sayfaya eklenecek denetimleri seçebileceğiniz Web Bölümleri denetimlerinin kataloğunu oluşturmak için bu bölgeyi kullanın. |
| EditorZone 'u | EditorPart denetimlerini içerir. Kullanıcıların bir sayfada Web Bölümleri denetimlerini düzenlemesini ve kişiselleştirmesini sağlamak için bu bölgeyi kullanın. |
| Belirtilmedi | , Bir sayfanın ana Kullanıcı arabirimini oluşturan WebPart denetimleri için genel düzen içerir ve sunar. Web Bölümleri denetimleri olan her sayfa oluşturduğunuzda bu bölgeyi kullanın. Sayfalar, bir veya daha fazla bölge içerebilir. |
| ConnectionsZone | WebPartConnection denetimlerini içerir ve bağlantıları yönetmek için bir kullanıcı arabirimi sağlar. |
| Web Bölümü (GenericWebPart) | Birincil Kullanıcı arabirimini işler; Çoğu Web Bölümleri UI denetimleri bu kategoriye girer. En yüksek programlı denetim için, temel **Web Bölümü** denetiminden türetilen özel Web Bölümleri denetimleri oluşturabilirsiniz. Ayrıca, var olan sunucu denetimlerini, kullanıcı denetimlerini veya özel denetimleri Web Bölümleri denetimleri olarak da kullanabilirsiniz. Bu denetimlerden herhangi biri bir bölgeye yerleştirildiğinde, **WebPartManager** denetimi çalışma zamanında onları otomatik olarak **GenericWebPart** denetimleriyle sarmalar ve böylece onları Web bölümleri işlevlerle kullanabilirsiniz. |
| 'Ta | Kullanıcıların sayfaya ekleyebileceğiniz kullanılabilir Web Bölümleri denetimlerinin bir listesini içerir. |
| WebPartConnection | Bir sayfada iki Web Bölümleri denetimi arasında bir bağlantı oluşturur. Bağlantı, Web Bölümleri denetimlerinden birini sağlayıcı (veri) ve diğer tüketici olarak tanımlar. |
| EditorPart | Özelleştirilmiş düzenleyici denetimleri için temel sınıf olarak işlev görür. |
| EditorPart denetimleri (AppearanceEditorPart, LayoutEditorPart, BehaviorEditorPart ve PropertyGridEditorPart) | Kullanıcıların bir sayfada Web Bölümleri UI denetimlerinin çeşitli yönlerini kişiselleştirmesine izin ver |

## <a name="lab-create-a-web-part-page"></a>Laboratuvar: Web Bölümü sayfası oluşturma

Bu laboratuvarda, ASP.NET profilleri aracılığıyla bilgileri kalıcı hale getirebileceği bir Web Bölümü sayfası oluşturacaksınız.

### <a name="creating-a-simple-page-with-web-parts"></a>Web Bölümleri basit sayfa oluşturma

İzlenecek yolun bu bölümünde, statik içerikleri göstermek için Web Bölümleri denetimleri kullanan bir sayfa oluşturacaksınız. Web Bölümleri ile çalışmanın ilk adımı, iki gerekli yapısal öğe içeren bir sayfa oluşturmaktır. İlk olarak, bir Web bölümleri sayfasının tüm Web Bölümleri denetimlerini izleyip koordine etmek için WebPartManager denetimine ihtiyacı vardır. İkinci olarak, bir Web Bölümleri sayfası, Web Bölümü veya diğer sunucu denetimlerini içeren ve bir sayfanın belirtilen bölgesini kaplayan bileşik denetimler olan bir veya daha fazla bölgeye ihtiyaç duyuyor.

> [!NOTE]
> Web Bölümleri kişiselleştirmesini etkinleştirmek için herhangi bir şey yapmanız gerekmez; Web Bölümleri denetim kümesi için varsayılan olarak etkindir. Bir sitede Web Bölümleri sayfası ilk kez çalıştırdığınızda, ASP.NET Kullanıcı Kişiselleştirme ayarlarını depolamak için varsayılan bir kişiselleştirme sağlayıcısı ayarlar. Kişiselleştirme hakkında daha fazla bilgi için bkz. Web Bölümleri kişiselleştirmeye genel bakış.

### <a name="to-create-a-page-for-containing-web-parts-controls"></a>Web Bölümleri denetimleri içeren bir sayfa oluşturmak için

1. Varsayılan sayfayı kapatın ve WebPartsDemo. aspx adlı siteye yeni bir sayfa ekleyin.
2. **Tasarım** görünümüne geçin.
3. **Görünüm** menüsünde, **görsel olmayan denetimler** ve **Ayrıntılar** seçeneklerinin seçildiğinden emin olun; böylece düzen etiketleri ve Kullanıcı arabirimi olmayan denetimler görebilirsiniz.
4. Ekleme noktasını tasarım yüzeyinde `<div>` etiketlerden önce yerleştirin ve yeni bir satır eklemek için ENTER tuşuna basın. Ekleme noktasını yeni satır karakterinden önce konumlandırın, menüdeki **blok biçimi** açılan liste denetimine tıklayın ve **Başlık 1** seçeneğini belirleyin. Başlıkta, metin **Web bölümleri tanıtım sayfasını**ekleyin.
5. Araç kutusunun **Web bölümleri** sekmesinden bir **WebPartManager** denetimini sayfaya sürükleyin, yeni satır karakterinden hemen sonra ve `<div>`etiketlerden önce konumlandırın.   
  
   **WebPartManager** denetimi herhangi bir çıkış oluşturmaz, bu nedenle tasarımcı yüzeyinde gri bir kutu olarak görünür.
6. Ekleme noktasını `<div>` etiketlerinin içine konumlandırın.
7. **Düzen** menüsünde **Tablo Ekle**' ye tıklayın ve bir satırı ve üç sütunu olan yeni bir tablo oluşturun. **Hücre özellikleri** düğmesine tıklayın, **Dikey Hizala** açılan listesinden **üst** ' i seçin, **Tamam**' a tıklayın ve tabloyu oluşturmak için yeniden **Tamam** ' a tıklayın.
8. Bir WebPartZone denetimini sol tablo sütununa sürükleyin. **WebPartZone** denetimine sağ tıklayın, **Özellikler**' i seçin ve aşağıdaki özellikleri ayarlayın:   
  
   KIMLIK: SidebarZone   
  
   HeaderText: kenar çubuğu
9. İkinci bir **WebPartZone** denetimini Ortadaki tablo sütununa sürükleyin ve aşağıdaki özellikleri ayarlayın:   
  
   KIMLIK: MainZone   
  
   HeaderText: Ana
10. Dosyayı kaydedin.

Sayfanızda artık ayrı ayrı denetleyebilmeniz için iki ayrı bölge vardır. Ancak, hiçbir bölgede içerik yoktur, bu nedenle içerik oluşturmak bir sonraki adımdır. Bu izlenecek yol için yalnızca statik içerik görüntüleyen Web Bölümleri denetimlerle çalışırsınız.

Web Bölümleri bölgenin düzeni, bir &lt;ZoneTemplate&gt; öğesi tarafından belirtilir. Bölge şablonu içinde, özel bir Web Bölümleri denetimi, bir kullanıcı denetimi veya var olan bir sunucu denetimi olup olmadığı herhangi bir ASP.NET denetimi ekleyebilirsiniz. Burada etiket denetimini kullandığınızı ve yalnızca statik metin eklemeyi unutmayın. Bir **WebPartZone** bölgesine düzenli bir sunucu denetimi yerleştirdiğinizde ASP.net, denetim üzerinde Web bölümleri özellikleri sağlayan denetimi çalışma zamanında Web bölümleri denetimi olarak değerlendirir.

**Ana bölgeye içerik oluşturmak için**

1. **Tasarım** görünümü ' nde, araç kutusunun **Standart** sekmesinden bir **etiket** denetimini, **ID** özelliği mainzone olarak ayarlanmış olan bölgenin içerik alanına sürükleyin.
2. **Kaynak** görünümüne geçin. Ana bölgedeki **etiket** denetimini kaydırmak için bir &lt;ZoneTemplate&gt; öğesinin eklendiğinden emin olun.
3. &lt;ASP: Label&gt; öğesine **title** adlı bir öznitelik ekleyin ve değerini içerik olarak ayarlayın. &lt;ASP: Label&gt; öğesinden Text = "label" özniteliğini kaldırın. &lt;ASP: Label&gt; öğesinin açılış ve kapanış etiketleri arasında, bir dizi &lt;H2&gt; öğesi etiketi içinde **giriş sayfasına hoş geldiniz** gibi bir metin ekleyin. Kodunuz aşağıdaki gibi görünmelidir. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample21.aspx)]
4. Dosyayı kaydedin.

Daha sonra, sayfaya Web Bölümleri denetimi olarak eklenebilen bir kullanıcı denetimi oluşturun.

### <a name="to-create-a-user-control"></a>Kullanıcı denetimi oluşturmak için

1. Bir arama denetimi olarak kullanılmak üzere sitenize yeni bir Web Kullanıcı denetimi ekleyin. **Kaynak kodu ayrı bir dosyaya yerleştirme**seçeneğinin seçimini kaldırın. Onu WebPartsDemo. aspx sayfasıyla aynı dizine ekleyin ve SearchUserControl. ascx olarak adlandırın.   
  
    > [!NOTE]
    > Bu izlenecek yol için Kullanıcı denetimi, gerçek arama işlevlerini uygulamaz; yalnızca Web Bölümleri özelliklerini göstermek için kullanılır.
2. **Tasarım** görünümüne geçin. Araç kutusunun **Standart** sekmesinden sayfaya bir TextBox denetimi sürükleyin.
3. Ekleme noktasını az önce eklediğiniz metin kutusundan sonra yerleştirin ve yeni bir satır eklemek için ENTER tuşuna basın.
4. Yeni eklediğiniz metin kutusunun altındaki yeni satırdaki sayfaya düğme denetimini sürükleyin.
5. **Kaynak** görünümüne geçin. Kullanıcı denetimi için kaynak kodunun aşağıdaki örnekte olduğu gibi göründüğünden emin olun. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample22.aspx)]
6. Dosyayı kaydedin ve kapatın.

Artık kenar çubuğu bölgesine Web Bölümleri denetimleri ekleyebilirsiniz. Bir bağlantı listesi ve bir önceki yordamda oluşturduğunuz Kullanıcı denetimi olan diğer bir deyişle, kenar çubuğu bölgesine iki denetim ekliyoruz. Bağlantılar, ana bölgenin statik metnini oluşturma yöntemine benzer şekilde standart bir **etiket** sunucu denetimi olarak eklenir. Ancak, Kullanıcı denetiminde bulunan bireysel sunucu denetimleri doğrudan bölgede bulunabilir (etiket denetimi gibi), bu durumda değildir. Bunun yerine, önceki yordamda oluşturduğunuz Kullanıcı denetiminin bir parçasıdır. Bu, bir kullanıcı denetiminde istediğiniz denetimleri ve ek işlevleri paketlemeyi ve sonra bir bölgede denetim Web Bölümleri denetimi olarak başvuruyu yapmanın yaygın bir yolunu gösterir.

Çalışma zamanında Web Bölümleri denetim kümesi, her iki denetimi de GenericWebPart denetimleriyle sarmalanmış. Bir **GenericWebPart** denetimi bir Web sunucusu denetimini sarmaladığı zaman, genel bölüm denetimi üst denetimdir ve sunucu denetimine üst denetimin ChildControl özelliği aracılığıyla erişebilirsiniz. Genel Bölüm denetimlerinin Bu kullanımı, standart Web sunucusu denetimlerinin, **WebPart** sınıfından türetilen Web bölümleri denetimlerle aynı temel davranışa ve özniteliklere sahip olmasını sağlar.

### <a name="to-add-web-parts-controls-to-the-sidebar-zone"></a>Kenar çubuğu bölgesine Web Bölümleri denetimleri eklemek için

1. WebPartsDemo. aspx sayfasını açın.
2. **Tasarım** görünümüne geçin.
3. Oluşturduğunuz Kullanıcı denetim sayfasını, SearchUserControl. ascx adlı **Çözüm Gezgini** , **ID** özelliği sidebarzone olarak ayarlanan bölgeye sürükleyin ve burada bırakın.
4. WebPartsDemo. aspx sayfasını kaydedin.
5. **Kaynak** görünümüne geçin.
6. Şu örnekte gösterildiği gibi, SidebarZone için &lt;ASP: WebPartZone&gt; öğesinin içinde, Kullanıcı denetiminizin başvurusunun hemen üzerinde bir &lt;ASP: Label&gt; öğesi ekleyin. Ayrıca, gösterildiği gibi, **arama**değeri ile Kullanıcı denetimi etiketine bir **title** özniteliği ekleyin. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample23.aspx)]
7. Dosyayı kaydedin ve kapatın.

Artık, tarayıcınızda tarayıcıda gezinerek sayfanızı test edebilirsiniz. Sayfada iki bölge görüntülenir. Aşağıdaki ekran görüntüsünde sayfa görüntülenir.

**İki bölge içeren Web Bölümleri tanıtım sayfası**

![Web Bölümleri VS Izlenecek yol 1 ekran görüntüsü](profiles-themes-and-web-parts/_static/image3.gif)

**Şekil 3**: Web bölümleri vs izlenecek yol 1 ekran görüntüsü

Her denetimin başlık çubuğunda, bir denetimde gerçekleştirebileceğiniz kullanılabilir eylemlerin fiiller menüsüne erişim sağlayan aşağı bir oktur. Denetimlerden biri için fiiller menüsüne tıklayın, sonra da fiili **simge durumuna küçült** ' e tıklayın ve denetimin simge durumuna küçültülmüş olduğunu unutmayın. Fiiller menüsünde, **geri yükle**' ye tıklayın ve denetim normal boyutuna geri döner.

### <a name="enabling-users-to-edit-pages-and-change-layout"></a>Kullanıcıların sayfaları düzenlemesini ve düzen değiştirmesini sağlama

Web Bölümleri, kullanıcılara bir bölgeden diğerine sürükleyerek Web Bölümleri denetimlerinin yerleşimini değiştirme yeteneği sağlar. Kullanıcıların, **Web Bölümü** denetimlerini bir bölgeden diğerine taşımasına izin vermenin yanı sıra, kullanıcıların görünümleri, düzeni ve davranışları dahil olmak üzere denetimlerin çeşitli özelliklerini düzenlemesine izin verebilirsiniz. Web Bölümleri denetim kümesi, **WebPart** denetimleri için temel düzen işlevlerini sağlar. Bu yönergeyi yapamasanız da, kullanıcıların **WebPart** denetimlerinin özelliklerini düzenlemesine izin veren özel düzenleyici denetimleri de oluşturabilirsiniz. Bir **Web Bölümü** denetiminin konumunu değiştirirken olduğu gibi, bir denetimin özelliklerinin düzenlenmesinin, kullanıcıların yaptığı değişiklikleri kaydetmek için ASP.net kişiselleştirmesini kullanır.

İzlenecek yolun bu bölümünde, kullanıcıların sayfadaki herhangi bir **WebPart** denetiminin temel özelliklerini düzenleme yeteneğini eklersiniz. Bu özellikleri etkinleştirmek için, sayfaya bir &lt;ASP: EditorZone&gt; öğesi ve iki Düzenle denetimi ile birlikte başka bir özel kullanıcı denetimi eklersiniz.

### <a name="to-create-a-user-control-that-enables-changing-page-layout"></a>Sayfa düzeninin değiştirilmesini sağlayan bir kullanıcı denetimi oluşturmak için

1. Visual Studio 'da, **Dosya** menüsünde **Yeni** alt menüyü seçin ve **Dosya** seçeneğine tıklayın.
2. **Yeni öğe Ekle** Iletişim kutusunda **Web Kullanıcı denetimi**' ni seçin. Yeni dosyayı DisplayModeMenu. ascx olarak adlandırın. **Kaynak kodu ayrı dosyaya yerleştirme**seçeneğinin seçimini kaldırın.
3. Yeni denetimi oluşturmak için Ekle ' ye tıklayın.
4. **Kaynak** görünümüne geçin.
5. Yeni dosyadaki tüm mevcut kodu kaldırın ve aşağıdaki kodu yapıştırın. Bu Kullanıcı denetimi kodu, bir sayfanın görünüm veya görüntüleme modunu değiştirmesini sağlayan Web Bölümleri denetim kümesinin özelliklerini kullanır ve ayrıca, belirli görüntü moddayken sayfanın fiziksel görünümünü ve yerleşimini değiştirmenizi sağlar. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample24.aspx)]
6. Araç çubuğundaki Kaydet simgesine tıklayarak veya **Dosya** menüsünde **Kaydet** ' i seçerek dosyayı kaydedin.

### <a name="to-enable-users-to-change-the-layout"></a>Kullanıcıların düzeni değiştirmesine olanak tanımak için

1. WebPartsDemo. aspx sayfasını açın ve **Tasarım** görünümüne geçin.
2. Ekleme noktasını, daha önce eklediğiniz **WebPartManager** denetiminden hemen sonra **Tasarım** görünümüne konumlandırın. **WebPartManager** denetiminden sonra boş bir satır olması için metinden sonra sabit bir dönüş ekleyin. Ekleme noktasını boş satıra yerleştirin.
3. Yeni oluşturduğunuz Kullanıcı denetimini (dosya DisplayModeMenu. ascx olarak adlandırılır) WebPartsDemo. aspx sayfasına sürükleyin ve boş satıra bırakın.
4. Araç kutusu ' ndan bir EditorZone denetimini WebPartsDemo. aspx sayfasındaki kalan açık tablo hücresine sürükleyin.
5. Araç kutusunun **WebParts** bölümünden bir AppearanceEditorPart denetimini ve LayoutEditorPart denetimini **EditorZone** denetimine sürükleyin.
6. **Kaynak** görünümüne geçin. Tablo hücresindeki sonuç kodu aşağıdaki koda benzer görünmelidir. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample25.aspx)]
7. WebPartsDemo. aspx dosyasını kaydedin. Görüntüleme modlarını değiştirmenize ve sayfa mizanpajını değiştirmenize olanak tanıyan bir kullanıcı denetimi oluşturdunuz ve birincil web sayfasında denetime başvurmuş olabilirsiniz.

Artık sayfaları düzenleme ve düzeni değiştirme yeteneklerini test edebilirsiniz.

### <a name="to-test-layout-changes"></a>Düzen değişikliklerini test etmek için

1. Sayfayı bir tarayıcıda yükleyin.
2. **Görüntüleme modu** açılır menüsüne tıklayın ve **Düzenle**' yi seçin. Bölge başlıkları görüntülenir.
3. **My Links** denetimini, kenar çubuğu bölgesindeki başlık çubuğuna, ana bölgenin altına sürükleyin. Sayfanız aşağıdaki ekran görüntüsü gibi görünmelidir.

### <a name="web-parts-demo-page-with-my-links-control-moved"></a>Bağlantı denetimiyle Web Bölümleri tanıtım sayfası taşındı

![Web Bölümleri VS Izlenecek yol 2 ekran görüntüsü](profiles-themes-and-web-parts/_static/image4.gif)

**Şekil 4**: Web bölümleri vs izlenecek yol 2 ekran görüntüsü

1. **Görüntüleme modu** açılan menüsüne tıklayın ve sonra da **Araştır**' ı seçin. Sayfa yenilenir, bölge adları kaybolur ve **bağlantılarım denetimi onu** yerleştirdiğiniz yerde kalır.
2. Kişiselleştirmenin çalıştığını göstermek için tarayıcıyı kapatın ve sonra sayfayı yeniden yükleyin. Yaptığınız değişiklikler gelecekteki tarayıcı oturumları için kaydedilir.
3. **Görüntüleme modu** menüsünde, **Düzenle**' yi seçin.   
  
   Sayfadaki her denetim, artık fiiller açılan menüsünü içeren başlık çubuğunda aşağı doğru bir oklu görüntülenir.
4. **My Links** denetimindeki Verbs menüsünü göstermek için oka tıklayın. **Düzenle** fiiline tıklayın.   
  
   **EditorZone** denetimi, eklediğiniz EditorPart denetimlerini görüntüleyerek görüntülenir.
5. Düzenleme denetiminin **Görünüm** bölümünde, **başlığı** Sık Kullanılanlarım olarak değiştirin, **Chrome türü** açılan listesini kullanarak **yalnızca başlık**' ı seçin ve ardından **Uygula**' ya tıklayın. Aşağıdaki ekran görüntüsünde sayfa düzenleme modunda gösterilmektedir.

### <a name="web-parts-demo-page-in-edit-mode"></a>Düzenleme modunda Web Bölümleri tanıtım sayfası

![Web Bölümleri VS Izlenecek yol 3 ekran görüntüsü](profiles-themes-and-web-parts/_static/image5.gif)

**Şekil 5**: Web bölümleri vs izlenecek yol 3 ekran görüntüsü

1. **Görüntüleme modu** menüsüne tıklayın ve gözden geçirme moduna dönmek için **Araştır** ' ı seçin.
2. Aşağıdaki ekran görüntüsünde gösterildiği gibi, denetimde artık güncelleştirilmiş bir başlık ve kenarlık yoktur.

### <a name="edited-web-parts-demo-page"></a>Web Bölümleri demo sayfası düzenlendi

![Web Bölümleri VS Izlenecek yol 4 ekran görüntüsü](profiles-themes-and-web-parts/_static/image6.gif)

**Şekil 4**: Web bölümleri vs izlenecek yol 4 ekran görüntüsü

### <a name="adding-web-parts-at-run-time"></a>Çalışma zamanında Web Bölümleri ekleme

Ayrıca, kullanıcıların çalışma zamanında sayfasına Web Bölümleri denetimleri eklemesine de izin verebilirsiniz. Bunu yapmak için, sayfayı, kullanıcılar için kullanılabilir hale getirmek istediğiniz Web Bölümleri denetimlerinin bir listesini içeren Web Bölümleri katalogla yapılandırın.

**Kullanıcıların çalışma zamanında Web Bölümleri eklemesine izin vermek için**

1. WebPartsDemo. aspx sayfasını açın ve **Tasarım** görünümüne geçin.
2. Araç kutusunun **Web bölümleri** sekmesinden, bir CatalogZone denetimini tablonun sağ alt sütununa, **EditorZone** denetiminin altına sürükleyin.   
  
   Her iki denetim aynı anda görüntülenmeyeceği için aynı tablo hücresinde olabilir.
3. Özellikler bölmesinde, **Add Web bölümleri** dize öğesini **CatalogZone** denetiminin HeaderText özelliğine atayın.
4. Araç kutusunun **WebParts** bölümünde, bir DeclarativeCatalogPart denetimini **CatalogZone** denetiminin içerik alanına sürükleyin.
5. **DeclarativeCatalogPart** denetiminin sağ üst köşesindeki oka tıklayarak görevler menüsünü kullanıma sunun ve ardından **Şablonları Düzenle**' yi seçin.
6. Araç kutusunun **Standart** bölümünde, bir **dosya yükleme** denetimi ve **Takvim** denetimini **DeclarativeCatalogPart** denetiminin **WebPartsTemplate** bölümüne sürükleyin.
7. **Kaynak** görünümüne geçin. &lt;ASP: CatalogZone&gt; öğesinin kaynak kodunu inceleyin. **DeclarativeCatalogPart** denetiminin, katalogdan sayfanıza ekleyebileceğiniz iki sunucu denetimi ile bir &lt;WebPartsTemplate&gt; öğesi içerdiğine dikkat edin.
8. Aşağıdaki kod örneğinde bulunan her başlık için gösterilen dize değerini kullanarak, kataloğa eklediğiniz denetimlerin her birine bir **title** özelliği ekleyin. Başlık bir özellik olmasa da, tasarım zamanında bu iki sunucu denetiminde ayarlanabilir. Kullanıcı, bu denetimleri çalışma zamanında katalogdan bir **WebPartZone** bölgesine eklediğinde, her biri bir **GenericWebPart** denetimiyle sarmalanır. Bu, Web Bölümleri denetimler olarak davranmalarını sağlar, bu nedenle başlıkları görüntüleyebilecektir.   
  
   **DeclarativeCatalogPart** denetiminde yer alan iki denetim için kod aşağıdaki gibi görünmelidir. 

    [!code-aspx[Main](profiles-themes-and-web-parts/samples/sample26.aspx)]
9. Sayfayı kaydedin.

Artık kataloğu test edebilirsiniz.

### <a name="to-test-the-web-parts-catalog"></a>Web Bölümleri kataloğunu test etmek için

1. Sayfayı bir tarayıcıda yükleyin.
2. **Görüntüleme modu** açılan menüsüne tıklayın ve **Katalog**' u seçin.   
  
   **Add Web bölümleri** adlı Katalog görüntülenir.
3. **Sık Kullanılanlarım** denetimini ana bölgeden kenar çubuğu bölgesinin en üstüne geri sürükleyin ve orada bırakın.
4. **Web Bölümleri Ekle** kataloğunda her iki onay kutusunu da seçin ve ardından kullanılabilir bölgeleri içeren açılan listeden **Main** ' i seçin.
5. Katalogda **Ekle** ' ye tıklayın. Denetimler ana bölgeye eklenir. İsterseniz, katalogdan sayfanıza birden fazla denetim örneği ekleyebilirsiniz.   
  
   Aşağıdaki ekran görüntüsünde, karşıya dosya yükleme denetimi ve ana bölgedeki takvimin bulunduğu sayfa gösterilmektedir. 

![Katalogdan ana bölgeye eklenen denetimler](profiles-themes-and-web-parts/_static/image7.gif)

    **Figure 5**: Controls added to Main zone from the catalog
6. **Görüntüleme modu** açılan menüsüne tıklayın ve sonra da **Araştır**' ı seçin. Katalog kaybolur ve sayfa yenilenir.
7. Tarayıcıyı kapatın. Sayfayı yeniden yükleyin. Yaptığınız değişiklikler kalıcı hale getirilir.
