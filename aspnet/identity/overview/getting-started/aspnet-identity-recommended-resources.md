---
uid: identity/overview/getting-started/aspnet-identity-recommended-resources
title: Önerilen kaynakları ASP.NET Identity-ASP.NET 4. x
author: Rick-Anderson
description: Bu konu, ASP.NET Identity kullanma hakkında belge kaynaklarına bağlantılar sağlar. Harika bir blog gönderisi, StackOverflow iş parçacığı veya başka bir bağla biliyorsanız...
ms.author: riande
ms.date: 04/09/2015
ms.assetid: 0f78aec2-f509-46fa-b20f-d5208425d8ec
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/aspnet-identity-recommended-resources
msc.type: authoredcontent
ms.openlocfilehash: 4b2a6689839f66121f4a32ee5934f6cda50ae812
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456576"
---
# <a name="aspnet-identity-recommended-resources"></a>ASP.NET Identity Önerilen Kaynaklar

[Rick Anderson](https://twitter.com/RickAndMSFT) tarafından

> Bu konu, ASP.NET Identity kullanma hakkında belge kaynaklarına bağlantılar sağlar.
>
> Harika bir blog gönderisi, [StackOverflow](http://stackoverflow.com) iş parçacığı veya yararlı olabilecek başka bir bağlantı biliyorsanız, bağlantıya sahip [bir e-posta gönderin](mailto:aspnetue@microsoft.com?subject=Identity recommended resources) veya bu sayfanın en altında bir ileti bırakın.

- [ASP.NET Identity ile Çalışmaya Başlama](#gettingstarted)
- [Yeni öne çıkan makaleler, makaleyi okumalıdır](#feat)
- [Ara ASP.NET Identity](#adv)
- [Videolar](#video)
- [Soru sormak, Özellikler istemek, hata ve gecelik derlemeler bildirmek](#samp)
- [Kimlik üzerindeki blog gönderileri](#blog)
- [ASP.NET Identity için özel depolama sağlayıcıları](#cust)
- [Ek kimlik kaynakları](#additional)
- [Soru-cevap &amp;](#qand)

<a id="gettingstarted"></a>

## <a name="getting-started-with-aspnet-identity"></a>ASP.NET Identity ile Çalışmaya Başlama

- [Facebook, Twitter, LinkedIn ve Google OAuth2 oturum açma Ile MVC 5 uygulaması](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) Bu öğreticide, Facebook ve Google OAuth 2 yetkilendirmesi ile ASP.NET MVC 5 uygulamasının nasıl yazılacağı gösterilmektedir. Ayrıca, kimlik veritabanına nasıl ek veri ekleneceğini gösterir.
- [Bir Azure 'A üyelik, OAuth ve SQL veritabanı Ile güvenli bir ASP.NET MVC uygulaması dağıtın](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Bu öğreticide, Azure dağıtımı, rollerle uygulamanızı güvenli hale getirme, Kullanıcı ve rolleri eklemek için üyelik API 'sini kullanma ve ek güvenlik özellikleri eklenir.
- [ASP.NET Identity’ye Giriş](introduction-to-aspnet-identity.md)
- [Oturum açma, e-posta onayı ve parola sıfırlama ile güvenli bir ASP.NET MVC 5 Web uygulaması oluşturma](../../../mvc/overview/security/create-an-aspnet-mvc-5-web-app-with-email-confirmation-and-password-reset.md)
- [SMS ve e-posta iki öğeli kimlik doğrulaması özellikli ASP.NET MVC 5 uygulaması](../../../mvc/overview/security/aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md)

<a id="feat"></a>

## <a name="new-featured-must-read-articles"></a>Yeni öne çıkan makaleler, makaleyi okumalıdır

- Izlenecek yol: [Benjamin günü](http://www.benday.com/about/) [Microsoft hesabı kimlik doğrulaması Ile ASP.NET MVC kimliği](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [ASP.NET Identity 2,0 kimlik modellerini genişletme ve dizeler yerine tamsayı anahtarlar kullanma](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
- [ASP.NET Web API 2, Owın ve Identity kullanarak AngularJS Token Authentication](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [WSAT yerine Thinktecture. IdentityManager](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [ASP.NET Identity 2,0: kullanıcıları ve rolleri özelleştirme](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)

<a id="adv"></a>

## <a name="intermediate-aspnet-identity"></a>Ara ASP.NET Identity

- [ASP.NET Identity ile hesap onaylama ve parola kurtarma](../features-api/account-confirmation-and-password-recovery-with-aspnet-identity.md)
- [ASP.NET Identity ile SMS ve e-posta kullanılan iki öğeli kimlik doğrulaması](../features-api/two-factor-authentication-using-sms-and-email-with-aspnet-identity.md)
- [Mevcut Bir Web Sitesini SQL Üyeliğinden ASP.NET Identity’ye Geçirme](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [Boş veya Mevcut Bir Web Forms Projesine ASP.NET Identity Ekleme](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md)
- Ino Esposito tarafından ASP.NET Identity MSDN Magazine [dış kimlik doğrulaması](https://msdn.microsoft.com/magazine/dn745860.aspx)
- MSDN Magazine, Dino Esposito tarafından[ASP.NET Identity Ilk bakış](https://msdn.microsoft.com/magazine/dn605872.aspx)
- [ASP.NET Identity – Kullanıcı kilitleme](http://tech.trailmax.info/2014/06/asp-net-identity-user-lockout/)

<a id="samp"></a>

## <a name="where-to-ask-questions-request-features-report-a-bug-and-nightly-builds"></a>Soru sormak, Özellikler istemek, hata ve gecelik derlemeler bildirmek

- StackOverflow için, [ASPNET-Identity](http://stackoverflow.com/questions/tagged/asp.net-identity) etiketini kullanın
- ASP.NET forumları için [güvenlik forumuna](https://forums.asp.net/25.aspx) gönderi yapın ve başlığa **ASP.NET Identity** ekleyin.
- [GitHub üzerinde ASP.NET Identity](https://github.com/aspnet/AspNetIdentity) Gecelik derlemeler, istek özellikleri ve açık hatalar alın.

<a id="blog"></a>

## <a name="blog-posts-on-identity"></a>Kimlik üzerindeki blog gönderileri

- [ASP.NET Identity SecurityStamp nedir?](http://stackoverflow.com/questions/19487322/what-is-asp-net-identitys-iusersecuritystampstoretuser-interface/19505060#19505060)
- [John Aton](https://twitter.com/xivSolutions) tarafından

    - [ASP.NET Identity 2,0 kimlik modellerini genişletme ve dizeler yerine tamsayı anahtarlar kullanma](http://typecastexception.com/post/2014/07/13/ASPNET-Identity-20-Extending-Identity-Models-and-Using-Integer-Keys-Instead-of-Strings.aspx)
    - [ASP.NET Identity 2,0: kullanıcıları ve rolleri özelleştirme](http://typecastexception.com/post/2014/06/22/ASPNET-Identity-20-Customizing-Users-and-Roles.aspx)
    - [ASP.NET MVC ve kimlik 2,0: temel kavramları anlama](http://typecastexception.com/post/2014/04/20/ASPNET-MVC-and-Identity-20-Understanding-the-Basics.aspx)
    - [Hesap doğrulama ve Iki öğeli yetkilendirme ayarlama](http://typecastexception.com/post/2014/04/20/ASPNET-Identity-20-Setting-Up-Account-Validation-and-Two-Factor-Authorization.aspx)
    - [ASP.NET MVC 5 ve Visual Studio 2013 'de kimlik hesapları için DB bağlantısı ve kod Ilk geçişini yapılandırma](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx)
- Sağlayan- [Taıer Joudeh](http://bitoftech.net/taiseer-joudeh-blog/)

    - [ASP.NET Web API 2, Owın ara yazılımı ve ASP.NET Identity kullanarak belirteç tabanlı kimlik doğrulaması](http://bitoftech.net/2014/06/01/token-based-authentication-asp-net-web-api-2-owin-asp-net-identity/)
    - [ASP.NET Web API 2, Owın ve Identity kullanarak AngularJS Token Authentication](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
    - [ASP .NET Web API 2 ve Owin – Part 3 kullanarak AngularJS uygulamasında OAuth yenileme belirteçlerini etkinleştirin.](http://bitoftech.net/2014/07/16/enable-oauth-refresh-tokens-angularjs-app-using-asp-net-web-api-2-owin/)
- [Anders Abel](https://twitter.com/anders_abel)

    - [Owın dış kimlik doğrulama ardışık düzenini anlama](http://coding.abel.nu/2014/06/understanding-the-owin-external-authentication-pipeline/)
    - [ASP.NET Identity ve Owın genel bakış](http://coding.abel.nu/2014/06/asp-net-identity-and-owin-overview/)

  By [K. Scott Allen](https://twitter.com/OdeToCode) , ODE 'dan koda

    - [ASP.NET Core kimliği](http://odetocode.com/blogs/scott/archive/2013/11/25/asp-net-core-identity.aspx) Bu blog, IUser, ıuserstore ve I\*Store arabirimleri dahil olmak üzere çekirdek soyutlamalarını inceler.
    - [Entity Framework ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/03/asp-net-identity-with-the-entity-framework.aspx) MVC 5 ' teki bireysel kullanıcı hesapları, Web API 'SI ve SPA uygulamaları, bağlantı dizeleri ve bağlamların yönetilmesi
    - [ASP.NET Identity özelleştirme seçenekleri](http://odetocode.com/blogs/scott/archive/2014/01/09/customization-options-with-asp-net-identity.aspx)
    - [ASP.NET Identity uygulama](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- [Benjamin günü](http://www.benday.com/about/)[izlenecek yol: ASP.NET MVC kimliği Ile Microsoft hesabı kimlik doğrulaması](http://www.benday.com/2014/02/25/walkthrough-asp-net-mvc-identity-with-microsoft-account-authentication/)
- [Brock Allen](https://twitter.com/BrockLAllen)

    - [OWıN/Katana kimlik doğrulama ara yazılımı ile harici oturum açma sağlayıcıları (sosyal oturumlar) üzerinde bir öncü](http://brockallen.com/2014/01/09/a-primer-on-external-login-providers-social-logins-with-owinkatana-authentication-middleware/)
    - [Identityreboot 'A giriş](http://brockallen.com/2014/02/11/introducing-identityreboot/): ASP.NET Identity için bir uzantılar kümesi.
- [Pranav Oystogi](https://twitter.com/rustd)

    - [Sosyal sağlayıcılardan daha fazla bilgi alın](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [@beabigrockstar](https://twitter.com/beabigrockstar) (Jerrie Pelser)

    - [2 faktörlü kimlik doğrulaması](http://www.beabigrockstar.com/blog/2-factor-authentication-with-asp-net-identity-2-0-beta-1/)
    - [ASP.NET Identity ile Google Authenticator kullanma](http://www.beabigrockstar.com/blog/using-google-authenticator-asp-net-identity/)
    - [ASP.NET MVC 5 kimlik doğrulama Kılavuzu](http://www.beabigrockstar.com/)
- [VS 2013 proje şablonlarında kullanılan sosyal sağlayıcılardan daha fazla bilgi alın](https://blogs.msdn.com/b/webdev/archive/2013/10/16/get-more-information-from-social-providers-used-in-the-vs-2013-project-templates.aspx)
- [ASP.NET Identity ile basit bir ToDo uygulaması oluşturma ve kullanıcıları TOA ile ilişkilendirme](https://blogs.msdn.com/b/webdev/archive/2013/10/20/building-a-simple-todo-application-with-asp-net-identity-and-associating-users-with-todoes.aspx)
- [ASP.NET Identity Ile Google OpenID tümleştirme sorunları](http://blog.technovert.com/2014/01/google-openid-integration-issues-asp-net-identity/) Hata alırsanız: HTTP hatası 404,15 – bulunamadı istek filtreleme modülü, sorgu dizesinin çok uzun olduğu bir isteği reddedecek şekilde yapılandırıldı
- [WSAT yerine Thinktecture. IdentityManager](http://www.hanselman.com/blog/ThinktectureIdentityManagerAsAReplacementForTheASPNETWebSiteAdministrationTool.aspx)
- [ASP.NET Web API 2, Owın ve Identity kullanarak AngularJS Token Authentication](http://bitoftech.net/2014/06/09/angularjs-token-authentication-using-asp-net-web-api-2-owin-asp-net-identity/)
- [Entity Framework olmadan basit Asp.net Identity Core](https://code.msdn.microsoft.com/Simple-Aspnet-Identiy-Core-7475a961)
- [Sheo Narayan](http://www.dotnetfunda.com/profile/sheonarayan.aspx) tarafından [MVC Için ASP.NET Identity rollerle çalışma](http://www.dotnetfunda.com/articles/show/2898/working-with-roles-in-aspnet-identity-for-mvc)
- Alistaar Matthews tarafından [ASP.net üyeliğinden ASP.NET Identity taşıma](http://webdojo.sharepoint.com/ajmatthews/_layouts/15/start.aspx#/Lists/Posts/Post.aspx?ID=2)

<a id="video"></a>

## <a name="videos"></a>Videolar

- Channel 9 [ASP.NET uygulamaları ve hizmetleri güvenli hale getirme:](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B421#fbid=PhVT9E1WRtr?hashlink=fbid) Ido Flatow tarafından modern uygulamalar için güvenlik
- Pranav Oystogi tarafından Channel 9 [ASP.NET Identity girişi](https://channel9.msdn.com/Events/dotnetConf/2014/ASP-NET-Identity-Security)
- Cory Fowler tarafından [ASP.NET Identity kullanarak kanal 9 ASP.NET kimlik doğrulaması](https://channel9.msdn.com/Shows/Web+Camps+TV/Special-Movember-Episode-ASPNET-Authentication-Provider)
- Channel 9 [Modern Web Apps oluşturma:](https://channel9.msdn.com/Series/Building-Modern-Web-Apps/03) Jeff Koch tarafından ASP.NET Identity
- Channel 9, Alex thissen tarafından [ASP.NET Identity Web sitenizin güvenliğini sağlama](https://channel9.msdn.com/Events/TechDays/Techdays-2014-the-Netherlands/Securing-your-website-with-ASP-NET-Identity)
- [ASP.NET Identity mevcut BIR DB-model üzerinde](https://www.youtube.com/watch?v=elfqejow5hM) , Alexander SCHMIDT tarafından kullanın
- Telerik Kenov [IBir kimlik ASP.net](https://www.youtube.com/watch?v=w8GD-QIusKk)
- [Çekçe ASP.NET Identity](https://www.youtube.com/watch?v=tVbZp5brcpY) Bu derde temel kimlik doğrulamasının nasıl dağıtılacağını, Twitter veya Facebook gibi dış kimlik sağlayıcıları için nasıl destek ekleneceğini ve tek seferlik parolaların (OTP) nasıl kullanılacağını göstereceğiz. [ASP.NET Identity je nástupce üyelik bir rol sağlayıcısı&#367; v ASP.net, tedy knihovna Pro zajišt&#283;Ní autentizace uživatel&#367;. V této p&#345;ednášce sı ukážeme, jak NASAD]

<a id="cust"></a>

## <a name="custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity için özel depolama sağlayıcıları

Kendi sağlayıcınızı yazmak istiyorsanız, [ASP.NET Identity Için özel depolama sağlayıcılarına genel bakış](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md) ' ı okuyun ve [ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx) ve ardından aşağıda listelenen OSS projelerinden birinin kaynağını inceleyin.

- Öğretici: Tom FitzMacken [ASP.NET Identity Için özel depolama sağlayıcılarına genel bakış](../extensibility/overview-of-custom-storage-providers-for-aspnet-identity.md)
- Blog: [uygulama ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- Öğretici:[temel kimlik hesapları ayarlama ve bunları bir dış veritabanına gösterme](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx). [@xivSolutions](https://twitter.com/xivSolutions).
- Öğretici[: özel bir MySQL ASP.NET Identity depolama sağlayıcısı uygulama](../extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- James Randall tarafından [Azure Tablo Depolaması](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) .
- Azure Tablo Depolama: [@stuartleeks](https://twitter.com/stuartleeks)göre [Aspnet. Identity. TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) .
- [Daniel Wertheım tarafından Couşdb/Cloudant.](https://github.com/danielwertheim/mycouch.aspnet.identity)
- [Elastik arama:](https://github.com/bmbsqd/elastic-identity) Bombsquad AB tarafından elastik kimlik.
- Jonathan Şekondan, şekondan [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) .
- [Nhazırda beklet. Aspnet. Identity](https://github.com/milesibastos/NHibernate.AspNet.Identity) by Antônio Milesi Bastos.
- [@tourismgeek](https://twitter.com/tourismgeek)tarafından [bvendb](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) .
- [Iltedb. Aspnet. Identity](https://github.com/ILMServices/RavenDB.AspNet.Identity) , [ılmservices](http://www.ilmservice.com/).
- Redsıs: [redsıs. Aspnet. Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- "İlk veritabanı" Kullanıcı deposu için EF kodu oluşturmak üzere T4 şablonları: [Aspnet. Identity. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)

<a id="additional"></a>

## <a name="additional-aspnet-identity-resources"></a>Ek ASP.NET Identity kaynakları

- Yahoo ve LinkedIn yönergeleri için Jerrie Pelser tarafından [OWıN Için Yahoo ve LinkedIn OAuth güvenlik sağlayıcılarına giriş](http://blog.beabigrockstar.com/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) .

<a id="qand"></a>

## <a name="qampa-questionanswer"></a>Soru-cevap&amp;

- S: "Beni anımsa" özelliğini etkinleştiren kullanıcılar kilitlendi (Bu nedenle, bu bilgisayarın/tarayıcının üzerinde 2FA 'ya gitmeleri gerekmez) kilitlenmez. Bunun neden ve nasıl önleyebilirim? [Burada](http://stackoverflow.com/questions/24312247/locked-out-users-can-login-if-they-have-auth-cookie)yanıtlayın.
- **S**: her istekte gereksiz veritabanı sorgularını önlemek için, kullanıcının gerçek adı gibi özel talepleri ASP.NET Identity tanımlama bilgisinde nasıl depolayabilirim? [Burada](http://stackoverflow.com/questions/23622047/identity-cookie-loses-custom-claim-information-after-a-period-of-time)yanıtlayın.
- **S: AspNetUser Parola karması güncelleştiriliyor**: 2 projeniz var. Bunlardan biri ASP.NET kimlik doğrulaması kullanıyor, diğeri yönetim tarafı olan Windows kimlik doğrulaması kullanıyor. Yönetici projenin diğer kullanıcılarını yönetebilmesini istiyorum. Parola hariç her şeyi değiştirebiliyorum. [Burada yanıtlayın](http://stackoverflow.com/questions/23880666/updating-aspnetuser-password-hash).
- **S**: parolayı, diğer kullanıcılar için yönetici olarak nasıl sıfırlayabilirim? [Burada](http://stackoverflow.com/questions/23783249/identity-2-0-reset-password-by-admin/24211766#24211766)yanıtlayın.
- **S**: ASP.NET MVC ıdentityuser Içindeki Kullanıcı adı alanının görünen adını değiştirebilir miyim? [Burada](http://stackoverflow.com/questions/23256650/can-i-change-the-displayed-name-of-the-username-field-in-asp-net-mvc-identityuse)yanıtlayın.
- **S**: kullanıcılara belirli rollere başka kullanıcılar ekleme izinleri Gran nasıl yapabilirim? [Burada](http://stackoverflow.com/questions/23695373/allow-users-to-grant-permissions-to-other-users-for-their-account-in-asp-net-ide)yanıtlayın.
- **S**: aspnetusers tablosu ve Aspnetuserclaim tablosu ile profil bilgilerini depolama. [Burada](http://stackoverflow.com/questions/23215727/is-there-any-benefit-to-storing-user-information-in-aspnetuserclaims-with-asp-ne)yanıtlayın.
- **S**: bir dış kimlik doğrulama sağlayıcısı kullanırken beni anımsa. [Burada](http://stackoverflow.com/questions/23180896/how-to-remember-the-login-in-mvc5-when-an-external-provider-is-used)yanıtlayın.
- **S**: her istek neden bir ApplicationDBContext gerektiriyor, çok fazla yük mi var?. Yanıt, Hayır, ek yük düşüktür.
- S: oturum açmış kullanıcıların listesini almak Nasıl yaparım? mı? [Burada](http://stackoverflow.com/questions/22995653/getting-a-list-of-logged-in-users-in-asp-net-identity/)yanıtlayın.
- S: bir kullanıcının Microsoft. AspNet. Identity ile oturum açtığı zaman nasıl belirleyebilirim? [Burada](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)yanıtlayın.
- S: Nasıl yaparım? kimlik için yerelleştirilmiş hata iletileri al? [Burada](http://stackoverflow.com/questions/22835981/asp-net-identity-localization-publickeytoken/22845864#22845864)yanıtlayın.
- S: her 30 dakikada bir yeni talepler almak için tanıtım ıeara yazılımını yapılandırmak Nasıl yaparım? mı? [Burada](http://stackoverflow.com/questions/22682663/how-to-hold-the-cookies-claims-updated-with-mcv5-owin/22796932#22796932)yanıtlayın.
- S: oturum açtıktan sonra Kullanıcı için talepler nasıl değiştirilir? [Burada](http://stackoverflow.com/questions/22768836/can-i-modify-claims-in-asp-net-identity-with-owin-after-calling-signin/22769963#22769963)yanıtlayın.
- S: Nasıl yaparım? güvenlik belirteçlerini geçersiz kılar? [Burada](http://stackoverflow.com/questions/22755700/revoke-token-generated-by-usertokenprovider-in-asp-net-identity-2-0/22767286#22767286)yanıtlayın.
- S: tanımlama bilgisi ara ortamında talepler nasıl depolanır? [Burada](http://stackoverflow.com/questions/22320632/storing-retrieving-user-data-without-database-when-using-owin-cookie-authenticat/22541856#22541856)yanıtlayın.
- S: MVC uygulamamda her bir eylem yönteminde PIN veya güvenlik denetimi yapmak istiyorum, ancak bu eylem yöntemine yapılan her istekte PIN 'ı girmeye gerek kalmayacak şekilde Kullanıcı başarısını depolamak istiyorum. [Burada](http://stackoverflow.com/questions/22479958/security-check-an-user-to-a-access-controller-action/22486075#22486075)yanıtlayın.
- S: bir sosyal sağlayıcıdan döndürülen e-posta adresini VERITABANıNA kaydetmek istiyorum, bunu nasıl yapabilirim? [Burada](http://stackoverflow.com/questions/22888397/save-claims-to-db-on-login/22970969#22970969)yanıtlayın:
- S: bir kullanıcının her ikisinde de bir "Beni anımsa" tanımlama bilgisi ile oturum açarken nasıl tespit edebilirim? [Burada](http://stackoverflow.com/questions/22956486/how-can-i-detect-when-a-user-logs-in-with-microsoft-aspnet-identity/22970698#22970698)yanıtlayın.
- S: oturum açma yöntemini çağırdıktan sonra OWıN ile ASP.NET Identity taleplerini değiştirebilir miyim? Cevap: oturum açma çağrısı, kullanıcının taleplerini değiştirmek istediğinizde tam olarak yapmanız gereken şeydir. Bu, temel olarak ClaimsIdentity 'nin tanımlama bilgisine serileştirilmesine neden olur. bu nedenle, yeni talepler sonraki isteklerde gösterilmektedir.
