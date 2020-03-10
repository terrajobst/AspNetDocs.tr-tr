---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: Mevcut bir Web sitesini SQL üyeliğinden ASP.NET Identity-ASP.NET 4. x öğesine geçirme
author: Rick-Anderson
description: Bu öğreticide, mevcut bir Web uygulamasını SQL üyeliği kullanılarak oluşturulan kullanıcı ve rol verileriyle yeni ASP.NET Identity s 'ye geçirme adımları gösterilmektedir...
ms.author: riande
ms.date: 12/19/2014
ms.custom: seoapril2019
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 633229cc4311d151121bf6a91b9fa8aeecca1197
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583729"
---
# <a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>Mevcut Bir Web Sitesini SQL Üyeliğinden ASP.NET Identity’ye Geçirme

by [Rick Anderson](https://twitter.com/RickAndMSFT), [Suwith Joshi](https://github.com/suhasj)

> Bu öğreticide, mevcut bir Web uygulamasını yeni ASP.NET Identity sistemine SQL üyeliği kullanılarak oluşturulan kullanıcı ve rol verileriyle geçirme adımları gösterilmektedir. Bu yaklaşım, var olan veritabanı şemasını ASP.NET Identity için gereken bir şekilde değiştirmeyi ve eski/yeni sınıflarda bu sınıfa kancalarını içerir. Bu yaklaşımı benimsediğinizde, veritabanınız geçirildikten sonra, sonraki kimlik güncelleştirmeleri daha kolay bir şekilde ele alınacaktır.

Bu öğreticide, Kullanıcı ve rol verileri oluşturmak için Visual Studio 2010 kullanılarak oluşturulan bir Web uygulaması şablonu (Web Forms) kullanacağız. Daha sonra, mevcut veritabanını kimlik sisteminin gerektirdiği tablolara geçirmek için SQL betikleri kullanacağız. Ardından, gerekli NuGet paketlerini yükleyeceğiz ve Üyelik yönetimi için kimlik sistemini kullanan yeni hesap yönetimi sayfaları ekleyeceğiz. Geçişin bir testi olarak, SQL üyeliği kullanılarak oluşturulan kullanıcıların oturum açabiliyor ve yeni kullanıcıların kayıt yapabilmesi gerekir. Örneğin tamamını [burada](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/) bulabilirsiniz. Ayrıca bkz. [ASP.net üyeliğinden ASP.NET Identity geçirme](http://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity.html).

## <a name="getting-started"></a>Başlarken

### <a name="creating-an-application-with-sql-membership"></a>SQL üyeliğiyle uygulama oluşturma

1. SQL üyeliği kullanan ve Kullanıcı ve rol verilerine sahip olan mevcut bir uygulamayla başlamamız gerekir. Bu makalenin amacı doğrultusunda, Visual Studio 2010 'de bir Web uygulaması oluşturalım.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. ASP.NET yapılandırma aracını kullanarak 2 Kullanıcı oluşturun: **Oldadminuser** ve **olduser.**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. Yönetici adlı bir rol oluşturun ve bu roldeki bir kullanıcı olarak ' oldAdminUser ' ekleyin.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. Site için default. aspx olan bir yönetici bölümü oluşturun. Yalnızca yönetici rollerindeki kullanıcılara erişimi etkinleştirmek için Web. config dosyasındaki yetkilendirme etiketini ayarlayın. Burada daha fazla bilgi bulabilirsiniz [https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. SQL üyelik sistemi tarafından oluşturulan tabloları anlamak için Sunucu Gezgini veritabanını görüntüleyin. Kullanıcı oturum açma verileri ASPNET\_Users ve ASPNET\_üyelik tablolarında depolanır, ancak rol verileri ASPNET\_roller tablosunda depolanır. Hangi kullanıcıların, ASPNET\_Usersınroles tablosunda hangi rollerin depolandığı hakkında bilgiler. Temel üyelik yönetimi için yukarıdaki tablolardaki bilgilerin ASP.NET Identity sistemine bağlantı noktası almak yeterlidir.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>Visual Studio 2013 geçiriliyor

1. Web veya Visual Studio 2013 için Visual Studio Express 2013 ' i [en son güncelleştirmelerle](https://www.microsoft.com/download/details.aspx?id=44921)birlikte yükler.
2. Yukarıdaki projeyi Visual Studio 'nun yüklü sürümünde açın. Makinede SQL Server Express yüklü değilse, bağlantı dizesi SQL Express kullandığından projeyi açtığınızda bir istem görüntülenir. SQL Express 'i yüklemeyi veya geçici bir çözüm olarak, bağlantı dizesini LocalDb olarak değiştirmeyi seçebilirsiniz. Bu makalede, LocalDb olarak değiştirilecek.
3. Web. config dosyasını açın ve bağlantı dizesini ' den değiştirin. SQLExpress (LocalDb) v 11.0. Bağlantı dizesinden ' User Instance = true ' değerini kaldırın.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. Sunucu Gezgini açın ve tablo şemasının ve verilerin gözlemlenebilir olduğunu doğrulayın.
5. ASP.NET Identity sistem Framework sürüm 4,5 veya üzeri sürümlerle birlikte çalışmaktadır. Uygulamayı 4,5 veya daha yüksek bir düzeye yeniden hedefleyin.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    Hata olmadığını doğrulamak için projeyi derleyin.

### <a name="installing-the-nuget-packages"></a>NuGet paketlerini yükleme

1. Çözüm Gezgini, **NuGet paketlerini yönetmek**&gt; projeye sağ tıklayın. Arama kutusuna "Asp.net Identity" yazın. Sonuçlar listesinden paketi seçin ve ardından yükler ' e tıklayın. "Kabul ediyorum" düğmesine tıklayarak lisans sözleşmesini kabul edin. Bu paketin bağımlılık paketlerini yükleyeceğini unutmayın: EntityFramework ve Microsoft ASP.NET Identity Core. Benzer şekilde, aşağıdaki paketleri yüklemek (OAuth oturum açma işlemini etkinleştirmek istemiyorsanız son 4 OWIN paketlerini atlayın):

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Microsoft. Owin. Security. Facebook
   - Microsoft. Owin. Security. Google
   - Microsoft.Owin.Security.MicrosoftAccount
   - Microsoft.Owin.Security.Twitter

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>Veritabanını yeni kimlik sistemine geçir

Sonraki adım, mevcut veritabanını ASP.NET Identity sisteminin gerektirdiği bir şemaya geçirmadır. Bunu başarmak için yeni tablolar oluşturmaya ve mevcut kullanıcı bilgilerini yeni tablolara geçirmeye yönelik bir komut kümesine sahip bir SQL betiği çalıştırdık. Betik dosyası [burada](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/Migrations.sql)bulunabilir.

Bu betik dosyası bu örneğe özeldir. SQL üyeliği kullanılarak oluşturulan tablolar için şema özelleştirildiyse veya değiştirilirse betiklerin uygun şekilde değiştirilmesi gerekir.

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>Şema geçişi için SQL betiği oluşturma

ASP.NET Identity sınıflarının mevcut kullanıcıların verileriyle birlikte çalışması için, veritabanı şemasını ASP.NET Identity için gereken birine geçirmemiz gerekir. Bunu, yeni tablolar ekleyerek ve var olan bilgileri bu tablolara kopyalayarak yapabiliriz. Varsayılan olarak ASP.NET Identity EntityFramework kullanarak kimlik modeli sınıflarını, bilgileri depolamak/almak üzere veritabanına geri eşlemek için kullanır. Bu model sınıfları, Kullanıcı ve rol nesnelerini tanımlayan temel kimlik arabirimlerini uygular. Veritabanındaki tablolar ve sütunlar bu model sınıflarını temel alır. Identity v 2.1.0 ve özellikleri içindeki EntityFramework model sınıfları aşağıda tanımlanmıştır

| **Identityuser** | **Tür** | **Identityrole** | **Identityuserrole** | **Identityuserlogin** | **Identityuserclaim** |
| --- | --- | --- | --- | --- | --- |
| Kimlik | dize | Kimlik | RoleID | ProviderKey | Kimlik |
| Kullanıcı adı | dize | Adı | UserID | UserID | ClaimType |
| PasswordHash | dize |  |  | LoginProvider | ClaimValue |
| SecurityStamp | dize |  |  |  | Kullanıcı\_kimliği |
| E-posta | dize |  |  |  |  |
| Emailonaylandı | bool |  |  |  |  |
| PhoneNumber | dize |  |  |  |  |
| Phonenumberonaylandı | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | DateTime |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

Özelliklere karşılık gelen sütunlarla bu modellerden her biri için tabloların olması gerekir. Sınıflar ve tablolar arasındaki eşleme `IdentityDBContext``OnModelCreating` yönteminde tanımlanmıştır. Bu, Fluent API yapılandırma yöntemi olarak bilinir ve [burada](https://msdn.microsoft.com/data/jj591617.aspx)daha fazla bilgi bulabilirsiniz. Sınıfların yapılandırması aşağıda belirtilmiştir

| **Sınıfı** | **Tablo** | **Birincil anahtar** | **Yabancı anahtar** |
| --- | --- | --- | --- |
| Identityuser | AspnetUsers | Kimlik |  |
| Identityrole | AspnetRoles | Kimlik |  |
| Identityuserrole | AspnetUserRole | UserID + RoleID | Kullanıcı\_kimliği-&gt;AspnetUsers RoleID-&gt;AspnetRoles |
| Identityuserlogin | AspnetUserLogins | ProviderKey + UserID + LoginProvider | UserID-&gt;AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | Kimlik | Kullanıcı\_kimliği-&gt;AspnetUsers |

Bu bilgilerle, yeni tablolar oluşturmak için SQL deyimleri oluşturuyoruz. Her bir ifadeyi ayrı ayrı yazabilir veya daha sonra gerektiği şekilde düzenleyebilmemiz için EntityFramework PowerShell komutlarını kullanarak tüm betiği oluşturabilirsiniz. Bunu yapmak için, VS 'de **Görünüm** veya **Araçlar** menüsünden **Paket Yöneticisi konsolunu** açın

- EntityFramework geçişlerini etkinleştirmek için "Enable-geçişler" komutunu çalıştırın.
- /Vbiçinde C#veritabanını oluşturmak için ilk kurulum kodunu oluşturan "Add-geçiş Initial" komutunu çalıştırın.
- Son adım, model sınıflarına dayalı olarak SQL betiğini üreten "güncelleştirme-veritabanı – komut dosyası" komutunu çalıştırmlarıdır.

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

Bu veritabanı oluşturma betiği, yeni sütun eklemek ve veri kopyalamak için ek değişiklikler yapmakta olduğumuz bir başlangıç olarak kullanılabilir. Bunun avantajı, model sınıfları kimlik sürümlerinin gelecek sürümleri için değişiklik yaparken, EntityFramework tarafından veritabanı şemasını değiştirmek için kullanılan `_MigrationHistory` tablosunu oluşturmamız.

SQL üyeliği kullanıcı bilgilerinin, kimlik Kullanıcı modeli sınıfındaki e-posta, parola denemeleri, son oturum açma tarihi, son kilit kapatma tarihi vb. gibi diğer özellikleri de vardır. Bu, yararlı bilgiler ve kimlik sistemine taşınmasını istiyoruz. Bu, Kullanıcı modeline ek özellikler eklenerek ve bunları veritabanındaki tablo sütunlarına geri eşleyerek yapılabilir. Bunu, `IdentityUser` modelini alt sınıflara uygulayan bir sınıf ekleyerek yapabiliriz. Bu özel sınıfa özellikleri ekleyebiliyoruz ve tabloyu oluştururken karşılık gelen sütunları eklemek için SQL betiğini düzenleyebiliriz. Bu sınıfın kodu, makalesinde daha ayrıntılı olarak açıklanmıştır. Yeni özellikler eklendikten sonra `AspnetUsers` tablosu oluşturmaya yönelik SQL betiği

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

Daha sonra, mevcut bilgileri SQL üyelik veritabanından kimlik için yeni eklenen tablolara kopyalamanız gerekir. Bu, verileri doğrudan bir tablodan diğerine kopyalayarak SQL üzerinden yapılabilir. Tablo satırlarına veri eklemek için `INSERT INTO [Table]` yapısını kullanırız. Başka bir tablodan kopyalamak için `SELECT` ifadesiyle birlikte `INSERT INTO` ifadesini kullanabiliriz. *Aspnet\_kullanıcıları* ve *ASPNET\_üyelik* tablolarını sorgulamak ve verileri *aspnetusers* tablosuna kopyalamak için gereken tüm Kullanıcı bilgilerini almak için. `JOIN` ve `LEFT OUTER JOIN` deyimleriyle birlikte `INSERT INTO` ve `SELECT` kullanırız. Tablolar arasında veri sorgulama ve kopyalama hakkında daha fazla bilgi için [Bu](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx) bağlantıya başvurun. Ayrıca, SQL üyeliğinde varsayılan olarak buna eşlenen hiçbir bilgi olmadığından, AspnetUserLogins ve Aspnetuserclaim tabloları ile başlamak için boştur. Yalnızca kullanıcılar ve roller için kopyalanmış bilgiler kullanılır. Önceki adımlarda oluşturulan proje için, bilgileri kullanıcılar tablosuna kopyalamak üzere SQL sorgusu şöyle olacaktır

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

Yukarıdaki SQL ifadesinde, *aspnet\_Users* ve *ASPNET\_Membership* tablolarından her bir kullanıcı hakkında bilgi, *aspnetusers* tablosunun sütunlarına kopyalanır. Burada yapılan tek değişiklik, parolayı kopyalayacağız. SQL üyeliğindeki parolalara yönelik şifreleme algoritması ' password, ' ve ' PasswordFormat ' kullandı, bu sayede parolanın kimliğe göre şifresini çözmek için kullanılabilmesi için onu karma parola ile birlikte kopyalayacağız. Bu, özel bir parola karmacısı oluştururken makalede daha ayrıntılı olarak açıklanmaktadır.

Bu betik dosyası bu örneğe özeldir. Geliştiriciler, ek tablolar içeren uygulamalar için, Kullanıcı modeli sınıfına ek özellikler eklemek ve bunları AspnetUsers tablosundaki sütunlarla eşlemek için benzer bir yaklaşımı izleyebilir. Betiği çalıştırmak için

1. Sunucu Gezgini açın. Tabloları göstermek için ' ApplicationServices ' bağlantısını genişletin. Tablolar düğümüne sağ tıklayın ve ' yeni sorgu ' seçeneğini belirleyin

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. Sorgu penceresinde, tüm SQL betiğini kopyalayıp geçişler. SQL dosyasından yapıştırın. Komut dosyasını ' Yürüt ' ok düğmesine vurarak çalıştırın.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    Sunucu Gezgini penceresini yenileyin. Veritabanında beş yeni tablo oluşturulur.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    SQL üyelik tablolarındaki bilgilerin yeni kimlik sistemine nasıl eşlendiğine aşağıda verilmiştir.

    ASPNET\_rolleri--&gt; AspNetRoles

    netUsers ve ASP\_netMembership ile ASP\_--&gt; AspNetUsers

    ASPNET\_Userınroles--&gt; AspNetUserRoles

    Yukarıdaki bölümde açıklandığı gibi, Aspnetuserclaim ve AspNetUserLogins tabloları boştur. AspNetUser tablosundaki ' ayrıştırıcı ' alanı, bir sonraki adım olarak tanımlanan model sınıfı adıyla eşleşmelidir. Ayrıca, PasswordHash sütunu ' şifreli parola | parola anahtar | parola biçimi ' biçiminde olur. Bu, eski parolaları yeniden kullanabilmeniz için özel SQL üyelik şifreleme mantığını kullanmanıza olanak sağlar. Bu makalede daha sonra makalesinde açıklanmaktadır.

### <a name="creating-models-and-membership-pages"></a>Modeller ve üyelik sayfaları oluşturma

Daha önce belirtildiği gibi, kimlik özelliği, varsayılan olarak hesap bilgilerini depolamak için veritabanı ile konuşmak üzere Entity Framework kullanır. Tablodaki mevcut verilerle çalışmak için, tablolara geri eşlenen ve bunları kimlik sisteminde bağlayan model sınıfları oluşturmanız gerekir. Kimlik sözleşmesinin bir parçası olarak model sınıfları, Identity. Core dll dosyasında tanımlanan arabirimleri uygulamalıdır ya da Microsoft. AspNet. Identity. EntityFramework içinde bulunan bu arabirimlerin mevcut uygulamasını genişletebilir.

Örneğimizde, AspNetRoles, Aspnetuserclaim, AspNetLogins ve AspNetUserRole tablolarında, kimlik sisteminin mevcut uygulamasına benzer sütunlar bulunur. Bu nedenle, bu tablolarla eşlemek için mevcut sınıfları yeniden kullanabiliriz. AspNetUser tablosunda, SQL üyelik tablolarından ek bilgileri depolamak için kullanılan bazı ek sütunlar bulunur. Bu, mevcut ' ıdentityuser ' uygulamasını genişleten ve ek özellikleri ekleyen bir model sınıfı oluşturularak eşleştirilebilir.

1. Projede modeller klasörü oluşturun ve bir sınıf kullanıcısı ekleyin. Sınıfın adı ' AspnetUsers ' tablosunun ' ayrıştırıcı ' sütununda eklenen verilerle eşleşmelidir.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    Kullanıcı sınıfı, *Microsoft. Aspnet. Identity. EntityFramework* dll dosyasında bulunan ıdentityuser sınıfını genişletmelidir. Bir sınıf içinde AspNetUser sütunlarına geri eşlenen özellikler bildirin. Özellik KIMLIĞI, Kullanıcı adı, PasswordHash ve SecurityStamp, ıdentityuser içinde tanımlanmıştır ve bu nedenle atlanır. Aşağıda, tüm özelliklerine sahip olan Kullanıcı sınıfının kodu verilmiştir

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. Modellerdeki verileri tablolara geri kalıcı hale getirmek ve modelleri doldurmak üzere tablolardan veri almak için Entity Framework DbContext sınıfı gerekir. *Microsoft. Aspnet. Identity. EntityFramework* dll, bilgileri almak ve depolamak için kimlik tablolarıyla etkileşim kuran ıdentitydbcontext sınıfını tanımlar. Identitydbcontext&lt;Tuser&gt;, ıdentityuser sınıfını genişleten herhangi bir sınıf olabilen bir ' TUser ' sınıfı alır.

    1\. adımda oluşturulan ' user ' sınıfını geçirerek ' modeller ' klasörü altında ıdentitydbcontext ' i genişleten yeni bir ApplicationDBContext sınıfı oluşturun

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. Yeni kimlik sistemindeki kullanıcı yönetimi, *Microsoft. Aspnet. Identity. EntityFramework* dll 'de tanımlanan usermanager&lt;tuser&gt; sınıfı kullanılarak yapılır. UserManager 'ı genişleten, 1. adımda oluşturulan ' user ' sınıfını geçirerek, özel bir sınıf oluşturuyoruz.

    Modeller klasöründe, UserManager&lt;kullanıcıyı genişleten yeni bir UserManager sınıfı oluşturun&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. Uygulama kullanıcılarının parolaları şifrelenir ve veritabanında depolanır. SQL üyeliğinde kullanılan şifre algoritması, yeni kimlik sisteminden farklı. Eski parolaları yeniden kullanmak için, yeni kullanıcılar için kimlik ' de şifre algoritmasını kullanırken eski kullanıcılar SQL üyelik algoritmasını kullanarak oturum açarken parolaların şifresini seçmeli olarak çözmemiz gerekir.

    UserManager sınıfı ' ıpasswordhasher ' arabirimini uygulayan bir sınıfın örneğini depolayan ' PasswordHasher ' özelliğine sahiptir. Bu, Kullanıcı kimlik doğrulama işlemleri sırasında parolaları şifrelemek/şifrelerini çözmek için kullanılır. Adım 3 ' te tanımlanan UserManager sınıfında, SQLPasswordHasher adlı yeni bir sınıf oluşturun ve aşağıdaki kodu kopyalayın.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    System. Text ve System. Security. Cryptography ad alanlarını içeri aktararak derleme hatalarını çözün.

    EncodePassword yöntemi, parolayı varsayılan SQL üyelik şifre uygulamasına göre şifreler. Bu, System. Web dll 'den alınmıştır. Eski uygulama özel bir uygulama kullanıyorsa buraya yansıtılmalıdır. Belirli bir parolayı karma hale getirmek için *Encodepassword* metodunu kullanan iki diğer yöntem *Hashpassword* ve *verifyhashedpassword* tanımladık veya veritabanında mevcut olan bir düz metin parolasının doğrulanması gerekir.

    SQL üyelik sistemi, parolalarını kaydederken veya değiştirdiklerinde kullanıcılar tarafından girilen parolayı karma hale almak için PasswordHash, Passwordanahtar ve PasswordFormat kullandı. Geçiş sırasında, tüm üç alan, ' | ' karakteriyle ayrılmış olan AspNetUser tablosundaki PasswordHash sütununda depolanır. Bir Kullanıcı oturum açtığında ve parolada bu alanlar varsa, parolayı denetlemek için SQL üyelik şifre ' nu kullanırız; Aksi takdirde, parolayı doğrulamak için kimlik sisteminin varsayılan şifresini kullanırız. Bu sayede, uygulama geçirildikten sonra eski kullanıcıların parolalarını değiştirmesi gerekmez.
5. UserManager sınıfı için oluşturucuyu bildirin ve bunu oluşturucudaki özelliğe SQLPasswordHasher olarak geçirin.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>Yeni hesap yönetimi sayfaları oluştur

Geçiş içindeki bir sonraki adım, bir kullanıcının kaydolmasına ve oturum açmasına izin verecek hesap yönetimi sayfaları eklemektir. SQL üyeliğinden eski hesap sayfaları, yeni kimlik sistemiyle çalışmayan denetimleri kullanır. Yeni Kullanıcı Yönetimi sayfalarını eklemek için, projeyi zaten oluşturduğumuz ve NuGet paketlerini eklediğimiz için, bu bağlantıdaki öğreticiyi [https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md) ' Web Forms uygulamanıza Kullanıcı ekleme ' adımından başlayarak

Burada, örnek için, burada yaptığımız projeyle birlikte çalışmak üzere bazı değişiklikler yapmanız gerekiyor.

- Register.aspx.cs ve Login.aspx.cs kodu sınıflarının arkasında bir kullanıcı oluşturmak için kimlik paketlerindeki `UserManager` kullanır. Bu örnekte, daha önce bahsedilen adımları izleyerek modeller klasörüne eklenen UserManager 'ı kullanın.
- Register.aspx.cs içinde ıdentityuser yerine oluşturulan kullanıcı sınıfını ve Login.aspx.cs arka plan kodu sınıflarını kullanın. Bu, Özel Kullanıcı sınıfımızda kimlik sistemine kanca oluşturur.
- Veritabanının oluşturulacağı bölüm atlanabilir.
- Geliştiricinin Yeni Kullanıcı için ApplicationId 'yi geçerli uygulama KIMLIĞIYLE eşleşecek şekilde ayarlaması gerekir. Bu, Register.aspx.cs sınıfında bir kullanıcı nesnesi oluşturulmadan ve Kullanıcı oluşturmadan önce ayarlanarak önce bu uygulama için ApplicationId sorgulanarak yapılabilir.

    Örnek:

    Register.aspx.cs sayfasında, ASPNET\_uygulamalar tablosunu sorgulamak ve uygulama adına göre uygulama kimliğini almak için bir yöntem tanımlayın

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    Şimdi bunu Kullanıcı nesnesinde ayarla ' yı al

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

Mevcut bir kullanıcının oturumu açmak için eski Kullanıcı adı ve parolayı kullanın. Yeni bir kullanıcı oluşturmak için kayıt sayfasını kullanın. Ayrıca, kullanıcıların rollerde beklendiği gibi olduğunu doğrulayın.

Kimlik sistemine taşıma, kullanıcının uygulamaya açık kimlik doğrulaması (OAuth) eklemesini sağlar. Lütfen bu örneğe OAuth etkin [olan örneği](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/) inceleyin.

## <a name="next-steps"></a>Sonraki Adımlar

Bu öğreticide, kullanıcıların SQL üyeliğinden ASP.NET Identity için bağlantı noktası alma, ancak profil verileri için bağlantı noktası yoktu. Sonraki öğreticide, SQL üyeliğinden yeni kimlik sistemine profil verilerini taşıma sayfasına bakacağız.

Bu makalenin en altında geri bildirim alabilirsiniz.

*Makaleyi gözden geçirmek için Tom Dykstra ve Rick Anderson için teşekkürler.*
