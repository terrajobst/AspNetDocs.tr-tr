---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-vb
title: Üretim Web sitesindeki kullanıcılar ve roller (VB) | Microsoft Docs
author: rick-anderson
description: ASP.NET Web sitesi yönetim aracı (WSAT), üyelik ve rol ayarlarını yapılandırmak ve oluşturma, düzenlemesi, bir... için Web tabanlı bir kullanıcı arabirimi sağlar.
ms.author: riande
ms.date: 06/09/2009
ms.assetid: 491ed5ae-9be1-4191-87be-65e4e1c57690
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-vb
msc.type: authoredcontent
ms.openlocfilehash: d4ce8b278322684be2d44faefd6e69fc524bbe18
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528268"
---
# <a name="users-and-roles-on-the-production-website-vb"></a>Üretim Web sitesindeki kullanıcılar ve roller (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[PDF 'YI indir](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial16_CustomAWAT_vb.pdf)

> ASP.NET Web sitesi yönetim aracı (WSAT), üyelik ve rol ayarlarını yapılandırmak ve Kullanıcı ve rolleri oluşturmak, düzenlemesi ve silmek için Web tabanlı bir kullanıcı arabirimi sağlar. Ne yazık ki, WSAT yalnızca localhost 'tan ziyaret edildiğinde, üretim Web sitesinin yönetim aracına tarayıcınız üzerinden ulaşamamanıza da yarar. İyi haberler, üretimde kullanıcıları ve rolleri yönetmeyi olanaklı kılan geçici çözümler de vardır. Bu öğreticide, bu geçici çözümler ve diğerleri sunulmaktadır.

## <a name="introduction"></a>Giriş

ASP.NET 2,0, Web uygulamanıza ekleyebileceğiniz bir yapı blok Hizmetleri paketi olan bir dizi *uygulama hizmeti*sunmuştur. Üyelik ve rol hizmetlerini, [ *uygulama hizmetleri öğreticisi kullanan bir Web sitesini yapılandırma* ](configuring-a-website-that-uses-application-services-vb.md)bölümünde yer alan kitap İncelemeleri Web sitesine geri ekledik. Üyelik hizmeti kullanıcı hesapları oluşturmayı ve yönetmeyi kolaylaştırır; Rol hizmeti, kullanıcıları gruplar halinde kategorilere ayırmak için bir API sunar. Book Incelemeleri sitesinde üç Kullanıcı hesabı vardır-Scott, Jisun ve Çiğdem ve yönetici rolünde Scott ve Jisun ile tek bir rol, yönetici.

ASP.net. NET ' in uygulama hizmetleri belirli bir uygulamaya bağlı değildir. Bunun yerine, uygulama hizmetlerinin belirli bir *sağlayıcıyı*kullanmasını ve bu sağlayıcının belirli bir teknolojiyi kullanarak hizmeti uyguladığını söyleyebilirsiniz. Book Incelemeleri Web uygulamasını, üyelik ve rol hizmetleri için `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcılarını kullanacak şekilde yapılandırdık. Bu iki sağlayıcı, Kullanıcı hesabı ve rol bilgilerini bir SQL Server veritabanında depolar ve bir Web barındırma şirketinde barındırılan Internet tabanlı Web uygulamaları için en yaygın olarak kullanılan sağlayıcılardır.

Üyelik ve rol hizmetlerini kullanan geliştiriciler için ortak bir zorluk, üretim ortamındaki kullanıcıları ve rolleri yönetmektir. Üretim Web sitesinden bir kullanıcı hesabı nasıl silinir, yeni bir rol ekleyebilir veya mevcut bir role var olan bir kullanıcıyı ekleyebilirsiniz? Bu öğretici, üretim web sitesinde kullanıcıları ve rolleri yönetmeye yönelik farklı teknikler araştırır.

## <a name="using-the-aspnet-web-site-administration-tool"></a>ASP.NET Web sitesi yönetim aracı 'nı kullanma

ASP.NET, Kullanıcı hesapları ve rolleri oluşturmayı ve yönetmeyi ve Kullanıcı ve rol tabanlı yetkilendirme kurallarını belirtmeyi kolaylaştıran bir [Web sitesi yönetim aracı](https://msdn.microsoft.com/library/yy40ytx0.aspx) (WSAT) içerir. WSAT 'ı kullanmak için Çözüm Gezgini ASP.NET yapılandırma simgesine tıklayın veya Web sitesine veya proje menüsüne gidin ve ASP.NET yapılandırma seçeneğini belirleyin. Her iki yaklaşım da bir Web tarayıcısı başlatır ve şunun gibi bir adreste WSAT 'a işaret eder: `http://localhost:portNumber/asp.netwebadminfiles/default.aspx?applicationPhysicalPath=pathToApplication`

WSAT üç bölüme ayrılmıştır:

- **Güvenlik** -kullanıcıları, rolleri ve yetkilendirme kurallarını yönetin.
- **ApplicationConfiguration** -&lt;appSettings&gt; ve SMTP ayarlarını buradan yönetin. Ayrıca, uygulamayı çevrimdışına alabilir ve hata ayıklama ve izleme ayarlarını buradan yönetebilir ve varsayılan özel hata sayfasını belirtebilirsiniz.
- **Providerconfiguration** -uygulama hizmetleri tarafından kullanılan sağlayıcıları yapılandırın.

Güvenlik Bölümü ( **Şekil 1**' de gösterilmiştir) Yeni Kullanıcı oluşturma, kullanıcıları yönetme, rolleri oluşturma ve yönetme ve erişim kuralları oluşturma ve yönetme bağlantılarını içerir. Buradan sisteme yeni bir rol ekleyebilir, mevcut bir kullanıcıyı silebilir veya belirli bir kullanıcı hesabından rol ekleyebilir veya kaldırabilirsiniz.

[![](users-and-roles-on-the-production-website-vb/_static/image2.png)](users-and-roles-on-the-production-website-vb/_static/image1.png)

**Şekil 1**: WSAT güvenlik bölümü, kullanıcıları ve rolleri yönetme seçeneklerini içerir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](users-and-roles-on-the-production-website-vb/_static/image3.png))

Ne yazık ki, WSAT yalnızca yerel olarak erişilebilir. Uzaktan üretim Web sitenizde WSAT 'ı ziyaret edemezsiniz; `www.yoursite.com/asp.netwebadminfiles/default.aspx` ziyaret ederseniz, 404 bulunmayan bir yanıt alırsınız. WSAT 'ı destekleyen kod, Kullanıcı ve rolleri oluşturmak, düzenlemek ve silmek için .NET Framework `Membership` ve `Roles` sınıflarını kullanır. Bu sınıflar, hangi sağlayıcının kullanılacağını belirlemek için Web uygulamasının yapılandırma bilgilerine başvurun; [ *uygulama hizmetleri öğreticisini kullanan bir Web sitesini yapılandırmaya* ](configuring-a-website-that-uses-application-services-vb.md) geri döndüğünüzde, `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcılarını kullanmak için Book İncelemeleri Web sitesini kuruyoruz. Bu, `Web.config``<membership>` ve `<roleManager>` bölümleri eklemeyi de kuyruklu.

[!code-xml[Main](users-and-roles-on-the-production-website-vb/samples/sample1.xml)]

`<membership>` ve `<roleManager>` bölümlerinin sırasıyla `type` özniteliğinde `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcılarına başvurdığına göz önünde olduğunu unutmayın. Bu sağlayıcılar, Kullanıcı ve rol bilgilerini belirtilen bir SQL Server veritabanında depolar. Bu sağlayıcılar tarafından kullanılan veritabanı, `~/ConfigSections/databaseConnectionStrings.config` dosyasında tanımlanan `connectionStringName` özniteliğiyle belirtilir `ReviewsConnectionString`. Geliştirme ortamındaki `databaseConnectionStrings.config` dosyasının geliştirme veritabanına bağlantı dizesini içerdiğini hatırlayın, üretimde `databaseConnectionStrings.config` dosyası üretim veritabanına olan bağlantı dizesini içerir.

Bir Nutshell 'de, WSAT 'ın geliştirme ortamı aracılığıyla yerel olarak erişilmesi ve `databaseConnectionStrings.config` dosyasında belirtilen veritabanındaki kullanıcı ve rol bilgileriyle birlikte çalışması gerekir. Sonuç olarak, geliştirme ortamındaki `databaseConnectionStrings.config` dosyadaki bağlantı dizesi bilgilerini değiştirdiğimiz takdirde, üretim ortamındaki kullanıcıları ve rolleri yönetmek için WSAT 'ı yerel olarak kullanabiliriz.

Bu işlevi göstermek için, Visual Studio 'da geliştirme ortamında `databaseConnectionStrings.config` dosyasını açın ve geliştirme veritabanı bağlantı dizesini üretim veritabanı bağlantı dizesiyle değiştirin. Ardından WSAT 'ı başlatın, Güvenlik sekmesine gidin ve "Password!" parolasıyla Sam adlı yeni bir kullanıcı ekleyin (tırnak işaretleri daha az). **Şekil 2** bu hesabı oluştururken WSAT ekranını gösterir.

[![](users-and-roles-on-the-production-website-vb/_static/image5.png)](users-and-roles-on-the-production-website-vb/_static/image4.png)

**Şekil 2**: üretim ortamında Sam adlı yeni bir Kullanıcı oluşturma  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](users-and-roles-on-the-production-website-vb/_static/image6.png))

`databaseConnectionStrings.config` 'deki bağlantı dizesini üretim veritabanı sunucusuna işaret etmek üzere değiştirdiğimiz için, Sam üretim ortamında bir kullanıcı olarak eklenmiştir. Bunu doğrulamak için, `databaseConnectionStrings.config` dosyasındaki bağlantı dizesini geliştirme veritabanına geri değiştirin ve ardından geliştirme ortamında `Login.aspx` sayfasını ziyaret edin. Sam olarak oturum açmayı deneyin (bkz. **Şekil 3**).

[![](users-and-roles-on-the-production-website-vb/_static/image8.png)](users-and-roles-on-the-production-website-vb/_static/image7.png)

**Şekil 3**: geliştirme ortamında Sam olarak oturum açılamıyor  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](users-and-roles-on-the-production-website-vb/_static/image9.png))

Kullanıcı hesabı bilgileri yerel veritabanında bulunmadığından, geliştirme ortamında Sam olarak oturum açılamıyor. Bunun yerine, üretim veritabanına eklenmiştir. Bunu doğrulamak için, `aspnet_Users` tablosunun içeriğini hem geliştirme hem de üretim veritabanlarında görüntüleyin. Geliştirme ortamında Scott, Jisun ve Gamze kullanıcıları için yalnızca üç kayıt olmalıdır. Ancak, üretim veritabanındaki `aspnet_Users` tablosu dört kayda sahiptir: Scott, Jisun, Çiğdem ve Sam. Sonuç olarak, Sam üretimde Web sitesinde oturum açabilir, ancak geliştirme ortamından oturum açabilir.

[![](users-and-roles-on-the-production-website-vb/_static/image11.png)](users-and-roles-on-the-production-website-vb/_static/image10.png)

**Şekil 4**: Sam üretim web sitesinde oturum açabilir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](users-and-roles-on-the-production-website-vb/_static/image12.png))

> [!NOTE]
> WSAT ile çalışmayı bitirdiğinizde `databaseConnectionStrings.config` dosyasındaki bağlantı dizesini geliştirme veritabanının bağlantı dizesine geri değiştirmeyi unutmayın, aksi takdirde siteyi geliştirme ortamı aracılığıyla sınarken üretim verileriyle birlikte çalışmanız gerekir. Ayrıca, az önce tartışdığımız teknikle kullanıcıları ve rolleri uzaktan yönetmek için WSAT 'ı kullanmamıza izin verdiğinden, diğer WSAT yapılandırma seçeneklerinde (erişim kuralları, SMTP ayarları, hata ayıklama ve izleme ayarları vb.) yapılan değişiklikler `Web.config` dosyayı değiştirin. Sonuç olarak, ayarlarda yapılan tüm değişiklikler, üretim ortamına değil, geliştirme ortamı için geçerlidir.

## <a name="creating-custom-user-and-role-management-web-pages"></a>Özel Kullanıcı ve rol yönetimi Web sayfaları oluşturma

WSAT, kullanıcıları ve rolleri yönetmeye yönelik kullanıma hazır bir sistem sağlar, ancak yalnızca yerel olarak başlatılabilir ve üretimde kullanıcıları ve rolleri yönetmek için bağlantı dizesi bilgilerinde değişiklik yapılmasını gerektirir. Kullanıcı hesaplarını destekleyen çoğu web sitesi, yöneticilerin site içindeki sayfalardan Kullanıcı ve rolleri yönetmesine olanak tanıyan bir dizi Kullanıcı ve rol yönetimi Web sayfası da içerir. Web tabanlı yönetim sayfaları, kullanıcıları ve rolleri yönetmeyi çok daha kolay hale getirir ve erişimi olmayan birçok yönetici ya da yönetici ya da WSAT 'yi başlatmak üzere Visual Studio 'Yu kullanmaya yönelik teknik arka plan olabilecek siteler için gereklidir.

ASP.NET, bu yönetim Web sayfalarının birçoğunu sürükleyip bırakma kadar kolay bir şekilde uygulamayı sağlayan yerleşik, oturum açma ile ilgili birçok Web denetimi içerir. Örneğin, CreateUserWizard denetimini sayfaya sürükleyip birkaç özellik ayarlayarak Yöneticiler için yeni bir kullanıcı hesabı oluşturmak üzere bir sayfa oluşturabilirsiniz. Aslında, **Şekil 2** ' de gösterilen WSAT 'da Kullanıcı oluşturmaya yönelik sayfa, sayfalarınıza ekleyebileceğiniz aynı CreateUserWizard denetimini kullanır. Ayrıca, üyelik ve rol hizmetleri 'nin işlevleri .NET Framework `Membership` ve `Roles` sınıfları aracılığıyla programlama yoluyla kullanılabilir. Bu sınıflarla kullanıcıları ve rolleri oluşturmak, düzenlemek ve silmek için kod yazabilir, ayrıca rollere kullanıcı ekleme veya kaldırma, hangi kullanıcıların hangi rollerde olduğunu belirleme ve diğer Kullanıcı ve rolle ilgili görevleri gerçekleştirme gibi işlemleri yapabilirsiniz.

[ *Uygulama hizmetleri kullanan bir Web sitesini yapılandırmak* için öğreticiyi](configuring-a-website-that-uses-application-services-vb.md) `CreateAccount.aspx`adlı `Admin` klasörüne bir sayfa ekledim. Bu sayfa, yöneticinin siteye yeni bir kullanıcı hesabı eklemesini ve yeni oluşturulan kullanıcının yönetici rolünde olup olmadığını belirtmesini sağlar (bkz. **Şekil 5**).

[![](users-and-roles-on-the-production-website-vb/_static/image14.png)](users-and-roles-on-the-production-website-vb/_static/image13.png)

**Şekil 5**: Yöneticiler yeni kullanıcı hesapları oluşturabilir  
([Tam boyutlu görüntüyü görüntülemek Için tıklayın](users-and-roles-on-the-production-website-vb/_static/image15.png))

Kullanıcı ve rol yönetimi sayfalarını oluşturma hakkında daha ayrıntılı bilgi için, `Membership` ve `Roles` sınıflarını ve oturum ile ilgili ASP.NET Web denetimlerini kullanma hakkında adım adım yönergeler içeren [Web sitesi güvenlik öğreticilerimi](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)okuduğunuzdan emin olun. Yeni hesap oluşturmak, Roller oluşturmak ve yönetmek, rollere kullanıcı atamak ve diğer yaygın yönetim görevleri için Web sayfaları oluşturma hakkında rehberlik bulacaksınız.

Üretim web sitesinde WSAT benzeri işlevselliği uygulamak için, her zaman WSAT 'ın özelliklerini uygulayan kendi Web sayfası serisini oluşturabilirsiniz. Kullanmaya başlamanıza yardımcı olmak için, `%WINDIR%\Microsoft.NET\Framework\v2.0.50727\ASP.NETWebAdminFiles`klasöründe bulunan WSAT kaynak kodunu inceleyin. Diğer bir seçenek de, [kendi web sitesi yönetim aracınızı sunarak kendi](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)makalesinde paylaştığı, can 'ın başka bir yerinde WSAT alternatifi kullanmaktır. Özel bir WSAT benzeri araç oluşturma işlemi boyunca okuyucular aracılığıyla, uygulamanın karşıdan yükleme için kaynak kodunu (içinde C#) içerir ve özel wcts 'yi barındırılan bir Web sitesine eklemek için adım adım yönergeler sağlar.

## <a name="summary"></a>Özet

ASP.NET Web sitesi yönetim aracı (WSAT), Web siteniz için Kullanıcı ve rol bilgilerini yönetmek üzere üyelik ve rol uygulama hizmetleri ile birlikte kullanılabilir. Ne yazık ki, WSAT yalnızca yerel olarak erişilebilir ve üretim Web sitenizde ziyaret edilemez. Ancak, geliştirme ortamındaki bağlantı dizesini üretim veritabanına işaret etmek üzere değiştirerek, üretim Web sitesindeki kullanıcıları ve rolleri yönetmek için WSAT 'ı kullanabilirsiniz.

WSAT yaklaşımı, kullanıcıları ve rolleri yönetmenin hızlı ve kolay bir yolunu sunarken, WSAT 'ı Visual Studio 'dan başlatmaya ve bağlantı dizesi bilgilerinde geçici değişikliklere de olanak sağlar. WSAT, üretimde kullanıcıları ve rolleri yönetmenin hızlı bir yolunu sunar, ancak çok sayıda yönetici olan veya Visual Studio ile WSAT sahibi olmayan ya da alışık olmayan yöneticiler için iyi bir şekilde çalışmaz. Bu nedenlerden dolayı, Kullanıcı hesaplarını destekleyen çoğu web sitesinin bir dizi yönetim Web sayfası vardır. Böyle bir Web sayfaları kümesi, WSAT gereksinimini ortadan kaldırır ve herhangi bir bilgisayardan çeşitli yönetici kullanıcılar tarafından kullanılır.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [ASP 'yi İnceleme. NET 'in üyelik, roller ve profil](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Kendi web sitesi yönetim aracınızı toplama](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [Web sitesi yönetim aracına genel bakış](https://msdn.microsoft.com/library/yy40ytx0.aspx)
- [Web sitesi güvenlik öğreticileri](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)

> [!div class="step-by-step"]
> [Öncekini](precompiling-your-website-vb.md)
