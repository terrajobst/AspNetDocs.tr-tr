---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: ASP.NET Identity-ASP.NET 4. x içindeki kullanıcılar için birincil anahtarı değiştirme
author: Rick-Anderson
description: Visual Studio 2013, varsayılan Web uygulaması, Kullanıcı hesapları için anahtar için bir dize değeri kullanır. ASP.NET Identity, türünü değiştirmenizi sağlar...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584464"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a>ASP.NET Identity’de Kullanıcılar için Birincil Anahtarı Değiştirme

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> Visual Studio 2013, varsayılan Web uygulaması, Kullanıcı hesapları için anahtar için bir dize değeri kullanır. ASP.NET Identity, anahtar türünü veri gereksinimlerinizi karşılayacak şekilde değiştirmenizi sağlar. Örneğin, anahtarın türünü bir dizeden tamsayı olarak değiştirebilirsiniz.
> 
> Bu konu başlığı altında, varsayılan Web uygulamasıyla nasıl başlayacağı ve Kullanıcı hesabı anahtarı bir tamsayı olarak nasıl değiştirileceği gösterilmektedir. Projenizdeki herhangi bir anahtar türünü uygulamak için aynı değişiklikleri kullanabilirsiniz. Varsayılan Web uygulamasında bu değişikliklerin nasıl yapılacağını gösterir, ancak özelleştirilmiş bir uygulamaya benzer değişiklikler uygulayabilirsiniz. MVC veya Web Forms çalışırken gereken değişiklikleri gösterir.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Güncelleştirme 2 ile Visual Studio 2013 (veya üzeri)
> - ASP.NET Identity 2,1 veya üzeri

Bu öğreticideki adımları gerçekleştirmek için, ASP.NET Web uygulaması şablonundan oluşturulmuş Visual Studio 2013 güncelleştirme 2 (veya üzeri) ve bir Web uygulaması olması gerekir. Şablon güncelleştirme 3 ' te değiştirildi. Bu konuda güncelleştirme 2 ve güncelleştirme 3 ' te şablonun nasıl değiştirileceği gösterilmektedir.

Bu konu aşağıdaki bölümleri içermektedir:

- [Identity User sınıfında anahtar türünü değiştirin](#userclass)
- [Anahtar türünü kullanan özelleştirilmiş kimlik sınıfları ekleyin](#customclass)
- [Anahtar türünü kullanmak için bağlam sınıfını ve Kullanıcı yöneticisini değiştirme](#context)
- [Anahtar türünü kullanmak için başlangıç yapılandırmasını değiştirme](#startup)
- [Güncelleştirme 2 ile MVC için, AccountController 'ı anahtar türünü geçirecek şekilde değiştirin](#mvcupdate2)
- [Güncelleştirme 3 ile MVC için AccountController ve ManageController değerlerini anahtar türünü geçirecek şekilde değiştirin](#mvcupdate3)
- [Güncelleştirme 2 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin](#webformsupdate2)
- [Güncelleştirme 3 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin](#webformsupdate3)
- [Uygulamayı çalıştır](#run)
- [Diğer kaynaklar](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a>Identity User sınıfında anahtar türünü değiştirin

ASP.NET Web uygulaması şablonundan oluşturulan projenizde, ApplicationUser sınıfının Kullanıcı hesapları için anahtar için bir tamsayı kullandığını belirtin. IdentityModels.cs içinde, ApplicationUser sınıfını TKey genel parametresi için bir **int** türüne sahip ıdentityuser öğesinden devralacak şekilde değiştirin. Henüz uygulamamış olduğunuz üç özelleştirilmiş sınıfın adlarını da geçitirsiniz.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

Anahtarın türünü değiştirdiniz, ancak varsayılan olarak uygulamanın geri kalanı anahtarın bir dize olduğunu varsaymaktadır. Bir dizeyi kabul eden koddaki anahtarın türünü açıkça belirtmeniz gerekir.

**ApplicationUser** sınıfında, aşağıdaki vurgulanan kodda gösterildiği gibi **Generateuserıdentityasync** yöntemini int öğesini içerecek şekilde değiştirin. Bu değişiklik, güncelleştirme 3 şablonuyla Web Forms projeler için gerekli değildir.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a>Anahtar türünü kullanan özelleştirilmiş kimlik sınıfları ekleyin

Identityuserrole, ıdentityuserclaim, ıdentityuserlogin, ıdentityrole, UserStore, RoleStore gibi diğer kimlik sınıfları yine de bir dize anahtarı kullanacak şekilde ayarlanmıştır. Bu sınıfların anahtar için bir tamsayı belirten yeni sürümlerini oluşturun. Bu sınıflarda çok fazla uygulama kodu sağlamanız gerekmez, birincil olarak yalnızca int 'i anahtar olarak ayarlamasınız.

Aşağıdaki sınıfları IdentityModels.cs dosyanıza ekleyin.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a>Anahtar türünü kullanmak için bağlam sınıfını ve Kullanıcı yöneticisini değiştirme

IdentityModels.cs içinde, **Applicationdbcontext** sınıfının tanımını, vurgulanan kodda gösterildiği gibi, yeni özelleştirilmiş sınıflarınızı ve anahtar için bir **int** kullanmak üzere değiştirin.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

ThrowIfV1Schema parametresi artık oluşturucuda geçerli değil. Oluşturucuyu bir ThrowIfV1Schema değeri geçirmemesi için değiştirin.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

IdentityConfig.cs 'i açın ve **Applicationusermanager** sınıfını kalıcı veriler için Yeni Kullanıcı Mağazası sınıfınızı ve anahtar için bir **int** kullanın.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

Güncelleştirme 3 şablonunda, Applicationsignınmanager sınıfını değiştirmeniz gerekir.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a>Anahtar türünü kullanmak için başlangıç yapılandırmasını değiştirme

Startup.Auth.cs ' de, Onvalidateıdentity kodunu aşağıda vurgulanan şekilde değiştirin. Getuserıdcallback tanımının dize değerini bir tamsayı olarak ayrıştırır olduğuna dikkat edin.

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

Projeniz **GetUserID** yönteminin genel uygulamasını tanımıyorsa, ASP.NET Identity NuGet paketini 2,1 sürümüne güncelleştirmeniz gerekebilir

ASP.NET Identity tarafından kullanılan altyapı sınıflarında çok sayıda değişiklik yaptınız. Projeyi derlemeyi denerseniz, çok sayıda hata olduğunu fark edeceksiniz. Neyse ki, kalan hataların hepsi benzerdir. Identity sınıfı anahtar için bir tamsayı bekliyor, ancak denetleyici (veya Web formu) bir dize değeri geçiriyoruyor. Her durumda **GetUserID&lt;int&gt;** çağırarak bir dizeden ve tamsayıya dönüştürmeniz gerekir. Derlemeden hata listesinden çalışabilirsiniz veya aşağıdaki değişiklikleri izleyebilirsiniz.

Kalan değişiklikler oluşturmakta olduğunuz proje türüne ve Visual Studio 'da hangi güncelleştirmeyi yüklediğinize bağlıdır. Aşağıdaki bağlantılar aracılığıyla doğrudan ilgili bölüme gidebilirsiniz

- [Güncelleştirme 2 ile MVC için, AccountController 'ı anahtar türünü geçirecek şekilde değiştirin](#mvcupdate2)
- [Güncelleştirme 3 ile MVC için AccountController ve ManageController değerlerini anahtar türünü geçirecek şekilde değiştirin](#mvcupdate3)
- [Güncelleştirme 2 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin](#webformsupdate2)
- [Güncelleştirme 3 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a>Güncelleştirme 2 ile MVC için, AccountController 'ı anahtar türünü geçirecek şekilde değiştirin

AccountController.cs dosyasını açın. Aşağıdaki yöntemleri değiştirmeniz gerekir.

**ConfirmEmail** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

**Ilişkiyi kaldırma** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

**Manage (ManageUserViewModel)** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

**Linklogincallback** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

**Removeaccountlist** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

**HasPassword** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

Şimdi [uygulamayı çalıştırabilir](#run) ve yeni bir kullanıcı kaydedebilirsiniz.

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a>Güncelleştirme 3 ile MVC için AccountController ve ManageController değerlerini anahtar türünü geçirecek şekilde değiştirin

AccountController.cs dosyasını açın. Aşağıdaki yöntemi değiştirmeniz gerekir.

**ConfirmEmail** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

**Sendcode** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

ManageController.cs dosyasını açın. Aşağıdaki yöntemleri değiştirmeniz gerekir.

**Index** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

**RemoveLogin** yöntemleri

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

**Addphonenumber** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

**Enabletwofactorayuthentication** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

**Disabletwofactorayuthentication** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

**Doğrulamaları Yphonenumber** yöntemleri

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

**Removephonenumber** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

**ChangePassword** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

**SetPassword** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

**ManageLogins** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

**Linklogincallback** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

**HasPassword** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

**Hasphonenumber** yöntemi

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

Şimdi [uygulamayı çalıştırabilir](#run) ve yeni bir kullanıcı kaydedebilirsiniz.

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a>Güncelleştirme 2 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin

Güncelleştirme 2 ile Web Forms için aşağıdaki sayfaları değiştirmeniz gerekir.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

Şimdi [uygulamayı çalıştırabilir](#run) ve yeni bir kullanıcı kaydedebilirsiniz.

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a>Güncelleştirme 3 ile Web Forms için, hesap sayfalarını anahtar türünü geçirecek şekilde değiştirin

Güncelleştirme 3 ile Web Forms için aşağıdaki sayfaları değiştirmeniz gerekir.

**Confirm.aspx.cx**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

**RegisterExternalLogin.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

**Manage.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

**VerifyPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

**AddPhoneNumber.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

**ManagePassword.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

**ManageLogins.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

**TwoFactorAuthenticationSignIn.aspx.cs**

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a>Uygulamayı çalıştır

Varsayılan Web uygulaması şablonunda gerekli tüm değişiklikleri tamamladınız. Uygulamayı çalıştırın ve yeni bir Kullanıcı kaydedin. Kullanıcı kaydedildikten sonra, AspNetUsers tablosunda tamsayı olan bir kimlik sütunu olduğunu fark edeceksiniz.

![Yeni birincil anahtar](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

Daha önce farklı bir birincil anahtarla ASP.NET Identity tabloları oluşturduysanız, bazı ek değişiklikler yapmanız gerekir. Mümkünse, var olan veritabanını silmeniz yeterlidir. Web uygulamasını çalıştırdığınızda ve yeni bir kullanıcı eklediğinizde, veritabanı doğru tasarımla yeniden oluşturulur. Silme mümkün değilse, tabloları değiştirmek için önce kod geçişlerini çalıştırın. Ancak, yeni tamsayı birincil anahtarı veritabanında bir SQL ıDENTITY özelliği olarak ayarlanmayacak. Kimlik sütununu KIMLIK olarak el ile ayarlamanız gerekir.

<a id="other"></a>
## <a name="other-resources"></a>Diğer kaynaklar

- [ASP.NET Identity için Özel Depolama Sağlayıcılarına Genel Bakış](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [Mevcut Bir Web Sitesini SQL Üyeliğinden ASP.NET Identity’ye Geçirme](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [Üyelik ve Kullanıcı profillerinin evrensel sağlayıcı verilerini ASP.NET Identity 'ye geçirme](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- Değiştirilen birincil anahtarla [örnek uygulama](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK)
