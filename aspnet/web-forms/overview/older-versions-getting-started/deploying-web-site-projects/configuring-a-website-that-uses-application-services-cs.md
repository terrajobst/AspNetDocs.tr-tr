---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
title: Uygulama Hizmetleri (C#) kullanan bir Web sitesini yapılandırma | Microsoft Docs
author: rick-anderson
description: ASP.NET sürüm 2,0, .NET Framework bir parçası olan ve yo... için bir yapı blok Hizmetleri paketi olarak hizmet veren bir dizi uygulama hizmeti sunmuştur.
ms.author: riande
ms.date: 04/23/2009
ms.assetid: 1e33d1c6-3f9f-4c26-81e2-2a8f8907bb05
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs
msc.type: authoredcontent
ms.openlocfilehash: 72aaca84b8c8d6e558d4c946faa57fa999d48bf8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/28/2019
ms.locfileid: "74570129"
---
# <a name="configuring-a-website-that-uses-application-services-c"></a>Uygulama Hizmetleri Kullanan Bir Web Sitesi Yapılandırma (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting) tarafından

[Kodu indirin](https://download.microsoft.com/download/E/6/F/E6FE3A1F-EE3A-4119-989A-33D1A9F6F6DD/ASPNET_Hosting_Tutorial_09_CS.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/C/3/9/C391A649-B357-4A7B-BAA4-48C96871FEA6/aspnet_tutorial09_AppServicesConfig_cs.pdf)

> ASP.NET sürüm 2,0, .NET Framework bir parçası olan ve Web uygulamanıza zengin işlevsellik eklemek için kullanabileceğiniz bir yapı blok Hizmetleri paketi olarak hizmet veren bir dizi uygulama hizmeti sunmuştur. Bu öğreticide, üretim ortamında uygulama hizmetlerini kullanmak için bir Web sitesinin nasıl yapılandırılacağı ve üretim ortamındaki Kullanıcı hesaplarını ve rolleri yönetme ile ilgili yaygın sorunları ele alınmaktadır.

## <a name="introduction"></a>Giriş

ASP.NET sürüm 2,0, .NET Framework bir parçası olan ve Web uygulamanıza zengin işlevsellik eklemek için kullanabileceğiniz bir yapı blok Hizmetleri paketi olarak hizmet veren bir dizi *uygulama hizmeti*sunmuştur. Uygulama Hizmetleri şunları içerir:

- **Üyelik** -Kullanıcı hesapları oluşturmak ve yönetmek IÇIN bir API.
- **Roller** -kullanıcıları gruplar halinde kategorilere ayırmak IÇIN bir API.
- **Profile** -özel, kullanıcıya özgü içerik depolamaya YÖNELIK bir API.
- **Site haritası** -daha sonra menüler ve içerik haritaları gibi gezinme denetimleriyle görüntülenebilecek bir hiyerarşi biçiminde bir site s mantıksal yapısını tanımlamaya YÖNELIK bir API.
- **Kişiselleştirme** -genellikle [*Web*](https://msdn.microsoft.com/library/e0s9t4ck.aspx)siteleriyle kullanılan özelleştirme TERCIHLERINI korumak için bir API.
- **Sistem durumu izleme** -çalışan bir Web uygulaması için performansı, güvenliği, hataları ve diğer sistem durumu ölçümlerini izlemeye YÖNELIK bir API.

Uygulama Hizmetleri API 'Leri belirli bir uygulamaya bağlı değildir. Bunun yerine, uygulama hizmetlerinin belirli bir *sağlayıcıyı*kullanmasını ve bu sağlayıcının belirli bir teknolojiyi kullanarak hizmeti uyguladığını söyleyebilirsiniz. Bir Web barındırma şirketinde barındırılan Internet tabanlı Web uygulamaları için en yaygın olarak kullanılan sağlayıcılar, SQL Server veritabanı uygulaması kullanan sağlayıcılardır. Örneğin `SqlMembershipProvider`, Kullanıcı hesabı bilgilerini bir Microsoft SQL Server veritabanında depolayan üyelik API 'SI için bir sağlayıcıdır.

Uygulama hizmetleri ve SQL Server sağlayıcılarının kullanılması, uygulamayı dağıtma sırasında bazı güçlükleri ekler. Başlangıçlara yönelik olarak, uygulama Hizmetleri veritabanı nesnelerinin hem geliştirme hem de üretim veritabanlarında doğru şekilde oluşturulması ve uygun şekilde başlatılmış olması gerekir. Ayrıca, yapılması gereken önemli yapılandırma ayarları vardır.

> [!NOTE]
> Uygulama Hizmetleri API 'Leri, çalışma zamanında API s uygulama ayrıntılarının sağlanmasını sağlayan bir tasarım [*modeli olan sağlayıcı modeli*](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)kullanılarak tasarlanmıştır. .NET Framework, bir SQL Server veritabanı uygulaması kullanan üyelik ve rol API 'Leri için sağlayıcılar olan `SqlMembershipProvider` ve `SqlRoleProvider`gibi kullanılabilecek bir dizi uygulama hizmeti sağlayıcısıyla birlikte gelir. Ayrıca özel bir sağlayıcı oluşturup eklenti ekleyebilirsiniz. Aslında, Book Incelemeleri Web uygulaması, site haritası API 'SI (`ReviewSiteMapProvider`) için bir özel sağlayıcı içerir. Bu, site haritasını, `Genres` ve veritabanındaki `Books` tablolardaki verileri oluşturur.

Bu öğreticide, üyelik ve rol API 'Lerini kullanmak için kitap Incelemelerinin Web uygulamasını nasıl genişlettiğiyle ilgili bir bakış açıklanır. Daha sonra, SQL Server veritabanı uygulamasıyla uygulama hizmetleri 'ni kullanan bir Web uygulamasını dağıtmaya ve üretim ortamındaki Kullanıcı hesaplarını ve rolleri yönetme ile ilgili yaygın sorunları gidermeye geçer.

## <a name="updates-to-the-book-reviews-application"></a>Kitap Inceleme uygulamasındaki güncelleştirmeler

Son iki öğreticilerde, kitap Incelemelerinin Web uygulaması statik bir Web sitesinden dinamik, veri odaklı bir Web uygulamasına, tarzları ve incelemeleri yönetmeye yönelik bir dizi yönetim sayfası ile tamamlanan bir şekilde güncelleştirildi. Ancak, bu yönetim bölümü şu anda korunmuyor. yönetim sayfası URL 'sini bilen (veya tahmin eden) herhangi bir Kullanıcı, sitemizdeki incelemeleri oluşturma, düzenleme veya silme işlemi yapabilir. Bir Web sitesinin belirli kısımlarını korumanın yaygın bir yolu, Kullanıcı hesaplarını uygulamak ve ardından belirli kullanıcılara veya rollere erişimi kısıtlamak için URL yetkilendirme kurallarını kullanmaktır. Bu öğreticiyle indirilebilir olan kitap Incelemeleri Web uygulaması, Kullanıcı hesaplarını ve rolleri destekler. Yönetici adlı tek bir role sahiptir ve yalnızca bu roldeki kullanıcılar yönetim sayfalarına erişebilir.

> [!NOTE]
> Kitap Incelemelerinin Web uygulamasında üç Kullanıcı hesabı oluşturduğdum: Scott, Jisun ve gamze. Üç kullanıcının tümü aynı parolaya sahiptir: **parola!** Scott ve Jisun yönetici rolünde, Çiğdem değil. Yönetim dışı site sayfalarına hala anonim kullanıcılar erişebilir. Diğer bir deyişle, yönetmek istemediğiniz sürece siteyi ziyaret etmek için oturum açmanız gerekmez, bu durumda yönetici rolünde bir kullanıcı olarak oturum açmanız gerekir.

Kitap Inceleme uygulaması ana sayfası, kimliği doğrulanmış ve anonim kullanıcılar için farklı bir kullanıcı arabirimi içerecek şekilde güncelleştirilmiştir. Anonim bir Kullanıcı, sağ üst köşedeki bir oturum açma bağlantısı gördüğü siteyi ziyaret ederse. Kimliği doğrulanmış bir Kullanıcı "hoş geldiniz geri, *Kullanıcı adı*!" iletisini görür ve oturumu kapatmak için bir bağlantı. Ayrıca, bir ziyaretçi kimlik doğrulaması için Kullanıcı arabirimi ve mantığını sağlayan bir oturum açma Web denetimi içeren bir oturum açma sayfası (`~/Login.aspx`) vardır. Yalnızca Yöneticiler yeni hesaplar oluşturabilir. (`~/Admin` klasöründe Kullanıcı hesapları oluşturmak ve yönetmek için sayfalar vardır.)

### <a name="configuring-the-membership-and-roles-apis"></a>Üyelik ve rol API 'Lerini yapılandırma

Kitap Incelemeleri Web uygulaması, Kullanıcı hesaplarını desteklemek ve bu kullanıcıları rollere (yani, yönetici rolü) gruplamak için üyelik ve rol API 'Lerini kullanır. `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcı sınıfları, hesap ve rol bilgilerini bir SQL Server veritabanında depolamak istediğimiz için kullanılır.

> [!NOTE]
> Bu öğreticide, üyelik ve rol API 'Lerini destekleyecek bir Web uygulamasını yapılandırma konusunda ayrıntılı bir inceleme olması amaçlanmamıştır. Bu API 'Lere tam bakış ve bu Web sitesini kullanmak üzere yapılandırmak için gerçekleştirmeniz gereken adımlar için lütfen [*Web sitesi güvenlik öğreticilerimi*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)okuyun.

Uygulama hizmetlerini bir SQL Server veritabanıyla kullanmak için, önce bu sağlayıcılar tarafından kullanılan veritabanı nesnelerini Kullanıcı hesabı ve rol bilgilerinin depolanmasını istediğiniz veritabanına eklemeniz gerekir. Bu önkoşul veritabanı nesneleri çeşitli tablolar, görünümler ve saklı yordamlar içerir. Aksi belirtilmedikçe, `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcı sınıfları uygulama s `App_Data` klasöründe bulunan `ASPNETDB` adlı bir SQL Server Express sürümü veritabanı kullanır; Böyle bir veritabanı yoksa, çalışma zamanında bu sağlayıcılar tarafından gerekli veritabanı nesneleriyle otomatik olarak oluşturulur.

Uygulama Hizmetleri veritabanı nesnelerini Web sitesinin uygulamaya özgü verilerin depolandığı veritabanında oluşturmak için bu mümkün ve genellikle idealdir. .NET Framework, veritabanı nesnelerini belirtilen bir veritabanına yükleyen `aspnet_regsql.exe` adlı bir araçla birlikte gönderilir. Bu aracı daha sonra bu nesneleri `App_Data` klasöründeki (geliştirme veritabanı) `Reviews.mdf` veritabanına eklemek için kullandınız. Bu nesneleri üretim veritabanına eklerken Bu öğreticinin ilerleyen kısımlarında bu aracı nasıl kullanacağınızı inceleyeceğiz.

Uygulama Hizmetleri veritabanı nesnelerini `ASPNETDB` dışında bir veritabanına eklerseniz, `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcı sınıfları yapılandırmalarının uygun veritabanını kullanmaları için özelleştirmeniz gerekir. Üyelik sağlayıcısını özelleştirmek için `Web.config``<system.web>` bölümünde [ *&lt;üyelik&gt; öğesi*](https://msdn.microsoft.com/library/1b9hw62f.aspx) ekleyin. Rol sağlayıcısını yapılandırmak için [ *&lt;roleManager&gt; öğesini*](https://msdn.microsoft.com/library/ms164660.aspx) kullanın. Aşağıdaki kod parçacığı, uygulama `Web.config` Inceler ve üyelik ve roller API 'Leri için yapılandırma ayarlarını gösterir. Her ikisinin de, sırasıyla `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcılarını kullanan yeni bir sağlayıcıyı `ReviewMembership` ve `ReviewRole` kaydedeceğini unutmayın.

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample1.xml)]

`Web.config` File s `<authentication>` öğesi form tabanlı kimlik doğrulamasını destekleyecek şekilde yapılandırılmıştır.

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample2.xml)]

### <a name="limiting-access-to-the-administration-pages"></a>Yönetim sayfalarına erişimi sınırlandırma

ASP.NET, belirli bir dosya veya klasöre Kullanıcı veya rol tarafından *URL yetkilendirmesi* özelliği aracılığıyla erişim izni vermenizi ya da reddetmeyi kolaylaştırır. ( *IIS ile ASP.NET geliştirme sunucusu öğreticisi arasındaki temel farklılıklara* ilişkin URL yetkilendirmesi kısaca ele ALıNMıŞTıR ve ııs Ile ASP.net GELIŞTIRME sunucusunun URL yetkilendirme kurallarını statik ve dinamik içerik için farklı şekilde nasıl uygulayacağınızı gösterdi.) Yönetici rolündeki kullanıcılar hariç `~/Admin` klasörüne erişimi yasakladığımızda, URL yetkilendirme kurallarını bu klasöre eklememiz gerekir. Özellikle, URL yetkilendirme kurallarının yönetici rolünde kullanıcılara izin vermemesi ve diğer tüm kullanıcıları reddetmesi gerekir. Bu, `~/Admin` klasörüne aşağıdaki içeriklerle bir `Web.config` dosyası eklenerek gerçekleştirilir:

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample3.xml)]

ASP.NET s URL yetkilendirme özelliği hakkında daha fazla bilgi edinmek ve kullanıcıların ve rollerinin yetkilendirme kurallarını öğrenmek için nasıl kullanılacağı hakkında daha fazla bilgi için, [*Web sitemin güvenlik öğreticilerimin*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) [*Kullanıcı tabanlı yetkilendirme*](../../older-versions-security/membership/user-based-authorization-cs.md) ve [*rol tabanlı yetkilendirme*](../../older-versions-security/roles/role-based-authorization-cs.md) öğreticilerini okuduğunuzdan emin olun.

## <a name="deploying-a-web-application-that-uses-application-services"></a>Uygulama Hizmetleri kullanan bir Web uygulamasını dağıtma

Uygulama hizmetleri ve bir veritabanında uygulama hizmetleri bilgilerini depolayan bir sağlayıcı kullanan bir Web sitesi dağıtıldığında, uygulama hizmetleri için gereken veritabanı nesnelerinin üretim veritabanında oluşturulması zorunludur. Başlangıçta üretim veritabanı bu nesneleri içermez, bu nedenle uygulama ilk kez dağıtıldığında (veya uygulama hizmetleri eklendikten sonra ilk kez dağıtıldığında), bu önkoşul veritabanı nesnelerini almak için ek adımlar gerçekleştirmeniz gerekir üretim veritabanı.

Geliştirme ortamında oluşturulan kullanıcı hesaplarını üretim ortamına çoğaltmak istiyorsanız, uygulama hizmetleri 'ni kullanan bir Web sitesi dağıtımında başka bir zorluk ortaya çıkabilir. Üyelik ve roller yapılandırmasına bağlı olarak, geliştirme ortamında oluşturulan kullanıcı hesaplarını üretim veritabanına başarıyla kopyalayasanız bile, bu kullanıcılar üretimde Web uygulamasında oturum açamasa da olasıdır. Bu sorunun nedenine bakacağız ve bunun oluşmasını nasıl önleyebiliriz.

ASP.NET, Visual Studio 'dan başlatılabilen iyi bir [*Web sitesi yönetim aracı (WSAT)* ](https://msdn.microsoft.com/library/yy40ytx0.aspx) ile birlikte gelir ve Kullanıcı hesabı, roller ve yetkilendirme kurallarının Web tabanlı bir arabirim aracılığıyla yönetilmesini sağlar. Ne yazık ki, WSAT yalnızca yerel Web siteleri için geçerlidir; Yani, üretim ortamındaki Web uygulaması için Kullanıcı hesaplarını, rolleri ve yetkilendirme kurallarını uzaktan yönetmek için kullanılamaz. Üretim Web sitenizdeki WSAT benzeri davranışları uygulamak için farklı yöntemlere bakacağız.

### <a name="adding-the-database-objects-using-aspnet_regsqlexe"></a>ASPNET\_regsql. exe ' yi kullanarak veritabanı nesneleri ekleme

*Veritabanı dağıtma* öğreticisi, verileri geliştirme veritabanından üretim veritabanına kopyalamayı ve bu tekniklerin uygulama Hizmetleri veritabanı nesnelerini üretim veritabanına kopyalamak için kesinlikle kullanılabileceğini gösterdi. Başka bir seçenek de, uygulama Hizmetleri veritabanı nesnelerini bir veritabanından ekleyen veya kaldıran `aspnet_regsql.exe` aracıdır.

> [!NOTE]
> `aspnet_regsql.exe` Aracı, belirtilen veritabanında veritabanı nesnelerini oluşturur. Bu veritabanı nesnelerindeki verileri geliştirme veritabanından üretim veritabanına geçirmez. Geliştirme veritabanındaki kullanıcı hesabı ve rol bilgilerini üretim veritabanına kopyalamak için *bir veritabanı dağıtma* Öğreticisi ' nde ele alınan teknikleri kullanın.

`aspnet_regsql.exe` aracını kullanarak veritabanı nesnelerinin üretim veritabanına nasıl ekleneceğini inceleyelim. Windows Gezgini 'ni açarak ve bilgisayarınızdaki .NET Framework sürüm 2,0 dizinine giderek başlayın,% WINDIR% \ Microsoft. NET\Framework\v2.0.50727. `aspnet_regsql.exe` aracını bulmanız gerekir. Bu araç, komut satırından kullanılabilir, ancak aynı zamanda bir grafik kullanıcı arabirimi de içerir; grafik bileşenini başlatmak için `aspnet_regsql.exe` dosyasına çift tıklayın.

Aracı, amacını açıklayan bir giriş ekranı görüntüleyerek başlar. Şekil 1 ' de gösterilen "Kurulum seçeneği seçin" ekranına ilerlemek için Ileri ' ye tıklayın. Buradan, uygulama Hizmetleri veritabanı nesnelerini eklemeyi veya bir veritabanından kaldırmayı seçebilirsiniz. Bu nesneleri üretim veritabanına eklemek istiyoruz, "uygulama hizmetleri için SQL Server Yapılandır" seçeneğini belirleyin ve Ileri ' ye tıklayın.

[Uygulama Hizmetleri için SQL Server yapılandırmayı ![seçin](configuring-a-website-that-uses-application-services-cs/_static/image2.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image1.jpg)

**Şekil 1**: Uygulama Hizmetleri Için SQL Server yapılandırmayı seçin ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-a-website-that-uses-application-services-cs/_static/image3.jpg))

"Sunucu ve veritabanını seçin" ekranında, veritabanına bağlanmak için bilgi ister. Web barındırma şirketiniz tarafından sağlanan veritabanı sunucusunu, güvenlik kimlik bilgilerini ve veritabanı adını girin ve Ileri ' ye tıklayın.

> [!NOTE]
> Veritabanı sunucunuzu ve kimlik bilgilerinizi girdikten sonra, veritabanı açılan listesini genişletirken bir hata alabilirsiniz. `aspnet_regsql.exe` Aracı, sunucudaki veritabanlarının listesini almak için `sysdatabases` sistem tablosunu sorgular, ancak bazı Web barındırma şirketleri bu bilgilerin genel kullanıma açık olmaması için veritabanı sunucularını kilitler. Bu hatayı alırsanız, doğrudan açılan listeye veritabanı adını yazabilirsiniz.

[![, veritabanı bağlantı bilgilerinizi Içeren Aracı sağlayın](configuring-a-website-that-uses-application-services-cs/_static/image5.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image4.jpg)

**Şekil 2**: veritabanını veritabanınızın bağlantı bilgileriyle sağlama ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-a-website-that-uses-application-services-cs/_static/image6.jpg))

Sonraki ekranda, uygulama Hizmetleri veritabanı nesneleri belirtilen veritabanına ekleneceklerinde, gerçekleşecek şekilde olan eylemler özetlenmektedir. Bu eylemi gerçekleştirmek için Ileri ' ye tıklayın. Birkaç dakika sonra, veritabanı nesnelerinin eklendiğini belirten son ekran görüntülenir (bkz. Şekil 3).

[Başarılı ![! Uygulama Hizmetleri veritabanı nesneleri üretim veritabanına eklendi](configuring-a-website-that-uses-application-services-cs/_static/image8.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image7.jpg)

**Şekil 3**: başarılı! Uygulama Hizmetleri veritabanı nesneleri üretim veritabanına eklendi ([tam boyutlu görüntüyü görüntülemek Için tıklayın](configuring-a-website-that-uses-application-services-cs/_static/image9.jpg))

Uygulama Hizmetleri veritabanı nesnelerinin üretim veritabanına başarıyla eklendiğini doğrulamak için SQL Server Management Studio açın ve üretim veritabanınıza bağlanın. Şekil 4 ' te gösterildiği gibi, artık veritabanınızda uygulama Hizmetleri veritabanı tablolarını, `aspnet_Applications`, `aspnet_Membership``aspnet_Users`ve benzerlerini görmeniz gerekir.

[![veritabanı nesnelerinin üretim veritabanına eklendiğini onaylayın](configuring-a-website-that-uses-application-services-cs/_static/image11.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image10.jpg)

**Şekil 4**: veritabanı nesnelerinin üretim veritabanına eklendiğini onaylayın ([tam boyutlu görüntüyü görüntülemek için tıklayın](configuring-a-website-that-uses-application-services-cs/_static/image12.jpg))

Yalnızca, uygulama hizmetlerini kullanmaya başladıktan sonra Web uygulamanızı ilk kez veya ilk kez dağıttığınızda `aspnet_regsql.exe` aracını kullanmanız gerekir. Bu veritabanı nesneleri üretim veritabanından olduktan sonra, yeniden eklenmesi veya değiştirilmesi gerekmez.

### <a name="copying-user-accounts-from-development-to-production"></a>Kullanıcı hesaplarını geliştirmeden üretime kopyalama

Uygulama hizmetleri bilgilerini bir SQL Server veritabanına depolamak için `SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcı sınıflarını kullanırken, Kullanıcı hesabı ve rol bilgileri, `aspnet_Users`, `aspnet_Membership`, `aspnet_Roles`ve `aspnet_UsersInRoles`dahil olmak üzere çeşitli veritabanı tablolarında depolanır (diğerleri arasında). Geliştirme sırasında geliştirme ortamında Kullanıcı hesapları oluşturursanız, ilgili kayıtları geçerli veritabanı tablolarından kopyalayarak, bu kullanıcı hesaplarını üretimde çoğaltabilirsiniz. Uygulama Hizmetleri veritabanı nesnelerini dağıtmak için veritabanı Yayımlama Sihirbazı 'Nı kullandıysanız kayıtları kopyalamak için de seçmiş olabilirsiniz; Bu, geliştirmede oluşturulan kullanıcı hesaplarının de üretimde olması ile sonuçlanacaktır. Ancak, yapılandırma ayarlarınıza bağlı olarak, hesaplarını geliştirmede oluşturulan ve üretime kopyalanan kullanıcıların üretim Web sitesinden oturum açmadığını fark edebilirsiniz. Ne sağlar?

`SqlMembershipProvider` ve `SqlRoleProvider` sağlayıcı sınıfları, tek bir veritabanının birden çok uygulama için kullanıcı deposu olarak kullanılabileceği şekilde tasarlanmıştı. bu şekilde, her uygulamanın teorik olarak, kullanıcıların aynı ada sahip olan ve çakışan Kullanıcı adları ve rolleri vardır. Bu esnekliğe izin vermek için, veritabanı `aspnet_Applications` tablosundaki uygulamaların bir listesini tutar ve her Kullanıcı bu uygulamalardan biriyle ilişkilendirilir. Özellikle `aspnet_Users` tablo, her kullanıcıyı `aspnet_Applications` tablosundaki bir kayda bağlayan bir `ApplicationId` sütununa sahiptir.

`ApplicationId` sütununa ek olarak, `aspnet_Applications` tablo, uygulama için daha fazla insan dostu bir ad sağlayan bir `ApplicationName` sütunu da içerir. Bir Web sitesi, oturum açma sayfasından bir kullanıcı kimlik bilgilerini doğrulama gibi bir kullanıcı hesabıyla çalışmayı denediğinde `SqlMembershipProvider` sınıfa hangi uygulamanın birlikte çalıştığını söylemelidir. Genellikle bunu uygulama adı sağlayarak yapar ve bu değer, `Web.config`-özel olarak `applicationName` özniteliği aracılığıyla sağlayıcının s yapılandırmasından gelir.

Ancak `applicationName` özniteliği `Web.config`belirtilmemişse ne olur? Böyle bir durumda, üyelik sistemi `applicationName` değer olarak uygulama kök yolunu kullanır. `applicationName` özniteliği `Web.config`açıkça ayarlanmamışsa, geliştirme ortamının ve üretim ortamının farklı bir uygulama kökü kullanmasına ve bu nedenle uygulama hizmetlerindeki farklı uygulama adlarıyla ilişkilendirilecektir. Bu tür bir uyuşmazlık oluşursa, geliştirme ortamında oluşturulan kullanıcıların, üretim ortamı için `ApplicationId` değeriyle eşleşmeyen bir `ApplicationId` değeri olacaktır. Net sonuç, bu kullanıcıların oturum açabilmeyeceği bir sonuçlardır.

> [!NOTE]
> Bu durumda kendinizi bulursanız, Kullanıcı hesapları, eşleşmeyen bir `ApplicationId` değeri ile üretime kopyalanmışsa, bu hatalı `ApplicationId` değerlerini üretimde kullanılan `ApplicationId` için güncelleştirmek üzere bir sorgu yazabilirsiniz. Güncelleştirildikten sonra, hesapları geliştirme ortamında oluşturulan kullanıcılar artık üretimde Web uygulamasında oturum açabiliyor.

İyi haberler, iki ortamın aynı `ApplicationId` kullandığından emin olmak için uygulayabileceğiniz basit bir adımdır. tüm uygulama hizmetleri sağlayıcılarınız için `Web.config` `applicationName` özniteliğini açıkça ayarlayın. `applicationName` özniteliğini, `<membership>` ve `<roleManager>` öğelerinde "Bookincelemeleri" olarak, `Web.config` tarafından gösterilen kod parçacığı olarak ayarlar.

[!code-xml[Main](configuring-a-website-that-uses-application-services-cs/samples/sample4.xml)]

`applicationName` özniteliğini ve bunun arkasındaki ktionale ayarlama hakkında daha fazla bilgi için [*Scott Guthrie*](https://weblogs.asp.net/scottgu/) s blog gönderisine bakın, [*ASP.NET üyeliğini ve diğer sağlayıcıları yapılandırırken her zaman ApplicationName özelliğini ayarlayın*](https://weblogs.asp.net/scottgu/443634).

### <a name="managing-user-accounts-in-the-production-environment"></a>Üretim ortamında kullanıcı hesaplarını yönetme

ASP.NET Web sitesi yönetim aracı (WSAT) Kullanıcı hesapları oluşturmayı ve yönetmeyi, rolleri tanımlamanızı ve uygulamayı ve Kullanıcı ve rol tabanlı yetkilendirme kurallarını yazımı kolaylaştırır. Çözüm Gezgini gidip ASP.NET yapılandırma simgesine tıklayarak veya Web sitesine veya proje menülerine gidip ASP.NET yapılandırma menü öğesini seçerek, Visual Studio 'dan WSAT 'ı başlatabilirsiniz. Ne yazık ki, WSAT yalnızca yerel Web siteleriyle çalışabilir. Bu nedenle, üretim ortamındaki Web sitesini yönetmek için iş istasyonunuzdan WSAT 'ı kullanamazsınız.

İyi haberler, WSAT tarafından sağlanan tüm işlevlerin üyelik ve roller API 'Leri aracılığıyla programlı bir şekilde kullanılabilmesini sağlamadır; Ayrıca, WSAT ekranlarından birçoğu standart ASP.NET login ile ilgili denetimleri kullanır. Kısaca, Web sitenize gerekli yönetim özelliklerini sunan ASP.NET sayfaları ekleyebilirsiniz.

Daha önceki bir öğreticinin, kitap Incelemeleri Web uygulamasını bir `~/Admin` klasörü içerecek şekilde güncelleştirdiklerini ve bu klasörün yalnızca yönetici rolündeki kullanıcılara izin verecek şekilde yapılandırıldığını unutmayın. `CreateAccount.aspx` adlı klasöre, yöneticinin yeni bir kullanıcı hesabı oluşturanan bir sayfa ekledim. Bu sayfa, yeni bir kullanıcı hesabı oluşturmak için Kullanıcı arabirimi ve arka uç mantığını göstermek üzere CreateUserWizard denetimini kullanır. Ne kadar çok, denetimi yeni kullanıcının da yönetici rolüne eklenip eklenmeyeceğini belirten bir onay kutusu içerecek şekilde özelleştirdim (bkz. Şekil 5). Biraz iş sayesinde, başka bir şekilde WSAT tarafından sağlanabilecek Kullanıcı ve rol yönetimiyle ilgili görevleri uygulayan özel bir sayfa kümesi oluşturabilirsiniz.

> [!NOTE]
> Üyelik ve rol API 'Lerini kullanma hakkında daha fazla bilgi için, oturum açma ile ilgili ASP.NET Web denetimleriyle birlikte, [*Web sitesi güvenlik öğreticilerimi*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)okuduğunuzdan emin olun. CreateUserWizard denetimini özelleştirme hakkında daha fazla bilgi için [*Kullanıcı hesapları oluşturma*](../../older-versions-security/membership/creating-user-accounts-cs.md) ve [*ek kullanıcı bilgileri*](../../older-versions-security/membership/storing-additional-user-information-cs.md) öğreticilerini depolama ya da [*CreateUserWizard denetimini özelleştiren*](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx) [*Erich Peterson*](http://www.erichpeterson.com/) s makalesini inceleyin.

[![yöneticileri yeni kullanıcı hesapları oluşturabilir](configuring-a-website-that-uses-application-services-cs/_static/image14.jpg)](configuring-a-website-that-uses-application-services-cs/_static/image13.jpg)

**Şekil 5**: Yöneticiler yeni kullanıcı hesapları oluşturabilir ([tam boyutlu görüntüyü görüntülemek için tıklatın](configuring-a-website-that-uses-application-services-cs/_static/image15.jpg))

WSAT 'ın tüm işlevlerine ihtiyacınız varsa, [*kendi web sitesi yönetim aracınızı*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)(yazarın can) özel bır WSAT benzeri araç oluşturma sürecinde izlenecek bir şekilde gözden geçirin. Dan uygulama kaynak kodunu paylaşır (içinde C#) ve barındırılan Web sitenize eklemek için adım adım yönergeler sağlar.

## <a name="summary"></a>Özet

Uygulama Hizmetleri veritabanı uygulamasını kullanan bir Web uygulaması dağıtıldığında, önce üretim veritabanının gerekli veritabanı nesnelerine sahip olduğundan emin olmanız gerekir. Bu nesneler, *veritabanı dağıtma* öğreticisinde açıklanan teknikler kullanılarak eklenebilir. Alternatif olarak, bu öğreticide gördüğünüz gibi `aspnet_regsql.exe` aracını kullanabilirsiniz. Geliştirme ve üretim ortamlarında kullanılan uygulama adının (geliştirme ortamında oluşturulan kullanıcı ve rollerin üretimde geçerli olmasını istiyorsanız önemli olan) ve teknikleri ile ilgili diğer sorunlar üretim ortamındaki kullanıcıları ve rolleri yönetme.

Programlamanın kutlu olsun!

### <a name="further-reading"></a>Daha Fazla Bilgi

Bu öğreticide ele alınan konular hakkında daha fazla bilgi için aşağıdaki kaynaklara bakın:

- [*ASP.NET SQL Server kayıt aracı (aspnet_regsql. exe)* ](https://msdn.microsoft.com/library/ms229862.aspx)
- [*SQL Server için Uygulama Hizmetleri veritabanı oluşturuluyor*](https://msdn.microsoft.com/library/x28wfk74.aspx)
- [*SQL Server üyelik şeması oluşturma*](../../older-versions-security/membership/creating-the-membership-schema-in-sql-server-cs.md)
- [*ASP.NET s üyeliğini, rolleri ve profilini İnceleme*](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [*Kendi web sitesi yönetim aracınızı toplama*](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [*Web sitesi güvenlik öğreticileri*](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md)
- [*Web sitesi yönetim aracına genel bakış*](https://msdn.microsoft.com/library/yy40ytx0.aspx)

> [!div class="step-by-step"]
> [Önceki](configuring-the-production-web-application-to-use-the-production-database-cs.md)
> [İleri](strategies-for-database-development-and-deployment-cs.md)
