---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: ASP.NET Identity-ASP.NET 4. x için özel depolama sağlayıcılarına genel bakış
author: Rick-Anderson
description: ASP.NET Identity, kendi depolama sağlayıcınızı oluşturmanızı ve appli 'ı yeniden çalıştırmadan uygulamanıza eklemenizi sağlayan genişletilebilir bir sistemdir...
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 21baedf6285b411f89627df9ca25d47a2a42e387
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584415"
---
# <a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>ASP.NET Identity için Özel Depolama Sağlayıcılarına Genel Bakış

[Tom FitzMacken](https://github.com/tfitzmac) tarafından

> ASP.NET Identity, kendi depolama sağlayıcınızı oluşturmanızı ve uygulamayı yeniden çalıştırmadan uygulamanıza takmanızı sağlayan genişletilebilir bir sistemdir. Bu konuda, ASP.NET Identity için özelleştirilmiş bir depolama sağlayıcısının nasıl oluşturulacağı açıklanmaktadır. Kendi depolama sağlayıcınızı oluşturmaya yönelik önemli kavramlar ele alınmaktadır, ancak özel bir depolama sağlayıcısı uygulamaya yönelik adım adım yönergeler değildir.
> 
> Özel bir depolama sağlayıcısı uygulama örneği için bkz. [özel bir MySQL ASP.NET Identity depolama sağlayıcısı uygulama](implementing-a-custom-mysql-aspnet-identity-storage-provider.md).
> 
> Bu konu ASP.NET Identity 2,0 için güncelleştirildi.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Öğreticide kullanılan yazılım sürümleri
> 
> 
> - Güncelleştirme 2 ile Visual Studio 2013
> - ASP.NET Identity 2

## <a name="introduction"></a>Giriş

Varsayılan olarak, ASP.NET Identity sistem kullanıcı bilgilerini bir SQL Server veritabanında depolar ve veritabanını oluşturmak için Entity Framework Code First kullanır. Birçok uygulama için bu yaklaşım iyi bir sonuç verir. Ancak, Azure Tablo depolaması gibi farklı bir Kalıcılık mekanizması türü kullanmayı tercih edebilir veya varsayılan uygulamadan çok farklı bir yapıya sahip olan veritabanı tablolarına sahip olabilirsiniz. Her iki durumda da, depolama mekanizmanız için özelleştirilmiş bir sağlayıcı yazabilir ve bu sağlayıcıyı uygulamanıza ekleyebilirsiniz.

ASP.NET Identity, Visual Studio 2013 şablonlarının çoğunda varsayılan olarak dahil edilir. ASP.NET Identity güncelleştirmelerini [Microsoft ASPNET Identity EntityFramework NuGet paketi](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/)ile edinebilirsiniz.

Bu konu aşağıdaki bölümleri içermektedir:

- [Mimariyi anlayın](#architecture)
- [Depolanan verileri anlayın](#data)
- [Veri erişim katmanını oluşturma](#dal)
- [Kullanıcı sınıfını özelleştirme](#user)
- [Kullanıcı deposunu özelleştirme](#userstore)
- [Rol sınıfını özelleştirme](#role)
- [Rol deposunu özelleştirme](#rolestore)
- [Yeni depolama sağlayıcısını kullanmak için uygulamayı yeniden yapılandırın](#reconfigure)
- [Özel depolama sağlayıcılarının diğer uygulamaları](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>Mimariyi anlayın

ASP.NET Identity, Yöneticiler ve depolar adlı sınıflardan oluşur. Yöneticiler, uygulama geliştiricisinin ASP.NET Identity sisteminde Kullanıcı oluşturma gibi işlemleri gerçekleştirmek için kullandığı üst düzey sınıflardır. Depolar, kullanıcılar ve roller gibi varlıkların nasıl kalıcı olduğunu belirten alt düzey sınıflardır. Depolar, kalıcılık mekanizmasıyla yakından ilişkilidir, ancak yöneticiler mağazalardan ayrılır, bu da tüm uygulamayı kesintiye uğratmadan Kalıcılık mekanizmasını değiştirebilirsiniz.

Aşağıdaki diyagramda Web uygulamanızın yöneticileriyle nasıl etkileşim kurduğu ve veri erişim katmanıyla etkileşim kuran bir şekilde nasıl depolandığı gösterilmektedir.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

ASP.NET Identity için özelleştirilmiş bir depolama sağlayıcısı oluşturmak için veri kaynağını, veri erişim katmanını ve bu veri erişim katmanıyla etkileşime geçen mağaza sınıflarını oluşturmanız gerekir. Kullanıcı üzerinde veri işlemleri gerçekleştirmek için aynı yönetici API 'Lerini kullanmaya devam edebilirsiniz, ancak artık veriler farklı bir depolama sistemine kaydedilir.

UserManager 'ın veya RoleManager 'ın yeni bir örneğini oluştururken Kullanıcı sınıfının türünü sağladığınızda ve depo sınıfının bir örneğini bağımsız değişken olarak geçirdiğinizde, yönetici sınıflarını özelleştirmeniz gerekmez. Bu yaklaşım özelleştirilmiş sınıflarınızı var olan yapıya eklemenize olanak sağlar. [Yeni depolama sağlayıcısını kullanmak için uygulamayı yeniden yapılandırma](#reconfigure)bölümünde özelleştirilmiş mağaza sınıflarınız Ile UserManager ve roleManager örneğini oluşturmayı öğreneceksiniz.

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>Depolanan verileri anlayın

Özel bir depolama sağlayıcısı uygulamak için, ASP.NET Identity ile kullanılan veri türlerini anlamanız ve uygulamanızla ilgili olan özelliklerin hangisi olduğuna karar vermelisiniz.

| Veri | Açıklama |
| --- | --- |
| Kullanıcılar | Web sitenizin kayıtlı kullanıcıları. Kullanıcı kimliğini ve Kullanıcı adını içerir. Kullanıcılar, sitenize özgü kimlik bilgileriyle oturum açıp (Facebook gibi bir dış siteden kimlik bilgilerini kullanmak yerine) ve Kullanıcı kimlik bilgilerinde herhangi bir şeyin değişip değişmediğini belirtmek için güvenlik damgasına sahip olabileceği karma bir parola içerebilir. Ayrıca, e-posta adresi, telefon numarası, iki öğeli kimlik doğrulamasının etkin olup olmadığını, geçerli başarısız oturum açma sayısını ve bir hesabın kilitlenip kilitlenmediğini de içerebilir. |
| Kullanıcı Talepleri | Kullanıcının kimliğini temsil eden kullanıcı hakkındaki deyimler (veya talepler) kümesi. Kullanıcı kimliğinin, roller aracılığıyla elde edilebileceğinden daha fazla ifadesini etkinleştirebilir. |
| Kullanıcı oturumu açma | Bir kullanıcıya oturum açarken kullanılacak dış kimlik doğrulama sağlayıcısı (Facebook gibi) hakkında bilgiler. |
| Roller | Sitenizin yetkilendirme grupları. Rol kimliği ve rol adı ("admin" veya "Employee" gibi) içerir. |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>Veri erişim katmanını oluşturma

Bu konuda, kullanacağınız Kalıcılık mekanizması hakkında bilgi sahibi olduğunuz ve bu mekanizma için nasıl varlık oluşturacağınız varsayılmaktadır. Bu konu, depoları veya veri erişim sınıflarını oluşturma hakkında ayrıntılı bilgi sağlamaz; Bunun yerine, ASP.NET Identity çalışırken yapmanız gereken tasarım kararları hakkında bazı öneriler sağlar.

Özelleştirilmiş bir mağaza sağlayıcısı için depoları tasarlarken çok fazla özgürlük vardır. Yalnızca uygulamanızda kullanmayı düşündüğünüz özellikler için depolar oluşturmanız yeterlidir. Örneğin, uygulamanızda roller kullanmıyorsanız, roller veya Kullanıcı rolleri için depolama oluşturmanız gerekmez. Teknolojiniz ve mevcut altyapınız, ASP.NET Identity varsayılan uygulamasından çok farklı bir yapı gerektirebilir. Veri erişim katmanında, havuzlarınızın yapısıyla çalışma mantığını sağlarsınız.

ASP.NET Identity 2,0 için veri depolarının MySQL uygulamasında, bkz. [Mysqlidentity. SQL](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql).

Veri erişim katmanında verileri ASP.NET Identity veri kaynağınıza kaydetme mantığını sağlarsınız. Özelleştirilmiş depolama sağlayıcınızla ilgili veri erişim katmanı, Kullanıcı ve rol bilgilerini depolamak için aşağıdaki sınıfları içerebilir.

| örneği | Açıklama | Örnek |
| --- | --- | --- |
| Bağlam | Kalıcılık mekanizmanıza bağlanmak ve sorguları yürütmek için bilgileri kapsüller. Bu sınıf, veri erişim katmanınıza yönelik bir merkezidir. Diğer veri sınıfları, işlemlerini gerçekleştirmek için bu sınıfın bir örneğini gerektirir. Mağaza sınıflarınızı bu sınıfın bir örneği ile de başlatacaksınız. | [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| Kullanıcı depolaması | Kullanıcı bilgilerini depolar ve alır (Kullanıcı adı ve parola karması gibi). | [UserTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| Rol depolama | Rol bilgilerini depolar ve alır (rol adı gibi). | [RoleTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| Userclaim depolaması | Kullanıcı talep bilgilerini depolar ve alır (talep türü ve değeri gibi). | [UserClaimsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| UserLogins depolaması | Kullanıcı oturum açma bilgilerini depolar ve alır (örneğin, bir dış kimlik doğrulama sağlayıcısı). | [UserLoginsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| UserRole depolaması | Bir kullanıcının hangi rollere atandığını depolar ve alır. | [UserRoleTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

Yine de, uygulamanızda kullanmayı düşündüğünüz sınıfları uygulamanız gerekir.

Veri erişim sınıflarında, belirli bir kalıcılık mekanizmanız için veri işlemlerini gerçekleştirmek üzere kod sağlarsınız. Örneğin, MySQL uygulamasının içinde UserTable sınıfı, kullanıcılar veritabanı tablosuna yeni bir kayıt eklemek için bir yöntem içerir. `_database` adlı değişken, MySQLDatabase sınıfının bir örneğidir.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

Veri erişim sınıflarınızı oluşturduktan sonra, veri erişim katmanındaki belirli yöntemleri çağıran mağaza sınıfları oluşturmanız gerekir.

<a id="user"></a>
## <a name="customize-the-user-class"></a>Kullanıcı sınıfını özelleştirme

Kendi depolama sağlayıcınızı uygularken, [Microsoft. asp. net. Identity. EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) ad alanındaki [ıdentityuser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx) sınıfına eşdeğer bir Kullanıcı sınıfı oluşturmanız gerekir:

Aşağıdaki diyagramda, oluşturmanız gereken ıdentityuser sınıfı ve bu sınıfta uygulanacak arabirim gösterilmektedir.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

[IUser&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) arabirimi, UserManager 'ın istenen işlemleri gerçekleştirirken çağrı yapmaya çalıştığı özellikleri tanımlar. Arabirim iki özellik içerir-kimlik ve Kullanıcı adı. [Iuser&lt;tkey&gt;](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) arabirimi, genel **TKey** parametresi aracılığıyla Kullanıcı için anahtar türünü belirtmenizi sağlar. ID özelliğinin türü, TKey parametresinin değeriyle eşleşir.

Kimlik çerçevesi, anahtar için bir dize değeri kullanmak istediğinizde, [IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx) arabirimini de (genel parametre olmadan) sağlar.

Identityuser sınıfı, IUser 'ı uygular ve Web sitenizdeki kullanıcılar için ek özellikler ya da oluşturucular içerir. Aşağıdaki örnek, anahtar için bir tamsayı kullanan bir ıdentityuser sınıfını gösterir. ID alanı, genel parametresinin değeriyle eşleşecek şekilde **int** olarak ayarlanır. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 Tüm uygulama için bkz. [ıdentityuser (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs). 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>Kullanıcı deposunu özelleştirme

Ayrıca, kullanıcının tüm veri işlemleri için yöntemler sağlayan bir UserStore sınıfı da oluşturursunuz. Bu sınıf, [Microsoft. asp. net. Identity. EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) ad alanındaki [userStore&lt;Tuser&gt;](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx) sınıfına eşdeğerdir. UserStore sınıfınıza [ıuserstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) ve isteğe bağlı arabirimlerden herhangi birini uygulayacağınızı uygulatyorsunuzdur. Uygulamanızda sağlamak istediğiniz işlevselliğe göre hangi isteğe bağlı arabirimlerin uygulanacağını seçersiniz.

Aşağıdaki görüntüde, oluşturmanız gereken UserStore sınıfı ve ilgili arabirimler gösterilmektedir.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

Visual Studio 'daki varsayılan proje şablonu, isteğe bağlı arabirimlerin çoğunun Kullanıcı deposunda uygulandığını varsayan kodu içerir. Varsayılan şablonu özelleştirilmiş bir kullanıcı deposu ile kullanıyorsanız, Kullanıcı deponuzda isteğe bağlı arabirimler uygulamanız veya uygulanmayan arabirimlerde yöntemi artık çağırmak için şablon kodunu değiştirmeniz gerekir.

 Aşağıdaki örnek bir basit kullanıcı deposu sınıfını göstermektedir. **Tuser** genel parametresi, genellikle tanımladığınız ıdentityuser sınıfı olan Kullanıcı sınıfınızın türünü alır. **TKey** genel parametresi, Kullanıcı anahtarınızın türünü alır. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 Bu örnekte, ExampleDatabase türünde *Database* adlı bir parametre alan Oluşturucu yalnızca veri erişim sınıfınıza nasıl geçilereceğine ilişkin bir örnektir. Örneğin, MySQL uygulamasında, bu Oluşturucu MySQLDatabase türünde bir parametre alır. 

UserStore sınıfınız içinde, işlemleri gerçekleştirmek için oluşturduğunuz veri erişim sınıflarını kullanırsınız. Örneğin, MySQL uygulamasında, UserStore sınıfının yeni bir kayıt eklemek için UserTable örneğini kullanan CreateAsync yöntemi vardır. **Usertable** nesnesindeki **Insert** yöntemi, önceki bölümde gösterilen yöntem ile aynıdır. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>Kullanıcı deposunu özelleştirirken uygulanacak arabirimler

Sonraki görüntüde, her arabirimde tanımlanan işlevlerle ilgili daha fazla ayrıntı gösterilmektedir. Tüm isteğe bağlı arabirimler ıuserstore 'dan devralınır.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **Iuserstore**  
  [Iuserstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx) arabirimi, Kullanıcı deponuzda uygulamanız gereken tek arabirimdir. Kullanıcıları oluşturma, güncelleştirme, silme ve alma yöntemlerini tanımlar.
- **Iuserclaimstore**  
  [Iuserclaimstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx) arabirimi Kullanıcı taleplerini etkinleştirmek için Kullanıcı deponuzda uygulamanız gereken yöntemleri tanımlar. Yöntemler içerir veya Kullanıcı taleplerini ekleme, kaldırma ve alma.
- **Iuserloginstore**  
  [Iuserloginstore&lt;TUser, TKey&gt;,](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx) dış kimlik doğrulama sağlayıcılarını etkinleştirmek için Kullanıcı deponuzda uygulamanız gereken yöntemleri tanımlar. Kullanıcı oturum açma bilgilerini ekleme, kaldırma ve alma ve oturum açma bilgilerine göre Kullanıcı alma yöntemi gibi yöntemleri içerir.
- **Iuserrolestore**  
  [Iuserrolestore&lt;TKey, tuser&gt;arabirimi,](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) bir kullanıcıyı bir rolle eşlemek için Kullanıcı deponuzda uygulamanız gereken yöntemleri tanımlar. Bir kullanıcının rollerini ekleme, kaldırma ve alma yöntemlerini ve bir rolün bir rolün atanıp atanmadığını denetlemek için bir yöntem içerir.
- **Iuserpasswordstore**  
  [Iuserpasswordstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx) arabirimi, Karma parolaları kalıcı hale getirmek için Kullanıcı deponuzda uygulamanız gereken yöntemleri tanımlar. Karma parolanın alınması ve ayarlanması için yöntemler ve kullanıcının bir parola ayarlayıp ayarlamadığını belirten bir yöntem içerir.
- **Iusersecuritystampstore**  
  [Iusersecuritystampstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx) arabirimi kullanıcının hesap bilgilerinin değişip değişmediğini belirten bir güvenlik damgası kullanmak için Kullanıcı deponuzda uygulamanız gereken yöntemleri tanımlar. Bu damga, Kullanıcı parolayı değiştirdiğinde veya oturum açma ekler veya kaldırdığında güncelleştirilir. Güvenlik damgasını alma ve ayarlama yöntemlerini içerir.
- **Iusertwofactorstore**  
  [Iusertwofactorstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx) arabirimi iki öğeli kimlik doğrulaması uygulamak için uygulamanız gereken yöntemleri tanımlar. Bir kullanıcı için iki öğeli kimlik doğrulamasının etkin olup olmadığını alma ve ayarlama yöntemlerini içerir.
- **Iuserphonenumberstore**  
  [Iuserphonenumberstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx) arabirimi, Kullanıcı telefon numaralarını depolamak için uygulamanız gereken yöntemleri tanımlar. Telefon numarasını alma ve ayarlama ve telefon numarasının onaylanıp onaylanmayacağı yöntemlerini içerir.
- **Iuseremailstore**  
  [Iuseremailstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx) arabirimi, kullanıcı e-posta adreslerini depolamak için uygulamanız gereken yöntemleri tanımlar. E-posta adresini alma ve ayarlama yöntemlerini ve e-postanın onaylanıp onaylanmadığını içerir.
- **Iuserlockoutstore**  
  [Iuserlockoutstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx) arabirimi, bir hesabı kilitleme hakkındaki bilgileri depolamak için uygulamanız gereken yöntemleri tanımlar. Bu, başarısız olan erişim girişimlerinin geçerli sayısını alma, hesabın kilitlenip kilitlenmeyeceğini alma, bitiş tarihini alma ve ayarlama, başarısız girişim sayısını artırma ve başarısız girişim sayısını sıfırlama yöntemlerini içerir.
- **Iqueryableuserstore**  
  [Iqueryableuserstore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx) arabirimi, bir sorgulanabilir kullanıcı deposu sağlamak için uygulamanız gereken üyeleri tanımlar. Bu, sorgulanabilir kullanıcıları tutan bir özelliği içerir.

  Uygulamanızda gerekli olan arabirimleri uygulamanız gerekir; Örneğin, ıuserclaimstore, ıuserloginstore, ıuserrolestore, ıuserpasswordstore ve ıusersecuritystampstore arabirimleri aşağıda gösterildiği gibi. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

Tüm uygulama için (tüm arabirimler dahil), bkz. [userStore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs).

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>Identityuserclaim, ıdentityuserlogin ve ıdentityuserrole

Microsoft. AspNet. Identity. EntityFramework ad alanı [ıdentityuserclaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx), [ıdentityuserlogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx)ve [ıdentityuserrole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx) sınıflarının uygulamalarını içerir. Bu özellikleri kullanıyorsanız, bu sınıfların kendi sürümlerinizi oluşturmak ve uygulamanız için özellikleri tanımlamak isteyebilirsiniz. Ancak bazen, temel işlemleri gerçekleştirirken bu varlıkların belleğe yüklenmemesinin (örneğin, bir kullanıcının talebini ekleme veya kaldırma) daha etkilidir. Bunun yerine, arka uç deposu sınıfları bu işlemleri doğrudan veri kaynağında yürütebilir. Örneğin, UserStore. GetClaimsAsync () yöntemi userClaimTable. Findbyuserıd (User) yöntemini çağırabilir. ID) yöntemi doğrudan bu tabloda bir sorgu yürütmek ve talepler listesini döndürmek için yöntem.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>Rol sınıfını özelleştirme

Kendi depolama sağlayıcınızı uygularken, [Microsoft. asp. net. Identity. EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) ad alanındaki [ıdentityrole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx) sınıfına eşdeğer bir rol sınıfı oluşturmanız gerekir:

Aşağıdaki diyagramda, oluşturmanız gereken ıdentityrole sınıfı ve bu sınıfta uygulanacak arabirim gösterilmektedir.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

[Irole&lt;TKey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) arabirimi, roleManager 'ın istenen işlemleri gerçekleştirirken çağrı yapmaya çalıştığı özellikleri tanımlar. Arabirim iki özellik kimliği ve adı içerir. [Irole&lt;tkey&gt;](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) arabirimi, genel **TKey** parametresi aracılığıyla rolün anahtar türünü belirtmenizi sağlar. ID özelliğinin türü, TKey parametresinin değeriyle eşleşir.

Kimlik çerçevesi, anahtar için bir dize değeri kullanmak istediğinizde [ırole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx) arabirimini de (genel parametre olmadan) sağlar.

Aşağıdaki örnek, anahtar için bir tamsayı kullanan bir ıdentityrole sınıfını gösterir. ID alanı, genel parametresinin değeriyle eşleşecek şekilde int olarak ayarlanır. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 Tüm uygulama için bkz. [ıdentityrole (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs). 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>Rol deposunu özelleştirme

Ayrıca, rollerdeki tüm veri işlemlerine yönelik yöntemleri sağlayan bir RoleStore sınıfı oluşturursunuz. Bu sınıf, Microsoft. ASP. NET. Identity. EntityFramework ad alanındaki [Rolestore&lt;TRole&gt;](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx) sınıfına eşdeğerdir. RoleStore sınıfınıza [ırolestore&lt;TRole, tkey&gt;](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx) ve isteğe bağlı olarak [ıqueryablerolestore&lt;trole, TKey&gt;](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx) arabirimini uygulaırsınız.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

Aşağıdaki örnekte bir rol deposu sınıfı gösterilmektedir. TRole genel parametresi, genellikle tanımladığınız ıdentityrole sınıfı olan rol sınıfınızın türünü alır. TKey genel parametresi, rol anahtarınızın türünü alır. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **Irolestore&lt;TRole&gt;**  
  [Irolestore](https://msdn.microsoft.com/library/dn468195.aspx) arabirimi, rol deposu sınıfınıza uygulanacak yöntemleri tanımlar. Rol oluşturma, güncelleştirme, silme ve alma yöntemlerini içerir.
- **RoleStore&lt;TRole&gt;**  
  RoleStore 'u özelleştirmek için, ırolestore arabirimini uygulayan bir sınıf oluşturun. Bu sınıfı yalnızca, sisteminizde roller kullanmak istiyorsanız uygulamanız gerekir. ExampleDatabase türünde *Database* adlı bir parametre alan Oluşturucu yalnızca veri erişim sınıfınıza nasıl geçilereceğine ilişkin bir örnekdir. Örneğin, MySQL uygulamasında, bu Oluşturucu MySQLDatabase türünde bir parametre alır.  
  
  Tüm uygulama için bkz. [Rolestore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) .

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>Yeni depolama sağlayıcısını kullanmak için uygulamayı yeniden yapılandırın

Yeni depolama sağlayıcınızı uyguladık. Şimdi, uygulamanızı bu depolama sağlayıcısını kullanacak şekilde yapılandırmanız gerekir. Varsayılan depolama sağlayıcısı projenize dahil edilmiştir, varsayılan sağlayıcıyı kaldırmalı ve sağlayıcınızla değiştirmelisiniz.

### <a name="replace-default-storage-provider-in-mvc-project"></a>MVC projesinde varsayılan depolama sağlayıcısını değiştirme

1. **NuGet Paketlerini Yönet** penceresinde **Microsoft ASP.NET Identity EntityFramework** paketini kaldırın. Bu paketi, Identity. EntityFramework yüklü paketlerinde arayarak bulabilirsiniz.  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png), Entity Framework kaldırmak isteyip istemediğiniz sorulur. Uygulamanızın diğer bölümlerinde gerekmiyorsa, bunu kaldırabilirsiniz.
2. Modeller klasöründeki IdentityModels.cs dosyasında, **ApplicationUser** ve **applicationdbcontext** sınıflarını silin veya not edin. MVC uygulamasında tüm IdentityModels.cs dosyasını silebilirsiniz. Web Forms bir uygulamada, iki sınıfı silin, ancak IdentityModels.cs dosyasında da bulunan yardımcı sınıfını kaydettiğinizden emin olun.
3. Depolama sağlayıcınız ayrı bir projede yer alıyorsa, Web uygulamanızda buna bir başvuru ekleyin.
4. `using Microsoft.AspNet.Identity.EntityFramework;` tüm başvuruları, depolama sağlayıcınızın ad alanı için bir using ifadesiyle değiştirin.
5. **Startup.auth.cs** sınıfında, **configureauth** yöntemini uygun bağlamın tek bir örneğini kullanacak şekilde değiştirin. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. Uygulama\_başlangıç klasöründe, **IdentityConfig.cs**' yi açın. ApplicationUserManager sınıfında, **Create** metodunu özelleştirilmiş Kullanıcı deponuzu kullanan bir Kullanıcı Yöneticisi döndürecek şekilde değiştirin. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. Tüm başvuruları, **ıdentityuser**Ile **ApplicationUser** ile değiştirin.
8. Varsayılan proje, Kullanıcı sınıfında, IUser arabiriminde tanımlanmayan bazı Üyeler içeriyor; e-posta, PasswordHash ve Generateuserıdentityasync gibi. Kullanıcı sınıfınız bu üyelere sahip değilse, bunları uygulamanız ya da bu üyeleri kullanan kodu değiştirmeniz gerekir.
9. RoleManager örnekleri oluşturduysanız, bu kodu yeni RoleStore sınıfınızı kullanacak şekilde değiştirin.  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. Varsayılan proje, anahtar için bir dize değeri olan bir Kullanıcı sınıfı için tasarlanmıştır. Kullanıcı sınıfınızın anahtar için farklı bir türü (örneğin, bir tamsayı) varsa, projeyi, sizin yazınızla çalışacak şekilde değiştirmeniz gerekir. Bkz. [ASP.NET Identity kullanıcılar Için birincil anahtarı değiştirme](change-primary-key-for-users-in-aspnet-identity.md).
11. Gerekirse, bağlantı dizesini Web. config dosyasına ekleyin.

<a id="other"></a>
## <a name="other-resources"></a>Diğer kaynaklar

- Blog: [uygulama ASP.NET Identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- Öğretici ve GIT kodu: [Simple. Data ASP.NET Identity Provider](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- Öğretici:[temel kimlik hesapları ayarlama ve bunları bir dış veritabanına gösterme](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx). [@xivSolutions](https://twitter.com/xivSolutions).
- Öğretici[: özel bir MySQL ASP.NET Identity depolama sağlayıcısı uygulama](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [Softfluent](http://www.softfluent.com/) 'e göre [Codefluent varlıkları](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/)
- James Randall tarafından [Azure Tablo Depolaması](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) .
- Azure Tablo Depolama: [@stuartleeks](https://twitter.com/stuartleeks)göre [Aspnet. Identity. TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) .
- [Daniel Wertheım tarafından Couşdb/Cloudant.](https://github.com/danielwertheim/mycouch.aspnet.identity)
- Elastik searc h: Bombsquad AB tarafından[elastik kimlik](https://github.com/bmbsqd/elastic-identity) .
- Jonathan Şekondan, şekondan [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) .
- [Nhazırda beklet. Aspnet. Identity](https://github.com/milesibastos/NHibernate.AspNet.Identity) by Antônio Milesi Bastos.
- [@tourismgeek](https://twitter.com/tourismgeek)tarafından [bvendb](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) .
- [Iltedb. Aspnet. Identity](https://github.com/ILMServices/RavenDB.AspNet.Identity) , [ılmservices](http://www.ilmservice.com/).
- Redsıs: [redsıs. Aspnet. Identity](https://github.com/aminjam/Redis.AspNet.Identity)
- "İlk veritabanı" Kullanıcı deposu için EF kodu oluşturmak üzere T4 şablonları: [Aspnet. Identity. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)
