---
uid: identity/overview/getting-started/introduction-to-aspnet-identity
title: ASP.NET Identity giriş-ASP.NET 4. x
author: jongalloway
description: ASP.NET üyelik sistemi 2005 ' de ASP.NET 2,0 ile tanıtılmıştı ve daha sonra Web uygulamalarının typicall... şeklinde birçok değişiklik yapılmıştır.
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 38717fc1-5989-43cf-952d-4007cc1dd923
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/introduction-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0268dfc16cd2cfb1e79ee14997a4c5eb247af950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583848"
---
# <a name="introduction-to-aspnet-identity"></a>ASP.NET Identity’ye Giriş

> ASP.NET üyelik sistemi 2005 ile ASP.NET 2,0 ile tanıtılmıştı ve bu yana Web uygulamalarının genellikle kimlik doğrulama ve yetkilendirmeyi işleme biçiminde çok sayıda değişiklik yapılmıştır. ASP.NET Identity, Web, telefon veya tablet için modern uygulamalar oluştururken üyelik sisteminin ne olması gerektiğini yepyeni bir bakış.

## <a name="background-membership-in-aspnet"></a>Arka plan: ASP.NET 'de üyelik

### <a name="aspnet-membership"></a>ASP.NET Üyeliği

[ASP.NET üyeliği](https://msdn.microsoft.com/library/yh26yfzy(v=VS.100).aspx) , form kimlik doğrulaması ve Kullanıcı adları, parolalar ve profil verileri için bir SQL Server veritabanı ile ilgili olarak 2005 ' de yaygın olan site üyeliği gereksinimlerini çözmeye yönelik olarak tasarlanmıştır. Günümüzde web uygulamaları için çok daha geniş bir veri depolama seçenekleri dizisi vardır ve çoğu geliştirici, sitelerinin kimlik doğrulama ve yetkilendirme işlevselliği için sosyal kimlik sağlayıcılarını kullanmasını sağlamak ister. ASP.NET üyelik tasarımının sınırlamaları bu geçişi zorlaştırır:

- Veritabanı şeması SQL Server için tasarlanmıştı ve bunu değiştiremezsiniz. Profil bilgilerini ekleyebilirsiniz, ancak ek veriler farklı bir tabloya paketlenmiştir ve bu sayede profil sağlayıcısı API 'SI dışında herhangi bir şekilde erişmeyi zorlaştırır.
- Sağlayıcı sistemi, yedekleme veri deposunu değiştirmenize olanak sağlar, ancak sistem ilişkisel bir veritabanı için uygun varsayımlar etrafında tasarlanmıştır. Üyelik bilgilerini Azure depolama tabloları gibi ilişkisel olmayan bir depolama mekanizmasına depolamak için bir sağlayıcı yazabilir, ancak NoSQL veritabanlarına uygulanamayan yöntemler için çok fazla kod ve çok sayıda `System.NotImplementedException` özel durum yazarak ilişkisel tasarıma geçici bir çözüm yapmanız gerekir.
- Oturum açma/çıkış işlevleri, Forms kimlik doğrulamasını temel aldığı için, üyelik sistemi [Owın](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)kullanamaz. OWIN, dış kimlik sağlayıcılarını (Microsoft hesapları, Facebook, Google, Twitter gibi) kullanan oturum açma işlemleri için destek ve şirket içi Active Directory veya kurumsal hesapları kullanan oturum açma işlemleri gibi kimlik doğrulaması için ara yazılım bileşenleri içerir Azure Active Directory. OWıN, OAuth 2,0, JWT ve CORS için de destek içerir.

### <a name="aspnet-simple-membership"></a>ASP.NET basit üyelik

[ASP.net basit üyelik](../../../web-pages/overview/security/16-adding-security-and-membership.md) , ASP.NET Web sayfaları için bir üyelik sistemi olarak geliştirilmiştir. WebMatrix ve Visual Studio 2010 SP1 ile yayınlanmıştır. Basit Üyeliğin amacı, üyelik işlevlerinin bir Web sayfaları uygulamasına kolayca ekleneceğini sağlamaktır.

Basit üyelik, Kullanıcı profili bilgilerini özelleştirmeyi daha kolay hale getirir, ancak ASP.NET üyeliğiyle diğer sorunları paylaşır ve bazı sınırlamalara sahiptir:

- Üyelik Sistemi verilerinin ilişkisel olmayan bir depoda kalıcı hale getirilmesi zor.
- OWIN ile kullanamazsınız.
- Mevcut ASP.NET üyelik sağlayıcılarıyla iyi çalışmaz ve genişletilebilir değildir.

### <a name="aspnet-universal-providers"></a>ASP.NET Evrensel Sağlayıcılar

[ASP.net evrensel sağlayıcılar](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) , üyelik bilgilerini Microsoft Azure SQL veritabanı kalıcı hale getirmek için geliştirilmiştir ve ayrıca SQL Server Compact de çalışır. Evrensel sağlayıcılar Entity Framework Code First kurulmuştur, yani evrensel sağlayıcılar, EF tarafından desteklenen tüm depolarda verileri kalıcı hale getirmek için kullanılabilir. Evrensel sağlayıcılar ile veritabanı şeması da çok büyük bir şekilde temizlenir.

Evrensel sağlayıcılar ASP.NET üyelik altyapısına kurulmuştur, bu nedenle yine de SqlMembership sağlayıcısıyla aynı sınırlamaları alırlar. Diğer bir deyişle, ilişkisel veritabanları için tasarlanırlar ve profil ve Kullanıcı bilgilerini özelleştirmek zordur. Bu sağlayıcılar, oturum açma ve oturum kapatma işlevselliği için de form kimlik doğrulaması kullanır.

## <a name="aspnet-identity"></a>ASP.NET Kimlik

ASP.NET 'deki üyelik hikayesi yıllarca gelişmiş olduğundan, ASP.NET ekibi müşterilerden gelen geri bildirimlerinden çok fazla öğrenmiştir.

Kullanıcıların kendi uygulamanızda kaydoldukları bir Kullanıcı adı ve parola girerek oturum açabilecekleri varsayımını artık geçerli değildir. Web, daha fazla sosyal hale geldi. Kullanıcılar Facebook, Twitter ve diğer sosyal web siteleri gibi sosyal kanallar aracılığıyla birbirleriyle gerçek zamanlı olarak etkileşime geçer. Geliştiriciler, kullanıcıların Web sitelerinde zengin bir deneyim alabilmesi için sosyal kimliklerle oturum açabilmesini ister. Modern bir üyelik sisteminin, yeniden yönlendirme tabanlı oturum açma işlemlerini Facebook, Twitter ve diğerleri gibi kimlik doğrulama sağlayıcılarına etkinleştirmeleri gerekir.

Web geliştirme geliştirmesinde Web geliştirme alışkanlıkları oldu. Uygulama kodu için birim testi uygulama geliştiricileri için temel bir sorun haline geldi. 2008 ' de, geliştiricilerin Unit Instable ASP.NET uygulamaları oluşturmasına yardımcı olmak için bir parçası olan Model-View-Controller (MVC) düzenine göre yeni bir çerçeve eklenmiştir. Birim testi yapmak isteyen geliştiriciler, uygulama mantığını da bunu üyelik sistemi ile yapabilmesini ister.

Web uygulaması geliştirmede bu değişiklikler düşünüldüğünde, ASP.NET Identity aşağıdaki hedeflerle geliştirilmiştir:

- **Bir ASP.NET Identity sistemi**

    - ASP.NET Identity, ASP.NET MVC, Web Forms, Web sayfaları, Web API ve SignalR gibi tüm ASP.NET çerçeveleri ile kullanılabilir.
    - ASP.NET Identity Web, telefon, mağaza veya karma uygulamalar oluştururken kullanılabilir.
- **Kullanıcı hakkında profil verilerini takma kolaylığı**

    - Kullanıcı ve profil bilgileri şeması üzerinde denetiminiz vardır. Örneğin, sistemde bir hesabı kaydettirdiklerinde kullanıcılara girilen Doğum tarihlerinin depolanmasını kolayca sağlayabilirsiniz.

- **Kalıcılık denetimi**

    - Varsayılan olarak, ASP.NET Identity sistem tüm Kullanıcı bilgilerini bir veritabanında depolar. ASP.NET Identity, tüm Kalıcılık mekanizmasını uygulamak için Entity Framework Code First kullanır.
    - Veritabanı şemasını kontrol ettiğiniz için, tablo adlarını değiştirme veya birincil anahtarların veri türünü değiştirme gibi ortak görevlerin yapması basittir.
    - SharePoint, Azure Depolama Tablo hizmeti, NoSQL veritabanları vb. gibi farklı depolama mekanizmalarına `System.NotImplementedExceptions` özel durumlar oluşturmak zorunda kalmadan kolayca takabilirsiniz.
- **Birim test edilebilirlik**

    - ASP.NET Identity Web uygulamasını daha fazla birim için daha kararlı hale getirir. ASP.NET Identity kullanan uygulamanızın parçaları için birim testleri yazabilirsiniz.
- **Rol sağlayıcısı**

    - Rollere göre uygulamanızın bölümlerine erişimi kısıtlamanızı sağlayan bir rol sağlayıcısı vardır. "Yönetici" gibi rolleri kolayca oluşturabilir ve rollere kullanıcı ekleyebilirsiniz.
- **Talepler tabanlı**

    - ASP.NET Identity, Kullanıcı kimliğinin bir talepler kümesi olarak temsil edildiği talep tabanlı kimlik doğrulamasını destekler. Talepler, geliştiricilerin rolün izin verenden çok daha açıklayıcı olmasını sağlar. Rol üyeliği yalnızca bir Boole (üye veya üye olmayan) olduğunda, bir talep kullanıcının kimliği ve üyeliği hakkında zengin bilgiler içerebilir.
- **Sosyal oturum açma sağlayıcıları**

    - Microsoft hesabı, Facebook, Twitter, Google ve diğerleri gibi sosyal günlükleri kolayca uygulamanıza ekleyebilir ve kullanıcıya özgü verileri uygulamanıza kaydedebilirsiniz.

- **OWıN tümleştirmesi**

    - ASP.NET kimlik doğrulaması artık, herhangi bir OWIN tabanlı konakta kullanılabilen OWıN ara yazılımını temel alır. ASP.NET Identity System. Web üzerinde hiçbir bağımlılığı yok. Bu, tamamen uyumlu bir OWIN çerçevesidir ve herhangi bir OWıN barındırılan uygulamasında kullanılabilir.
    - ASP.NET Identity, Web sitesindeki kullanıcıların oturum açma/kapatma için OWıN kimlik doğrulamasını kullanır. Bunun anlamı, tanımlama bilgisini oluşturmak için FormsAuthentication kullanmak yerine, uygulamanın bunu yapmak için OWIN tanıtım ıeauthentication ' ı kullanmasını sağlar.
- **NuGet paketi**

    - ASP.NET Identity, Visual Studio 2017 ile birlikte gelen ASP.NET MVC, Web Forms ve Web API şablonlarına yüklenen bir NuGet paketi olarak yeniden dağıtılır. NuGet galerisinden bu NuGet paketini indirebilirsiniz.
    - NuGet paketi olarak ASP.NET Identity serbest bırakmak, ASP.NET ekibinin yeni özellikler ve hata düzeltmeleri üzerinde yineleme yapmayı kolaylaştırır ve bunları çevik bir şekilde geliştiricilere sunar.

## <a name="get-started-with-aspnet-identity"></a>ASP.NET Identity kullanmaya başlayın

ASP.NET Identity, ASP.NET MVC, Web Forms, Web API ve SPA için Visual Studio 2017 proje şablonlarında kullanılır. Bu kılavuzda, proje şablonlarının kaydetme, oturum açma ve Kullanıcı oturumu kapatma işlevleri eklemek için ASP.NET Identity nasıl kullandığını göstereceğiz.

ASP.NET Identity, aşağıdaki yordam kullanılarak uygulanır. Bu makalenin amacı ASP.NET Identity, size yüksek düzeyde bir genel bakış sunvermektir. Bu adımı adım adım takip edebilir veya yalnızca ayrıntıları okuyabilirsiniz. ASP.NET Identity kullanarak uygulama oluşturma hakkında daha ayrıntılı yönergeler için, Kullanıcı, rol ve profil bilgileri eklemek üzere yeni API 'yi kullanma dahil, bu makalenin sonundaki sonraki adımlar bölümüne bakın.

1. Bireysel hesaplarla bir ASP.NET MVC uygulaması oluşturun. ASP.NET MVC, Web Forms, Web API, SignalR vb. ASP.NET Identity kullanabilirsiniz. Bu makalede bir ASP.NET MVC uygulaması ile başlayacağız.  
  
    ![](introduction-to-aspnet-identity/_static/image1.png)
2. Oluşturulan proje, ASP.NET Identity için aşağıdaki üç paketi içerir.

    - [`Microsoft.AspNet.Identity.EntityFramework`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)  
   Bu paket, SQL Server için ASP.NET Identity verileri ve şemayı kalıcı hale getirmek ASP.NET Identity Entity Framework uygulamasına sahiptir.
    - [`Microsoft.AspNet.Identity.Core`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Core/)  
   Bu paketin ASP.NET Identity için temel arabirimleri vardır. Bu paket, Azure Tablo depolama, NoSQL veritabanları vb. gibi farklı Kalıcılık depolarını hedefleyen ASP.NET Identity bir uygulama yazmak için kullanılabilir.
    - [`Microsoft.AspNet.Identity.OWIN`](http://www.nuget.org/packages/Microsoft.AspNet.Identity.Owin/)  
   Bu paket, ASP.NET uygulamalarında ASP.NET Identity ile OWıN kimlik doğrulamasını fişe eklemek için kullanılan işlevselliği içerir. Bu, uygulamanıza oturum açma işlevselliği eklediğinizde ve bir tanımlama bilgisi oluşturmak için OWıN tanımlama bilgisi kimlik doğrulama ara yazılımını çağırdığınızda kullanılır.
3. Kullanıcı oluşturma.  
   Uygulamayı başlatın ve ardından Kullanıcı oluşturmak için **Kaydet** bağlantısına tıklayın. Aşağıdaki görüntüde, Kullanıcı adını ve parolayı toplayan Kaydet sayfası gösterilmektedir.  
  
    ![](introduction-to-aspnet-identity/_static/image2.png)  
  
   Kullanıcı **Kaydet** düğmesini seçtiğinde, hesap denetleyicisinin `Register` eylemi, aşağıda vurgulanan şekılde ASP.NET Identity API 'sini çağırarak kullanıcı oluşturur:

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample1.cs?highlight=8-9)]
4. Oturum Aç.  
   Kullanıcı başarıyla oluşturulduysa `SignInAsync` yöntemi tarafından oturum açmış olur.  

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample6.cs?highlight=12)]

   `SignInManager.SignInAsync` yöntemi bir [ClaimsIdentity](https://msdn.microsoft.com/library/system.security.claims.claimsidentity.aspx)oluşturur. ASP.NET Identity ve OWıN tanımlama bilgisi kimlik doğrulaması talep tabanlı sistem olduğundan, çerçeve, uygulamanın kullanıcı için bir ClaimsIdentity oluşturmasını gerektirir. ClaimsIdentity, kullanıcının ait olduğu roller gibi kullanıcı için tüm taleplerle ilgili bilgiler içerir.   
 
5. Oturumunuzu kapatın.  
   Hesap denetleyicisindeki oturum kapatma eylemini çağırmak için **Oturumu Kapat** bağlantısını seçin. 

    [!code-csharp[Main](introduction-to-aspnet-identity/samples/sample5.cs?highlight=6)]

   Yukarıdaki vurgulanmış kod, OWIN `AuthenticationManager.SignOut` yöntemini gösterir. Bu, Web Forms öğesinde [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) modülü tarafından kullanılan [FormsAuthentication. SignOut](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) yöntemine benzerdir.

## <a name="components-of-aspnet-identity"></a>ASP.NET Identity bileşenleri

Aşağıdaki diyagramda ASP.NET Identity sisteminin bileşenleri gösterilmektedir (bunu genişletmek için [Bu](introduction-to-aspnet-identity/_static/image3.png) veya diyagramda seçin). Yeşil renkte paketler ASP.NET Identity sistemi oluşturun. Diğer tüm paketler, ASP.NET uygulamalarında ASP.NET Identity sistemi kullanmak için gereken bağımlılıklardır.

[![](introduction-to-aspnet-identity/_static/image5.png)](introduction-to-aspnet-identity/_static/image4.png)

Aşağıda, daha önce belirtilmeyen NuGet paketlerinin kısa bir açıklaması verilmiştir:

- [Microsoft.Owin.Security.Cookies](http://www.nuget.org/packages/Microsoft.Owin.Security.Cookies/)  
 Uygulamanın, ASP 'ye benzer tanımlama bilgisi tabanlı kimlik doğrulama kullanmasını sağlayan ara yazılım. NET ' in Forms kimlik doğrulaması.
- [EntityFramework](http://www.nuget.org/packages/EntityFramework/)  
 Entity Framework, Microsoft 'un ilişkisel veritabanları için önerilen veri erişim teknolojisidir.

## <a name="migrating-from-membership-to-aspnet-identity"></a>Üyeliğinden ASP.NET Identity geçirme

Yeni ASP.NET Identity sistemine ASP.NET üyeliği veya basit üyelik kullanan mevcut uygulamalarınızı geçirmeye yönelik yönergeler sağlıyoruz.

## <a name="next-steps"></a>Sonraki Adımlar

- [Facebook ve Google OAuth2 ve OpenID oturum açma ile ASP.NET MVC 5 uygulaması oluşturma](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md)  
 Öğretici, kullanıcı veritabanına profil bilgileri eklemek ve Google ve Facebook ile kimlik doğrulaması yapmak için ASP.NET Identity API 'sini kullanır.
- [Auth ve SQL DB ile ASP.NET MVC uygulaması oluşturma ve Azure App Service dağıtma](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)  
 Bu öğreticide, Kullanıcı ve rol eklemek için kimlik API 'sinin nasıl kullanılacağı gösterilmektedir.
- [https://github.com/rustd/AspnetIdentitySample](https://github.com/rustd/AspnetIdentitySample)  
 Temel rollerin ve Kullanıcı desteğinin nasıl ekleneceğini ve rollerin ve Kullanıcı yönetiminin nasıl yapılacağını gösteren örnek uygulama.
